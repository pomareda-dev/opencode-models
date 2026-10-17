# OpenCode Go - Guía de Modelos

> **Revisión:** 17 de octubre de 2026 (UTC)<br>
> **Modelo usado para esta revisión:** `opencode-go/glm-5.3`<br>
> **Fuente principal:** [opencode.ai/docs/go](https://opencode.ai/docs/go/)<br>
> **Catálogo live:** <https://opencode.ai/zen/go/v1/models>

OpenCode Go ofrece acceso a modelos de código seleccionados y evaluados por OpenCode. La lista y los límites pueden cambiar; esta guía refleja la información publicada en la fuente oficial durante la revisión indicada.

## Planes y límites

| Plan | Precio | Límite mensual incluido |
|------|--------|-------------------------|
| Go | **$10/mes** | Límite mensual por modelo indicado abajo |
| Go Plus | **$40/mes** | Límite superior por modelo; ver tabla Go Plus abajo |

Los precios por token son iguales en ambos planes. Para cada modelo, el límite de uso es **20% del límite mensual en 5 horas**, **50% por semana** y **100% por mes**. Al alcanzar el límite se puede activar **Use balance** en la consola para continuar con créditos de Zen, o seguir usando los modelos gratuitos.

## Cambios desde la revisión anterior (4 de octubre de 2026)

- **Agregados:** Claude Haiku 5.5, Gemini 4 Argon Contributor, Step 5 Preview y Beam Free (gratis por tiempo limitado, con regiones excluidas).
- **Retirados de la lista oficial:** Grok 4.6, Kimi K2.6, MiniMax M2.7, DeepSeek V4 Flash y DeepSeek V4 Flash Vision Exp. Algunos (Grok 4.6, Kimi K2.6, MiniMax M2.7) siguen apareciendo en el catálogo live, junto con otros modelos legados no listados en la documentación (GLM-5.1, Omen Alpha, Qwen3.6 Plus, Qwen3.7 Max, MiniMax M2.5).
- **Space Bunny** dejó de ser gratuito: ahora es de pago, con límite mensual de **$30** y precios por token.
- **DeepSeek V4.1 Flash** subió su límite mensual de $60 a **$80**.
- **Step 5 Preview** y **Gemini 4 Argon Contributor** tienen límites promocionales temporales (4x y 2x respectivamente).

## Catálogo actual

La lista oficial incluye:

- **Grok:** 4.7
- **GLM:** 5.3-Flash, 5.3, 5.2
- **GPT:** 6 Luna, 5.6 Luna
- **Claude:** Haiku 5.5
- **Gemini:** 4 Argon Contributor
- **Kimi:** K3, K2.7 Code
- **LongCat:** 2.0, 2.5 Preview Free (gratis por tiempo limitado)
- **Step:** 5 Preview (límite 4x por tiempo limitado)
- **Beam Free** (gratis por tiempo limitado, regiones limitadas)
- **MiMo:** V2.6-Flash, V2.6-Pro, V2.5, V2.5-Pro
- **MiniMax:** M3
- **Muse:** Spark 1.3 Contributor, Spark 1.2 Contributor (regiones limitadas)
- **Qwen:** 3.8 Max, 3.8 Flash, 3.7 Plus
- **DeepSeek:** V4.1 Flash, V4 Pro
- **Hy:** Hy4 preview, Hy3
- **Space Bunny** (de pago desde esta revisión)

## Requests estimados y límites de Go

Son estimaciones basadas en patrones de uso típicos; el consumo real depende de los tokens enviados y generados.

| Modelo | req/5h | req/semana | req/mes | Límite mensual |
|--------|--------:|-----------:|--------:|---------------:|
| Grok 4.7 | 169 | 423 | 845 | $15 |
| GLM-5.3-Flash | 6,320 | 15,790 | 31,580 | $60 |
| GLM-5.3 | 220 | 540 | 1,080 | $15 |
| GLM-5.2 | 880 | 2,150 | 4,300 | $60 |
| GPT 6 Luna | 4,230 | 10,560 | 21,130 | $15 |
| GPT 5.6 Luna | 2,050 | 5,100 | 10,250 | $15 |
| Claude Haiku 5.5 | 3,850 | 9,620 | 19,230 | $15 |
| Gemini 4 Argon Contributor | 440* | 1,080* | 2,120* | $60 (2x)* |
| Kimi K3 | 110 | 250 | 490 | $15 |
| Kimi K2.7 Code | 1,350 | 3,380 | 6,750 | $60 |
| LongCat-2.0 | 11,400 | 28,600 | 57,200 | $60 |
| LongCat 2.5 Preview Free | Ilimitado | Ilimitado | Ilimitado | Gratis** |
| Step 5 Preview | 1,720* | 4,280* | 8,520* | $60 (4x)* |
| Beam Free | Ilimitado | Ilimitado | Ilimitado | Gratis** |
| MiMo-V2.6-Flash | 30,100 | 75,200 | 150,400 | $60 |
| MiMo-V2.6-Pro | 3,250 | 8,150 | 16,300 | $15 |
| MiMo-V2.5 | 30,100 | 75,200 | 150,400 | $60 |
| MiMo-V2.5-Pro | 3,250 | 8,150 | 16,300 | $15 |
| MiniMax M3 | 3,200 | 8,000 | 16,000 | $60 |
| Muse Spark 1.3/1.2 Contributor | 45,300 | 113,300 | 226,600 | $60 |
| Qwen3.8 Max | 160 | 400 | 810 | $15 |
| Qwen3.8 Flash | 5,400 | 13,500 | 27,000 | $30 |
| Qwen3.7 Plus | 4,300 | 10,800 | 21,600 | $60 |
| DeepSeek V4.1 Flash | 34,670 | 86,670 | 173,330 | $80 |
| DeepSeek V4 Pro | 1,050 | 2,600 | 5,200 | $15 |
| Hy4 preview | 1,350 | 3,380 | 6,770 | $30 |
| Hy3 | 4,300 | 10,750 | 21,500 | $60 |
| Space Bunny | 3,130 | 7,810 | 15,630 | $30 |

\* Valores con bonificación temporal (2x / 4x por tiempo limitado).<br>
\*\* Gratis por tiempo limitado.

## Límites mensuales de Go Plus

El precio por token es el mismo; solo cambia el cupo incluido.

| Modelo | Límite Go Plus |
|--------|---------------:|
| GLM-5.3-Flash | $180 |
| GLM-5.3 | $120 |
| GLM-5.2 | $180 |
| Kimi K3 | $60 |
| Kimi K2.7 Code | $180 |
| LongCat-2.0 | $240 |
| LongCat 2.5 Preview Free / Beam Free | Ilimitado |
| Step 5 Preview | $240 (4x por tiempo limitado) |
| MiMo-V2.6-Flash / V2.5 | $120 |
| MiMo-V2.6-Pro / V2.5-Pro | $60 |
| MiniMax M3 | $180 |
| Muse Spark 1.3/1.2 Contributor | $120 |
| Qwen3.8 Max | $60 |
| Qwen3.8 Flash | $90 |
| Qwen3.7 Plus | $180 |
| DeepSeek V4.1 Flash | $160 |
| DeepSeek V4 Pro | $60 |
| Hy4 preview | $120 |
| Hy3 | $240 |
| Space Bunny | $120 |
| Grok 4.7 | $60 |
| GPT 6 Luna / GPT 5.6 Luna | $60 |
| Claude Haiku 5.5 | $60 |
| Gemini 4 Argon Contributor | $240 (2x por tiempo limitado) |

## Precios por 1M tokens (plan Go)

| Modelo | Entrada | Salida | Cache read | Cache write | Límite |
|--------|--------:|-------:|-----------:|------------:|-------:|
| Grok 4.7 (≤200K) | $2.00 | $6.00 | $0.50 | - | $15 |
| Grok 4.7 (>200K) | $4.00 | $12.00 | $1.00 | - | $15 |
| GPT 6 Luna (≤272K) | $0.10 | $0.50 | $0.01 | $0.125 | $15 |
| GPT 6 Luna (>272K) | $0.20 | $0.75 | $0.02 | $0.25 | $15 |
| GPT 5.6 Luna (≤272K) | $0.20 | $1.20 | $0.02 | $0.25 | $15 |
| GPT 5.6 Luna (>272K) | $0.40 | $1.80 | $0.04 | $0.50 | $15 |
| Claude Haiku 5.5 (≤100K) | $0.10 | $0.50 | $0.01 | $0.125 | $15 |
| Claude Haiku 5.5 (>100K) | $0.50 | $2.50 | $0.05 | $0.625 | $15 |
| Gemini 4 Argon Contributor | $4.00 | $20.00 | $0.20 | - | $60 (2x)* |
| GLM-5.3-Flash | $0.15 | $0.50 | $0.03 | - | $60 |
| GLM-5.3 | $1.40 | $4.40 | $0.26 | - | $15 |
| GLM-5.2 | $1.40 | $4.40 | $0.26 | - | $60 |
| Kimi K3 | $3.00 | $15.00 | $0.30 | - | $15 |
| Kimi K2.7 Code | $0.95 | $4.00 | $0.19 | - | $60 |
| LongCat-2.0 | $0.30 | $1.20 | $0.006 | - | $60 |
| Step 5 Preview | $1.00 | $2.70 | $0.10 | - | $60 (4x)* |
| MiMo-V2.6-Flash / V2.5 | $0.14 | $0.28 | $0.0028 | - | $60 |
| MiMo-V2.6-Pro / V2.5-Pro | $0.435 | $0.87 | $0.003625 | - | $15 |
| MiniMax M3 | $0.30 | $1.20 | $0.06 | - | $60 |
| Muse Spark 1.3/1.2 Contributor | $0.10 | $0.20 | $0.002 | - | $60 |
| Qwen3.8 Max | $2.00 | $6.00 | $0.25 | $2.50 | $15 |
| Qwen3.8 Flash | $0.15 | $0.47 | $0.016 | $0.20 | $30 |
| Qwen3.7 Plus (≤256K) | $0.40 | $1.60 | $0.04 | $0.50 | $60 |
| Qwen3.7 Plus (>256K) | $1.20 | $4.80 | $0.12 | $1.50 | $60 |
| DeepSeek V4.1 Flash (off-peak / peak) | $0.15 / $0.30 | $0.60 / $1.20 | $0.003 / $0.006 | - | $80 |
| DeepSeek V4 Pro (off-peak / peak) | $0.66 / $1.32 | $1.98 / $3.96 | $0.022 / $0.044 | - | $15 |
| Hy4 preview | $0.834 | $2.501 | $0.042 | - | $30 |
| Hy3 | $0.14 | $0.58 | $0.035 | - | $60 |
| Space Bunny | $0.15 | $0.60 | $0.03 | - | $30 |

\* Límite promocional por tiempo limitado (el valor base tachado en la fuente era $30 para Gemini 4 Argon y $15 para Step 5 Preview).

Los modelos gratuitos (LongCat 2.5 Preview Free, Beam Free) no tienen precios por token. DeepSeek cobra tarifa **peak** entre 01:00–04:00 y 06:00–10:00 UTC, de lunes a viernes; el resto (incluidos los fines de semana) es **off-peak**.

## Recomendaciones y estrategias por caso de uso

> Las recomendaciones combinan el posicionamiento de cada modelo en el catálogo (modelos de razonamiento, modelos ajustados para código, modelos flash de alto volumen) con la economía del plan: límite mensual, precio por token y costo de cache read. En sesiones largas de agente, la mayoría del consumo es **cache read**, no salida; ese es el factor dominante para elegir modelo de trabajo diario.

### Para código

**Estrategia general:** separar las tareas de alta dificultad (donde un error de razonamiento cuesta caro) del trabajo diario (donde domina el volumen), y elegir el modelo según qué recurso agota primero.

- **Máxima calidad / refactorings complejos / arquitectura:** **Kimi K3**, **Grok 4.7**, **GLM-5.3**, **Qwen3.8 Max**, **DeepSeek V4 Pro** o **Gemini 4 Argon Contributor** (con la advertencia de privacidad de más abajo). Son los modelos de mayor razonamiento del catálogo, pero su límite mensual es de **$15** (Kimi K3: apenas ~490 requests/mes). Reservalos para las decisiones difíciles, no para el día a día.
- **Desarrollo diario (equilibrio calidad/volumen):** **Kimi K2.7 Code** (ajustado específicamente para código, $60 de límite, ~6,750 req/mes, cache read $0.19), **DeepSeek V4.1 Flash** ($80 de límite, ~173,330 req/mes, cache read $0.003) o **GPT 6 Luna** (límite de $15 pero tokens muy baratos: ~21,130 req/mes con cache read de $0.01).
- **Alto volumen / agentes con muchos pasos:** **MiMo-V2.6-Flash** o **MiMo-V2.5** (~150,400 req/mes, cache read $0.0028), **Muse Spark Contributor** (~226,600 req/mes; ojo: no es ZDR) y **LongCat-2.0** (~57,200 req/mes, cache read $0.006).
- **Gratis temporal:** **LongCat 2.5 Preview Free** y **Beam Free** para proyectos de prueba o cuando el cupo mensual ya está agotado.

**Tácticas:**
- En sesiones largas de agente, el costo real lo manda el cache read: MiMo ($0.0028), DeepSeek V4.1 Flash ($0.003), LongCat-2.0 ($0.006) y GPT 6 Luna ($0.01) son los más económicos para mantener una conversación con mucho contexto.
- Mantené la misma sesión y el mismo modelo mientras iterás sobre un archivo: cambiar de modelo pierde el cache y encarece cada request.
- Los modelos con límite de $15 agotan el cupo en ~220–1,080 requests/mes según el modelo; si tu flujo de trabajo dispara cientos de requests, trabajá con modelos de $60–$80 y reservá los premium para puntos puntuales.

### Para planificación

**Estrategia general:** la planificación genera pocas requests y poco texto de salida, así que el límite mensual pesa mucho menos que en código. Acá conviene **pagar el modelo más capaz disponible** en lugar del más barato.

- **Primera opción (razonamiento profundo):** **Kimi K3**, **GLM-5.3**, **Grok 4.7** o **Qwen3.8 Max**. Con ~110–220 req/5h de techo, una sesión de planificación consume una fracción mínima del cupo, pero la calidad del plan condiciona todo el trabajo posterior.
- **Planificación dentro de sesiones largas de agente:** **GPT 6 Luna** (cache read $0.01; mantener la planificación y la ejecución en la misma sesión reutiliza el contexto cacheado) o **Claude Haiku 5.5** hasta 100K de contexto ($0.10 entrada / $0.50 salida).
- **Descomposición masiva de tareas / borradores de plan:** **GLM-5.3-Flash**, **Qwen3.7 Plus** o **Hy3**, y corregir/elaborar el plan final con un modelo de mayor razonamiento.

**Tácticas:**
- Patrón recomendado: planificar con el modelo fuerte en una sesión propia, y delegar la ejecución de cada tarea a un modelo económico; el plan explícito le sirve de guía al modelo barato.
- Para planes con contexto enorme (monorepos), los modelos con contexto extendido y pricing escalonado (Grok 4.7 >200K, Qwen3.7 Plus >256K, GPT 6/5.6 Luna >272K) cobran más caro por encima del umbral; medí el tamaño del contexto antes de elegir.

### Para testing

**Estrategia general:** dividir el trabajo de testing en dos fases con modelos distintos: **diseño** de tests (requiere razonamiento) e **iteración masiva** (requiere volumen barato).

- **Diseño de tests / casos límite / tests complejos:** **GLM-5.3**, **DeepSeek V4 Pro**, **MiMo-V2.6-Pro** (o V2.5-Pro) o **Kimi K2.7 Code**. Detectar casos límite y dependencias ocultas es trabajo de razonamiento; las respuestas cortas de esta fase hacen viable incluso un modelo de $15.
- **Generación masiva y repetitiva (fixtures, tests paramétricos, data de prueba):** **GLM-5.3-Flash** (~31,580 req/mes), **DeepSeek V4.1 Flash** (~173,330 req/mes), **Qwen3.8 Flash** (~27,000 req/mes) o **MiMo-V2.6-Flash** (~150,400 req/mes).
- **Corrección en bucle (fix → run → fix):** el mismo modelo flash con el que generaste los tests, para aprovechar el cache read entre iteraciones.

**Tácticas:**
- Con DeepSeek, ejecutá las baterías masivas en **off-peak**: fuera de 01:00–04:00 y 06:00–10:00 UTC de lunes a viernes (todos los fines de semana son off-peak) pagás la mitad.
- Patrón recomendado: los primeros tests de una funcionalidad (los que definen la cobertura) los escribís con un modelo fuerte; la explosión de variantes y casos repetitivos, con un modelo flash.
- Verificá que el modelo elegido entienda el framework de testing de tu stack antes de masificar: los modelos flash rinden mucho mejor con instrucciones concretas y ejemplos previos en el contexto.

### Para documentación

**Estrategia general:** la documentación produce mucho texto de salida (lo más caro por token), pero tolera más errores que el código. Conviene **masificar con modelos baratos** y **revisar con un modelo capaz**.

- **Documentación de alta calidad (guías, READMEs, RFCs, docs de arquitectura):** **GPT 6 Luna** (entrada $0.10, salida $0.50: prosa extensa a costo mínimo), **GLM-5.3** o **Claude Haiku 5.5** hasta 100K de contexto ($0.10/$0.50). Para un RFC o decisión de arquitectura, **Kimi K3** o **Grok 4.7** justifican su precio.
- **Documentación masiva (changelogs, docstrings, JSDoc, comentarios, traducciones):** **GLM-5.3-Flash**, **DeepSeek V4.1 Flash**, **Hy3** (~21,500 req/mes, salida $0.58), **LongCat-2.0** o **MiMo-V2.6-Flash**.
- **Gratis temporal:** **LongCat 2.5 Preview Free** y **Beam Free** son ideales para borradores masivos de documentación sin costo, dejando la revisión final para un modelo de pago.

**Tácticas:**
- El costo de la documentación está dominado por la **salida** ($0.28–$1.20 por 1M en los modelos flash vs. $4.40–$15 en los premium): no documentes en volumen con modelos premium.
- Patrón recomendado: borrador completo con flash → revisión y pulido de estilo/estructura con el modelo capaz → solo el índice o resumen ejecutivo con el premium si hace falta.
- Si la documentación se genera a partir del código de la misma sesión, el cache read barato del modelo flash ya pagó el contexto; no lo rehagas desde cero con otro modelo.

## Recomendaciones rápidas (resumen)

- **Máxima calidad y razonamiento:** Kimi K3, GLM-5.3, Grok 4.7, Qwen3.8 Max, DeepSeek V4 Pro o Gemini 4 Argon Contributor.
- **Código diario:** Kimi K2.7 Code, DeepSeek V4.1 Flash, GPT 6 Luna, GLM-5.3-Flash o MiniMax M3.
- **Alto volumen:** MiMo-V2.6-Flash, MiMo-V2.5, Muse Spark Contributor o LongCat-2.0.
- **Tests complejos:** GLM-5.3, DeepSeek V4 Pro, MiMo-V2.6-Pro o Kimi K2.7 Code.
- **Tests repetitivos y documentación masiva:** GLM-5.3-Flash, DeepSeek V4.1 Flash, Qwen3.8 Flash o Hy3.
- **Uso gratuito temporal:** LongCat 2.5 Preview Free o Beam Free.

Los modelos con límite mensual de **$15** agotan antes el cupo efectivo. **Muse Spark Contributor** y **Gemini 4 Argon Contributor** pueden usar prompts y completions para entrenar (Meta y Google respectivamente) y tienen restricciones geográficas; evitalos con información sensible.

## Endpoints e integración

El ID de modelo en la configuración es `opencode-go/<model-id>`, por ejemplo `opencode-go/kimi-k3`.

- **OpenAI Responses API:** Grok 4.7, GPT 6 Luna, GPT 5.6 Luna y Muse Spark Contributor.
- **OpenAI-compatible chat completions:** GLM, Kimi, LongCat, Step 5 Preview, Beam Free, MiMo, DeepSeek, Hy y Space Bunny.
- **Anthropic Messages API:** Claude Haiku 5.5, Qwen (3.8 Max, 3.8 Flash, 3.7 Plus) y MiniMax M3.
- **Google API (v1beta):** Gemini 4 Argon Contributor.

Clientes validados además de OpenCode: Hermes (con el fix indicado en la documentación oficial), Claude Code, Codex, ZCode, Pi, jcode (v0.81.6 o posterior) y Kilo Code CLI (con el fix correspondiente). DeepSeek Harness, GitHub Copilot Chat, Kimi Code y MiMo Code tienen soporte incompleto o pendiente para la información de sesión.

## Privacidad

- Grok 4.7, GPT 6/5.6 Luna, Claude Haiku 5.5 y Beam Free: no usan los datos para entrenamiento; retención de hasta **30 días** por monitoreo de abuso o políticas del proveedor.
- La mayoría de los modelos (GLM, Kimi, LongCat, Step, MiMo, MiniMax, Qwen, DeepSeek, Hy, Space Bunny): no usan los datos para entrenamiento y tienen retención de **0 días**.
- Muse Spark 1.3/1.2 Contributor: **sí** puede usar prompts y completions para entrenar modelos de Meta; no es ZDR.
- Gemini 4 Argon Contributor: **sí** puede usar prompts y completions para entrenar modelos de Google; no es ZDR.
- DeepSeek: ZDR renovado mensualmente; el acuerdo publicado durante esta revisión es válido hasta el **31 de octubre de 2026**.

## Notas

- Solo un miembro por workspace puede suscribirse a Go (workspaces con suscripción Go no pueden invitar miembros).
- Los modelos están hosteados en EE. UU.; verificá la política vigente antes de enviar información sensible.
- Beam Free no está disponible en una lista de países restringidos (incluye China, Rusia, Bielorrusia, Irán, Corea del Norte, Venezuela, entre otros).
- La disponibilidad y los límites pueden cambiar a medida que OpenCode prueba y agrega modelos; los límites promocionales (Step 5 Preview 4x, Gemini 4 Argon 2x) son temporales.
- El catálogo live (`/zen/go/v1/models`) incluye además modelos legados no listados en la documentación oficial (GLM-5.1, Omen Alpha, Qwen3.6 Plus, Qwen3.7 Max, MiniMax M2.5, Kimi K2.6, Grok 4.6, MiniMax M2.7); pueden desaparecer sin aviso.
- Consultá `/models` en la TUI o el catálogo live para confirmar disponibilidad antes de fijar un modelo en una configuración.
