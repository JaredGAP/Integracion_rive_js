# 🧠 Buenas Prácticas al Usar Rive con JavaScript

A medida que tu proyecto crece, aplicar buenas prácticas con Rive te ayuda a mantener tu código organizado, tus animaciones eficientes y tu lógica clara. Aquí tienes una recopilación de consejos útiles para usar Rive de forma profesional.

---

## 🗂️ Organización del archivo `.riv`

- ✅ Usa **nombres descriptivos** para artboards, state machines e inputs (ej: `buttonMachine`, `hoverTrigger`).
- ✅ Agrupa animaciones relacionadas en un solo archivo si comparten contexto.
- ❌ No uses nombres genéricos como `Artboard 1`, `Untitled` o `StateMachine 3`.

---

## 🎛️ Buen uso de inputs

- ✅ Usa **Boolean Inputs** para estados simples (on/off).
- ✅ Usa **Trigger Inputs** para acciones puntuales (clic, submit, tap).
- ✅ Usa **Number Inputs** para niveles, scroll, progreso o múltiples estados.
- ❌ No abuses de triggers cuando un boolean o number encajaría mejor.

---

## 💾 Carga y rendimiento

- ✅ Usa `resizeDrawingSurfaceToCanvas()` para ajustar el tamaño correctamente.
- ✅ Evita redibujar innecesariamente el canvas (no recargues animaciones cada frame).
- ✅ Usa CDN en prototipos y bundlers (`npm`) en producción.
- ❌ No cargues animaciones en segundo plano si no se van a usar.

---

## 🛠️ Control desde JavaScript

- ✅ Verifica que el input exista antes de usar `.value` o `.fire()`.
- ✅ Encapsula la lógica Rive en funciones reutilizables.
- ✅ Usa eventos del DOM (`click`, `hover`, `scroll`) para activar animaciones.
- ❌ No pongas toda la lógica en el constructor de Rive: separa responsabilidades.

---

## 🧪 Testing y depuración

- ✅ Usa `console.log()` para inspeccionar eventos y estados al principio.
- ✅ Añade clases CSS visibles al DOM al recibir eventos de Rive para depurar.
- ✅ Testea diferentes valores de inputs en tiempo real desde la consola.
- ❌ No des por hecho que los inputs se cargan al instante: espera al `onLoad()`.

---

## 📦 Optimización del `.riv`

- ✅ Minimiza los artboards y capas innecesarias antes de exportar.
- ✅ Usa animaciones vectoriales, evita imágenes pesadas si no son necesarias.
- ✅ Exporta a 60 fps solo si realmente necesitas esa fluidez (puede pesar más).
- ❌ No dupliques animaciones idénticas para diferentes estados: usa lógica.

---

## 🧩 Integración en proyectos reales

- ✅ Combina Rive con GSAP, React, Vue o frameworks modernos sin miedo.
- ✅ Diseña tus animaciones pensando en la **interacción real** desde el principio.
- ✅ Usa Rive para complementar tu UX, no para reemplazar todo el contenido.

---

## ✅ Conclusión

Aplicar buenas prácticas con Rive no solo mejora el rendimiento y la organización, también te ahorra tiempo en el desarrollo.

Mantén tus animaciones limpias, tu lógica clara y tu código escalable, y Rive se convertirá en una herramienta fundamental para tus proyectos. 🚀

