# Guía de modelos gratuitos de OpenCode Zen (Console)

> Guía práctica sobre los **modelos gratuitos** de [OpenCode Zen / Console](https://opencode.ai/docs/zen/) y cómo elegir el mejor según la tarea y el perfil: **Máxima Calidad**, **Balanceado** y **Económico**.
>
> **Revisión:** 13 de noviembre de 2026 (UTC)<br>
> **Modelo usado para esta revisión:** `opencode-go/qwen3.8-max`<br>
> **Fuente primaria:** [opencode.ai/docs/zen](https://opencode.ai/docs/zen/)<br>
> **Catálogo live:** `curl -s https://opencode.ai/zen/v1/models` (o `https://opencode.ai/inference/v1/models`; el 13/11/2026 ambos devuelven la misma lista)<br>
> **Documento hermano:** [gentle-ai-profiles.md](./gentle-ai-profiles.md) — asignación de modelos a los roles de Gentle-AI

Los modelos gratuitos son **"por tiempo limitado"** y pueden retirarse sin aviso. Este documento refleja el catálogo vivo de la fecha de revisión.

---

## Índice

1. [Qué cambió desde el 17 de octubre](#1-qué-cambió-desde-el-17-de-octubre)
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

## 1. Qué cambió desde el 17 de octubre

Otra rotación fuerte del catálogo gratuito en menos de un mes:

- ➕ **Cuatro gratuitos nuevos**: `minimax-m3.1-flash-free` (🟢 zero-retention, coding "frontera" con 1M de contexto — es el gemelo gratis del MiniMax M3.1 Flash de pago de Go), `iceman-free` (stealth, 🟡 feedback), `flint-40b-free` (open-weight MoE de ~2.5B activos, 🟡 feedback) e `inkling-2-small-free` (Thinking Machines, 🔴🔴 **puede entrenar con tus datos**).
- 🔄 **`longcat-2.5-preview-free` pasó a ser `longcat-2.5-free`** y perdió el carácter ilimitado: ahora tiene **100 requests por día** y está **hosteado en China**. Sigue siendo zero-retention.
- ➖ **`space-bunny-free` desapareció** del catálogo live, y con él todo Space Bunny (también el de pago). `jev-1.13-free` ya no figura en el endpoint de modelos (sigue documentado como System One).
- 💳 **El catálogo de pago de Console creció mucho**: GPT 6 Astra / 6 Sol / 6.1 Sol, Claude Fable 5.2 y Sonnet 5.5, Gemini 4 Carbon e Hydrogen, Muse Ember 1.0 y Wonder 1.0, entre otros. Gemini 4 Argon en Zen ya **no** es versión *Contributor*.
- 💰 **La comisión de tarjeta subió**: ahora es **4.6% + $0.31** por recarga (antes 4.4% + $0.30).
- 🙈 **Nuevo switch**: `OPENCODE_DISABLE_FREE_MODELS=1` oculta los gratuitos en OpenCode.

---

## 2. ¿Qué es Zen / Console?

OpenCode Console es la pasarela (gateway) de modelos curada por el equipo de OpenCode: **pay-as-you-go** por request, con créditos. "Zen" es el nombre con el que siguen viviendo sus endpoints (`/zen/v1/...`), y es el saldo que se activa con **Extra Usage / Use balance** cuando se agota el cupo del plan Go.

A diferencia de usar un modelo vía OpenRouter u otro intermediario, acá cada combinación modelo/proveedor fue probada y evaluada para funcionar bien como **agente de código** (tool calling, ediciones multi-archivo).

Los modelos gratuitos cuestan **$0 en input, output y cache read**. Las razones por las que son gratis cambian según el modelo: algunos son *stealth* en evaluación, otros recopilan feedback, otros son endpoints *trial* de un proveedor, y los mejores simplemente siguen una política zero-retention mientras el equipo junta datos de uso agregados.

El ID de configuración en OpenCode es siempre `opencode/<model-id>`.

---

## 3. Lista vigente de modelos gratuitos

Verificado contra el catálogo live el 13/11/2026. **12 modelos**, y los 12 declaran soporte de tool calling.

| Modelo | Model ID | Origen | Tipo | Contexto | Privacidad |
|---|---|---|---|---|---|
| **DeepSeek V4.1 Flash Free** | `deepseek-v4.1-flash-free` | DeepSeek | Flash code-capable (mismo modelo que el de pago) | 200K | 🟢 Zero-retention, **no entrena** |
| **GLM-5.3-Flash Free** | `glm-5.3-flash-free` | GLM (Zhipu) | Flash code-oriented (mismo modelo que el de pago) | 200K | 🟢 Zero-retention, **no entrena** |
| **MiniMax M3.1 Flash Free** | `minimax-m3.1-flash-free` | MiniMax | Coding frontera multimodal (mismo modelo que el de pago) | 1M | 🟢 Zero-retention, **no entrena** |
| **LongCat 2.5 Free** | `longcat-2.5-free` | LongCat (Meituan) | Razonamiento multimodal, **100 req/día** | 1M | 🟢 Zero-retention, **no entrena** (hosteado en China) |
| **Beam Free** | `beam-free` | Stealth (no revelada) | Razonamiento MoE (23B activos) | 1M | 🟢 No entrena, retención 30 días por seguridad |
| **Big Pickle** | `big-pickle` | Stealth (no revelada) | Razonamiento deliberado, multi-paso y tool use | 200K | 🟡 Datos para mejorar el modelo |
| **Iceman Free** | `iceman-free` | Stealth (no revelada) | Gama alta en evaluación | 262K | 🟡 Datos retenidos y usados para mejorar el modelo |
| **Flint 40B Free** | `flint-40b-free` | Open-weight | MoE pequeño (~2.5B activos) | 262K | 🟡 Feedback, retención 30 días |
| **MiMo-V2.6-Flash Free** | `mimo-v2.6-flash-free` | MiMo (Xiaomi) | Flash multimodal de alto volumen | 200K | 🟡 Datos para mejorar el modelo |
| **Nemotron 3.5 Lightning Free** | `nemotron-3.5-lightning-free` | NVIDIA | Flash de baja latencia | 262K | 🔴 Endpoint trial: uso registrado |
| **Nemotron 3.5 Super VL Free** | `nemotron-3.5-super-vl-free` | NVIDIA | **Vision-language** (multimodal) | 1M | 🔴 Endpoint trial: uso registrado |
| **Inkling 2 Small Free** | `inkling-2-small-free` | Thinking Machines | Small de 1M de contexto | 1M | 🔴🔴 Retenido y **puede usarse para entrenamiento** |

**Documentados pero fuera del catálogo live** (no los asignes hasta confirmarlos en `/models`): `jev-1.13-free` (endpoint System One de TypeSafe AI; decisiones tipadas, **no es un modelo de chat**) y `nemotron-3-ultra-free` (🔴 trial). `muse-spark-*-contributor-free` ya no existe en ninguna lista.

### Endpoints

Todos los gratuitos del catálogo live usan `https://opencode.ai/inference/openai/v1/chat/completions` (`@ai-sdk/openai-compatible`). El documentado `jev-1.13-free` usa el endpoint System One (`/inference/systemone/v1/systemone`). En OpenCode no necesitás armarlo a mano: `/models` te muestra lo que tu proveedor activo expone.

---

## 4. Privacidad: la decisión que importa

Como todos cuestan $0, **la privacidad es el criterio que desempata**. Estado vigente:

| Nivel | Modelos | Implicación |
|---|---|---|
| 🟢 **Apto para código privado** | `deepseek-v4.1-flash-free`, `glm-5.3-flash-free`, `minimax-m3.1-flash-free`, `longcat-2.5-free` | Zero-retention y **sin entrenamiento** con tus datos. Ojo con `longcat-2.5-free`: está **hosteado en China** y tiene 100 req/día; si el hosting en China es un problema para tu proyecto, usá los otros tres |
| 🟢 **No entrena, retiene 30 días** | `beam-free` | Sin entrenamiento, pero retención de 30 días por seguridad. Restringido en una lista larga de países (Angola, Bielorrusia, Camboya, China incl. Hong Kong y Macao, Cuba, RDC, Guinea Ecuatorial, Irán, Irak, Laos, Libia, Nigeria, Corea del Norte, Rusia, Siria, Turkmenistán, Uzbekistán, Venezuela, y Crimea/Donetsk/Luhansk) |
| 🟡 **Recopila feedback** | `big-pickle`, `iceman-free`, `flint-40b-free` (retención 30 días), `mimo-v2.6-flash-free` | Durante el periodo gratuito tus conversaciones pueden usarse para mejorar el modelo. Evitá secretos, credenciales y lógica propietaria crítica |
| 🔴 **Endpoint trial registrado** | `nemotron-3.5-lightning-free`, `nemotron-3.5-super-vl-free`, `nemotron-3-ultra-free` (documentado) | Endpoints *trial* de NVIDIA: el uso se registra para seguridad y para mejorar sus productos. **No enviar datos personales ni confidenciales** |
| 🔴🔴 **Entrenamiento posible** | `inkling-2-small-free` | Thinking Machines retiene tus datos y **puede usarlos para monitoreo de rendimiento real y entrenamiento** (free research API tier). Además no está disponible en la Unión Europea, Islandia, Liechtenstein, Noruega, Cuba, Irán, Corea del Norte, Rusia, Ucrania ni Venezuela. **Nunca con código propio o de clientes** |

Detalles generales: toda la infraestructura está en **US y EU** (excepción: `longcat-2.5-free` en China); la política por defecto de los proveedores de pago es zero-retention sin entrenamiento; **OpenAI** y **Anthropic** retienen 30 días según sus políticas; **Mistral** no entrena y retiene según su política de retención.

> **Regla práctica:** si el código es tuyo o de un cliente, trabajá con `deepseek-v4.1-flash-free`, `glm-5.3-flash-free` o `minimax-m3.1-flash-free`. Dejá `big-pickle`, `iceman-free` y `mimo-v2.6-flash-free` para repos públicos, spikes y experimentos, e `inkling-2-small-free` solo para pruebas sin nada sensible.

---

## 5. Los tres perfiles

Igual que en [gentle-ai-profiles.md](./gentle-ai-profiles.md), tres perfiles según qué priorizás. Acá "calidad" es la del modelo gratis más capaz y "económico" es el que más volumen tolera (todos cuestan lo mismo: **$0**).

| Necesidad | 🥇 MÁXIMA CALIDAD | ⚖️ BALANCEADO | 💰 ECONÓMICO |
|---|---|---|---|
| **Modelo base del perfil** | `big-pickle` | `deepseek-v4.1-flash-free` | `mimo-v2.6-flash-free` |
| **Alternativa principal** | `minimax-m3.1-flash-free` | `glm-5.3-flash-free` | `flint-40b-free` |
| **Planeamiento** | `big-pickle` | `minimax-m3.1-flash-free` | `deepseek-v4.1-flash-free` |
| **Código** | `minimax-m3.1-flash-free` | `deepseek-v4.1-flash-free` | `glm-5.3-flash-free` |
| **Refactorización** | `minimax-m3.1-flash-free` | `glm-5.3-flash-free` | `deepseek-v4.1-flash-free` |
| **Tests** | `deepseek-v4.1-flash-free` | `glm-5.3-flash-free` | `nemotron-3.5-lightning-free` |
| **Documentación** | `big-pickle` | `longcat-2.5-free` | `beam-free` |
| **Exploración / volumen** | `iceman-free` | `beam-free` | `mimo-v2.6-flash-free` |
| **Privacidad** | 🟡 / 🟢 mixto | 🟢 zero-retention | 🟡 / 🔴 según elección |

**Cómo leer esto:**

- **Máxima calidad** apuesta a `big-pickle` (stealth de razonamiento deliberado) cuando el repo no es sensible, o a `minimax-m3.1-flash-free` cuando necesitás zero-retention: es el modelo coding "frontera" de MiniMax con 1M de contexto, servido gratis. `iceman-free` es la tercera pata stealth para explorar.
- **Balanceado** sigue siendo el perfil recomendado por defecto: `deepseek-v4.1-flash-free`, `glm-5.3-flash-free` y ahora también `minimax-m3.1-flash-free` **son los modelos de pago servidos gratis**, con tool calling probado y política zero-retention. Es la mejor relación capacidad/privacidad del catálogo gratuito.
- **Económico** prioriza volumen: `mimo-v2.6-flash-free` y `flint-40b-free` (⚠️ ambos 🟡 feedback) aguantan muchas iteraciones; `beam-free` (🟢, 1M de contexto, sin límite diario) es la opción de volumen que sí admite código privado. Ojo: `longcat-2.5-free` ya **no** es el campeón de volumen — tiene 100 requests por día.

---

## 6. Recomendación por tarea

> Nota honesta: OpenCode no publica benchmarks por tarea y estos modelos cambian con frecuencia. Lo que sigue combina lo que **sí** está documentado (política de privacidad, si es el mismo modelo que el de pago, si es flash o de gama alta, si es stealth o de proveedor conocido) con el comportamiento típico de cada familia. Como todos son gratis, la recomendación real es **probar 2–3 con tu proyecto y comparar**.

### Resumen rápido

| Tarea | Primera opción | Alternativa | Evitar |
|---|---|---|---|
| 🗺️ Planeamiento | `big-pickle` | `iceman-free`, `minimax-m3.1-flash-free` | `nemotron-3.5-lightning-free` |
| 💻 Escritura de código | `deepseek-v4.1-flash-free` | `minimax-m3.1-flash-free`, `glm-5.3-flash-free` | `flint-40b-free` (muy chico) |
| ♻️ Refactorización | `minimax-m3.1-flash-free` | `glm-5.3-flash-free`, `big-pickle` | `flint-40b-free` |
| 🧪 Tests | `glm-5.3-flash-free` | `deepseek-v4.1-flash-free`, `nemotron-3.5-lightning-free` | `nemotron-3.5-super-vl-free` |
| 📝 Documentación | `longcat-2.5-free` | `beam-free`, `big-pickle` | `nemotron-3.5-lightning-free` |
| 🔎 Exploración masiva | `beam-free` | `mimo-v2.6-flash-free` | `inkling-2-small-free` (puede entrenar) |

### 6.1 Planeamiento (arquitectura, descomposición, diseño)

**Recomendado: `big-pickle`.** El catálogo live lo describe como "reasoning model for deliberate analysis, multi-step problem solving, and tool use": justo lo que exige planear, y el costo es el mismo ($0). Si el repo es privado, **`minimax-m3.1-flash-free`** es la alternativa zero-retention con 1M de contexto; `iceman-free` (stealth 🟡) sirve como segundo opinante de familia distinta.

Evitá `nemotron-3.5-lightning-free`: sacrifica profundidad por latencia, justo lo contrario de lo que necesitás al planear.

### 6.2 Código (features, funciones, implementación)

**Recomendado: `deepseek-v4.1-flash-free`.** Es exactamente el modelo de pago `deepseek-v4.1-flash` — rápido, code-capable, con cupo de proveedor holgado — servido gratis y con zero-retention. Es la mejor opción gratuita para el ciclo escribir → correr → corregir.

Alternativas:
- **`minimax-m3.1-flash-free`**: el gemelo gratuito del MiniMax M3.1 Flash de pago, "frontier multimodal coding model" con 1M de contexto y profundidad de razonamiento ajustable. Ideal cuando la sesión necesita mucho contexto.
- **`glm-5.3-flash-free`**: el hermano gratuito de `glm-5.3-flash`, orientado a código. Cambiá a este si DeepSeek te da latencia alta en horas pico.
- **`big-pickle`**: para features grandes y difíciles donde la capacidad agéntica pesa más que la latencia (⚠️ datos de feedback).

Dejá `flint-40b-free` para experimentos: con ~2.5B parámetros activos es un modelo chico, pensado más para agentes locales que para features complejas.

### 6.3 Refactorización (reestructurar sin romper comportamiento)

**Recomendado: `minimax-m3.1-flash-free`.** Refactorizar exige entender dependencias entre archivos y no inventar APIs inexistentes; un modelo coding frontera con **1M de contexto** y zero-retention permite cargar el repo entero en la sesión sin recortes.

Alternativas:
- **`glm-5.3-flash-free`**: refactors code-oriented con menor latencia.
- **`big-pickle`**: para refactors grandes y delicados que atraviesan muchos módulos (⚠️ feedback).

Evitá los modelos chicos o preview para refactors estructurales: no tienen el ajuste de código.

**Consejo:** pedí primero un **plan** con el modelo de planeamiento, revisalo, y después ejecutá con el de código.

### 6.4 Tests (unitarios, integración, TDD)

**Recomendado: `glm-5.3-flash-free`.** Los tests son código con contrato explícito: conviene el modelo code-oriented, y su política zero-retention permite usarlo sobre el repo real.

Alternativas:
- **`deepseek-v4.1-flash-free`**: ciclos rápidos escribir → correr → corregir con mucho contexto repetido (su punto fuerte es el volumen).
- **`nemotron-3.5-lightning-free`**: acá sí brilla la velocidad, para lotes de tests rutinarios o casos borde derivados de una función ya definida (🔴 endpoint trial: no le pases fixtures con datos reales).

Evitá `nemotron-3.5-super-vl-free`: es un modelo vision-language; no es la herramienta para tests (sí sirve para leer capturas de un fallo de UI).

### 6.5 Documentación, guías y manuales

**Recomendado: `longcat-2.5-free`.** Razonamiento multimodal con 1M de contexto y zero-retention: ideal para guías que se apoyan en capturas o en el repo entero. **Pero ojo con el límite de 100 requests por día**: para una sesión larga de documentación se queda corto.

Alternativas:
- **`beam-free`**: 🟢 sin entrenamiento, 1M de contexto y sin límite diario — el mejor para borradores masivos sobre código privado.
- **`big-pickle`**: para un README o un RFC donde la estructura y el estilo importan más que el volumen (⚠️ feedback).
- **`mimo-v2.6-flash-free`**: volumen puro sin preocupación por el límite diario (⚠️ feedback).

Evitá `nemotron-3.5-lightning-free`: privilegia velocidad sobre profundidad narrativa y la doc queda superficial.

**Consejo:** para una guía larga, pedí primero el **índice/estructura** con el modelo de planeamiento, revisalo, y después redactá cada sección con `longcat-2.5-free` o `beam-free` para mantener consistencia.

---

## 7. Zen como respaldo de Gentle-AI

Cuando se agota el cupo de Go, los gratuitos de Console son el respaldo natural de los roles del documento hermano. **Cambia el prefijo**: acá es `opencode/<id>`, no `opencode-go/<id>`.

| Rol de Gentle-AI | Respaldo gratuito | Por qué |
|---|---|---|
| `gentle-ai-explore` | `opencode/beam-free` | Lecturas masivas con 1M de contexto, sin costo ni límite diario, y sin entrenamiento |
| `gentle-ai-verify` | `opencode/deepseek-v4.1-flash-free` | Ejecuta y compara con razonamiento suficiente |
| `gentle-ai-worker` | `opencode/glm-5.3-flash-free` → `opencode/minimax-m3.1-flash-free` | Escritura de código con zero-retention |
| `review-readability` / `reliability` / `resilience` | `opencode/deepseek-v4.1-flash-free` | Volumen por lens sin costo |
| `review-risk` | `opencode/big-pickle` | Es el lens que más razonamiento exige (⚠️ feedback) |
| `review-refuter` | `opencode/minimax-m3.1-flash-free` | Razonamiento frontera + zero-retention (reemplaza a `space-bunny-free`, retirado) |
| `jd-judge-a` | `opencode/big-pickle` | Juez de máxima calidad |
| `jd-judge-b` | `opencode/iceman-free` | **Familia distinta** al juez A (⚠️ feedback: solo repos no sensibles) |
| `jd-fix-agent` | `opencode/glm-5.3-flash-free` | Parche acotado con modelo de código |
| `gentle-orchestrator` | `opencode/deepseek-v4.1-flash-free` | Cientos de llamadas: necesita latencia y cupo, no un flagship |

⚠️ **Antes de asignarlos a un rol de Gentle-AI, confirmá en `/models` que el modelo soporte tool calling**: es requisito duro de todos los roles. Según el catálogo live del 13/11/2026 los 12 gratuitos lo declaran, pero los probados en la práctica son los que sirven el mismo modelo que el de pago (`deepseek-v4.1-flash-free`, `glm-5.3-flash-free`, `minimax-m3.1-flash-free`); los stealth (`big-pickle`, `iceman-free`) siguen siendo la apuesta menos verificable. **Nunca asignes `inkling-2-small-free` a un rol**: puede entrenar con tus datos.

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
opencode -m opencode/minimax-m3.1-flash-free
# 3. Testear e iterar
opencode -m opencode/deepseek-v4.1-flash-free
# 4. Documentar
opencode -m opencode/longcat-2.5-free
```

### 8.5 Roles y subagentes de Gentle-AI

Los gratuitos también aparecen en el selector de Gentle-AI (**Configure Models**) si el proveedor `opencode` está conectado. Se persisten igual que cualquier rol:

```json
{
  "agent": {
    "gentle-ai-worker": { "model": "opencode/glm-5.3-flash-free" },
    "review-refuter":   { "model": "opencode/minimax-m3.1-flash-free" }
  }
}
```

Si preferís que no aparezcan gratuitos en el selector, exportá `OPENCODE_DISABLE_FREE_MODELS=1`.

---

## 9. Buenas prácticas y advertencias

1. **No mandes secretos a un modelo 🟡 o 🔴.** Con los 🟢 (`deepseek-v4.1-flash-free`, `glm-5.3-flash-free`, `minimax-m3.1-flash-free`, `longcat-2.5-free`, `beam-free`) el riesgo de entrenamiento desaparece, pero igual evitá `.env`, API keys y datos de clientes en el prompt.
2. **Son temporales.** No construyas CI crítico dependiendo solo de un gratuito: el catálogo volvió a rotar en menos de 4 semanas (cayeron `space-bunny-free` y `jev-1.13-free`; entraron cuatro nuevos).
3. **Verificá el código generado**, sobre todo en refactors: corré tu suite después de cada cambio.
4. **Combiná modelos por fase** (plan → code → test) en vez de usar uno solo para todo.
5. **No cambies de modelo a mitad de iteración de un archivo**: perder el cache y re-enviar el contexto es lo único que te puede costar tiempo real, incluso con modelos gratis.
6. **Nunca uses un modelo del que no sepas qué es.** `big-pickle` e `iceman-free` son *stealth*: identidad no revelada, pueden cambiar o desaparecer sin aviso (como Space Bunny). Si eso te incomoda, usá `deepseek-v4.1-flash-free`, `glm-5.3-flash-free` o `minimax-m3.1-flash-free`, que son modelos conocidos.
7. **Los 👁️ vision-language no son para código.** `nemotron-3.5-super-vl-free` es multimodal: útil para leer capturas y diagramas; no lo asignes como agente de implementación.
8. **`longcat-2.5-free` tiene límite duro de 100 requests/día y está hosteado en China.** Ya no sirve para volumen; si el hosting en China choca con tus políticas de datos, no lo uses.
9. **`inkling-2-small-free` puede entrenar con tus datos** (Thinking Machines) y no está disponible en la UE ni en varios países. Es el sucesor espiritual de `muse-spark-*-contributor-free`: nunca con código propio o de clientes.
10. **`jev-1.13-free` ya no está en el catálogo live.** Si lo ves documentado, recordá que tampoco era un LLM de chat: devolvía decisiones tipadas contra un `state`.
11. **Migrar de Go a Zen es cambiar el prefijo**: `opencode-go/<id>` → `opencode/<id>`.
12. Consultá siempre la [documentación oficial](https://opencode.ai/docs/zen/) y el catálogo live antes de fijar un modelo.

### Funciones de cuenta

- **Auto-recarga**: si el saldo baja de $5, Console recarga $20 (configurable o desactivable).
- **Límites mensuales (budgets)**: por workspace y por miembro; con auto-recarga activo, el gasto puede superarlo cuando el saldo baja de $5.
- **Workspaces** para equipos: restricción de modelos por miembro, presupuestos y *bring-your-own-key* de proveedores.
- **Comisión de tarjeta**: **4.6% + $0.31** por recarga de créditos (subió desde 4.4% + $0.30), pasado a costo.
- OpenCode usa modelos baratos (Haiku, Nano, Flash) para generar los títulos de sesión.

---

## 10. Deprecaciones vigentes

No uses estos modelos en configuraciones nuevas (tabla oficial al 13/11/2026):

| Modelo | Fecha de deprecación |
|---|---|
| Crouton Alpha Free | 9 de noviembre de 2026 |
| Pulse Alpha Free | 6 de noviembre de 2026 |
| DeepSeek V4 Flash | 26 de octubre de 2026 |
| Claude Opus 4.1 · MiniMax M2.5 · Kimi K2.5 | 5 de agosto de 2026 |
| GPT 5 Codex · GPT 5.1 Codex · GPT 5.1 Codex Max · GPT 5.1 Codex Mini · GPT 5.2 Codex | 23 de julio de 2026 |
| Claude Sonnet 4 | 15 de junio de 2026 |
| GLM 5 | 14 de mayo de 2026 |
| MiniMax M2.1 · GLM 4.7 · GLM 4.6 | 15 de marzo de 2026 |
| Gemini 3 Pro | 9 de marzo de 2026 |
| Kimi K2 · Kimi K2 Thinking | 6 de marzo de 2026 |
| Claude Haiku 3.5 | 16 de febrero de 2026 |
| Qwen3 Coder 480B | 6 de febrero de 2026 |

⚠️ Varios deprecados (GLM 5, MiniMax M2.5, Kimi K2.5, Grok 4.6, GLM 5.1…) **siguen apareciendo en el catálogo live**: no los asignes en configuraciones nuevas aunque respondan.

**Ofertas temporales vigentes:** **Gemini 4 Argon** y **Gemini 4 Carbon** con 50% de descuento hasta el **30 de noviembre de 2026**; **Gemini 3.6 / 3.7 / 3.8 Flash** con 50% hasta el **31 de diciembre de 2026**; **Mistral Large 4** con 50% de descuento; los gratuitos de la sección 3, "por tiempo limitado".

⚠️ Ojo con la **privacidad**: en Zen el modelo que entrena con tus datos ahora es `inkling-2-small-free` (Thinking Machines); los Gemini 4 Argon/Carbon de Console ya no son versión *Contributor*. Las versiones *Contributor* que sí entrenan (Muse Spark 1.2/1.3, Iceman) viven en **Go** — ver el documento hermano. En los roles de review de Gentle-AI los que entrenan están explícitamente excluidos.
