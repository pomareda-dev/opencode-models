# Perfiles SDD para gentle-orchestrator (OpenCode Go)

> **Información actualizada:** 13 de septiembre de 2026
> Modelos: [modelos-opencode-go.md](./modelos-opencode-go.md) · [OpenCode Go docs](https://opencode.ai/docs/go/)
> Runtime: [gentle-ai OpenCode SDD Profiles](https://github.com/Gentleman-Programming/gentle-ai/blob/main/docs/opencode-profiles.md)

Tres perfiles listos para `gentle-orchestrator` / multi-mode OpenCode:

| Perfil | Nombre slug | Cuándo usarlo |
|--------|-------------|---------------|
| **Top** | `top` | Cambios críticos, arquitectura nueva, specs difíciles |
| **Balanceado** | `balanced` | Día a día SDD (recomendado por defecto) |
| **Económico** | `cheap` | Exploración, prototipos, ciclos largos con poco presupuesto |

En OpenCode (Tab):

| Perfil | Orchestrator visible |
|--------|----------------------|
| default (base) | `gentle-orchestrator` |
| top | `sdd-orchestrator-top` |
| balanced | `sdd-orchestrator-balanced` |
| cheap | `sdd-orchestrator-cheap` |

Cada perfil nombrado genera **11 agentes**: 1 conductor (`sdd-orchestrator-{name}`) + 10 subagentes de fase (`sdd-{phase}-{name}`). El conductor base `gentle-orchestrator` se mantiene aparte. Los prompts de fase se comparten; normalmente solo cambia el `model`.

Formato de model ID: `opencode-go/<model-id>`.

---

## Lógica por fase (aplica a los 3 perfiles)

| Fase / agente | Tipo de trabajo | Prioridad |
|---------------|-----------------|-----------|
| **gentle-orchestrator** / `sdd-orchestrator-*` | Delega, decide fase, resume estado | Razonamiento de routing (pocas llamadas, alto impacto) |
| **sdd-init** | Stack, testing, context del proyecto | Contexto largo + detección confiable |
| **sdd-explore** | Investigación multi-archivo | Iteraciones + comprensión de código |
| **sdd-propose** | Intent, scope, approach | Razonamiento de producto/plan (crítico) |
| **sdd-spec** | Requirements + escenarios G/W/T | Precisión y cobertura de edge cases |
| **sdd-design** | ADRs, arquitectura, tradeoffs | Mejor razonamiento de diseño |
| **sdd-tasks** | Checklist ordenado y acotado | Planificación práctica, no “literatura” |
| **sdd-apply** | Implementación + TDD | Código + alto throughput (más requests del ciclo) |
| **sdd-verify** | Auditoría vs spec/design/tasks | Razonamiento adversarial / detección de huecos |
| **sdd-archive** | Merge deltas, cierre | Bajo riesgo, barato |
| **sdd-onboard** | Ingesta amplia del repo | Contexto enorme + volumen |

Regla: **planear caro, ejecutar barato** — propose/design/verify arriba; apply/explore/archive abajo. Las asignaciones son recomendaciones, no una garantía de calidad: el catálogo y sus límites cambian.

## Cambios operativos de OpenCode SDD

### Subagentes en segundo plano nativos

OpenCode SDD usa subagentes nativos mediante el permiso `task`; Gentle AI ya no instala por defecto el plugin legado `background-agents.ts`. El comportamiento se controla con `auto`, `on` u `off`:

```bash
gentle-ai install --agent opencode --component sdd --opencode-background-subagents=on
gentle-ai sync --opencode-background-subagents=off
```

También podés usar `GENTLE_AI_OPENCODE_BACKGROUND_SUBAGENTS=auto|on|off`. La prioridad es flag CLI, variable de entorno, elección guardada y, por último, `auto`. Los trabajos en segundo plano son locales al proceso, no sobreviven a un reinicio y no aíslan el sistema de archivos: no los uses para fases dependientes ni ejecutes escritores en paralelo en el mismo worktree.

### Variantes de esfuerzo de razonamiento

Cuando un modelo expone variantes (`low`, `medium`, `high`, `xhigh`), el selector de modelos permite fijar el nivel de esfuerzo. Las variantes disponibles se refrescan mediante el plugin `model-variants` en `~/.gentle-ai/cache/model-variants.json`. Después de sincronizar, iniciá OpenCode una vez para llenar la caché y volvé a abrir el selector. Si la caché no existe, se usa el esfuerzo predeterminado del proveedor.

### Estrategias de perfiles

- `generated-multi` es el modo clásico: conserva `gentle-orchestrator`, genera cada `sdd-orchestrator-{name}` y sus 10 subagentes con sufijo en `opencode.json`.
- `external-single-active` se activa si detecta perfiles en `~/.config/opencode/profiles/*.json`; mantiene los assets SDD base y deja que el gestor externo controle el perfil activo.

Podés forzar una estrategia con `--sdd-profile-strategy generated-multi` o `--sdd-profile-strategy external-single-active`.

---

## 1. Perfil TOP (`top`)

Máxima calidad por fase. Usa flagships en decisiones y diseño; no quema K3/Grok en apply.

| Agente | Modelo | ID | req/5h | Por qué |
|--------|--------|-----|--------|---------|
| **orchestrator** | GLM-5.3 | `opencode-go/glm-5.3` | ~220 | Mejor routing de nueva gen GLM; más requests que K3 |
| **sdd-init** | Qwen3.8 Max | `opencode-go/qwen3.8-max` | ~160 | Max calidad + contexto largo para mapear el sistema |
| **sdd-explore** | Kimi K2.6 | `opencode-go/kimi-k2.6` | ~1,150 | Razonamiento fuerte + multi-archivo sin gastar K3 |
| **sdd-propose** | Kimi K3 | `opencode-go/kimi-k3` | ~110 | Flagship: intent/scope/approach de máxima calidad |
| **sdd-spec** | GLM-5.2 | `opencode-go/glm-5.2` | ~880 | Requisitos y escenarios con razonamiento profundo |
| **sdd-design** | Qwen3.8 Max | `opencode-go/qwen3.8-max` | ~160 | Arquitectura y tradeoffs al techo Qwen |
| **sdd-tasks** | GLM-5.2 | `opencode-go/glm-5.2` | ~880 | Desglose preciso alineado al design |
| **sdd-apply** | Kimi K2.7 Code | `opencode-go/kimi-k2.7-code` | ~1,350 | Mejor modelo *code-specialized* sin matar el cupo |
| **sdd-verify** | GLM-5.3 | `opencode-go/glm-5.3` | ~220 | Verificación con razonamiento de primer nivel |
| **sdd-archive** | Qwen3.7 Plus | `opencode-go/qwen3.7-plus` | ~4,300 | Cierre documental barato y sólido |
| **sdd-onboard** | Kimi K2.6 | `opencode-go/kimi-k2.6` | ~1,150 | Onboarding profundo con buen contexto |

**Uso estimado del cupo:** alto en propose/design/verify ($15 usage en K3/Qwen3.8/GLM-5.3). Ideal para 1–2 cambios serios por ventana, no para spam de `/sdd-ff`.

**CLI:**

```bash
gentle-ai sync \
  --profile top:opencode-go/glm-5.3 \
  --profile-phase top:sdd-init:opencode-go/qwen3.8-max \
  --profile-phase top:sdd-explore:opencode-go/kimi-k2.6 \
  --profile-phase top:sdd-propose:opencode-go/kimi-k3 \
  --profile-phase top:sdd-spec:opencode-go/glm-5.2 \
  --profile-phase top:sdd-design:opencode-go/qwen3.8-max \
  --profile-phase top:sdd-tasks:opencode-go/glm-5.2 \
  --profile-phase top:sdd-apply:opencode-go/kimi-k2.7-code \
  --profile-phase top:sdd-verify:opencode-go/glm-5.3 \
  --profile-phase top:sdd-archive:opencode-go/qwen3.7-plus \
  --profile-phase top:sdd-onboard:opencode-go/kimi-k2.6
```

**Sustitutos TOP (si preferís otra familia):**

| Slot | Alternativa |
|------|-------------|
| orchestrator | `opencode-go/kimi-k3` o `opencode-go/grok-4.6` |
| sdd-design | `opencode-go/grok-4.6` o `opencode-go/glm-5.3` |
| sdd-apply | `opencode-go/deepseek-v4-pro` (más razonamiento, menos “code-tuned”) |
| sdd-propose | `opencode-go/glm-5.3` (si K3 se agota) |

---

## 2. Perfil BALANCEADO (`balanced`) — daily driver

Mejor relación calidad/request. Casi todo el ciclo cabe cómodo en límites Go.

| Agente | Modelo | ID | req/5h | Por qué |
|--------|--------|-----|--------|---------|
| **orchestrator** | GLM-5.2 | `opencode-go/glm-5.2` | ~880 | Excelente routing con buen cupo ($60 usage) |
| **sdd-init** | Kimi K2.6 | `opencode-go/kimi-k2.6` | ~1,150 | Contexto largo para bootstrap del proyecto |
| **sdd-explore** | Kimi K2.7 Code | `opencode-go/kimi-k2.7-code` | ~1,350 | Explorar código con modelo code-first |
| **sdd-propose** | GLM-5.2 | `opencode-go/glm-5.2` | ~880 | Propuestas sólidas sin flagship $15 |
| **sdd-spec** | DeepSeek V4 Pro | `opencode-go/deepseek-v4-pro` | ~1,050 | Specs paso a paso con buen razonamiento |
| **sdd-design** | MiMo-V2.5-Pro | `opencode-go/mimo-v2.5-pro` | ~3,250 | Diseño/código de negocio; mucho volumen |
| **sdd-tasks** | Kimi K2.7 Code | `opencode-go/kimi-k2.7-code` | ~1,350 | Tasks accionables orientadas a implementación |
| **sdd-apply** | DeepSeek V4 Flash | `opencode-go/deepseek-v4-flash` | ~13,000 | Implementar e iterar TDD a full speed |
| **sdd-verify** | DeepSeek V4 Pro | `opencode-go/deepseek-v4-pro` | ~1,050 | Detectar gaps vs spec sin ir a premium |
| **sdd-archive** | Qwen3.7 Plus | `opencode-go/qwen3.7-plus` | ~4,300 | Archive confiable y barato |
| **sdd-onboard** | MiniMax M3 | `opencode-go/minimax-m3` | ~3,200 | Onboard amplio, API Anthropic, buen costo |

**Uso estimado del cupo:** medio. Apply/explore no rompen la ventana de 5h. Propose/design/verify siguen siendo “buenos” sin quemar K3.

**CLI:**

```bash
gentle-ai sync \
  --profile balanced:opencode-go/glm-5.2 \
  --profile-phase balanced:sdd-init:opencode-go/kimi-k2.6 \
  --profile-phase balanced:sdd-explore:opencode-go/kimi-k2.7-code \
  --profile-phase balanced:sdd-propose:opencode-go/glm-5.2 \
  --profile-phase balanced:sdd-spec:opencode-go/deepseek-v4-pro \
  --profile-phase balanced:sdd-design:opencode-go/mimo-v2.5-pro \
  --profile-phase balanced:sdd-tasks:opencode-go/kimi-k2.7-code \
  --profile-phase balanced:sdd-apply:opencode-go/deepseek-v4-flash \
  --profile-phase balanced:sdd-verify:opencode-go/deepseek-v4-pro \
  --profile-phase balanced:sdd-archive:opencode-go/qwen3.7-plus \
  --profile-phase balanced:sdd-onboard:opencode-go/minimax-m3
```

**Sustitutos balanced:**

| Slot | Alternativa |
|------|-------------|
| orchestrator | `opencode-go/deepseek-v4-pro` |
| sdd-design | `opencode-go/minimax-m3` o `opencode-go/glm-5.2` |
| sdd-apply | `opencode-go/kimi-k2.7-code` (más calidad de código, menos volumen) |
| sdd-verify | `opencode-go/minimax-m3` |
| sdd-spec | `opencode-go/qwen3.7-plus` |

---

## 3. Perfil ECONÓMICO (`cheap`)

Máximo throughput. Calidad “suficiente” para explorar y entregar cambios chicos/medios.

| Agente | Modelo | ID | req/5h | Por qué |
|--------|--------|-----|--------|---------|
| **orchestrator** | Qwen3.7 Plus | `opencode-go/qwen3.7-plus` | ~4,300 | Routing barato y decente |
| **sdd-init** | MiniMax M3 | `opencode-go/minimax-m3` | ~3,200 | Init confiable sin premium |
| **sdd-explore** | DeepSeek V4 Flash | `opencode-go/deepseek-v4-flash` | ~13,000 | Muchas lecturas/iteraciones |
| **sdd-propose** | MiniMax M3 | `opencode-go/minimax-m3` | ~3,200 | Mejor del tier barato para scope |
| **sdd-spec** | Qwen3.7 Plus | `opencode-go/qwen3.7-plus` | ~4,300 | Specs legibles y rápidas |
| **sdd-design** | MiniMax M3 | `opencode-go/minimax-m3` | ~3,200 | Diseño OK sin subir a Pro/Max |
| **sdd-tasks** | Hy3 | `opencode-go/hy3` | ~4,300 | Tasks simples, alto volumen |
| **sdd-apply** | DeepSeek V4 Flash | `opencode-go/deepseek-v4-flash` | ~13,000 | Implementación masiva / TDD loop |
| **sdd-verify** | Qwen3.7 Plus | `opencode-go/qwen3.7-plus` | ~4,300 | Verify liviano pero útil |
| **sdd-archive** | MiMo-V2.5 | `opencode-go/mimo-v2.5` | ~30,100 | Archive casi gratis |
| **sdd-onboard** | MiMo-V2.5 | `opencode-go/mimo-v2.5` | ~30,100 | Ingesta enorme de codebase |

**Uso estimado del cupo:** bajo. Podés correr varios ciclos SDD por día. No uses este perfil para arquitectura crítica o contratos de producción sin review humano fuerte.

**CLI:**

```bash
gentle-ai sync \
  --profile cheap:opencode-go/qwen3.7-plus \
  --profile-phase cheap:sdd-init:opencode-go/minimax-m3 \
  --profile-phase cheap:sdd-explore:opencode-go/deepseek-v4-flash \
  --profile-phase cheap:sdd-propose:opencode-go/minimax-m3 \
  --profile-phase cheap:sdd-spec:opencode-go/qwen3.7-plus \
  --profile-phase cheap:sdd-design:opencode-go/minimax-m3 \
  --profile-phase cheap:sdd-tasks:opencode-go/hy3 \
  --profile-phase cheap:sdd-apply:opencode-go/deepseek-v4-flash \
  --profile-phase cheap:sdd-verify:opencode-go/qwen3.7-plus \
  --profile-phase cheap:sdd-archive:opencode-go/mimo-v2.5 \
  --profile-phase cheap:sdd-onboard:opencode-go/mimo-v2.5
```

**Modo ultra-barato (opcional):** mientras dure la promo (hasta el **20 de septiembre de 2026**), `deepseek-v4.1-flash` tiene **4x de usage** (~26,000 req/5h). Podés poner archive/onboard/explore ahí:

```bash
--profile-phase cheap:sdd-archive:opencode-go/deepseek-v4.1-flash \
--profile-phase cheap:sdd-onboard:opencode-go/deepseek-v4.1-flash
```

⚠️ No uses `muse-spark-1.2-contributor` ni `muse-spark-1.3-contributor` en perfiles de trabajo real si te importa privacy (entrenan con tus prompts).

---

## Comparación rápida

| Fase | TOP | BALANCED | CHEAP |
|------|-----|----------|-------|
| orchestrator | GLM-5.3 | GLM-5.2 | Qwen3.7 Plus |
| sdd-init | Qwen3.8 Max | Kimi K2.6 | MiniMax M3 |
| sdd-explore | Kimi K2.6 | Kimi K2.7 Code | DeepSeek V4 Flash |
| sdd-propose | Kimi K3 | GLM-5.2 | MiniMax M3 |
| sdd-spec | GLM-5.2 | DeepSeek V4 Pro | Qwen3.7 Plus |
| sdd-design | Qwen3.8 Max | MiMo-V2.5-Pro | MiniMax M3 |
| sdd-tasks | GLM-5.2 | Kimi K2.7 Code | Hy3 |
| sdd-apply | Kimi K2.7 Code | DeepSeek V4 Flash | DeepSeek V4 Flash |
| sdd-verify | GLM-5.3 | DeepSeek V4 Pro | Qwen3.7 Plus |
| sdd-archive | Qwen3.7 Plus | Qwen3.7 Plus | MiMo-V2.5 |
| sdd-onboard | Kimi K2.6 | MiniMax M3 | MiMo-V2.5 |

---

## Crear los 3 de una

```bash
# TOP
gentle-ai sync \
  --profile top:opencode-go/glm-5.3 \
  --profile-phase top:sdd-init:opencode-go/qwen3.8-max \
  --profile-phase top:sdd-explore:opencode-go/kimi-k2.6 \
  --profile-phase top:sdd-propose:opencode-go/kimi-k3 \
  --profile-phase top:sdd-spec:opencode-go/glm-5.2 \
  --profile-phase top:sdd-design:opencode-go/qwen3.8-max \
  --profile-phase top:sdd-tasks:opencode-go/glm-5.2 \
  --profile-phase top:sdd-apply:opencode-go/kimi-k2.7-code \
  --profile-phase top:sdd-verify:opencode-go/glm-5.3 \
  --profile-phase top:sdd-archive:opencode-go/qwen3.7-plus \
  --profile-phase top:sdd-onboard:opencode-go/kimi-k2.6 \
  --profile balanced:opencode-go/glm-5.2 \
  --profile-phase balanced:sdd-init:opencode-go/kimi-k2.6 \
  --profile-phase balanced:sdd-explore:opencode-go/kimi-k2.7-code \
  --profile-phase balanced:sdd-propose:opencode-go/glm-5.2 \
  --profile-phase balanced:sdd-spec:opencode-go/deepseek-v4-pro \
  --profile-phase balanced:sdd-design:opencode-go/mimo-v2.5-pro \
  --profile-phase balanced:sdd-tasks:opencode-go/kimi-k2.7-code \
  --profile-phase balanced:sdd-apply:opencode-go/deepseek-v4-flash \
  --profile-phase balanced:sdd-verify:opencode-go/deepseek-v4-pro \
  --profile-phase balanced:sdd-archive:opencode-go/qwen3.7-plus \
  --profile-phase balanced:sdd-onboard:opencode-go/minimax-m3 \
  --profile cheap:opencode-go/qwen3.7-plus \
  --profile-phase cheap:sdd-init:opencode-go/minimax-m3 \
  --profile-phase cheap:sdd-explore:opencode-go/deepseek-v4-flash \
  --profile-phase cheap:sdd-propose:opencode-go/minimax-m3 \
  --profile-phase cheap:sdd-spec:opencode-go/qwen3.7-plus \
  --profile-phase cheap:sdd-design:opencode-go/minimax-m3 \
  --profile-phase cheap:sdd-tasks:opencode-go/hy3 \
  --profile-phase cheap:sdd-apply:opencode-go/deepseek-v4-flash \
  --profile-phase cheap:sdd-verify:opencode-go/qwen3.7-plus \
  --profile-phase cheap:sdd-archive:opencode-go/mimo-v2.5 \
  --profile-phase cheap:sdd-onboard:opencode-go/mimo-v2.5
```

O vía TUI: `gentle-ai` → **OpenCode SDD Profiles** → Create (`top` / `balanced` / `cheap`).

---

## Recomendación de uso

| Situación | Perfil |
|-----------|--------|
| Feature nueva con impacto de arquitectura | `top` |
| Bugfix / feature media con SDD completo | `balanced` |
| Spike, explore, docs, cleanup, onboard | `cheap` |
| Default del día a día en `gentle-orchestrator` | copiá `balanced` al base (TUI edit default) |
| Plan caro + apply barato en un solo ciclo | empezá en `top` hasta tasks; Tab a `cheap`/`balanced` para apply |

**Hybrid tip:** planificá en `top` (explore → propose → spec → design → tasks), después Tab a `balanced` o `cheap` para apply/verify/archive. Los artefactos SDD viven en Engram/OpenSpec; el perfil solo cambia el modelo del sub-agente.

---

## Notas operativas (gentle-ai + OpenCode Go)

1. **Prerrequisito:** `/connect` → OpenCode Go, y `opencode models` para comprobar el catálogo antes de crear perfiles.
2. **Base conductor:** `gentle-orchestrator` (no se borra). Named profiles = `sdd-orchestrator-{name}`.
3. **Legacy:** `sdd-orchestrator` se migra a `gentle-orchestrator` en sync.
4. **Solo un subscriber Go por workspace.**
5. **DeepSeek Peak hours** (01:00–04:00 y 06:00–10:00 UTC) cuestan el doble → preferí Flash/Pro off-peak si podés.
6. **Usage $15** (K3, GLM-5.3, Qwen3.8 Max, Grok 4.6, GPT 5.6 Luna, DeepSeek V4 Pro / Flash Vision Exp / V4.1, MiMo-V2.5-Pro…): no los pongas en apply masivo. GLM-5.3-Flash ahora es $60 y DeepSeek V4 Flash pasó a $30.
7. **Judgment Day** (`jd-judge-a`, `jd-judge-b`, `jd-fix-agent`) es independiente de estos perfiles; se configura aparte en el model picker de gentle-ai.
8. **Strategy sync:** `generated-multi` (default) escribe los 11 agentes en `opencode.json`. Si usás profiles externos en `~/.config/opencode/profiles/*.json`, gentle-ai pasa a `external-single-active`.
9. Si te quedás sin límite Go: activá **Use balance** (Zen) o bajá a `cheap` / free models.
10. **Catálogo Go (sep 2026):** entró `deepseek-v4.1-flash` (promo 4x: ~26,000 req/5h hasta el 20 sep; regular ~6,500). `glm-5.3-flash` subió a usage $60 (~6,320 req/5h). DeepSeek V4 Flash subió a ~13,000 req/5h y Vision Exp a ~6,500 (precios más baratos). `omen-alpha` ya no está en el catálogo. Siguen disponibles `qwen3.8-flash` (~5,400 req/5h), `hy4-preview` (~1,350 req/5h) y `muse-spark-1.3-contributor`. Ojo: Qwen3.7 Max bajó su usage de $60 a $30 (~170 req/5h).

---

## Checklist post-sync

1. Abrí OpenCode → **Tab** y verificá `sdd-orchestrator-top|balanced|cheap`.
2. Corré un `/sdd-explore` chico en `cheap` para validar routing.
3. Un `/sdd-propose` en `balanced` o `top` para validar calidad de plan.
4. Confirmá en consola Go que el usage baja como esperás por fase.
