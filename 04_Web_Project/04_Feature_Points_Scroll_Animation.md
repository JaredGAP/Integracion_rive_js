# 🧭 Animación por Secciones: Feature Points Scroll

En este ejemplo aprenderás a crear un efecto de **navegación visual por secciones**, donde cada punto destacado (feature) se representa con una animación en Rive que cambia al hacer scroll.

Utilizaremos un **Number Input** para reflejar el estado actual según la sección visible, y GSAP ScrollTrigger para detectar el scroll del usuario.

---

## 🧱 Estructura del HTML

```html
<main class="feature">
  <div class="content">
    <div class="section intro">Introducción</div>
    <div class="section feature-1">Feature A</div>
    <div class="section feature-2">Feature B</div>
    <div class="section feature-3">Feature C</div>
    <div class="section feature-4">Feature D</div>
  </div>
  <canvas width="500" height="500"></canvas>
</main>
```

- `.content` contiene las secciones de texto.
- El `<canvas>` a la derecha muestra la animación correspondiente a cada sección.

---

## 🎬 Script en `app.js`

```javascript
let activeInput;

const feature = new rive.Rive({
  src: "features.riv",
  canvas: document.querySelector("canvas"),
  stateMachines: "state-machine",
  autoplay: true,
  onLoad: () => {
    feature.resizeDrawingSurfaceToCanvas();
    const inputs = feature.stateMachineInputs("state-machine");
    activeInput = inputs.find(i => i.name === "active");
  }
});

// Crear triggers por sección
document.querySelectorAll(".section").forEach((el, index) => {
  ScrollTrigger.create({
    trigger: el,
    start: "top center",
    end: "bottom center",
    onEnter: () => {
      if (activeInput) activeInput.value = index;
    },
    onEnterBack: () => {
      if (activeInput) activeInput.value = index;
    }
  });
});
```

---

## 📖 Explicación paso a paso

| Elemento                        | Función                                                                 |
|---------------------------------|-------------------------------------------------------------------------|
| `activeInput.value = index`     | Cambia el valor del Number Input en función de la sección visible.     |
| `ScrollTrigger.create(...)`     | Detecta entrada/salida de cada sección en el viewport.                 |
| `onEnter`, `onEnterBack`        | Se activan al hacer scroll hacia adelante o retroceder.                |

---

## ✨ Usos típicos de este patrón

- Mostrar características de un producto paso a paso.
- Storytelling visual (timeline animado).
- Introducciones o guías con navegación sincronizada.

---

## ✅ Buenas prácticas

- ✔️ Asegúrate de que el nombre del Number Input (`active`) coincida exactamente con el usado en Rive.
- ✔️ Mantén un orden lógico en tus secciones para que el valor del input tenga sentido progresivo.
- ❌ Evita sobrecargar el canvas con muchas actualizaciones simultáneas.

---

## 🏁 Conclusión

Este patrón permite crear experiencias interactivas donde **el contenido y la animación avanzan juntos**, reforzando el mensaje visual y textual de tu web. Ideal para secciones informativas o presentaciones paso a paso. 🪄