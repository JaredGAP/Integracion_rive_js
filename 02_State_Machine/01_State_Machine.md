# 🔄 Uso de State Machines en Rive

Las *State Machines* en Rive permiten gestionar lógicas de animación complejas de forma visual y eficiente. Con ellas puedes crear transiciones automáticas, responder a eventos del usuario y controlar comportamientos sin tener que manipular directamente cada animación.

---

## ⚙️ Configuración básica en JavaScript

Para utilizar una *State Machine* desde JavaScript, necesitas referenciar su nombre con la propiedad `stateMachines` al crear la instancia `rive.Rive`:

```javascript
const animation = new rive.Rive({
  src: "state_machine.riv",
  canvas: document.querySelector("canvas"),
  stateMachines: "state-machine",
  autoplay: true,
  onLoad: () => {
    animation.resizeDrawingSurfaceToCanvas();
  }
});
```

### 📖 Explicación:
- `src`: Ruta al archivo `.riv` exportado desde Rive.
- `canvas`: Elemento donde se mostrará la animación.
- `stateMachines`: Nombre exacto de la *State Machine* creada en Rive.
- `autoplay`: Inicia automáticamente la animación.

---

## 🧠 ¿Qué es una State Machine?

Una *State Machine* en Rive es un sistema visual de control de estados. Permite:

- Transitar entre diferentes animaciones según condiciones.
- Usar entradas (inputs) como botones, variables booleanas, números o trigger.
- Reaccionar a eventos del usuario como clics, teclas o desplazamientos.

---

## ✋ Control de Inputs desde JavaScript

Puedes acceder y modificar los inputs de una *State Machine* con los métodos `stateMachineInputs()` y `fire()` (para triggers):

```javascript
// Obtener un input booleano
const inputs = animation.stateMachineInputs("state-machine");
const toggle = inputs.find(input => input.name === "activo");

// Cambiar el valor del input
if (toggle) toggle.value = true;

// Lanzar un trigger
const trigger = inputs.find(input => input.name === "disparar");
if (trigger) trigger.fire();
```

---

## 🎯 Beneficios de usar State Machines

- ✅ **Interactividad avanzada:** Responde a eventos del usuario en tiempo real.
- ✅ **Animaciones fluidas:** Las transiciones se gestionan visualmente, sin lógica complicada.
- ✅ **Reutilización y mantenimiento:** Puedes organizar lógicas complejas sin repetir código.

---

## ✅ Conclusión

Las *State Machines* son una de las herramientas más potentes de Rive para construir animaciones interactivas y adaptables. Son ideales para interfaces, botones animados, personajes interactivos y cualquier experiencia que requiera lógica de estados.