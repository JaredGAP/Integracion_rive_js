# 🚀 Uso Avanzado de Trigger Inputs en Rive

Los **Trigger Inputs** en Rive son una herramienta esencial para crear animaciones reactivas. Funcionan como botones de acción: no almacenan un valor como los booleanos o los numéricos, sino que **se activan en un momento puntual**, provocando transiciones o efectos definidos en la máquina de estados.

---

## ⚙️ ¿Qué es un Trigger Input?

Un **Trigger** es un tipo de entrada en una *State Machine* que se dispara una sola vez y no guarda estado. Es perfecto para situaciones donde quieres que algo ocurra *cuando sucede un evento*, como un clic o una acción concreta en tu aplicación.

---

## 🧪 Ejemplo básico en JavaScript

```html
<canvas width="500" height="500"></canvas>

<script>
  let notifyTrigger;

  const animation = new rive.Rive({
    src: "icon.riv",
    canvas: document.querySelector("canvas"),
    autoplay: true,
    stateMachines: "state-machine",
    onLoad: () => {
      animation.resizeDrawingSurfaceToCanvas();

      // Obtener los inputs de la state machine
      const inputs = animation.stateMachineInputs("state-machine");

      // Buscar el trigger por su nombre
      notifyTrigger = inputs.find(input => input.name === "notify");

      // Disparar el trigger una vez cargado
      if (notifyTrigger) notifyTrigger.fire();
    }
  });

  // Disparar el trigger manualmente al hacer clic en el canvas
  document.querySelector("canvas").addEventListener("click", () => {
    if (notifyTrigger) notifyTrigger.fire();
  });
</script>
```

### 📖 ¿Qué está pasando aquí?

| Elemento                       | Función                                                             |
|-------------------------------|---------------------------------------------------------------------|
| `stateMachineInputs()`        | Obtiene todos los inputs de una máquina de estados                  |
| `input.name === "notify"`     | Busca el input llamado "notify" (debe coincidir con el nombre en Rive) |
| `fire()`                      | Dispara el trigger para ejecutar una transición o efecto puntual   |

---

## 🎯 ¿Cuándo usar Trigger Inputs?

Los triggers son ideales para reacciones inmediatas. Algunos ejemplos:

- 🔔 Mostrar una notificación animada.
- 💥 Lanzar una explosión tras un evento en un juego.
- 📬 Ejecutar la animación de “mensaje enviado” al hacer clic.
- 🧤 Animación de saludo al pasar el mouse por encima de un avatar.
- 🔄 Reiniciar una animación que debe reproducirse desde el inicio.

---

## 🌟 Casos de uso prácticos

### En interfaces gráficas:
- Botones que lanzan una animación al presionarlos.
- Microinteracciones (como un icono que salta al ser activado).

### En dashboards o apps empresariales:
- Reproducir una animación de éxito o error tras validar un formulario.

### En sitios creativos o animados:
- Disparar partículas, reacciones o efectos visuales según la interacción del usuario.

---

## ✅ Buenas prácticas

- ✔️ Verifica siempre que el trigger exista antes de usar `.fire()`.
- ✔️ Usa nombres descriptivos para tus triggers (ej: `onClick`, `explode`, `submitForm`).
- ✔️ Mantén la lógica visual en Rive y la lógica de eventos en JavaScript.
- ❌ No intentes asignarles valores: los triggers no son variables, solo se disparan.

---

## 📌 Conclusión

Los **Trigger Inputs** te permiten conectar tu animación con la interacción del usuario de manera inmediata y fluida. Son el puente perfecto entre eventos de la interfaz y las transiciones visuales diseñadas en Rive.

En los siguientes capítulos exploraremos otros tipos de inputs (como booleanos y números) para enriquecer aún más la lógica visual de tus proyectos. 🚀

