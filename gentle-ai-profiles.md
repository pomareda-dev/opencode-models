# Perfiles de modelos para Gentle-AI (OpenCode)

> **Revisión:** 17 de octubre de 2026 (UTC)<br>
> **Modelo usado para esta revisión:** `opencode-go/deepseek-v4.1-flash` (esfuerzo: `high`)<br>
> **Catálogo de referencia:** [modelos-opencode-go.md](./modelos-opencode-go.md) · [Zen gratuito](./modelos-opencode-zen.md)<br>
> **Fuentes del runtime:** [orchestrator.md](https://github.com/Gentleman-Programming/gentle-ai/blob/main/internal/assets/opencode/orchestrator.md) · [agents/](https://github.com/Gentleman-Programming/gentle-ai/tree/main/internal/assets/opencode/agents) · [docs/agents.md](https://github.com/Gentleman-Programming/gentle-ai/blob/main/docs/agents.md) · [docs/usage.md](https://github.com/Gentleman-Programming/gentle-ai/blob/main/docs/usage.md)

Este documento define **qué modelo poner en cada rol configurable de Gentle-AI** bajo tres perfiles: **Máxima Calidad**, **Balanceado** y **Económico**. Todos los IDs son de OpenCode Go (`opencode-go/<model-id>`).

---

## 0. Qué cambió respecto del documento anterior (`sdd-profiles.md`)

El documento anterior describía **perfiles SDD nombrados** (`top` / `balanced` / `cheap`) creados con `gentle-ai sync --profile … --profile-phase …`, que generaban 11 agentes `sdd-*` por perfil.

Eso **ya no existe** en `main`:

- El componente SDD y sus assets están retirados: `sync` los **migra y retira** (`retiredSDDAssetSteps`, `retiredSDDAgentSteps`, `retiredOpenCodeSDDSettingsSteps`).
- Los flags `--profile`, `--profile-phase`, `--sdd-mode` y `--sdd-profile-strategy` fueron **eliminados** (una prueba del CLI verifica que ya no aparezcan en la ayuda ni en los errores).
- Las identidades `sdd-*` sobreviven solo para **parsear estado guardado**; el propio código lo dice: *"It is not an active model-picker role list"* y *"legacy assignments are not offered for new edits"*.

Lo que **sí** se configura hoy es el conjunto de roles de ODD, Judgment Day y Review RDD (sección 1). Este documento reemplaza el contenido SDD; el histórico queda en el commit anterior del repositorio.

---

## 1. Los roles configurables hoy

El model picker de OpenCode (`ModelPickerRows`) expone exactamente estas filas, en este orden:

```
gentle-orchestrator
--- Gentle AI agents ---
  gentle-ai-explore
  gentle-ai-verify
  gentle-ai-worker
--- Judgment Day ---
  jd-judge-a
  jd-judge-b
  jd-fix-agent
--- Review agents ---
  review-risk
  review-readability
  review-reliability
  review-resilience
  review-refuter
  review-validator
--- OpenCode native agents ---
  general
  explore
--- Custom / Native agents ---
  (Set all custom agents)
  <tus agentes propios>
```

| Rol | Qué hace realmente | Qué exige del modelo |
|---|---|---|
| **gentle-orchestrator** | Conduce: decide topología, delega, resume estado, escribe el feature doc | Razonamiento de routing, seguimiento estricto de reglas, **altísima frecuencia de llamadas** |
| **gentle-ai-explore** | Explorador read-only: mapea archivos/símbolos con `codegraph_explore` y devuelve handoff ≤2k tokens | Contexto largo, comprensión de código, tool calling, volumen moderado-alto |
| **gentle-ai-verify** | Verificador read-only: derivación propia de probes, invariantes, baseline diferencial, veredicto por `S#` | Razonamiento adversarial, obediencia estricta, ejecución de comandos. Es una **compuerta** |
| **gentle-ai-worker** | Escritor: TDD RED→GREEN→PRESERVE→REFACTOR, edita repo, corre tests enfocados | Mejor capacidad de código + throughput + disciplina de scope. **Máximo volumen** |
| **jd-judge-a** | Juez A de Judgment Day: barrido adversarial ciego, salida JSON estricta | Razonamiento fuerte + formato exacto; **familia distinta de jd-judge-b** |
| **jd-judge-b** | Juez B: mismo contrato, ángulo distinto (edge cases, gaps de test, integración) | Ídem, con sesgo complementario |
| **jd-fix-agent** | Parche quirúrgico sobre hallazgos confirmados, un solo dispatch | Capability de código + disciplina de scope extremo |
| **review-risk** (R1) | Lens de seguridad: secretos hardcodeados, authz en frontend, inyección, cookies | Razonamiento de seguridad |
| **review-readability** (R2) | Lens de claridad: números mágicos, duplicación, código muerto, naming | Comprensión estructural, sin sobre-reportar |
| **review-reliability** (R3) | Lens de tests y comportamiento: contratos visibles, edge cases, determinismo | Razonamiento sobre tests |
| **review-resilience** (R4) | Lens operacional: fallbacks, retry, degradación, observabilidad, SLO | Razonamiento operativo/ops |
| **review-refuter** | Refuta claims inferenciales de los 4R | **Razonamiento adversarial de primer nivel**, independiente de la familia de los lenses |
| **review-validator** | Validación read-only post-corrección contra árboles inmutables | Comprensión de código + protocolo de inspección estricto |

Notas del runtime:

- Los **6 roles de review** se despachan como agentes OpenCode (`REVIEW_AGENTS` en `opencode-review-transport.ts`), aunque `review-refuter` y `review-validator` solo se materializan cuando el contrato nativo los pide (el refuter, por ejemplo, solo cuando hay hallazgos severos candidato-causados).
- **Judgment Day y Review son independientes entre sí** y de los roles ODD. Un cambio de perfil no toca los otros.
- `general` y `explore` son agentes nativos de OpenCode: configuralos solo si los usás.

---

## 2. Cómo se configuran

### 2.1 Vía TUI (recomendado)

```
gentle-ai  →  Model Configuration  →  Configure OpenCode models  →  <rol>  →  <proveedor/modelo>  →  <esfuerzo>
```

El picker ofrece únicamente los modelos del/los proveedores activos que soportan `tool_call` (requisito para todos estos roles).

### 2.2 Persistencia

Se escribe en `~/.config/opencode/opencode.json` (o `$XDG_CONFIG_HOME/opencode/opencode.json`):

```json
{
  "agent": {
    "gentle-ai-worker": { "model": "opencode-go/kimi-k2.7-code" },
    "review-risk":      { "model": "opencode-go/glm-5.3", "variant": "high" }
  }
}
```

- `model` acepta `provider/modelo` o el selector expandido `provider/modelo#variante`.
- `variant` es el **esfuerzo de razonamiento** (`low`/`medium`/`high`/`xhigh`) cuando el modelo los expone.
- Editar el JSON a mano es válido y se preserva; si además elegís un modelo desde el picker para ese rol, la elección del picker manda.
- El orquestador lee `agent.gentle-orchestrator.model` del `opencode.json`; el resto del trabajo delegado usa el modelo configurado del agente o el default del runtime.

### 2.3 Qué **no** configura este picker

- No hay perfiles nombrados ni un flag que aplique un tier completo: cada tier de este documento es un **conjunto curado de asignaciones por rol**.
- Los roles `sdd-*` retirados no se ofrecen para roles nuevos.

---

## 3. Criterios de asignación

Cinco reglas gobiernan las recomendaciones:

1. **Planear y juzgar caro, ejecutar y explorar barato.** Los roles que se corren una vez por cambio (verify, judges, refuter, validator) pueden pagar un modelo de $15. Los que se corren en volumen (worker, explore, lenses) necesitan cupo real.
2. **El cupo es por modelo, no por rol.** Si 7 roles apuntan al mismo modelo de ~220 req/5h, se pelean el mismo bucket. En el tier de máxima calidad los flagships se **reparten** entre roles en lugar de apilarse.
3. **Diversidad real donde el contrato la exige.** `jd-judge-a` y `jd-judge-b` deben ser de **familias distintas** (ceguera + sesgos complementarios); el refuter debe ser de familia distinta a la de los lenses.
4. **Privacidad.** Ningún rol que lea código privado puede usar modelos que entrenen con tus prompts: **excluí `gemini-4-argon-contributor` y `muse-spark-1.2/1.3-contributor`** de todos los roles de este documento.
5. **El cache read manda en sesiones largas.** En agentes con contexto grande, la mayor parte del consumo es cache read, no salida: `MiMo-V2.6-Flash` ($0.0028), `DeepSeek V4.1 Flash` ($0.003), `LongCat-2.0` ($0.006), `Qwen3.8 Flash` ($0.016) contra $0.19–$0.50 en los premium.

---

## 4. Perfil MÁXIMA CALIDAD (`calidad`)

Máximo razonamiento por rol, con los flagships **repartidos** para no agotar un cupo de ~220 req/5h con siete roles.

| Rol | Modelo | ID | req/5h | Por qué |
|---|---|---|---|---|
| **gentle-orchestrator** | GLM-5.3 | `opencode-go/glm-5.3` | ~220 | Mejor routing de la generación; pocas llamadas de alto impacto por decisión |
| **gentle-ai-explore** | Kimi K2.7 Code | `opencode-go/kimi-k2.7-code` | ~1,350 | Explorar código no necesita flagship: necesita code-specialized + cupo |
| **gentle-ai-verify** | GLM-5.3 | `opencode-go/glm-5.3` | ~220 | Compuerta adversarial; se corre una vez por cambio |
| **gentle-ai-worker** | Kimi K2.7 Code | `opencode-go/kimi-k2.7-code` | ~1,350 | El mejor code-specialized con cupo suficiente para implementar y testear |
| **jd-judge-a** | Kimi K3 | `opencode-go/kimi-k3` | ~110 | Flagship de razonamiento; salida JSON corta, el costo de salida no pesa |
| **jd-judge-b** | Qwen3.8 Max | `opencode-go/qwen3.8-max` | ~160 | Familia distinta a K3 → sesgo distinto |
| **jd-fix-agent** | Kimi K2.7 Code | `opencode-go/kimi-k2.7-code` | ~1,350 | Parche quirúrgico: capability de código por encima de todo |
| **review-risk** (R1) | GLM-5.3 | `opencode-go/glm-5.3` | ~220 | El lens más exigente en razonamiento |
| **review-readability** (R2) | Qwen3.8 Max | `opencode-go/qwen3.8-max` | ~160 | Claridad estructural con juicio de techo |
| **review-reliability** (R3) | DeepSeek V4 Pro | `opencode-go/deepseek-v4-pro` | ~1,050 | Razonamiento sobre tests con cupo holgado |
| **review-resilience** (R4) | Grok 4.7 | `opencode-go/grok-4.7` | ~169 | Ángulo operacional distinto, otra familia |
| **review-refuter** | Kimi K3 | `opencode-go/kimi-k3` | ~110 | Refutar claims inferenciales es la tarea de máxima exigencia |
| **review-validator** | GLM-5.3 | `opencode-go/glm-5.3` | ~220 | Validación final del árbol congelado |

**Uso estimado:** alto. Un ciclo completo con review de 4 lenses consume ~6–8 requests de modelos de $15, más las llamadas propias del orquestador.

⚠️ **El punto frágil de este perfil es el orquestador.** GLM-5.3 tiene ~220 req/5h y el orquestador es el que más llamadas hace. Si trabajás sesiones largas, el primer ajuste es bajar `gentle-orchestrator` a **GLM-5.2** (`~880 req/5h`) y dejar GLM-5.3 para verify/lenses/validator. Es la diferencia entre "una corrida de máxima calidad por ventana" y "varias".

**Alternativas:**

| Rol | Alternativa |
|---|---|
| orchestrator | `opencode-go/glm-5.2` (por cupo) · `opencode-go/kimi-k3` |
| worker / explore | `opencode-go/glm-5.3` (más razonamiento, 1/6 del cupo) |
| judge-a / refuter | `opencode-go/glm-5.3` · `opencode-go/grok-4.7` |
| lenses | es válido poner **los 4 en el mismo modelo** (mismo prompt family, distinto mandato); repartirlos agrega diversidad y reparte cupo |
| validator | `opencode-go/qwen3.8-max` · `opencode-go/deepseek-v4-pro` |

```json
{
  "agent": {
    "gentle-orchestrator": { "model": "opencode-go/glm-5.3" },
    "gentle-ai-explore":   { "model": "opencode-go/kimi-k2.7-code" },
    "gentle-ai-verify":    { "model": "opencode-go/glm-5.3" },
    "gentle-ai-worker":    { "model": "opencode-go/kimi-k2.7-code" },
    "jd-judge-a":          { "model": "opencode-go/kimi-k3" },
    "jd-judge-b":          { "model": "opencode-go/qwen3.8-max" },
    "jd-fix-agent":        { "model": "opencode-go/kimi-k2.7-code" },
    "review-risk":         { "model": "opencode-go/glm-5.3" },
    "review-readability":  { "model": "opencode-go/qwen3.8-max" },
    "review-reliability":  { "model": "opencode-go/deepseek-v4-pro" },
    "review-resilience":   { "model": "opencode-go/grok-4.7" },
    "review-refuter":      { "model": "opencode-go/kimi-k3" },
    "review-validator":    { "model": "opencode-go/glm-5.3" }
  }
}
```

---

## 5. Perfil BALANCEADO (`balanceado`) — daily driver

Mejor relación calidad/cupo: casi todo el ciclo entra cómodo en los límites de Go.

| Rol | Modelo | ID | req/5h | Por qué |
|---|---|---|---|---|
| **gentle-orchestrator** | GLM-5.2 | `opencode-go/glm-5.2` | ~880 | Excelente routing con cupo para un orquestador que llama todo el día |
| **gentle-ai-explore** | Kimi K2.7 Code | `opencode-go/kimi-k2.7-code` | ~1,350 | Exploración code-first |
| **gentle-ai-verify** | DeepSeek V4 Pro | `opencode-go/deepseek-v4-pro` | ~1,050 | Detección de gaps de spec sin pagar flagship |
| **gentle-ai-worker** | DeepSeek V4.1 Flash | `opencode-go/deepseek-v4.1-flash` | ~34,670 | El mayor cupo del catálogo ($80) con buena calidad de código |
| **jd-judge-a** | Qwen3.7 Plus | `opencode-go/qwen3.7-plus` | ~4,300 | Razonamiento sólido + cupo masivo, familia Anthropic API |
| **jd-judge-b** | MiniMax M3 | `opencode-go/minimax-m3` | ~3,200 | Familia distinta a Qwen → diversidad real |
| **jd-fix-agent** | DeepSeek V4.1 Flash | `opencode-go/deepseek-v4.1-flash` | ~34,670 | Parches chicos y bounded, muchas veces |
| **review-risk** (R1) | Kimi K2.7 Code | `opencode-go/kimi-k2.7-code` | ~1,350 | Code-specialized para leer el diff con criterio |
| **review-readability** (R2) | Kimi K2.7 Code | `opencode-go/kimi-k2.7-code` | ~1,350 | Ídem |
| **review-reliability** (R3) | Kimi K2.7 Code | `opencode-go/kimi-k2.7-code` | ~1,350 | Ídem |
| **review-resilience** (R4) | Kimi K2.7 Code | `opencode-go/kimi-k2.7-code` | ~1,350 | Ídem (4 requests por review sobre el mismo bucket) |
| **review-refuter** | DeepSeek V4 Pro | `opencode-go/deepseek-v4-pro` | ~1,050 | Independiente de la familia de los lenses + razonamiento fuerte |
| **review-validator** | Qwen3.7 Plus | `opencode-go/qwen3.7-plus` | ~4,300 | Validación final barata y sólida |

**Uso estimado:** medio. `explore` + los 4 lenses comparten `kimi-k2.7-code` (~1,350): un review consume 4 requests de ese bucket, así que entran varios candidatos por ventana. `deepseek-v4.1-flash` sostiene el volumen de implementación.

**Alternativas:**

| Rol | Alternativa |
|---|---|
| orchestrator | `opencode-go/deepseek-v4.1-flash` (más cupo, menos finura) |
| worker | `opencode-go/minimax-m3` (mejor código, 1/10 del cupo) · `opencode-go/glm-5.3-flash` |
| lenses | `opencode-go/deepseek-v4.1-flash` (máximo volumen) · `opencode-go/qwen3.8-flash` |
| refuter | `opencode-go/hy4-preview` · `opencode-go/space-bunny` (otra familia, $30) |
| judge-b | `opencode-go/hy3` · `opencode-go/deepseek-v4.1-flash` |

```json
{
  "agent": {
    "gentle-orchestrator": { "model": "opencode-go/glm-5.2" },
    "gentle-ai-explore":   { "model": "opencode-go/kimi-k2.7-code" },
    "gentle-ai-verify":    { "model": "opencode-go/deepseek-v4-pro" },
    "gentle-ai-worker":    { "model": "opencode-go/deepseek-v4.1-flash" },
    "jd-judge-a":          { "model": "opencode-go/qwen3.7-plus" },
    "jd-judge-b":          { "model": "opencode-go/minimax-m3" },
    "jd-fix-agent":        { "model": "opencode-go/deepseek-v4.1-flash" },
    "review-risk":         { "model": "opencode-go/kimi-k2.7-code" },
    "review-readability":  { "model": "opencode-go/kimi-k2.7-code" },
    "review-reliability":  { "model": "opencode-go/kimi-k2.7-code" },
    "review-resilience":   { "model": "opencode-go/kimi-k2.7-code" },
    "review-refuter":      { "model": "opencode-go/deepseek-v4-pro" },
    "review-validator":    { "model": "opencode-go/qwen3.7-plus" }
  }
}
```

---

## 6. Perfil ECONÓMICO (`economico`)

Máximo throughput con calidad suficiente. No lo uses para contratos de producción sin review humano fuerte.

| Rol | Modelo | ID | req/5h | Por qué |
|---|---|---|---|---|
| **gentle-orchestrator** | Qwen3.7 Plus | `opencode-go/qwen3.7-plus` | ~4,300 | Routing decente y baratísimo por request |
| **gentle-ai-explore** | DeepSeek V4.1 Flash | `opencode-go/deepseek-v4.1-flash` | ~34,670 | Muchísimas lecturas e iteraciones, cache read $0.003 |
| **gentle-ai-verify** | Qwen3.7 Plus | `opencode-go/qwen3.7-plus` | ~4,300 | Verificación liviana pero útil |
| **gentle-ai-worker** | GLM-5.3-Flash | `opencode-go/glm-5.3-flash` | ~6,320 | Code-oriented a $0.15/$0.50, el mejor punto calidad/precio para escribir |
| **jd-judge-a** | Qwen3.7 Plus | `opencode-go/qwen3.7-plus` | ~4,300 | Juez barato de otra familia |
| **jd-judge-b** | DeepSeek V4.1 Flash | `opencode-go/deepseek-v4.1-flash` | ~34,670 | Familia distinta a Qwen |
| **jd-fix-agent** | GLM-5.3-Flash | `opencode-go/glm-5.3-flash` | ~6,320 | Fix acotado con modelo de código |
| **review-risk** (R1) | DeepSeek V4.1 Flash | `opencode-go/deepseek-v4.1-flash` | ~34,670 | Rápido y masivo |
| **review-readability** (R2) | DeepSeek V4.1 Flash | `opencode-go/deepseek-v4.1-flash` | ~34,670 | Ídem |
| **review-reliability** (R3) | DeepSeek V4.1 Flash | `opencode-go/deepseek-v4.1-flash` | ~34,670 | Ídem |
| **review-resilience** (R4) | DeepSeek V4.1 Flash | `opencode-go/deepseek-v4.1-flash` | ~34,670 | Ídem |
| **review-refuter** | Qwen3.7 Plus | `opencode-go/qwen3.7-plus` | ~4,300 | El rol que más razonamiento necesita en este tier |
| **review-validator** | DeepSeek V4.1 Flash | `opencode-go/deepseek-v4.1-flash` | ~34,670 | Validación barata |

**Uso estimado:** bajo. Podés correr varios ciclos ODD por día. Un review de 4 lenses + refuter + validator consume ~6 requests sobre buckets de 34,670.

⚠️ **DeepSeek cobra tarifa peak** (01:00–04:00 y 06:00–10:00 UTC, lunes a viernes): el resto —incluidos todos los fines de semana— es off-peak y **cuesta la mitad**. Si tu ventana de trabajo cae en peak, `deepseek-v4.1-flash` deja de ser el más barato y conviene `MiMo-V2.6-Flash` (30,100 req/5h, $0.0028 de cache read) para explore/lenses.

**Alternativas:**

| Rol | Alternativa |
|---|---|
| worker / fix | `opencode-go/mimo-v2.6-flash` (30,100 req/5h) · `opencode-go/longcat-2.0` |
| explore / lenses | `opencode-go/mimo-v2.6-flash` · `opencode-go/qwen3.8-flash` |
| orchestrator / verify | `opencode-go/deepseek-v4.1-flash` · `opencode-go/glm-5.3-flash` |
| último recurso | `opencode-go/longcat-2.5-preview-free` y `opencode-go/beam-free` (gratis temporal, regiones limitadas) |

```json
{
  "agent": {
    "gentle-orchestrator": { "model": "opencode-go/qwen3.7-plus" },
    "gentle-ai-explore":   { "model": "opencode-go/deepseek-v4.1-flash" },
    "gentle-ai-verify":    { "model": "opencode-go/qwen3.7-plus" },
    "gentle-ai-worker":    { "model": "opencode-go/glm-5.3-flash" },
    "jd-judge-a":          { "model": "opencode-go/qwen3.7-plus" },
    "jd-judge-b":          { "model": "opencode-go/deepseek-v4.1-flash" },
    "jd-fix-agent":        { "model": "opencode-go/glm-5.3-flash" },
    "review-risk":         { "model": "opencode-go/deepseek-v4.1-flash" },
    "review-readability":  { "model": "opencode-go/deepseek-v4.1-flash" },
    "review-reliability":  { "model": "opencode-go/deepseek-v4.1-flash" },
    "review-resilience":   { "model": "opencode-go/deepseek-v4.1-flash" },
    "review-refuter":      { "model": "opencode-go/qwen3.7-plus" },
    "review-validator":    { "model": "opencode-go/deepseek-v4.1-flash" }
  }
}
```

---

## 7. Comparación rápida

| Rol | MÁXIMA CALIDAD | BALANCEADO | ECONÓMICO |
|---|---|---|---|
| gentle-orchestrator | GLM-5.3 | GLM-5.2 | Qwen3.7 Plus |
| gentle-ai-explore | Kimi K2.7 Code | Kimi K2.7 Code | DeepSeek V4.1 Flash |
| gentle-ai-verify | GLM-5.3 | DeepSeek V4 Pro | Qwen3.7 Plus |
| gentle-ai-worker | Kimi K2.7 Code | DeepSeek V4.1 Flash | GLM-5.3-Flash |
| jd-judge-a | Kimi K3 | Qwen3.7 Plus | Qwen3.7 Plus |
| jd-judge-b | Qwen3.8 Max | MiniMax M3 | DeepSeek V4.1 Flash |
| jd-fix-agent | Kimi K2.7 Code | DeepSeek V4.1 Flash | GLM-5.3-Flash |
| review-risk | GLM-5.3 | Kimi K2.7 Code | DeepSeek V4.1 Flash |
| review-readability | Qwen3.8 Max | Kimi K2.7 Code | DeepSeek V4.1 Flash |
| review-reliability | DeepSeek V4 Pro | Kimi K2.7 Code | DeepSeek V4.1 Flash |
| review-resilience | Grok 4.7 | Kimi K2.7 Code | DeepSeek V4.1 Flash |
| review-refuter | Kimi K3 | DeepSeek V4 Pro | Qwen3.7 Plus |
| review-validator | GLM-5.3 | Qwen3.7 Plus | DeepSeek V4.1 Flash |

Todos los IDs llevan el prefijo `opencode-go/`.

---

## 8. Esfuerzo de razonamiento (`variant`)

Cuando el modelo expone variantes, el picker permite fijarlas. Guía por tipo de rol:

| Grupo de roles | Esfuerzo sugerido | Motivo |
|---|---|---|
| orchestrator | `medium` / `high` | Routing: más esfuerzo ayuda, pero es el rol que más llama |
| explore, lenses `readability` | `low` / `medium` | Volumen; el mandato del lens ya acota el trabajo |
| worker, fix-agent | `medium` / `high` | Código con TDD y verificación propia |
| verify, judges, refuter, validator, `risk`/`reliability`/`resilience` | `high` / `xhigh` | Son compuertas y juicios adversariales: acá el esfuerzo rinde |

Detalles operativos:

- Las variantes disponibles se refrescan con el plugin `model-variants.ts` hacia `~/.gentle-ai/cache/model-variants.json`. Después de sincronizar, abrí OpenCode una vez para llenar la caché y volvé a abrir el selector.
- Si la caché no existe, se usa el esfuerzo predeterminado del proveedor.
- Omitir `variant` en un rol ya configurado **preserva** el valor existente; elegir un esfuerzo explícito lo reemplaza.

---

## 9. Reglas transversales

1. **Dos jueces, dos familias.** `jd-judge-a` y `jd-judge-b` deben usar modelos de familias distintas; si compartís modelo perdés la ceguera. Lo mismo aplica al refuter respecto de los lenses (por eso en este documento el refuter nunca comparte modelo con los 4R).
2. **Los 4 lenses pueden compartir modelo** (mismo prompt family, distinto mandato) o repartirse; repartir agrega diversidad y reparte cupo, compartir simplifica la lectura del consumo.
3. **Nunca pongas un modelo de $15 en el rol de volumen.** El worker y explore necesitan cientos de requests; los buckets de $15 (~110–1,050 req/5h) se agotan en una tarde.
4. **Privacidad ≠ negociable.** Ningún rol que lea código privado con `gemini-4-argon-contributor` ni `muse-spark-1.2/1.3-contributor`.
5. **Modelos retirados: no volver a ellos.** `kimi-k2.6`, `deepseek-v4-flash`, `grok-4.6` y `minimax-m2.7` salieron de la lista oficial aunque algunos sigan apareciendo como legados en el catálogo live; van a desaparecer sin aviso.
6. **Base conductor y roles son independientes.** `gentle-orchestrator` es el único conductor; no hay `sdd-orchestrator-{name}` ni perfiles nombrados que lo reemplacen.
7. **Cupo agotado:** activá **Use balance** (Zen) en la consola, o pasá explore/lenses a `longcat-2.0` / `mimo-v2.6-flash`, o a los gratuitos temporales.

---

## 10. Verificación post-configuración

1. `gentle-ai doctor` → diagnóstico read-only de la instalación.
2. `gentle-ai sync --dry-run` → previsualizá qué se escribiría sin tocar nada.
3. Abrí OpenCode → **Configure Models** y verificá que las filas de la sección 1 estén todas asignadas y que **judge A y judge B sean de familias distintas**.
4. Corré un cambio chico end-to-end: delegá un `gentle-ai-explore`, mirá el handoff, y después un `gentle-ai-worker` con TDD.
5. Si tenés RDD habilitado, corré un review de un candidato chico y confirmá en la consola Go que el consumo por lens es el esperado.
6. Si tocás Judgment Day, confirmá que `jd-judge-a ≠ jd-judge-b` **y** que `jd-fix-agent` tiene capability de código.

---

## 11. Notas operativas del catálogo (17 oct 2026)

- **Cupos y precios cambian.** Este documento usa los `req/5h` y precios de [modelos-opencode-go.md](./modelos-opencode-go.md); confirmá el ID exacto en el selector antes de fijarlo.
- Modelos con límite mensual de **$15** (Kimi K3, GLM-5.3, Qwen3.8 Max, Grok 4.7, DeepSeek V4 Pro, GPT 6/5.6 Luna, Claude Haiku 5.5, MiMo-V2.6-Pro/V2.5-Pro): agotan rápido. Reservalos para roles de una sola corrida por cambio.
- **Subagentes en segundo plano** (OpenCode nativo, permiso `task`): `--opencode-background-subagents=auto|on|off`, o `GENTLE_AI_OPENCODE_BACKGROUND_SUBAGENTS`. Son locales al proceso, no sobreviven un reinicio y no aíslan el filesystem: usalos solo para trabajo read-only independiente, nunca para escritores en paralelo en el mismo worktree.
- **DeepSeek ZDR**: el acuerdo publicado rige hasta el **31 de octubre de 2026** y se renueva mensualmente; involucra a `deepseek-v4-pro` y `deepseek-v4.1-flash`.
- Los IDs de este documento usan la convención `opencode-go/<model-id>` vista en el catálogo Go. Los modelos gratuitos de Zen usan `opencode/<model-id>` (ver [modelos-opencode-zen.md](./modelos-opencode-zen.md)).
- Las recomendaciones combinan el posicionamiento de cada modelo en el catálogo con la naturaleza de cada rol. **No son benchmarks**: son un punto de partida defendible que conviene medir contra tu propio consumo.
