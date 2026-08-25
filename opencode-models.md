# OpenCode Go - Guía de Modelos

> **Información actualizada:** 22 de agosto de 2026
> Fuente: [opencode.ai/docs/go](https://opencode.ai/docs/go/)

Suscripción: **$10/mes** ($5 primer mes) | Límites: $12/5h, $30/semana, $60/mes

---

## Modelos Premium (máxima calidad, menos requests)

| Modelo | req/5h | req/semana | req/mes | Mejor para |
|--------|--------|------------|---------|------------|
| Kimi K3 | ~110 | ~250 | ~490 | Flagship Kimi, razonamiento top, contexto largo |
| Grok 4.5 | ~120 | ~300 | ~600 | Razonamiento fuerte xAI, tareas complejas |
| Qwen3.8 Max | ~160 | ~400 | ~810 | Máxima calidad Qwen, arquitectura y sistemas grandes |
| GLM-5.3 | ~220 | ~540 | ~1,080 | Nueva generación GLM, razonamiento de primer nivel |
| Qwen3.7 Max | ~340 | ~840 | ~1,690 | Razonamiento avanzado con contexto extenso |
| GLM-5.2 | ~880 | ~2,150 | ~4,300 | Tareas complejas de razonamiento y refactorización profunda |
| GLM-5.1 | ~880 | ~2,150 | ~4,300 | Similar a GLM-5.2, razonamiento de primer nivel |
| DeepSeek V4 Pro | ~1,050 | ~2,600 | ~5,200 | Razonamiento fuerte, buena relación calidad/precio |
| Kimi K2.6 | ~1,150 | ~2,880 | ~5,750 | Razonamiento avanzado, código multi-archivo |

**Úsalos cuando:** Necesites la mejor calidad posible — refactors grandes, arquitectura, debugging complejo. No los gastes en tareas triviales. Kimi K3, Grok 4.5 y Qwen3.8 Max tienen usage reducido ($15), usalos con criterio.

---

## Modelos Balanceados (calidad/request)

| Modelo | req/5h | req/semana | req/mes | Mejor para |
|--------|--------|------------|---------|------------|
| Kimi K2.7 Code | ~1,350 | ~3,380 | ~6,750 | Código optimizado, buen balance calidad/volumen |
| GPT 5.6 Luna | ~2,050 | ~5,100 | ~10,250 | Modelo OpenAI en Go, buena calidad general |
| MiniMax M3 | ~3,200 | ~8,000 | ~16,000 | API Anthropic, nueva generación con buen rendimiento |
| MiMo-V2.5-Pro | ~3,250 | ~8,150 | ~16,300 | Generación de código complejo, lógica de negocio |
| Qwen3.6 Plus | ~3,300 | ~8,200 | ~16,300 | Tareas generales de codificación, rápido |
| MiniMax M2.7 | ~3,400 | ~8,500 | ~17,000 | API Anthropic, buena calidad probada |
| DeepSeek V4 Flash Vision Exp | ~3,800 | ~9,450 | ~18,900 | Flash con visión (experimental) |
| Qwen3.7 Plus | ~4,300 | ~10,800 | ~21,600 | Versión mejorada de Qwen, más rápido que Qwen3.6 |
| Hy3 | ~4,300 | ~10,750 | ~21,500 | Alto volumen, buen costo-efectividad |
| DeepSeek V4 Flash | ~7,600 | ~18,900 | ~37,800 | Código rápido, alto throughput |

**Úsalos cuando:** Quieras buena calidad sin gastar tu límite premium. Son tu "daily driver" para la mayoría del trabajo.

---

## Modelos High-Volume (máximo rendimiento)

| Modelo | req/5h | req/semana | req/mes | Mejor para |
|--------|--------|------------|---------|------------|
| MiMo-V2.5 | ~30,100 | ~75,200 | ~150,400 | Ultra económico, contextos enormes, tareas de bajo riesgo |
| Muse Spark 1.2 Contributor | ~45,300 | ~113,300 | ~226,600 | Máximo volumen (regiones limitadas; datos usados para train) |
| Ox Alpha Free | ∞ | ∞ | ∞ | Gratis por tiempo limitado |

**Úsalos cuando:** Estés haciendo muchas iteraciones rápidas, prototipado, o tareas de bajo riesgo donde la velocidad importa más que la perfección.

⚠️ **Muse Spark 1.2 Contributor:** precio muy bajo a cambio de permitir que Meta use prompts/completions para entrenar. Solo en regiones permitidas por Meta.

---

## Código vs Planeamiento vs Testing vs Documentación

### Para Código (generación, implementación, debugging)

| Modelo | Por qué |
|--------|---------|
| DeepSeek V4 Flash | Optimizado para código, máxima velocidad entre modelos de calidad, ~7,600 req/5h |
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
| Grok 4.5 | Razonamiento fuerte xAI para diseño y arquitectura |
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
- **Cobertura masiva / tests repetitivos** → DeepSeek V4 Flash, Hy3 o MiMo-V2.5
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

- **Tareas complejas/críticas** → Kimi K3, GLM-5.3, Grok 4.5, o Qwen3.8 Max
- **Día a día** → DeepSeek V4 Flash, Qwen3.7 Plus, Kimi K2.7 Code, o MiniMax M3
- **Iteraciones rápidas / prototipado** → DeepSeek V4 Flash, Hy3, MiMo-V2.5
- **Testing** → GLM-5.3 (complejo), Kimi K2.7 Code (TDD), DeepSeek V4 Flash (cobertura)
- **Documentación** → Kimi K3/GLM-5.3 (crítica), GLM-5.2/GPT 5.6 Luna (manuales), Hy3/DeepSeek V4 Flash (volumen)
- **Compatibilidad Anthropic** → MiniMax M3 / M2.7, Qwen3.8/3.7 Max/Plus
- **Visión** → DeepSeek V4 Flash Vision Exp
- **Planear + ejecutar** → Usa Kimi K3 / GLM-5.3 / Grok 4.5 para el plan, luego cambia a DeepSeek V4 Flash o Qwen3.7 Plus para la ejecución
- **Un solo modelo para todo** → DeepSeek V4 Pro, Kimi K2.7 Code, o MiniMax M3
- **Máximo volumen gratis** → Ox Alpha Free (tiempo limitado)
- **Cuidado con usage $15** → Kimi K3, Grok 4.5, GLM-5.3, Qwen3.8 Max, GPT 5.6 Luna, MiMo-V2.5-Pro, DeepSeek V4 Pro/Vision — se agotan más rápido del cupo mensual efectivo

---

## Precios por 1M tokens

| Modelo | Entrada | Salida | Cache Read | Cache Write | Usage incl. |
|--------|---------|--------|------------|-------------|-------------|
| Grok 4.5 | $2.00 | $6.00 | $0.30 | - | $15 |
| GPT 5.6 Luna (≤272K) | $0.20 | $1.20 | $0.02 | $0.25 | $15 |
| GPT 5.6 Luna (>272K) | $0.40 | $1.80 | $0.04 | $0.50 | $15 |
| GLM-5.3 | $1.40 | $4.40 | $0.26 | - | $15 |
| GLM-5.2 | $1.40 | $4.40 | $0.26 | - | $60 |
| GLM-5.1 | $1.40 | $4.40 | $0.26 | - | $60 |
| Kimi K3 | $3.00 | $15.00 | $0.30 | - | $15 |
| Kimi K2.7 Code | $0.95 | $4.00 | $0.19 | - | $60 |
| Kimi K2.6 | $0.95 | $4.00 | $0.16 | - | $60 |
| MiMo-V2.5 | $0.14 | $0.28 | $0.0028 | - | $60 |
| MiMo-V2.5-Pro | $0.435 | $0.87 | $0.003625 | - | $15 |
| MiniMax M3 | $0.30 | $1.20 | $0.06 | - | $60 |
| MiniMax M2.7 | $0.30 | $1.20 | $0.06 | $0.375 | $60 |
| Muse Spark 1.2 Contributor | $0.10 | $0.20 | $0.002 | - | $60 |
| Qwen3.8 Max | $2.00 | $6.00 | $0.25 | $2.50 | $15 |
| Qwen3.7 Max | $2.50 | $7.50 | $0.50 | $3.125 | $60 |
| Qwen3.7 Plus (≤256K) | $0.40 | $1.60 | $0.04 | $0.50 | $60 |
| Qwen3.7 Plus (>256K) | $1.20 | $4.80 | $0.12 | $1.50 | $60 |
| Qwen3.6 Plus (≤256K) | $0.50 | $3.00 | $0.05 | $0.625 | $60 |
| Qwen3.6 Plus (>256K) | $2.00 | $6.00 | $0.20 | $2.50 | $60 |
| DeepSeek V4 Pro (Off-Peak) | $0.66 | $1.98 | $0.022 | - | $15 |
| DeepSeek V4 Pro (Peak) | $1.32 | $3.96 | $0.044 | - | $15 |
| DeepSeek V4 Flash (Off-Peak) | $0.22 | $0.66 | $0.007 | - | $30 |
| DeepSeek V4 Flash (Peak) | $0.44 | $1.32 | $0.014 | - | $30 |
| DeepSeek V4 Flash Vision Exp (Off-Peak) | $0.22 | $0.66 | $0.007 | - | $15 |
| DeepSeek V4 Flash Vision Exp (Peak) | $0.44 | $1.32 | $0.014 | - | $15 |
| Hy3 | $0.14 | $0.58 | $0.035 | - | $60 |
| Ox Alpha Free | - | - | - | - | - |

**DeepSeek peak hours:** 01:00–04:00 y 06:00–10:00 UTC; el resto es Off-Peak.

---

## Notas adicionales

- Si te quedás sin límite, activá **"Use balance"** en la consola para usar créditos de Zen como respaldo
- Los modelos están hosteados en **US, EU y Singapur** para acceso global estable
- La mayoría de proveedores siguen **zero-retention (0 days)** y no usan tus datos para entrenamiento
- **Excepciones de privacy:**
  - Grok 4.5 y GPT 5.6 Luna: retención 30 días (abuse monitoring / features stateful)
  - Muse Spark 1.2 Contributor: **SÍ usa datos para train** (no es ZDR)
  - DeepSeek: ZDR renovado mensualmente; válido hasta **31 de agosto de 2026**
- Solo **un miembro por workspace** puede suscribirse a Go
- La lista de modelos puede cambiar a medida que se agregan nuevos
- **API style:**
  - MiniMax M3/M2.7 y Qwen (3.8/3.7/3.6): API estilo Anthropic (`@ai-sdk/anthropic`)
  - Grok 4.5, GPT 5.6 Luna, Muse Spark: OpenAI Responses API (`@ai-sdk/openai`)
  - Resto: OpenAI-compatible chat completions
- Qwen3.7/3.6 Plus y GPT 5.6 Luna tienen precios diferentes según el tamaño de contexto
- Model ID en config: `opencode-go/<model-id>` (ej. `opencode-go/kimi-k3`)
- Catálogo live: `https://opencode.ai/zen/go/v1/models`
