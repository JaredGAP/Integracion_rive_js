# 📱 Diseño Responsive con Rive, GSAP y HTML/CSS

Este documento explica cómo adaptar una animación de Rive dentro de un layout web **responsive**, asegurando que se visualice correctamente tanto en pantallas grandes como pequeñas. Nos centraremos especialmente en la sección `.points`, que incluye una animación sincronizada con el scroll y contenido textual asociado.

---

## 🧠 ¿Por qué es importante el diseño responsive?

Un diseño **responsive** garantiza que tu sitio web y sus animaciones:
- Se vean bien en móviles, tabletas y ordenadores.
- Carguen correctamente en distintas resoluciones.
- No recorten o deformen las animaciones al redimensionar la ventana.

---

## 🎯 ¿Qué se ha implementado?

La animación de Rive en la sección `.points`:
- Se encuentra dentro de un contenedor `.points-rive-container` con `position: sticky` para permanecer visible.
- Se sincroniza con el scroll usando ScrollTrigger.
- Cambia dinámicamente según el paso visible de una lista `<ul class="points">`.
- Adapta su altura y comportamiento visual mediante media queries.

---

## 🧱 Estructura HTML clave

```html
<section class="points">
  <div class="wrapper">
    <div class="header"><h1>Unlock all the features</h1></div>
    <div class="points-rive-container">
      <canvas width="400" height="400"></canvas>
    </div>
    <div class="points-wrapper">
      <ul class="points">
        <!-- lista de pasos -->
      </ul>
    </div>
  </div>
</section>
```

---

## 🎨 Explicación detallada de los estilos CSS

```css
section.points {
  height: 240vh; /* Hace que toda la sección sea larga, permitiendo scroll */
}

section.points > .wrapper {
  height: 100vh; /* Toma toda la altura de la ventana */
  position: sticky; /* Permanece en su lugar mientras se hace scroll */
  top: 0;
  display: flex; /* Diseño horizontal por defecto */
  align-items: center;
  justify-content: center;
}

.points-rive-container {
  position: sticky;
  top: 0;
  height: 100vh; /* Ocupa toda la altura del viewport */
}

.points-wrapper {
  --height: 50vh; /* Altura dinámica de cada punto */
  height: var(--height);
  overflow: hidden;
  mask-image: linear-gradient(to bottom, transparent, white 16% 84%, transparent); /* Efecto de desvanecimiento en los extremos */
}

ul.points > li {
  height: var(--height); /* Cada punto toma la misma altura que el wrapper */
}

@media (width < 800px) {
  .wrapper {
    flex-direction: column; /* En móviles, el diseño cambia a vertical */
  }

  .header {
    height: 8vh; /* Reduce el encabezado en pantallas pequeñas */
  }

  .points-rive-container {
    height: 48vh; /* Reduce la altura de la animación en móviles */
    width: 100%;
  }

  .points-wrapper {
    --height: 34vh; /* Altura más compacta para los pasos */
  }

  ul.points > li {
    align-items: center;
    text-align: center; /* Centra el texto para pantallas pequeñas */
  }
}
```

Este CSS permite que el contenido y la animación:
- Se ajusten dinámicamente al tamaño de la pantalla.
- Mantengan proporciones visuales agradables.
- Sigan funcionando correctamente con ScrollTrigger.

---

## ⚙️ JavaScript de adaptación al tamaño

En `app.js`, también se llama a `resizeDrawingSurfaceToCanvas()` en un listener de `resize`:

```javascript
window.addEventListener("resize", () => {
  pointsAnimation.resizeDrawingSurfaceToCanvas();
});
```

Esto garantiza que cuando el usuario cambie el tamaño de la ventana, el canvas se redimensione correctamente para evitar que se vea pixelado o estirado.

---

## ✅ Conclusión

El uso de media queries, unidades relativas (`vh`, `%`, `--height`) y la función `resizeDrawingSurfaceToCanvas()` de Rive permite que las animaciones se vean perfectas en cualquier dispositivo. Este tipo de integración es ideal para experiencias visuales modernas y profesionales.

