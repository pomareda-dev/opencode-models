# OpenCode Go - Guía de Modelos

> **Revisión:** 4 de octubre de 2026 (UTC)<br>
> **Modelo usado para esta revisión:** `opencode-go/gpt-5.6-luna`<br>
> **Fuente principal:** [opencode.ai/docs/go](https://opencode.ai/docs/go/)<br>
> **Catálogo live:** <https://opencode.ai/zen/go/v1/models>

OpenCode Go ofrece acceso a modelos de código seleccionados y evaluados por OpenCode. La lista y los límites pueden cambiar; esta guía refleja la información publicada en la fuente oficial durante la revisión indicada.

## Planes y límites

| Plan | Precio | Límite mensual incluido |
|------|--------|-------------------------|
| Go | **$10/mes** | Límite mensual por modelo indicado abajo |
| Go Plus | **$40/mes** | Límite superior por modelo; ver la consola |

Los precios por token son iguales en ambos planes. Para cada modelo, el límite de uso es **20% del límite mensual en 5 horas**, **50% por semana** y **100% por mes**. Al alcanzar el límite se puede activar **Use balance** en la consola para continuar con créditos de Zen.

## Catálogo actual

La lista oficial incluye:

- **Grok:** 4.7, 4.6
- **GLM:** 5.3-Flash, 5.3, 5.2
- **GPT:** 6 Luna, 5.6 Luna
- **Kimi:** K3, K2.7 Code, K2.6
- **LongCat:** 2.0, 2.5 Preview Free (gratis por tiempo limitado)
- **MiMo:** V2.6-Flash, V2.6-Pro, V2.5, V2.5-Pro
- **MiniMax:** M3, M2.7
- **Muse:** Spark 1.3 Contributor, Spark 1.2 Contributor (regiones limitadas)
- **Qwen:** 3.8 Max, 3.8 Flash, 3.7 Plus
- **DeepSeek:** V4.1 Flash, V4 Pro, V4 Flash, V4 Flash Vision Exp
- **Hy:** Hy4 preview, Hy3
- **Space Bunny Free** (gratis por tiempo limitado)

## Requests estimados y límites de Go

Son estimaciones basadas en patrones de uso típicos; el consumo real depende de los tokens enviados y generados.

| Modelo | req/5h | req/semana | req/mes | Límite mensual |
|--------|--------:|-----------:|--------:|---------------:|
| Grok 4.7 | 169 | 423 | 845 | $15 |
| Grok 4.6 | 169 | 423 | 845 | $15 |
| GLM-5.3-Flash | 6,320 | 15,790 | 31,580 | $60 |
| GLM-5.3 | 220 | 540 | 1,080 | $15 |
| GLM-5.2 | 880 | 2,150 | 4,300 | $60 |
| GPT 6 Luna | 4,230 | 10,560 | 21,130 | $15 |
| GPT 5.6 Luna | 2,050 | 5,100 | 10,250 | $15 |
| Kimi K3 | 110 | 250 | 490 | $15 |
| Kimi K2.7 Code | 1,350 | 3,380 | 6,750 | $60 |
| Kimi K2.6 | 1,150 | 2,880 | 5,750 | $60 |
| LongCat-2.0 | 11,400 | 28,600 | 57,200 | $60 |
| LongCat 2.5 Preview Free | Ilimitado | Ilimitado | Ilimitado | Gratis* |
| MiMo-V2.6-Flash | 30,100 | 75,200 | 150,400 | $60 |
| MiMo-V2.6-Pro | 3,250 | 8,150 | 16,300 | $15 |
| MiMo-V2.5 | 30,100 | 75,200 | 150,400 | $60 |
| MiMo-V2.5-Pro | 3,250 | 8,150 | 16,300 | $15 |
| MiniMax M3 | 3,200 | 8,000 | 16,000 | $60 |
| MiniMax M2.7 | 3,400 | 8,500 | 17,000 | $60 |
| Muse Spark 1.3/1.2 Contributor | 45,300 | 113,300 | 226,600 | $60 |
| Qwen3.8 Max | 160 | 400 | 810 | $15 |
| Qwen3.8 Flash | 5,400 | 13,500 | 27,000 | $30 |
| Qwen3.7 Plus | 4,300 | 10,800 | 21,600 | $60 |
| DeepSeek V4.1 Flash | 26,000 | 65,000 | 130,000 | $60 |
| DeepSeek V4 Pro | 1,050 | 2,600 | 5,200 | $15 |
| DeepSeek V4 Flash | 13,000 | 32,500 | 65,000 | $30 |
| DeepSeek V4 Flash Vision Exp | 6,500 | 16,250 | 32,500 | $15 |
| Hy4 preview | 1,350 | 3,380 | 6,770 | $30 |
| Hy3 | 4,300 | 10,750 | 21,500 | $60 |
| Space Bunny Free | Ilimitado | Ilimitado | Ilimitado | Gratis* |

\* Gratis por tiempo limitado.

## Precios por 1M tokens (plan Go)

| Modelo | Entrada | Salida | Cache read | Cache write | Límite |
|--------|--------:|-------:|-----------:|------------:|-------:|
| Grok 4.7 / 4.6 (≤200K) | $2.00 | $6.00 | $0.50 | - | $15 |
| Grok 4.7 / 4.6 (>200K) | $4.00 | $12.00 | $1.00 | - | $15 |
| GPT 6 Luna (≤272K) | $0.10 | $0.50 | $0.01 | $0.125 | $15 |
| GPT 6 Luna (>272K) | $0.20 | $0.75 | $0.02 | $0.25 | $15 |
| GPT 5.6 Luna (≤272K) | $0.20 | $1.20 | $0.02 | $0.25 | $15 |
| GPT 5.6 Luna (>272K) | $0.40 | $1.80 | $0.04 | $0.50 | $15 |
| GLM-5.3-Flash | $0.15 | $0.50 | $0.03 | - | $60 |
| GLM-5.3 | $1.40 | $4.40 | $0.26 | - | $15 |
| GLM-5.2 | $1.40 | $4.40 | $0.26 | - | $60 |
| Kimi K3 | $3.00 | $15.00 | $0.30 | - | $15 |
| Kimi K2.7 Code | $0.95 | $4.00 | $0.19 | - | $60 |
| Kimi K2.6 | $0.95 | $4.00 | $0.16 | - | $60 |
| LongCat-2.0 | $0.30 | $1.20 | $0.006 | - | $60 |
| MiMo-V2.6-Flash / V2.5 | $0.14 | $0.28 | $0.0028 | - | $60 |
| MiMo-V2.6-Pro / V2.5-Pro | $0.435 | $0.87 | $0.003625 | - | $15 |
| MiniMax M3 | $0.30 | $1.20 | $0.06 | - | $60 |
| MiniMax M2.7 | $0.30 | $1.20 | $0.06 | $0.375 | $60 |
| Muse Spark 1.3/1.2 Contributor | $0.10 | $0.20 | $0.002 | - | $60 |
| Qwen3.8 Max | $2.00 | $6.00 | $0.25 | $2.50 | $15 |
| Qwen3.8 Flash | $0.15 | $0.47 | $0.016 | $0.20 | $30 |
| Qwen3.7 Plus (≤256K) | $0.40 | $1.60 | $0.04 | $0.50 | $60 |
| Qwen3.7 Plus (>256K) | $1.20 | $4.80 | $0.12 | $1.50 | $60 |
| DeepSeek V4.1 Flash (off-peak / peak) | $0.15 / $0.30 | $0.60 / $1.20 | $0.003 / $0.006 | - | $60 |
| DeepSeek V4 Pro (off-peak / peak) | $0.66 / $1.32 | $1.98 / $3.96 | $0.022 / $0.044 | - | $15 |
| DeepSeek V4 Flash (off-peak / peak) | $0.15 / $0.30 | $0.60 / $1.20 | $0.003 / $0.006 | - | $30 |
| DeepSeek V4 Flash Vision Exp (off-peak / peak) | $0.15 / $0.30 | $0.60 / $1.20 | $0.003 / $0.006 | - | $15 |
| Hy4 preview | $0.834 | $2.501 | $0.042 | - | $30 |
| Hy3 | $0.14 | $0.58 | $0.035 | - | $60 |

Los modelos gratuitos no tienen precios por token. DeepSeek cobra tarifa **peak** entre 01:00–04:00 y 06:00–10:00 UTC, de lunes a viernes; el resto es **off-peak**. En Vision Exp, las imágenes se convierten en tokens de entrada y se facturan junto con el texto.

## Recomendaciones prácticas

- **Máxima calidad y razonamiento:** Kimi K3, GLM-5.3, Grok 4.7/4.6, Qwen3.8 Max o DeepSeek V4 Pro.
- **Código diario:** Kimi K2.7 Code, DeepSeek V4.1 Flash, GLM-5.3-Flash, Qwen3.7 Plus o MiniMax M3.
- **Alto volumen:** MiMo-V2.6-Flash, MiMo-V2.5, Muse Spark Contributor o DeepSeek V4 Flash.
- **Tests complejos:** GLM-5.3, DeepSeek V4 Pro, MiMo-V2.6-Pro o Kimi K2.7 Code.
- **Tests repetitivos y documentación masiva:** GLM-5.3-Flash, DeepSeek V4 Flash, Qwen3.7 Plus o Hy3.
- **Visión:** DeepSeek V4 Flash Vision Exp.
- **Uso gratuito temporal:** LongCat 2.5 Preview Free o Space Bunny Free.

Los modelos con límite mensual de **$15** agotan antes el cupo efectivo. Muse Spark Contributor permite el uso de prompts y completions para entrenar modelos de Meta y está limitado geográficamente; evitá usarlo con información sensible.

## Endpoints e integración

El ID de modelo en la configuración es `opencode-go/<model-id>`, por ejemplo `opencode-go/kimi-k3`.

- **OpenAI Responses API:** Grok 4.7/4.6, GPT 6 Luna, GPT 5.6 Luna y Muse Spark Contributor.
- **OpenAI-compatible chat completions:** GLM, Kimi, LongCat, MiMo, DeepSeek, Hy y Space Bunny.
- **Anthropic Messages API:** Qwen, MiniMax M3 y MiniMax M2.7.

Clientes validados además de OpenCode: Hermes (con el fix indicado en la documentación oficial), Claude Code, Codex, ZCode, Pi, jcode (v0.81.6 o posterior) y Kilo Code CLI (con el fix correspondiente). DeepSeek Harness, GitHub Copilot Chat, Kimi Code y MiMo Code tienen soporte incompleto o pendiente para la información de sesión.

## Privacidad

- Grok 4.7/4.6 y GPT 6/5.6 Luna: no usan los datos para entrenamiento; retención de hasta **30 días** por monitoreo de abuso o funciones stateful.
- La mayoría de los modelos: no usan los datos para entrenamiento y tienen retención de **0 días**.
- Muse Spark 1.3/1.2 Contributor: **sí** puede usar prompts y completions para entrenamiento; no es ZDR.
- DeepSeek: ZDR renovado mensualmente; el acuerdo publicado durante esta revisión es válido hasta el **31 de octubre de 2026**.

## Notas

- Solo un miembro por workspace puede suscribirse a Go.
- Los modelos están hosteados en EE. UU.; verificá la política vigente antes de enviar información sensible.
- La disponibilidad y los límites pueden cambiar a medida que OpenCode prueba y agrega modelos.
- Consultá `/models` en la TUI o el catálogo live para confirmar disponibilidad antes de fijar un modelo en una configuración.
