# Guía de modelos gratuitos de OpenCode Zen (Console)

> Guía práctica sobre los **modelos gratuitos** de [OpenCode Zen / Console](https://opencode.ai/docs/zen/) y cómo elegir el mejor según la tarea y el perfil: **Máxima Calidad**, **Balanceado** y **Económico**.
>
> **Revisión:** 17 de octubre de 2026 (UTC)<br>
> **Modelo usado para esta revisión:** `opencode-go/deepseek-v4.1-flash` (esfuerzo: `high`)<br>
> **Fuente primaria:** [opencode.ai/docs/zen](https://opencode.ai/docs/zen/)<br>
> **Catálogo live:** `curl -s https://opencode.ai/zen/v1/models` (o `https://opencode.ai/inference/v1/models`; el 17/10/2026 ambos devuelven la misma lista)<br>
> **Documento hermano:** [gentle-ai-profiles.md](./gentle-ai-profiles.md) — asignación de modelos a los roles de Gentle-AI

Los modelos gratuitos son **"por tiempo limitado"** y pueden retirarse sin aviso. Este documento refleja el catálogo vivo de la fecha de revisión.

---

## Índice

1. [Qué cambió desde el 13 de septiembre](#1-qué-cambió-desde-el-13-de-septiembre)
2. [¿Qué es Zen / Console?](#2-qué-es-zen--console)
3. [Lista vigente de modelos gratuitos](#3-lista-vigente-de-modelos-gratuitos)
4. [Privacidad: la decisión que importa](#4-privacidad-la-decisión-que-importa)
5. [Los tres perfiles](#5-los-tres-perfiles)
6. [Recomendación por tarea](#6-recomendación-por-tarea)
7. [Zen como respaldo de Gentle-AI](#7-zen-como-respaldo-de-gentle-ai)
8. [Cómo configurarlos](#8-cómo-configurarlos)
9. [Buenas prácticas y advertencias](#9-buenas-prácticas-y-advertencias)
10. [Deprecaciones vigentes](#10-deprecaciones-vigentes)

---

## 1. Qué cambió desde el 13 de septiembre

El catálogo gratuito cambió por completo, y esta vez **para mejor**:

- ✅ **Ahora hay modelos gratuitos con zero-retention y sin entrenamiento**: `deepseek-v4.1-flash-free`, `glm-5.3-flash-free`, `space-bunny-free`, `longcat-2.5-preview-free`. La revisión anterior concluía que *ningún* modelo gratuito era apto para código sensible; **eso ya no es cierto**.
- 🎁 **Dos gratuitos son literalmente los modelos de pago**: `deepseek-v4.1-flash-free` y `glm-5.3-flash-free` sirven gratis los mismos modelos que en Go cuestan dinero (`deepseek-v4.1-flash`, `glm-5.3-flash`) y con la misma política de privacidad.
- ➕ **Nuevos**: `beam-free`, `space-bunny-free`, `deepseek-v4.1-flash-free`, `glm-5.3-flash-free`, `longcat-2.5-preview-free`, `nemotron-3.5-super-vl-free`, `jev-1.13-free`.
- ➖ **Salieron del catálogo live**: `ling-3.0-flash-fin-free`, `nemotron-3-ultra-free`, `mimo-v2.5-free`, `muse-spark-1.3-contributor-free` (siguen documentados, pero el endpoint de modelos ya no los sirve).
- ⚠️ **`jev-1.13-free` no es un modelo de chat**: es un modelo *System One* de TypeSafe AI que evalúa estados contra preguntas tipadas y devuelve valores y probabilidades. No sirve como agente de código.

---

## 2. ¿Qué es Zen / Console?

OpenCode Console es la pasarela (gateway) de modelos curada por el equipo de OpenCode: **pay-as-you-go** por request, con créditos. "Zen" es el nombre con el que siguen viviendo sus endpoints (`/zen/v1/...`), y es el saldo que se activa con **Use balance** cuando se agota el cupo del plan Go.

A diferencia de usar un modelo vía OpenRouter u otro intermediario, acá cada combinación modelo/proveedor fue probada y evaluada para funcionar bien como **agente de código** (tool calling, ediciones multi-archivo).

Los modelos gratuitos cuestan **$0 en input, output y cache read**. Las razones por las que son gratis cambian según el modelo: algunos son *stealth* en evaluación, otros recopilan feedback, otros son endpoints *trial* de un proveedor, y los mejores simplemente siguen una política zero-retention mientras el equipo junta datos de uso agregados.

El ID de configuración en OpenCode es siempre `opencode/<model-id>`.

---

## 3. Lista vigente de modelos gratuitos

Verificado contra el catálogo live el 17/10/2026. **10 modelos** (el `test` del endpoint es una entrada espuria del catálogo).

| Modelo | Model ID | Origen | Tipo | Privacidad |
|---|---|---|---|---|
| **DeepSeek V4.1 Flash Free** | `deepseek-v4.1-flash-free` | DeepSeek | Flash code-capable | 🟢 Zero-retention, **no entrena** |
| **GLM-5.3-Flash Free** | `glm-5.3-flash-free` | GLM (Zhipu) | Flash code-oriented | 🟢 Zero-retention, **no entrena** |
| **Space Bunny Free** | `space-bunny-free` | Stealth (no revelada) | Gama alta no revelada | 🟢 Zero-retention, **no entrena** |
| **LongCat 2.5 Preview Free** | `longcat-2.5-preview-free` | LongCat (Meituan) | Generalista preview | 🟢 Zero-retention, **no entrena** |
| **Big Pickle** | `big-pickle` | Stealth (no revelada) | Gama alta en evaluación | 🟡 Datos para mejorar el modelo |
| **MiMo-V2.6-Flash Free** | `mimo-v2.6-flash-free` | MiMo (Xiaomi) | Flash de alto volumen | 🟡 Datos para mejorar el modelo |
| **Beam Free** | `beam-free` | Stealth (no revelada) | Generalista | 🟢 No entrena, retención 30 días por seguridad |
| **Nemotron 3.5 Lightning Free** | `nemotron-3.5-lightning-free` | NVIDIA | Flash de baja latencia | 🔴 Endpoint trial: uso registrado |
| **Nemotron 3.5 Super VL Free** | `nemotron-3.5-super-vl-free` | NVIDIA | **Vision-language** (multimodal) | 🔴 Endpoint trial: uso registrado |
| **Jev 1.13 Free** | `jev-1.13-free` | TypeSafe AI (System One) | **Decisiones estructuradas, no chat** | ⚪ No figura entre las excepciones de privacidad publicadas |

**Documentados pero fuera del catálogo live** (no los asignes hasta confirmarlos en `/models`): `ll-alpha-free` (🟡 feedback, retención 30 días), `exo-free` (🟡 feedback), `nemotron-3-ultra-free` (🔴 trial), `mimo-v2.5-free` (🟡 feedback), **`muse-spark-1.3-contributor-free`** (🔴🔴 cede tus prompts y completions como datos de entrenamiento de Meta).

### Endpoints

Todos los gratuitos usan `https://opencode.ai/inference/openai/v1/chat/completions` (`@ai-sdk/openai-compatible`), excepto `muse-spark-*-contributor-free` (endpoint Responses) y `jev-1.13-free` (endpoint System One). En OpenCode no necesitás armarlo a mano: `/models` te muestra lo que tu proveedor activo expone.

---

## 4. Privacidad: la decisión que importa

Como todos cuestan $0, **la privacidad es el criterio que desempata**. Estado vigente:

| Nivel | Modelos | Implicación |
|---|---|---|
| 🟢 **Apto para código privado** | `deepseek-v4.1-flash-free`, `glm-5.3-flash-free`, `space-bunny-free`, `longcat-2.5-preview-free` | Zero-retention y **sin entrenamiento** con tus datos. Podés usarlos con código propietario sin ceder entrenamiento |
| 🟢 **No entrena, retiene 30 días** | `beam-free` | Sin entrenamiento, pero retención de 30 días por seguridad. Restringido en una lista larga de países (Angola, Bielorrusia, Camboya, China incl. Hong Kong y Macao, Cuba, RDC, Guinea Ecuatorial, Irán, Irak, Laos, Libia, Nigeria, Corea del Norte, Rusia, Siria, Turkmenistán, Uzbekistán, Venezuela, y Crimea/Donetsk/Luhansk) |
| 🟡 **Recopila feedback** | `big-pickle`, `mimo-v2.6-flash-free`, `ll-alpha-free`, `exo-free`, `mimo-v2.5-free` | Durante el periodo gratuito tus conversaciones pueden usarse para mejorar el modelo. Evitá secretos, credenciales y lógica propietaria crítica |
| 🔴 **Endpoint trial registrado** | `nemotron-3.5-lightning-free`, `nemotron-3.5-super-vl-free`, `nemotron-3-ultra-free` | Endpoints *trial* de NVIDIA: el uso se registra para seguridad y para mejorar sus productos. **No enviar datos personales ni confidenciales** |
| 🔴🔴 **Entrenamiento directo** | `muse-spark-1.3-contributor-free` | A cambio de la gratuidad, cedés prompts y completions como datos de entrenamiento de Meta. **Nunca con código tuyo** |

Detalles generales: toda la infraestructura está en **US y EU**; la política por defecto de los proveedores de pago es zero-retention sin entrenamiento; **OpenAI** y **Anthropic** retienen 30 días según sus políticas; **Mistral** no entrena y retiene según su política de retención.

> **Regla práctica:** si el código es tuyo o de un cliente, trabajá con `deepseek-v4.1-flash-free`, `glm-5.3-flash-free` o `space-bunny-free`. Dejá `big-pickle` y `mimo-v2.6-flash-free` para repos públicos, spikes y experimentos.

---

## 5. Los tres perfiles

Igual que en [gentle-ai-profiles.md](./gentle-ai-profiles.md), tres perfiles según qué priorizás. Acá "calidad" es la del modelo gratis más capaz y "económico" es el que más volumen tolera (todos cuestan lo mismo: **$0**).

| Necesidad | 🥇 MÁXIMA CALIDAD | ⚖️ BALANCEADO | 💰 ECONÓMICO |
|---|---|---|---|
| **Modelo base del perfil** | `big-pickle` | `deepseek-v4.1-flash-free` | `longcat-2.5-preview-free` |
| **Alternativa principal** | `space-bunny-free` | `glm-5.3-flash-free` | `mimo-v2.6-flash-free` |
| **Planeamiento** | `big-pickle` | `space-bunny-free` | `deepseek-v4.1-flash-free` |
| **Código** | `big-pickle` | `deepseek-v4.1-flash-free` | `glm-5.3-flash-free` |
| **Refactorización** | `big-pickle` | `glm-5.3-flash-free` | `deepseek-v4.1-flash-free` |
| **Tests** | `deepseek-v4.1-flash-free` | `glm-5.3-flash-free` | `nemotron-3.5-lightning-free` |
| **Documentación** | `big-pickle` | `longcat-2.5-preview-free` | `longcat-2.5-preview-free` |
| **Exploración / volumen** | `space-bunny-free` | `longcat-2.5-preview-free` | `mimo-v2.6-flash-free` |
| **Privacidad** | 🟡 feedback | 🟢 zero-retention | 🟡/🔴 según elección |

**Cómo leer esto:**

- **Máxima calidad** apuesta a `big-pickle` (stealth de gama alta en evaluación) o `space-bunny-free` si necesitás zero-retention. Son los que mejor siguen instrucciones complejas y editan varios archivos de forma coherente.
- **Balanceado** es el perfil recomendado por defecto: `deepseek-v4.1-flash-free` y `glm-5.3-flash-free` **son los modelos de pago servidos gratis**, con tool calling probado y política zero-retention. Es la mejor relación capacidad/privacidad del catálogo gratuito.
- **Económico** prioriza volumen e ingesta larga: `longcat-2.5-preview-free` (zero-retention) y `mimo-v2.6-flash-free` (⚠️ feedback) aguantan muchas iteraciones.

---

## 6. Recomendación por tarea

> Nota honesta: OpenCode no publica benchmarks por tarea y estos modelos cambian con frecuencia. Lo que sigue combina lo que **sí** está documentado (política de privacidad, si es el mismo modelo que el de pago, si es flash o de gama alta, si es stealth o de proveedor conocido) con el comportamiento típico de cada familia. Como todos son gratis, la recomendación real es **probar 2–3 con tu proyecto y comparar**.

### Resumen rápido

| Tarea | Primera opción | Alternativa | Evitar |
|---|---|---|---|
| 🗺️ Planeamiento | `big-pickle` | `space-bunny-free`, `deepseek-v4.1-flash-free` | `nemotron-3.5-lightning-free` |
| 💻 Escritura de código | `deepseek-v4.1-flash-free` | `glm-5.3-flash-free`, `big-pickle` | `nemotron-3.5-lightning-free` |
| ♻️ Refactorización | `glm-5.3-flash-free` | `big-pickle`, `deepseek-v4.1-flash-free` | `longcat-2.5-preview-free` |
| 🧪 Tests | `glm-5.3-flash-free` | `deepseek-v4.1-flash-free`, `nemotron-3.5-lightning-free` | `nemotron-3.5-super-vl-free` |
| 📝 Documentación | `longcat-2.5-preview-free` | `big-pickle`, `glm-5.3-flash-free` | `nemotron-3.5-lightning-free` |
| 🔎 Exploración masiva | `longcat-2.5-preview-free` | `mimo-v2.6-flash-free` | `jev-1.13-free` (no es de chat) |

### 6.1 Planeamiento (arquitectura, descomposición, diseño)

**Recomendado: `big-pickle`.** Es un stealth de gama alta en evaluación: los problemas de planear exigen la mejor calidad de razonamiento disponible, y el costo es el mismo ($0). Si el repo es privado, **`space-bunny-free`** es la alternativa con zero-retention; `deepseek-v4.1-flash-free` rinde bien para planes medianos.

Evitá `nemotron-3.5-lightning-free`: sacrifica profundidad por latencia, justo lo contrario de lo que necesitás al planear.

### 6.2 Código (features, funciones, implementación)

**Recomendado: `deepseek-v4.1-flash-free`.** Es exactamente el modelo de pago `deepseek-v4.1-flash` — rápido, code-capable, con cupo de proveedor holgado — servido gratis y con zero-retention. Es la mejor opción gratuita para el ciclo escribir → correr → corregir.

Alternativas:
- **`glm-5.3-flash-free`**: el hermano gratuito de `glm-5.3-flash`, orientado a código. Cambiá a este si DeepSeek te da latencia alta en horas pico.
- **`big-pickle`**: para features grandes y difíciles donde la capacidad agéntica pesa más que la latencia (⚠️ datos de feedback).

### 6.3 Refactorización (reestructurar sin romper comportamiento)

**Recomendado: `glm-5.3-flash-free`.** Refactorizar exige entender dependencias entre archivos y no inventar APIs inexistentes; un modelo code-oriented con zero-retention es la combinación correcta.

Alternativas:
- **`big-pickle`**: para refactors grandes y delicados que atraviesan muchos módulos.
- **`deepseek-v4.1-flash-free`**: refactors acotados, con mejor latencia.

Evitá los generalistas preview para refactors estructurales: no tienen el ajuste de código.

**Consejo:** pedí primero un **plan** con el modelo de planeamiento, revisalo, y después ejecutá con el de código.

### 6.4 Tests (unitarios, integración, TDD)

**Recomendado: `glm-5.3-flash-free`.** Los tests son código con contrato explícito: conviene el modelo code-oriented, y su política zero-retention permite usarlo sobre el repo real.

Alternativas:
- **`deepseek-v4.1-flash-free`**: ciclos rápidos escribir → correr → corregir con mucho contexto repetido (su punto fuerte es el volumen).
- **`nemotron-3.5-lightning-free`**: acá sí brilla la velocidad, para lotes de tests rutinarios o casos borde derivados de una función ya definida (🔴 endpoint trial: no le pases fixtures con datos reales).

Evitá `nemotron-3.5-super-vl-free`: es un modelo vision-language; no es la herramienta para tests.

### 6.5 Documentación, guías y manuales

**Recomendado: `longcat-2.5-preview-free`.** La documentación produce mucho texto de salida, y es la tarea donde el volumen domina: un generalista preview con zero-retention y sin límite de requests es ideal.

Alternativas:
- **`big-pickle`**: para un README o un RFC donde la estructura y el estilo importan más que el volumen (⚠️ feedback).
- **`glm-5.3-flash-free`**: documentación pegada al código de la misma sesión, aprovechando el contexto ya cargado.

Evitá `nemotron-3.5-lightning-free`: privilegia velocidad sobre profundidad narrativa y la doc queda superficial.

**Consejo:** para una guía larga, pedí primero el **índice/estructura** con el modelo de planeamiento, revisalo, y después redactá cada sección con `longcat-2.5-preview-free` para mantener consistencia.

---

## 7. Zen como respaldo de Gentle-AI

Cuando se agota el cupo de Go, los gratuitos de Console son el respaldo natural de los roles del documento hermano. **Cambia el prefijo**: acá es `opencode/<id>`, no `opencode-go/<id>`.

| Rol de Gentle-AI | Respaldo gratuito | Por qué |
|---|---|---|
| `gentle-ai-explore` | `opencode/longcat-2.5-preview-free` | Lecturas masivas sin costo ni límite |
| `gentle-ai-verify` | `opencode/deepseek-v4.1-flash-free` | Ejecuta y compara con razonamiento suficiente |
| `gentle-ai-worker` | `opencode/glm-5.3-flash-free` → `opencode/deepseek-v4.1-flash-free` | Escritura de código con zero-retention |
| `review-readability` / `reliability` / `resilience` | `opencode/deepseek-v4.1-flash-free` | Volumen por lens sin costo |
| `review-risk` | `opencode/big-pickle` | Es el lens que más razonamiento exige (⚠️ feedback) |
| `review-refuter` | `opencode/space-bunny-free` | Razonamiento adversarial + zero-retention |
| `jd-judge-a` | `opencode/big-pickle` | Juez de máxima calidad |
| `jd-judge-b` | `opencode/space-bunny-free` | **Familia distinta** al juez A |
| `jd-fix-agent` | `opencode/glm-5.3-flash-free` | Parche acotado con modelo de código |
| `gentle-orchestrator` | `opencode/deepseek-v4.1-flash-free` | Cientos de llamadas: necesita latencia y cupo, no un flagship |

⚠️ **Antes de asignarlos a un rol de Gentle-AI, confirmá en `/models` que el modelo soporte tool calling**: es requisito duro de todos los roles. Los gratuitos con tool calling probado son los que sirven el mismo modelo que el de pago (`deepseek-v4.1-flash-free`, `glm-5.3-flash-free`); los stealth son la apuesta menos verificable.

---

## 8. Cómo configurarlos

### 8.1 Conectar

1. Iniciá sesión en [opencode.ai/auth](https://opencode.ai/auth) y copiá tu API key.
2. En la TUI: `/connect` → **OpenCode** (pay-as-you-go) → pegá la key.

### 8.2 Elegir en la sesión

```
/models
```

y elegí `opencode/<model-id>`. También podés arrancar directo:

```bash
opencode -m opencode/deepseek-v4.1-flash-free
```

### 8.3 Fijar uno como predeterminado

```json
{
  "$schema": "https://opencode.ai/config.json",
  "model": "opencode/glm-5.3-flash-free"
}
```

### 8.4 Cambiar según la fase de trabajo

```bash
# 1. Planear
opencode -m opencode/big-pickle
# 2. Implementar / refactorizar
opencode -m opencode/glm-5.3-flash-free
# 3. Testear e iterar
opencode -m opencode/deepseek-v4.1-flash-free
# 4. Documentar
opencode -m opencode/longcat-2.5-preview-free
```

### 8.5 Roles y subagentes de Gentle-AI

Los gratuitos también aparecen en el selector de Gentle-AI (**Configure Models**) si el proveedor `opencode` está conectado. Se persisten igual que cualquier rol:

```json
{
  "agent": {
    "gentle-ai-worker": { "model": "opencode/glm-5.3-flash-free" },
    "review-refuter":   { "model": "opencode/space-bunny-free" }
  }
}
```

---

## 9. Buenas prácticas y advertencias

1. **No mandes secretos a un modelo 🟡 o 🔴.** Con los 🟢 (`deepseek-v4.1-flash-free`, `glm-5.3-flash-free`, `space-bunny-free`, `longcat-2.5-preview-free`) el riesgo de entrenamiento desaparece, pero igual evitá `.env`, API keys y datos de clientes en el prompt.
2. **Son temporales.** No construyas CI crítico dependiendo solo de un gratuito: el catálogo cambió por completo en ~5 semanas.
3. **Verificá el código generado**, sobre todo en refactors: corré tu suite después de cada cambio.
4. **Combiná modelos por fase** (plan → code → test) en vez de usar uno solo para todo.
5. **No cambies de modelo a mitad de iteración de un archivo**: perder el cache y re-enviar el contexto es lo único que te puede costar tiempo real, incluso con modelos gratis.
6. **Nunca uses un modelo del que no sepas qué es.** `space-bunny-free` y `big-pickle` son *stealth*: identidad no revelada, pueden cambiar o desaparecer sin aviso. Si eso te incomoda, usá `deepseek-v4.1-flash-free` o `glm-5.3-flash-free`, que son modelos conocidos.
7. **Los 👁️ vision-language no son para código.** `nemotron-3.5-super-vl-free` es multimodal: útil para leer capturas y diagramas; no lo asignes como agente de implementación.
8. **`jev-1.13-free` no es un LLM de chat.** Devuelve decisiones tipadas (sí/no, opción múltiple, score) contra un `state`. Sirve para clasificar, no para escribir código.
9. **Migrar de Go a Zen es cambiar el prefijo**: `opencode-go/<id>` → `opencode/<id>`.
10. Consultá siempre la [documentación oficial](https://opencode.ai/docs/zen/) y el catálogo live antes de fijar un modelo.

### Funciones de cuenta (sin cambios)

- **Auto-recarga**: si el saldo baja de $5, Console recarga $20 (configurable o desactivable).
- **Límites mensuales**: por workspace y por miembro; con auto-recarga activo, el gasto puede superarlo cuando el saldo baja de $5.
- **Workspaces** para equipos: restricción de modelos por miembro, presupuestos y *bring-your-own-key* de OpenAI/Anthropic.
- **Comisión de tarjeta**: 4.4% + $0.30 por transacción, pasado a costo.
- OpenCode usa modelos baratos (Haiku, Nano, Flash) para generar los títulos de sesión.

---

## 10. Deprecaciones vigentes

No uses estos modelos en configuraciones nuevas (tabla oficial al 17/10/2026):

| Modelo | Fecha de deprecación |
|---|---|
| Qwen3 Coder 480B | 6 de febrero de 2026 |
| Claude Haiku 3.5 | 16 de febrero de 2026 |
| Kimi K2 · Kimi K2 Thinking | 6 de marzo de 2026 |
| Gemini 3 Pro | 9 de marzo de 2026 |
| MiniMax M2.1 · GLM 4.7 · GLM 4.6 | 15 de marzo de 2026 |
| GLM 5 | 14 de mayo de 2026 |
| Claude Sonnet 4 | 15 de junio de 2026 |
| GPT 5 Codex · GPT 5.1 Codex · GPT 5.1 Codex Max · GPT 5.1 Codex Mini · GPT 5.2 Codex | 23 de julio de 2026 |
| MiniMax M2.5 · Kimi K2.5 · Claude Opus 4.1 | 5 de agosto de 2026 |

**Ofertas temporales vigentes:** **Gemini 4 Argon** con 50% de descuento hasta el **30 de noviembre de 2026**; **Mistral Large 4** con 50% de descuento; los gratuitos de la sección 3, "por tiempo limitado".

⚠️ Ojo con la **privacidad de los de pago**: los *Contributor* (`muse-spark-1.3`, `muse-spark-1.2`, `gemini-4-argon`) tienen descuento o gratuidad a cambio de entrenar con tus prompts. En los roles de review de Gentle-AI ya están explícitamente excluidos.
