# 👆 Interacciones Hover en la Sección Hero

Además de animar con scroll, también podemos conectar nuestras animaciones de Rive con **eventos del DOM** como `mouseover`, `mouseout` o `click`. En este ejemplo, haremos que nuestro personaje reaccione con una animación especial al pasar el cursor por encima del canvas.

Este tipo de interacción es ideal para interfaces modernas donde los elementos "responden" al usuario.

---

## 🧱 Estructura del HTML

```html
<main>
  <section class="hero">
    <canvas width="500" height="500"></canvas>
  </section>
</main>
```

---

## 🎬 Script en `app.js`

```javascript
let hoverTrigger;

const hero = new rive.Rive({
  src: "hero.riv",
  canvas: document.querySelector("canvas"),
  stateMachines: "state-machine",
  autoplay: true,
  onLoad: () => {
    hero.resizeDrawingSurfaceToCanvas();
    const inputs = hero.stateMachineInputs("state-machine");
    hoverTrigger = inputs.find(i => i.name === "hover");
  }
});

// Escuchar evento de mouseover en el canvas
const canvas = document.querySelector("canvas");

canvas.addEventListener("mouseenter", () => {
  if (hoverTrigger) hoverTrigger.fire();
});
```

---

## 📖 ¿Qué hace este código?

| Parte                      | Función                                                                 |
|----------------------------|-------------------------------------------------------------------------|
| `hoverTrigger.fire()`      | Dispara el Trigger Input definido en la máquina de estados.             |
| `mouseenter`               | Evento que se activa cuando el cursor entra al área del canvas.         |
| `stateMachines`            | Carga la lógica de animación reactiva desde Rive.                       |

---

## 🧠 ¿Por qué usar hover con Rive?

- Añade microinteracciones sutiles que enriquecen la experiencia.
- Mejora la percepción de dinamismo y calidad del sitio.
- Permite representar "estados activos" como sorpresa, alegría, activación, etc.

---

## 💡 Ideas para extender este patrón

- Cambiar entre múltiples estados (hover, click, leave).
- Enviar datos desde eventos a funciones de analítica.
- Sincronizar la animación con otros elementos del DOM (mostrar info adicional al pasar el mouse).

---

## ✅ Buenas prácticas

- ✔️ Usa nombres de inputs descriptivos en Rive (`hover`, `tap`, `focus`, etc).
- ✔️ Asegúrate de que el trigger existe antes de llamar `.fire()`.
- ❌ Evites usar `click` o `hover` si el mismo canvas ya está vinculado a scroll.

---

## 🏁 Conclusión

Las interacciones con eventos como `hover` permiten que tus animaciones en Rive respondan a acciones del usuario de forma fluida y expresiva. Este patrón es excelente para dar vida a tu sitio y mejorar la interacción desde el primer contacto visual. ✨

