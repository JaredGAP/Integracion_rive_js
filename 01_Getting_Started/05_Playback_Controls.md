# ⏯️ Controles de Reproducción en Rive

Rive proporciona métodos sencillos pero potentes para controlar la reproducción de animaciones. Puedes iniciar, pausar, detener o manipular animaciones de forma dinámica, permitiendo experiencias interactivas y personalizadas en tus proyectos web.

---

## ⚙️ Configuración de una Animación con Controles

```html
<canvas width="500" height="500"></canvas>
<button onclick="toggleRotate()">Play Rotate</button>

<script>
  const animation = new rive.Rive({
    src: "icon.riv",
    canvas: document.querySelector("canvas"),
    animations: ["rotate", "float"],
    autoplay: false, // Iniciamos el control manualmente
    onLoad: () => {
      animation.resizeDrawingSurfaceToCanvas();
      animation.play("float"); // Reproducimos "float" al inicio
    }
  });

  let isRotating = false;
  const btn = document.querySelector("button");

  function toggleRotate() {
    if (isRotating) {
      animation.pause("rotate");
      btn.innerText = "Play Rotate";
    } else {
      animation.play("rotate");
      btn.innerText = "Pause Rotate";
    }
    isRotating = !isRotating;
  }
</script>
```

### 📖 ¿Qué hace este ejemplo?
- Carga una animación `.riv` con dos animaciones: `rotate` y `float`.
- Inicia solo `float` automáticamente.
- Permite al usuario iniciar o pausar la animación `rotate` con un botón.

---

## 🛠️ Métodos de Control

### ▶️ `play()`
Inicia la animación especificada (o todas si no se indica):
```js
animation.play(); // Todas
animation.play("rotate"); // Solo rotate
```

### ⏸️ `pause()`
Pausa la animación en el fotograma actual:
```js
animation.pause();
animation.pause("rotate");
```

### ⏹️ `stop()`
Detiene y reinicia la animación desde el principio:
```js
animation.stop();
animation.stop("float");
```

### ⏭️ `scrub()`
Ubica la animación en una posición específica (de 0 a 1):
```js
animation.scrub("rotate", 0.5); // 50% del tiempo total
```

---

## 💡 Tip de Interactividad

Al combinar estos métodos con eventos del DOM (clics, desplazamientos, entrada de datos), puedes hacer que tus animaciones respondan a la interacción del usuario de forma precisa y fluida.

---

## ✅ Conclusión

Los controles de reproducción en Rive permiten una integración muy versátil en aplicaciones web. Puedes crear animaciones que reaccionan al usuario, se sincronizan con otras acciones o simplemente ofrecen una experiencia más rica y personalizada.

