# 🚀 Uso de GSAP ScrollTrigger con Rive y HTML

**GSAP** (GreenSock Animation Platform) junto con el plugin **ScrollTrigger** permite animar elementos HTML en función del desplazamiento del usuario. Este enfoque se puede complementar perfectamente con animaciones de Rive, logrando interfaces visualmente impresionantes que reaccionan al scroll.

---

## 🧱 Estructura básica del HTML

```html
<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Scroll + Rive + GSAP</title>
  <link rel="stylesheet" href="css/style.css">
</head>
<body>
  <main>
    <section></section>
    <section>
      <div class="label">Texto animado</div>
      <div class="container">
        <canvas width="500" height="500"></canvas>
      </div>
    </section>
    <section></section>
  </main>

  <!-- Cargar las librerías -->
  <script src="https://cdn.jsdelivr.net/npm/gsap@3.12.5/dist/gsap.min.js"></script>
  <script src="https://cdn.jsdelivr.net/npm/gsap@3.12.5/dist/ScrollTrigger.min.js"></script>
  <script src="https://unpkg.com/@rive-app/canvas@2.8.3"></script>
  <script src="app.js"></script>
</body>
</html>
```

---

## ⚙️ Implementación en `app.js`

```javascript
// Registrar el plugin ScrollTrigger
gsap.registerPlugin(ScrollTrigger);

// Animar una div al hacer scroll
gsap.from(".container", {
  opacity: 0,
  y: 50,
  duration: 1.5,
  scrollTrigger: {
    trigger: ".container",
    start: "top 80%",
    end: "top 30%",
    scrub: true
  }
});

// Cargar animación de Rive
let scrollInput;

const animation = new rive.Rive({
  src: "scroll-linked.riv",
  canvas: document.querySelector("canvas"),
  stateMachines: "ScrollMachine",
  autoplay: true,
  onLoad: () => {
    animation.resizeDrawingSurfaceToCanvas();
    const inputs = animation.stateMachineInputs("ScrollMachine");
    scrollInput = inputs.find(i => i.name === "scrollValue");
  }
});

// Vincular scroll con la animación de Rive
window.addEventListener("scroll", () => {
  const scrollRatio = window.scrollY / (document.body.scrollHeight - window.innerHeight);
  const value = Math.min(Math.round(scrollRatio * 10), 10);
  if (scrollInput) scrollInput.value = value;
});
```

---

## 📖 Explicación de los elementos clave

| Elemento | Descripción |
|----------|-------------|
| `gsap.from()` | Anima desde un estado inicial hacia el estado actual del elemento. |
| `scrollTrigger` | Configura la animación para que reaccione al scroll. |
| `scrub: true` | Hace que la animación avance o retroceda según el desplazamiento. |
| `rive.Rive(...)` | Carga una animación de Rive con una State Machine. |
| `scrollInput.value = n` | Actualiza el Number Input de la animación en tiempo real. |

---

## 🎯 Casos de uso recomendados

- Animaciones de introducción sincronizadas con el scroll.
- Efectos de aparición, fade in/out, y desplazamiento de contenido.
- Interactividad visual donde la animación se desarrolla a medida que el usuario baja por la página.
- Control progresivo de una animación Rive usando el `scrollValue` como input numérico.

---

## 🧰 Consejos y buenas prácticas

- ✅ Usa `scrub: true` para una experiencia más fluida.
- ✅ Siempre comprueba si el input de Rive está disponible antes de usar `.value`.
- ✅ Divide la página en secciones claras para coordinar mejor los disparadores de scroll.
- ❌ No abuses de animaciones pesadas si tienes muchos elementos animados simultáneamente.

---

## ✅ Conclusión

**GSAP + ScrollTrigger** es una herramienta potente para crear animaciones de desplazamiento reactivas y elegantes. Combinado con **Rive**, permite controlar visualmente animaciones en función del scroll del usuario, lo que resulta ideal para páginas web creativas, narrativas interactivas y diseños de experiencia envolventes.

