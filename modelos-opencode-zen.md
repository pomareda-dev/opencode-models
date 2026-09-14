# Guía de modelos gratuitos de OpenCode Zen

> Guía práctica sobre los modelos gratuitos disponibles en [OpenCode Zen](https://opencode.ai/docs/zen/) y cómo elegir el más adecuado según la tarea: planeamiento, código, refactorización y tests.
>
> Última actualización: 13 de septiembre de 2026. Los modelos gratuitos son "por tiempo limitado" y pueden cambiar o retirarse sin aviso.

---

## Índice

1. [¿Qué es OpenCode Zen?](#1-qué-es-opencode-zen)
2. [Lista de modelos gratuitos](#2-lista-de-modelos-gratuitos)
3. [Diferencias clave entre ellos](#3-diferencias-clave-entre-ellos)
4. [¿Cuál usar según la tarea?](#4-cuál-usar-según-la-tarea)
5. [Cómo configurarlos](#5-cómo-configurarlos)
6. [Buenas prácticas y advertencias](#6-buenas-prácticas-y-advertencias)

---

## 1. ¿Qué es OpenCode Zen?

OpenCode Zen es la pasarela (gateway) de modelos curada por el equipo de OpenCode. A diferencia de usar un modelo vía OpenRouter u otro intermediario, en Zen cada combinación modelo/proveedor ha sido probada y evaluada para funcionar bien como **agente de código** (tool calling, ediciones multi-archivo, etc.).

Los modelos gratuitos (`Free`) cuestan **$0 en input, output y lectura de caché**, pero existen porque los equipos detrás de ellos recopilan feedback para mejorarlos. Son ideales para experimentar sin gastar créditos.

---

## 2. Lista de modelos gratuitos

| Modelo | Model ID | Familia / Origen | Tipo | Política de privacidad |
|---|---|---|---|---|
| **Big Pickle** | `big-pickle` | Stealth (no revelada) | Modelo misterioso de gama alta | ⚠️ Los datos pueden usarse para mejorar el modelo durante el periodo gratuito |
| **MiMo-V2.5 Free** | `mimo-v2.5-free` | MiMo (Xiaomi) | Razonamiento eficiente | ⚠️ Los datos se recopilan para mejorar el modelo |
| **Ling 3.0 Flash Fin Free** | `ling-3.0-flash-fin-free` | Ling (Ant Group) | Variante flash, orientada a finanzas | ⚠️ Los datos se recopilan para mejorar el modelo |
| **Nemotron 3 Ultra Free** | `nemotron-3-ultra-free` | NVIDIA | Razonamiento profundo (pesado) | ⚠️ Endpoint trial de NVIDIA: no enviar datos confidenciales; las sesiones se registran |
| **Nemotron 3.5 Lightning Free** | `nemotron-3.5-lightning-free` | NVIDIA | Variante ligera/rápida | ⚠️ Endpoint trial de NVIDIA: mismas condiciones que Ultra |
| **Muse Spark 1.3 Contributor Free** | `muse-spark-1.3-contributor-free` | Meta | Generalista | ⚠️⚠️ **Tus prompts y respuestas se usan para entrenar futuros modelos de Meta** |

Los modelos no usan todos el mismo endpoint. El ID de configuración siempre es `opencode/<model-id>`, pero el endpoint depende de la familia: Responses para GPT/Grok/Muse, Messages para Claude/Qwen, endpoints Google para Gemini y chat completions compatibles con OpenAI para el resto.

El catálogo completo, los precios y los metadatos se pueden consultar en `https://opencode.ai/zen/v1/models`.

### Privacidad vigente

Todos los modelos se sirven desde infraestructura en **US**. La política general es zero-retention y no entrenamiento, con estas excepciones documentadas:

- **Big Pickle**, **MiMo-V2.5 Free** y **Ling 3.0 Flash Fin Free**: durante el periodo gratuito pueden recopilar datos para mejorar el modelo.
- **Nemotron 3 Ultra/Lightning Free**: endpoints trial de NVIDIA; las sesiones se registran y no deben recibir datos personales o confidenciales.
- **OpenAI y Anthropic**: sus APIs pueden retener solicitudes hasta 30 días según sus políticas.
- **Muse Spark 1.3 Contributor Free**: permite usar prompts y respuestas para entrenar futuros modelos de Meta.

---

## 3. Diferencias clave entre ellos

### 3.1 Privacidad (la diferencia más importante)

Este es el criterio que deberías ponderar primero, porque el precio es igual ($0) para todos:

| Nivel | Modelos | Implicación |
|---|---|---|
| 🟢 Más seguro | **Ninguno** | Los modelos gratuitos actuales tienen condiciones de recopilación, trial o entrenamiento. No son aptos para código sensible. |
| 🟡 Uso para mejora | Big Pickle, MiMo-V2.5, Ling 3.0 Flash Fin | Tus conversaciones pueden revisarse/usarse para mejorar el modelo durante el periodo gratuito. Evita secretos (API keys, credenciales, lógica propietaria crítica). |
| 🔴 Revisión activa | Nemotron 3 Ultra / Lightning | Endpoints *trial* de NVIDIA: uso registrado por seguridad, términos de prueba. No enviar datos personales ni confidenciales. |
| 🔴 Entrenamiento directo | Muse Spark 1.3 Contributor | A cambio de la gratuidad, **cedes tus prompts/completions como datos de entrenamiento** para futuros modelos de Meta. |

### 3.2 Estilo del modelo

- **Stealth / misterioso (Big Pickle)**: identidad no revelada. Sigue disponible gratis por tiempo limitado y puede cambiar sin aviso.
- **Razonadores (MiMo-V2.5, Nemotron 3 Ultra)**: priorizan cadenas de razonamiento antes de responder. Mejores en problemas que requieren planear o deducir, a costa de mayor latencia y más tokens de salida.
- **Ligeros/rápidos (Nemotron 3.5 Lightning, Ling 3.0 Flash Fin)**: optimizados para baja latencia. Ideales para ciclos cortos y tareas repetitivas, menos profundos en problemas grandes.
- **Contributor (Muse Spark 1.3)**: mismo modelo de pago que la versión normal, pero gratis a cambio de tus datos. Rendimiento de generalista moderno.

---

## 4. ¿Cuál usar según la tarea?

> Nota honesta: OpenCode no publica benchmarks por tarea para los modelos gratuitos, y estos cambian con frecuencia. Las recomendaciones siguientes combinan lo documentado (tamaño, variante, tipo de modelo) con la experiencia típica de estas familias. Como todos son gratis, **lo mejor es probar 2–3 con tu propio proyecto** y comparar.

### Resumen rápido

| Tarea | Primera opción | Alternativa | Evitar |
|---|---|---|---|
| 🗺️ Planeamiento | **Nemotron 3 Ultra Free** | Big Pickle, MiMo-V2.5 Free | Nemotron 3.5 Lightning |
| 💻 Escritura de código | **Big Pickle** | MiMo-V2.5 Free, Muse Spark 1.3 Contributor Free | — |
| ♻️ Refactorización | **Big Pickle** | Nemotron 3 Ultra Free | Nemotron 3.5 Lightning |
| 🧪 Tests | **Big Pickle** | Nemotron 3.5 Lightning Free | — |
| 📝 Documentación / guías / manuales | **Big Pickle** | MiMo-V2.5 Free | Nemotron 3.5 Lightning |

### 4.1 Planeamiento (arquitectura, descomposición de tareas, diseño)

**Recomendado: `nemotron-3-ultra-free`** — Es la variante "grande" de NVIDIA, orientada a razonamiento profundo. Para decidir arquitectura, dividir una feature en pasos o evaluar trade-offs quieres máxima calidad de razonamiento, aunque tarde más.

Alternativas:
- **Big Pickle**: si el planeamiento requiere mucho contexto del repo, suele manejar bien instrucciones complejas.
- **MiMo-V2.5 Free**: razonador eficiente; buena relación profundidad/velocidad para planes medianos.

Evita: **Lightning**, que sacrifica profundidad por velocidad, justo lo contrario de lo que necesitas al planear.

### 4.2 Código (escribir features, implementar funciones)

**Recomendado: `big-pickle`** — Al ser un stealth model de gama alta en evaluación gratuita, tiende al mejor rendimiento agéntico general (seguir instrucciones, usar herramientas, editar varios archivos coherentemente).

Alternativas:
- **MiMo-V2.5 Free**: buen razonamiento para diseñar casos límite; no lo uses con datos sensibles.
- **Muse Spark 1.3 Contributor Free**: generalista moderno; solo si no te importa ceder tus datos para entrenamiento.

### 4.3 Refactorización (reestructurar sin romper comportamiento)

**Recomendado: `big-pickle`** — Refactorizar exige entender dependencias entre archivos, mantener consistencia de estilo y no "inventar" APIs inexistentes. Los modelos de mayor capacidad agéntica fallan menos aquí.

Alternativas:
- **Nemotron 3 Ultra Free**: muy cuidadoso y metódico; buena segunda opción para refactors grandes y delicados, aunque más lento.
- **Ling 3.0 Flash Fin Free**: para refactors locales y rápidos, con la advertencia de que es una variante flash (menos profundidad).

Consejo: para refactors, pide primero un **plan** (con el modelo de planeamiento), revísalo, y luego ejecuta con el modelo de código.

### 4.4 Tests (unitarios, integración, TDD)

**Recomendado: `big-pickle`** — Generar tests es un ciclo iterativo de escribir → correr → corregir, con muchos contextos repetidos. Es un modelo generalista de alta capacidad agéntica; aun así, no envíes código sensible durante su periodo gratuito.

Alternativas:
- **Nemotron 3.5 Lightning Free**: aquí sí brilla su velocidad; perfecto para generar lotes de tests unitarios rutinarios o casos borde a partir de una función ya definida.
- **MiMo-V2.5 Free**: bueno para diseñar casos límite gracias a su razonamiento (edge cases, invariantes).

### 4.5 Documentación, guías y manuales (READMEs, onboarding, arquitectura)

**Recomendado: `big-pickle`** — Tras la retirada de Hy3 Free, Big Pickle es la mejor opción gratuita para documentación: es un modelo de gama alta que mantiene estructura y consistencia en textos largos y combina prosa con bloques de código.

Alternativas:
- **MiMo-V2.5 Free**: su razonamiento ayuda a estructurar manuales con jerarquía clara (secciones, pasos, casos de uso) y a anticipar dudas del lector.
- **Ling 3.0 Flash Fin Free**: para documentación corta o autogenerada de bajo riesgo (referencias, changelogs), aprovechando su baja latencia.

Evita: **Nemotron 3.5 Lightning**, que privilegia velocidad sobre profundidad narrativa; la documentación suele quedar superficial o desordenada.

Consejo: si la guía es larga o de varios archivos, pide primero un **índice/estructura** (con el modelo de planeamiento `nemotron-3-ultra-free`), revísalo, y luego redacta cada sección con `big-pickle` para mantener consistencia.

---

## 5. Cómo configurarlos

### 5.1 Conectar Zen

1. Inicia sesión en [opencode.ai/auth](https://opencode.ai/auth) y copia tu API key.
2. En la TUI ejecuta `/connect`, elige **OpenCode Zen** y pega la key.

### 5.2 Seleccionar modelo en la sesión

```
/models
```

y elige el modelo `opencode/<model-id>`. También puedes arrancar directamente:

```bash
opencode -m opencode/big-pickle
```

### 5.3 Fijar uno como predeterminado

En `opencode.json`:

```json
{
  "$schema": "https://opencode.ai/config.json",
  "model": "opencode/big-pickle"
}
```

### 5.4 Cambiar según la fase de trabajo (flujo recomendado)

```bash
# 1. Planear
opencode -m opencode/nemotron-3-ultra-free
# 2. Implementar / refactorizar
opencode -m opencode/big-pickle
# 3. Testear e iterar
opencode -m opencode/big-pickle
```

---

## 6. Buenas prácticas y advertencias

1. **No envíes secretos a ningún modelo gratuito**. Esto incluye `.env`, API keys, datos de clientes y algoritmos propietarios.
2. **Son temporales**: todos los modelos gratuitos pueden desaparecer. No construyas flujos de CI críticos dependiendo solo de uno.
3. **Verifica siempre el código generado**, especialmente en refactors: ejecuta tu suite de tests después de cada cambio.
4. **Combina modelos por fase** (plan → code → test) en vez de usar uno solo para todo: es gratis y obtienes lo mejor de cada uno.
5. Si un modelo gratuito responde mal en tu dominio (p. ej. legacy PHP/Laravel en este proyecto), prueba otro de la lista antes de pagar por uno de pago.
6. Consulta siempre la [documentación oficial de Zen](https://opencode.ai/docs/zen/) para ver la lista vigente, precios y fechas de deprecación.

### Cambios relevantes del catálogo (13/09/2026)

- **Modelos gratuitos:** la lista vigente no cambia (Big Pickle, MiMo-V2.5 Free, Ling 3.0 Flash Fin Free, Nemotron 3 Ultra/Lightning Free y Muse Spark 1.3 Contributor Free). En la revisión anterior se había sumado **Ling 3.0 Flash Fin Free**, retirado **Hy3 Free** y reemplazado **Muse Spark 1.2 Contributor Free** por el 1.3.
- **Deprecados** (no usar en configuraciones nuevas): la lista oficial se amplía con **Qwen3 Coder 480B** (6 feb), **Claude Haiku 3.5** (16 feb), **Kimi K2 y K2 Thinking** (6 mar), **MiniMax M2.1, GLM 4.7 y GLM 4.6** (15 mar), y **Claude Sonnet 4** (15 jun). Ya figuraban: **Gemini 3 Pro** (9 mar), las variantes **GPT Codex** — GPT 5.2/5.1/5.1 Max/5.1 Mini/5 Codex — (23 jul), **GLM 5** (14 may) y **MiniMax M2.5, Kimi K2.5 y Claude Opus 4.1** (5 ago).
- Zen sigue incorporando **GPT 6 Astra** (flagship), **GPT 5.6 Sol** y **GPT 5.6 Terra**, además de **Claude Fable 5.1/5**, **Claude Opus 5** y **Claude Sonnet 5**. GPT 5.6 Sol tiene un descuento del 50% vigente hasta el 18 de septiembre de 2026.
- **Auto-recarga** (saldo < $5 → recarga $20, configurable) y **workspaces** (restricción de modelos, límites mensuales por miembro, bring-your-own-key de OpenAI/Anthropic): sin cambios.
