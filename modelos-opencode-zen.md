# Guía de modelos gratuitos de OpenCode Zen

> Guía práctica sobre los modelos gratuitos disponibles en [OpenCode Zen](https://opencode.ai/docs/zen/) y cómo elegir el más adecuado según la tarea: planeamiento, código, refactorización y tests.
>
> Última actualización: agosto de 2026. Los modelos gratuitos son "por tiempo limitado" y pueden cambiar o retirarse sin aviso.

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

OpenCode Zen es la pasarela (gateway) de modelos curada por el equipo de OpenCode. A diferencia de usar un modelo vía OpenRouter u otro intermediario, en Zen cada combinación modelo/proveedor ha sido probada y benchmarked para funcionar bien como **agente de código** (tool calling, ediciones multi-archivo, etc.).

Los modelos gratuitos (`Free`) cuestan **$0 en input, output y lectura de caché**, pero existen porque los equipos detrás de ellos recopilan feedback para mejorarlos. Son ideales para experimentar sin gastar créditos.

---

## 2. Lista de modelos gratuitos

| Modelo | Model ID | Familia / Origen | Tipo | Política de privacidad |
|---|---|---|---|---|
| **Big Pickle** | `big-pickle` | Stealth (no revelada) | Modelo misterioso de gama alta | ⚠️ Los datos pueden usarse para mejorar el modelo durante el periodo gratuito |
| **Ox Alpha Free** | `x-preview-f-free` | Stealth (no revelada) | Modelo misterioso de gama alta | ✅ **Zero-retention**: no usan tus datos para entrenar |
| **MiMo-V2.5 Free** | `mimo-v2.5-free` | MiMo (Xiaomi) | Razonamiento eficiente | ⚠️ Los datos se recopilan para mejorar el modelo |
| **Hy3 Free** | `hy3-free` | Hunyuan 3 (Tencent) | Generalista grande | ⚠️ Los datos se recopilan para mejorar el modelo |
| **Nemotron 3 Ultra Free** | `nemotron-3-ultra-free` | NVIDIA | Razonamiento profundo (pesado) | ⚠️ Endpoint trial de NVIDIA: no enviar datos confidenciales; las sesiones se registran |
| **Nemotron 3.5 Lightning Free** | `nemotron-3.5-lightning-free` | NVIDIA | Variante ligera/rápida | ⚠️ Endpoint trial de NVIDIA: mismas condiciones que Ultra |
| **Muse Spark 1.2 Contributor Free** | `muse-spark-1.2-contributor-free` | Meta | Generalista | ⚠️⚠️ **Tus prompts y respuestas se usan para entrenar futuros modelos de Meta** |

Todos usan el endpoint `https://opencode.ai/zen/v1/chat/completions`, compatible con `@ai-sdk/openai-compatible`.

---

## 3. Diferencias clave entre ellos

### 3.1 Privacidad (la diferencia más importante)

Este es el criterio que deberías ponderar primero, porque el precio es igual ($0) para todos:

| Nivel | Modelos | Implicación |
|---|---|---|
| 🟢 Más seguro | **Ox Alpha Free** | Zero-retention explícito. El proveedor no retiene ni entrena con tus datos. Único gratuito apto para código sensible. |
| 🟡 Uso para mejora | Big Pickle, MiMo-V2.5, Hy3 | Tus conversaciones pueden revisarse/usarse para mejorar el modelo durante el periodo gratuito. Evita secretos (API keys, credenciales, lógica propietaria crítica). |
| 🔴 Revisión activa | Nemotron 3 Ultra / Lightning | Endpoints *trial* de NVIDIA: uso registrado por seguridad, términos de prueba. No enviar datos personales ni confidenciales. |
| 🔴 Entrenamiento directo | Muse Spark 1.2 Contributor | A cambio de la gratuidad, **cedes tus prompts/completions como datos de entrenamiento** para futuros modelos de Meta. |

### 3.2 Estilo del modelo

- **Stealth / misteriosos (Big Pickle, Ox Alpha)**: identidad no revelada. En Zen este tipo de modelos suelen ser candidatos a gama alta en evaluación, con buen rendimiento agéntico general. Suelen ser la apuesta segura como "modelo principal".
- **Razonadores (MiMo-V2.5, Nemotron 3 Ultra)**: priorizan cadenas de razonamiento antes de responder. Mejores en problemas que requieren planear o deducir, a costa de mayor latencia y más tokens de salida.
- **Ligeros/rápidos (Nemotron 3.5 Lightning)**: optimizados para baja latencia. Ideales para ciclos cortos y tareas repetitivas, menos profundos en problemas grandes.
- **Generalistas grandes (Hy3)**: buen equilibrio entre conocimiento amplio, redacción y código.
- **Contributor (Muse Spark 1.2)**: mismo modelo de pago que la versión normal, pero gratis a cambio de tus datos. Rendimiento de generalista moderno.

---

## 4. ¿Cuál usar según la tarea?

> Nota honesta: OpenCode no publica benchmarks por tarea para los modelos gratuitos, y estos cambian con frecuencia. Las recomendaciones siguientes combinan lo documentado (tamaño, variante, tipo de modelo) con la experiencia típica de estas familias. Como todos son gratis, **lo mejor es probar 2–3 con tu propio proyecto** y comparar.

### Resumen rápido

| Tarea | Primera opción | Alternativa | Evitar |
|---|---|---|---|
| 🗺️ Planeamiento | **Nemotron 3 Ultra Free** | Big Pickle, MiMo-V2.5 Free | Nemotron 3.5 Lightning |
| 💻 Escritura de código | **Big Pickle** | Ox Alpha Free, Hy3 Free | — |
| ♻️ Refactorización | **Big Pickle** | Nemotron 3 Ultra Free, Hy3 Free | Nemotron 3.5 Lightning |
| 🧪 Tests | **Ox Alpha Free** | Nemotron 3.5 Lightning Free | — |
| 📝 Documentación / guías / manuales | **Hy3 Free** | Big Pickle, MiMo-V2.5 Free | Nemotron 3.5 Lightning |

### 4.1 Planeamiento (arquitectura, descomposición de tareas, diseño)

**Recomendado: `nemotron-3-ultra-free`** — Es la variante "grande" de NVIDIA, orientada a razonamiento profundo. Para decidir arquitectura, dividir una feature en pasos o evaluar trade-offs quieres máxima calidad de razonamiento, aunque tarde más.

Alternativas:
- **Big Pickle**: si el planeamiento requiere mucho contexto del repo, suele manejar bien instrucciones complejas.
- **MiMo-V2.5 Free**: razonador eficiente; buena relación profundidad/velocidad para planes medianos.

Evita: **Lightning**, que sacrifica profundidad por velocidad, justo lo contrario de lo que necesitas al planear.

### 4.2 Código (escribir features, implementar funciones)

**Recomendado: `big-pickle`** — Al ser un stealth model de gama alta en evaluación gratuita, tiende al mejor rendimiento agéntico general (seguir instrucciones, usar herramientas, editar varios archivos coherentemente).

Alternativas:
- **Ox Alpha Free**: rendimiento comparable y la mejor privacidad; elige esta opción primero si tu código es sensible.
- **Hy3 Free**: sólido como generalista cuando la tarea mezcla código con explicaciones o documentación.

### 4.3 Refactorización (reestructurar sin romper comportamiento)

**Recomendado: `big-pickle`** — Refactorizar exige entender dependencias entre archivos, mantener consistencia de estilo y no "inventar" APIs inexistentes. Los modelos de mayor capacidad agéntica fallan menos aquí.

Alternativas:
- **Nemotron 3 Ultra Free**: muy cuidadoso y metódico; buena segunda opción para refactors grandes y delicados, aunque más lento.
- **Hy3 Free**: adecuado para refactors locales (un módulo, una clase).

Consejo: para refactors, pide primero un **plan** (con el modelo de planeamiento), revísalo, y luego ejecuta con el modelo de código.

### 4.4 Tests (unitarios, integración, TDD)

**Recomendado: `x-preview-f-free` (Ox Alpha Free)** — Generar tests es un ciclo iterativo de escribir → correr → corregir, con muchos contextos repetidos. Un modelo de gama alta con zero-retention es ideal: rápido en iterar y seguro si tus tests exponen estructura interna del proyecto.

Alternativas:
- **Nemotron 3.5 Lightning Free**: aquí sí brilla su velocidad; perfecto para generar lotes de tests unitarios rutinarios o casos borde a partir de una función ya definida.
- **MiMo-V2.5 Free**: bueno para diseñar casos límite gracias a su razonamiento (edge cases, invariantes).

### 4.5 Documentación, guías y manuales (READMEs, onboarding, arquitectura)

**Recomendado: `hy3-free`** — Es un generalista grande con buen equilibrio entre redacción, conocimiento amplio y código. La documentación técnica exige explicar conceptos con claridad, mantener estructura y consistencia a lo largo de un texto largo, y combinar prosa con bloques de código: justo el perfil de un generalista sólido.

Alternativas:
- **Big Pickle**: gama alta; mejor cuando la guía mezcla mucha referencia al repo y requiere seguir instrucciones complejas de formato/estilo.
- **MiMo-V2.5 Free**: su razonamiento ayuda a estructurar manuales con jerarquía clara (secciones, pasos, casos de uso) y a anticipar dudas del lector.

Evita: **Nemotron 3.5 Lightning**, que privilegia velocidad sobre profundidad narrativa; la documentación suele quedar superficial o desordenada.

Consejo: si la guía es larga o de varios archivos, pide primero un **índice/estructura** (con el modelo de planeamiento `nemotron-3-ultra-free`), revísalo, y luego redacta cada sección con `hy3-free` o `big-pickle` para mantener consistencia.

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
opencode -m opencode/x-preview-f-free
```

---

## 6. Buenas prácticas y advertencias

1. **No envíes secretos a ningún modelo gratuito** salvo quizá Ox Alpha Free (zero-retention). Esto incluye `.env`, API keys, datos de clientes y algoritmos propietarios.
2. **Son temporales**: todos los modelos gratuitos pueden desaparecer. No construyas flujos de CI críticos dependiendo solo de uno.
3. **Verifica siempre el código generado**, especialmente en refactors: ejecuta tu suite de tests después de cada cambio.
4. **Combina modelos por fase** (plan → code → test) en vez de usar uno solo para todo: es gratis y obtienes lo mejor de cada uno.
5. Si un modelo gratuito responde mal en tu dominio (p. ej. legacy PHP/Laravel en este proyecto), prueba otro de la lista antes de pagar por uno de pago.
6. Consulta siempre la [documentación oficial de Zen](https://opencode.ai/docs/zen/) para ver la lista vigente, precios y fechas de deprecación.
