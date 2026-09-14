# OpenCode Go - Guía de Modelos

> **Información actualizada:** 13 de septiembre de 2026
> Fuente: [opencode.ai/docs/go](https://opencode.ai/docs/go/)

Suscripción: **$10/mes** | Límites: $12/5h, $30/semana, $60/mes

---

## Modelos Premium (máxima calidad, menos requests)

| Modelo | req/5h | req/semana | req/mes | Mejor para |
|--------|--------|------------|---------|------------|
| Kimi K3 | ~110 | ~250 | ~490 | Flagship Kimi, razonamiento top, contexto largo |
| Qwen3.8 Max | ~160 | ~400 | ~810 | Máxima calidad Qwen, arquitectura y sistemas grandes |
| Grok 4.6 | ~169 | ~423 | ~845 | Razonamiento fuerte xAI, tareas complejas |
| Qwen3.7 Max | ~170 | ~420 | ~840 | Razonamiento avanzado con contexto extenso |
| GLM-5.3 | ~220 | ~540 | ~1,080 | Nueva generación GLM, razonamiento de primer nivel |
| GLM-5.2 | ~880 | ~2,150 | ~4,300 | Tareas complejas de razonamiento y refactorización profunda |
| GLM-5.1 | ~880 | ~2,150 | ~4,300 | Similar a GLM-5.2, razonamiento de primer nivel |
| DeepSeek V4 Pro | ~1,050 | ~2,600 | ~5,200 | Razonamiento fuerte, buena relación calidad/precio |
| Kimi K2.6 | ~1,150 | ~2,880 | ~5,750 | Razonamiento avanzado, código multi-archivo |

**Úsalos cuando:** Necesites la mejor calidad posible — refactors grandes, arquitectura, debugging complejo. No los gastes en tareas triviales. Kimi K3, Grok 4.6, Qwen3.8 Max y GLM-5.3 tienen usage reducido ($15), usalos con criterio.

---

## Modelos Balanceados (calidad/request)

| Modelo | req/5h | req/semana | req/mes | Mejor para |
|--------|--------|------------|---------|------------|
| Kimi K2.7 Code | ~1,350 | ~3,380 | ~6,750 | Código optimizado, buen balance calidad/volumen |
| Hy4 preview | ~1,350 | ~3,380 | ~6,770 | Preview de la nueva gen Hunyuan, razonamiento |
| GPT 5.6 Luna | ~2,050 | ~5,100 | ~10,250 | Modelo OpenAI en Go, buena calidad general |
| MiniMax M3 | ~3,200 | ~8,000 | ~16,000 | API estilo Anthropic, nueva generación con buen rendimiento |
| MiMo-V2.5-Pro | ~3,250 | ~8,150 | ~16,300 | Generación de código complejo, lógica de negocio |
| Qwen3.6 Plus | ~3,300 | ~8,200 | ~16,300 | Tareas generales de codificación, rápido |
| MiniMax M2.7 | ~3,400 | ~8,500 | ~17,000 | API estilo Anthropic, buena calidad probada |
| Qwen3.7 Plus | ~4,300 | ~10,800 | ~21,600 | Versión mejorada de Qwen, más rápido que Qwen3.6 |
| Hy3 | ~4,300 | ~10,750 | ~21,500 | Alto volumen, buen costo-efectividad |
| Qwen3.8 Flash | ~5,400 | ~13,500 | ~27,000 | Qwen rápido y económico, alto throughput |
| GLM-5.3-Flash | ~6,320 | ~15,790 | ~31,580 | GLM rápido, ahora con usage $60 |
| DeepSeek V4.1 Flash | ~6,500 | ~16,250 | ~32,500 | Nuevo flash DeepSeek; promo 4x hasta el 20 sep |
| DeepSeek V4 Flash Vision Exp | ~6,500 | ~16,250 | ~32,500 | Flash con visión (experimental) |
| LongCat-2.0 | ~11,400 | ~28,600 | ~57,200 | Alto volumen, tareas de bajo riesgo y contexto largo |
| DeepSeek V4 Flash | ~13,000 | ~32,500 | ~65,000 | Código rápido, alto throughput |

**Úsalos cuando:** Quieras buena calidad sin gastar tu límite premium. Son tu "daily driver" para la mayoría del trabajo.

---

## Modelos High-Volume (máximo rendimiento)

| Modelo | req/5h | req/semana | req/mes | Mejor para |
|--------|--------|------------|---------|------------|
| MiMo-V2.5 | ~30,100 | ~75,200 | ~150,400 | Ultra económico, contextos enormes, tareas de bajo riesgo |
| Muse Spark 1.3 Contributor | ~45,300 | ~113,300 | ~226,600 | Máximo volumen (regiones limitadas; datos usados para train) |
| Muse Spark 1.2 Contributor | ~45,300 | ~113,300 | ~226,600 | Máximo volumen (regiones limitadas; datos usados para train) |

**Úsalos cuando:** Estés haciendo muchas iteraciones rápidas, prototipado, o tareas de bajo riesgo donde la velocidad importa más que la perfección.

⚠️ **Muse Spark 1.3/1.2 Contributor:** precio muy bajo a cambio de permitir que Meta use prompts/completions para entrenar. Solo en regiones permitidas por Meta.

---

## Código vs Planeamiento vs Testing vs Documentación

### Para Código (generación, implementación, debugging)

| Modelo | Por qué |
|--------|---------|
| DeepSeek V4 Flash | Optimizado para código, máxima velocidad entre modelos de calidad, ~13,000 req/5h |
| DeepSeek V4.1 Flash | Nuevo flash de DeepSeek, alto throughput para código (promo 4x hasta el 20 sep) |
| GLM-5.3-Flash | Código rápido y consistente, ~6,320 req/5h |
| DeepSeek V4 Pro | Versión más pesada de DeepSeek, mejor razonamiento para código complejo |
| Kimi K2.7 Code | Modelo específicamente optimizado para código, buena relación calidad/volumen |
| MiMo-V2.5-Pro | Especializado en generación de código, calidad cercana a modelos premium |
| Qwen3.7 Plus | Muy buen código costo-efectivo, ~4,300 req/5h |
| MiniMax M3 | Buen balance y API estilo Anthropic |
| GLM-5.3 / GLM-5.2 | Fuerte en generación de código y refactors de alta calidad |
| Kimi K3 | Flagship cuando el código es crítico y necesitás lo mejor |

### Para Planeamiento (arquitectura, diseño, razonamiento multi-paso)

| Modelo | Por qué |
|--------|---------|
| Kimi K3 | Mejor Kimi disponible — ideal para planes complejos y sistemas grandes |
| GLM-5.3 | Nueva generación GLM, razonamiento de primer nivel |
| Grok 4.6 | Razonamiento fuerte xAI para diseño y arquitectura |
| Qwen3.8 Max / Qwen3.7 Max | Razonamiento avanzado con contexto extenso |
| GLM-5.2 | Excelente para planes de implementación y diseño |
| Kimi K2.6 | Buen razonamiento y contexto largo sin gastar K3 |
| DeepSeek V4 Pro | Razonamiento sólido para planes detallados paso a paso |

### Para Testing (generación de tests, TDD, validación)

| Modelo | Por qué |
|--------|---------|
| GLM-5.3 / GLM-5.2 | Genera tests con razonamiento profundo — edge cases y escenarios complejos |
| DeepSeek V4 Pro | Excelente para tests que requieren entender la lógica de negocio completa |
| MiMo-V2.5-Pro | Especializado en código, tests unitarios e integración de alta calidad |
| Kimi K2.7 Code | Optimizado para código — bueno para suites de tests completas |
| DeepSeek V4 Flash | Para iterar rápido en tests — generación masiva de cobertura |
| MiniMax M3 | Buen balance para tests de regresión y validación de contratos |
| Qwen3.7 Plus / Hy3 | Rápidos y costo-efectivos para tests repetitivos y de humo |

**Estrategia Testing:**
- **Tests complejos / edge cases** → GLM-5.3, GLM-5.2 o DeepSeek V4 Pro
- **TDD rápido** → Kimi K2.7 Code o MiMo-V2.5-Pro
- **Cobertura masiva / tests repetitivos** → DeepSeek V4 Flash, Hy3, MiMo-V2.5 o DeepSeek V4.1 Flash (promo)
- **Tests de regresión / validación** → MiniMax M3 o Qwen3.7 Plus

### Para Documentación (guías, manuales, READMEs, onboarding, arquitectura)

| Modelo | Por qué |
|--------|---------|
| GLM-5.3 / GLM-5.2 | Razonamiento profundo: estructura lógica, consistencia en textos largos, precisa explicación de conceptos |
| Kimi K3 | Calidad top para documentación crítica de arquitectura y guías complejas de alto nivel |
| GPT 5.6 Luna | Buena calidad general de redacción técnica y tono profesional |
| Hy3 | Alto volumen y costo-efectivo: ideal para generar manuales extensos o docs repetitivas |
| Qwen3.7 Plus / Qwen3.6 Plus | Rápidos y versátiles para documentación de API, guías de onboarding y docs de features |
| DeepSeek V4 Flash | Velocidad para iterar documentación masiva (referencias de API, changelogs, docs autogeneradas) |
| MiniMax M3 | Buen balance para guías que mezclan prosa técnica con ejemplos de código |

**Estrategia Documentación:**
- **Documentación crítica / arquitectura** → Kimi K3 o GLM-5.3 (calidad top, razonamiento profundo)
- **Guías y manuales extensos** → GLM-5.2 o GPT 5.6 Luna (consistencia narrativa en textos largos)
- **Onboarding / guías paso a paso** → Qwen3.7 Plus o MiniMax M3 (claridad y rapidez)
- **Documentación masiva / autogenerada** → Hy3 o DeepSeek V4 Flash (volumen y velocidad)
- **Referencias de API / changelogs** → DeepSeek V4 Flash (iteración rápida y alto throughput)

---

## Estrategia recomendada

- **Tareas complejas/críticas** → Kimi K3, GLM-5.3, Grok 4.6, o Qwen3.8 Max
- **Día a día** → DeepSeek V4 Flash, Qwen3.7 Plus, Kimi K2.7 Code, o MiniMax M3
- **Iteraciones rápidas / prototipado** → DeepSeek V4 Flash, Hy3, MiMo-V2.5 (o DeepSeek V4.1 Flash mientras dure la promo 4x, hasta el 20 sep)
- **Testing** → GLM-5.3 (complejo), Kimi K2.7 Code (TDD), DeepSeek V4 Flash (cobertura)
- **Documentación** → Kimi K3/GLM-5.3 (crítica), GLM-5.2/GPT 5.6 Luna (manuales), Hy3/DeepSeek V4 Flash (volumen)
- **Compatibilidad Anthropic** → Qwen3.8/3.7/3.6 y MiniMax M3/M2.7 (Messages API)
- **Visión** → DeepSeek V4 Flash Vision Exp
- **Planear + ejecutar** → Usa Kimi K3 / GLM-5.3 / Grok 4.6 para el plan, luego cambia a GLM-5.3-Flash, DeepSeek V4 Flash o Qwen3.7 Plus para la ejecución
- **Un solo modelo para todo** → DeepSeek V4 Pro, Kimi K2.7 Code, o MiniMax M3
- **Máximo volumen** → MiMo-V2.5 o Muse Spark 1.3/1.2 Contributor (si están disponibles en tu región)
- **Cuidado con usage $15** → Kimi K3, Grok 4.6, GLM-5.3, Qwen3.8 Max, GPT 5.6 Luna, MiMo-V2.5-Pro, DeepSeek V4 Pro/Vision Exp/V4.1 — se agotan más rápido del cupo mensual efectivo. Ojo: GLM-5.3-Flash subió a $60 y DeepSeek V4 Flash a $30

---

## Precios por 1M tokens

| Modelo | Entrada | Salida | Cache Read | Cache Write | Usage incl. |
|--------|---------|--------|------------|-------------|-------------|
| Grok 4.6 (≤200K) | $2.00 | $6.00 | $0.50 | - | $15 |
| Grok 4.6 (>200K) | $4.00 | $12.00 | $1.00 | - | $15 |
| GPT 5.6 Luna (≤272K) | $0.20 | $1.20 | $0.02 | $0.25 | $15 |
| GPT 5.6 Luna (>272K) | $0.40 | $1.80 | $0.04 | $0.50 | $15 |
| GLM-5.3 | $1.40 | $4.40 | $0.26 | - | $15 |
| GLM-5.3-Flash | $0.15 | $0.50 | $0.03 | - | $60 |
| GLM-5.2 | $1.40 | $4.40 | $0.26 | - | $60 |
| GLM-5.1 | $1.40 | $4.40 | $0.26 | - | $60 |
| Kimi K3 | $3.00 | $15.00 | $0.30 | - | $15 |
| Kimi K2.7 Code | $0.95 | $4.00 | $0.19 | - | $60 |
| Kimi K2.6 | $0.95 | $4.00 | $0.16 | - | $60 |
| LongCat-2.0 | $0.30 | $1.20 | $0.006 | - | $60 |
| MiMo-V2.5 | $0.14 | $0.28 | $0.0028 | - | $60 |
| MiMo-V2.5-Pro | $0.435 | $0.87 | $0.003625 | - | $15 |
| MiniMax M3 | $0.30 | $1.20 | $0.06 | - | $60 |
| MiniMax M2.7 | $0.30 | $1.20 | $0.06 | $0.375 | $60 |
| MiniMax M2.5 | $0.30 | $1.20 | $0.06 | $0.375 | $60 |
| Muse Spark 1.3 Contributor | $0.10 | $0.20 | $0.002 | - | $60 |
| Muse Spark 1.2 Contributor | $0.10 | $0.20 | $0.002 | - | $60 |
| Qwen3.8 Max | $2.00 | $6.00 | $0.25 | $2.50 | $15 |
| Qwen3.8 Flash | $0.15 | $0.47 | $0.016 | $0.20 | $30 |
| Qwen3.7 Max | $2.50 | $7.50 | $0.50 | $3.125 | $30 |
| Qwen3.7 Plus (≤256K) | $0.40 | $1.60 | $0.04 | $0.50 | $60 |
| Qwen3.7 Plus (>256K) | $1.20 | $4.80 | $0.12 | $1.50 | $60 |
| Qwen3.6 Plus (≤256K) | $0.50 | $3.00 | $0.05 | $0.625 | $60 |
| Qwen3.6 Plus (>256K) | $2.00 | $6.00 | $0.20 | $2.50 | $60 |
| DeepSeek V4.1 Flash (Off-Peak) | $0.15 | $0.60 | $0.003 | - | $15 (4x→$60 hasta 20 sep) |
| DeepSeek V4.1 Flash (Peak) | $0.30 | $1.20 | $0.006 | - | $15 (4x→$60 hasta 20 sep) |
| DeepSeek V4 Pro (Off-Peak) | $0.66 | $1.98 | $0.022 | - | $15 |
| DeepSeek V4 Pro (Peak) | $1.32 | $3.96 | $0.044 | - | $15 |
| DeepSeek V4 Flash (Off-Peak) | $0.15 | $0.60 | $0.003 | - | $30 |
| DeepSeek V4 Flash (Peak) | $0.30 | $1.20 | $0.006 | - | $30 |
| DeepSeek V4 Flash Vision Exp (Off-Peak) | $0.15 | $0.60 | $0.003 | - | $15 |
| DeepSeek V4 Flash Vision Exp (Peak) | $0.30 | $1.20 | $0.006 | - | $15 |
| Hy4 preview | $0.834 | $2.501 | $0.042 | - | $30 |
| Hy3 | $0.14 | $0.58 | $0.035 | - | $60 |

**DeepSeek peak hours:** 01:00–04:00 y 06:00–10:00 UTC, de lunes a viernes; fines de semana y el resto del horario son Off-Peak.

**DeepSeek V4.1 Flash:** nuevo en Go. Promo **4x de usage** (límite mensual $15 → $60, ~26,000 req/5h) vigente hasta el **20 de septiembre de 2026**; después vuelve a ~6,500 req/5h.

**DeepSeek V4 Flash Vision Exp:** las imágenes se convierten en tokens según sus dimensiones y se facturan como tokens de entrada además del texto.

---

## Notas adicionales

- Si te quedás sin límite, activá **"Use balance"** en la consola para usar créditos de Zen como respaldo, o seguí usando los modelos gratuitos de Zen
- Los modelos están hosteados en **US**; los proveedores siguen una política de zero-retention
- La mayoría de modelos no usa tus datos para entrenamiento y tiene retención de **0 días**
- **Excepciones de privacy:**
  - Grok 4.6 y GPT 5.6 Luna: retención 30 días (abuse monitoring / features stateful)
  - Muse Spark 1.3/1.2 Contributor: **SÍ usa datos para train** (no es ZDR; regiones limitadas)
  - DeepSeek: ZDR renovado mensualmente; válido hasta **30 de septiembre de 2026**
- Solo **un miembro por workspace** puede suscribirse a Go
- La lista de modelos puede cambiar a medida que se agregan nuevos
- **Clientes validados** además de OpenCode (soportan el header de sesión `x-opencode-session`, que optimiza routing y prompt caching): Hermes, Claude Code, Codex, ZCode, Pi, jcode (≥ v0.81.6) y Kilo Code CLI. Problemáticos sin soporte completo: Kimi Code, MiMo Code (fix en PR sin merge), GitHub Copilot Chat y DeepSeek Harness
- **API style:**
   - Qwen (3.8/3.7/3.6) y MiniMax M3/M2.7/M2.5: API Messages (`@ai-sdk/anthropic`)
   - Grok 4.6, GPT 5.6 Luna y Muse Spark 1.3/1.2 Contributor: OpenAI Responses API (`@ai-sdk/openai`)
   - GLM, Kimi, LongCat, MiMo, DeepSeek (incl. V4.1 Flash), Hy4 preview y Hy3: OpenAI-compatible chat completions
- Qwen3.7/3.6 Plus, GPT 5.6 Luna y Grok 4.6 tienen precios diferentes según el tamaño de contexto
- MiniMax M2.5 aparece en endpoints/precios de Go pero está deprecado (retirada 5 de agosto de 2026); no lo uses en configuraciones nuevas
- Model ID en config: `opencode-go/<model-id>` (ej. `opencode-go/kimi-k3`)
- Catálogo live: `https://opencode.ai/zen/go/v1/models`
