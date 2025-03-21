# 🔄 Uso de State Machines en Rive

Las **State Machines** (máquinas de estados) son una de las funciones más potentes de Rive. Permiten controlar la lógica de las animaciones de forma visual, definiendo cómo deben comportarse ante distintas situaciones o interacciones del usuario. Esto es ideal para botones, personajes, formularios interactivos, entre otros casos.

---

## 🧠 ¿Qué es una State Machine?

Una *State Machine* es un sistema de transición entre estados. En lugar de reproducir animaciones de forma manual, puedes diseñar en el editor de Rive **cómo se pasa de un estado a otro** según ciertas condiciones:

- 🔁 Transiciones automáticas entre animaciones.
- 🎯 Reacción a entradas (inputs) como booleanos, números o *triggers*.
- 🖱️ Respuesta a eventos como clics, teclado, scroll u otros eventos del DOM.

Esto te permite separar la lógica de animación del código JavaScript, haciéndola más modular y visual.

---

## ⚙️ Ejemplo básico en JavaScript

```javascript
const animation = new rive.Rive({
  src: "state_machine.riv",
  canvas: document.querySelector("canvas"),
  stateMachines: "state-machine", // nombre exacto definido en Rive
  autoplay: true,
  onLoad: () => {
    animation.resizeDrawingSurfaceToCanvas();
  }
});
```

### 🧩 Explicación rápida:
- `src`: archivo `.riv` exportado desde Rive.
- `canvas`: el elemento donde se mostrará la animación.
- `stateMachines`: nombre de la máquina de estados que deseas activar.
- `autoplay`: indica si debe empezar automáticamente.

---

## 🎚️ Control de Inputs desde JavaScript

Para interactuar con tu máquina de estados desde código, puedes acceder a sus *inputs* (entradas) y modificarlos.

```javascript
// Obtener todos los inputs de la state machine
const inputs = animation.stateMachineInputs("state-machine");

// Cambiar un booleano
const toggle = inputs.find(input => input.name === "activo");
if (toggle) toggle.value = true;

// Activar un trigger
const trigger = inputs.find(input => input.name === "disparar");
if (trigger) trigger.fire();
```

### 📌 Tipos de Inputs comunes:
- **Boolean**: Encendido/apagado (ideal para estados binarios).
- **Trigger**: Pulsadores que activan una transición una sola vez.
- **Number**: Valores numéricos continuos (como velocidad, dirección, etc.).

---

## 🎯 ¿Por qué usar State Machines?

- ✅ **Mayor interactividad**: permite que tus animaciones respondan al comportamiento del usuario.
- ✅ **Menos lógica en el código**: se gestiona desde el editor de Rive.
- ✅ **Mejor mantenimiento**: puedes cambiar el comportamiento sin tocar JavaScript.

---

## ✅ Conclusión

Usar *State Machines* en Rive te da el poder de crear **animaciones reactivas y lógicas** sin tener que escribir toda la lógica desde cero en JavaScript. 

En los próximos apartados verás cómo trabajar con distintos tipos de inputs (triggers, booleanos, números) y cómo capturar eventos de las máquinas de estado desde tu código para llevar la interactividad al siguiente nivel. 🚀

