# 🦸‍♂️ Animación Scroll en la Sección Hero

En este ejemplo aplicamos lo aprendido sobre **GSAP ScrollTrigger** y lo llevamos a una sección **hero** típica de una web, donde un personaje animado cobra vida a medida que el usuario hace scroll.

Este patrón es ideal para crear primeras impresiones impactantes con una animación que **avanza progresivamente** conforme se revela el contenido.

---

## 🧱 Estructura del HTML

```html
<main>
  <section class="hero">
    <canvas width="500" height="500"></canvas>
  </section>
  <section class="hero-text">
    <h1>Domina Rive como un héroe 🦸‍♂️</h1>
  </section>
</main>
```

- La sección `.hero` contiene el canvas de la animación.
- La sección `.hero-text` es el contenido que aparecerá con el desplazamiento.

---

## 🎬 Script en `app.js`

```javascript
// Registrar ScrollTrigger
gsap.registerPlugin(ScrollTrigger);

let scrollInput;

// Cargar animación de Rive
const hero = new rive.Rive({
  src: "hero.riv",
  canvas: document.querySelector("canvas"),
  stateMachines: "state-machine",
  autoplay: true,
  onLoad: () => {
    hero.resizeDrawingSurfaceToCanvas();
    const inputs = hero.stateMachineInputs("state-machine");
    scrollInput = inputs.find(i => i.name === "scroll");
  }
});

// Enlazar el scroll con el input de Rive
ScrollTrigger.create({
  trigger: ".hero-text",
  start: "top bottom",
  end: "bottom top",
  scrub: true,
  onUpdate: ({ progress }) => {
    if (scrollInput) scrollInput.value = Math.round(progress * 10);
  }
});
```

---

## 📖 ¿Qué hace este código?

| Parte                     | Función                                                                 |
|---------------------------|-------------------------------------------------------------------------|
| `.hero`                   | Contiene el canvas con el personaje animado.                           |
| `ScrollTrigger.create()`  | Crea una animación que reacciona al scroll.                            |
| `progress * 10`           | Escala el progreso del scroll a un rango de 0 a 10.                    |
| `scrollInput.value = ...` | Actualiza el valor del Number Input en la animación de Rive.           |

---

## 🎯 ¿Dónde aplicar este patrón?

- Páginas de presentación de producto o servicio.
- Portadas con storytelling visual.
- Secciones que introducen un personaje, logotipo o mensaje clave.
- Hero banners interactivos en landings creativas.

---

## ✅ Buenas prácticas

- ✔️ Asegúrate de que el input esté correctamente nombrado y conectado.
- ✔️ Usa `scrub: true` para que la animación siga suavemente el scroll.
- ❌ Evita saturar la sección hero con mucho texto si ya hay animación visual.

---

## 🏁 Conclusión

Animar tu sección hero con scroll le da vida a la página desde el primer momento. Este tipo de integración entre **GSAP + ScrollTrigger + Rive** es perfecta para crear una experiencia envolvente, profesional y memorable desde el primer scroll. 🚀

