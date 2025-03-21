# ⏯️ Controles de Reproducción en Rive

Rive proporciona métodos sencillos pero potentes para **controlar la reproducción de animaciones**. Esto te permite iniciar, pausar, detener o manipular animaciones de forma dinámica, creando experiencias interactivas y personalizadas para los usuarios.

---

## ⚙️ Ejemplo con controles manuales

```html
<canvas width="500" height="500"></canvas>
<button onclick="toggleRotate()">Play Rotate</button>

<script>
  const animation = new rive.Rive({
    src: "icon.riv",
    canvas: document.querySelector("canvas"),
    animations: ["rotate", "float"],
    autoplay: false, // Desactivamos autoplay para control manual
    onLoad: () => {
      animation.resizeDrawingSurfaceToCanvas();
      animation.play("float"); // Inicia solo la animación "float"
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

### 📖 ¿Qué está pasando aquí?
- Se carga una animación con dos movimientos: `rotate` y `float`.
- Solo se inicia `float` automáticamente.
- Se añade un botón para que el usuario controle cuándo se reproduce o se pausa `rotate`.

---

## 🛠️ Métodos disponibles

### ▶️ `play()`
Reproduce una o todas las animaciones:
```js
animation.play(); // Reproduce todas las animaciones del artboard
animation.play("rotate"); // Solo reproduce "rotate"
```

### ⏸️ `pause()`
Pausa la animación en su estado actual:
```js
animation.pause(); // Pausa todas
animation.pause("rotate"); // Pausa solo "rotate"
```

### ⏹️ `stop()`
Detiene completamente la animación y la reinicia desde el inicio:
```js
animation.stop(); // Todas
animation.stop("float"); // Solo "float"
```

### ⏭️ `scrub()`
Avanza a una parte específica de la animación (valor entre 0 y 1):
```js
animation.scrub("rotate", 0.5); // Posición en el 50%
```

---

## 💡 Tip: interacción con el usuario

Puedes vincular estos métodos con eventos del DOM como:

- Clics (`onclick`)
- Movimiento del mouse (`mousemove`)
- Scroll (`onscroll`)
- Entrada de texto (`oninput`)

Esto permite crear experiencias realmente interactivas. Por ejemplo:

- Un ícono que gira al pasar el mouse
- Un personaje que reacciona cuando se envía un formulario
- Una animación que avanza con el scroll de la página

---

## ✅ Conclusión

Los controles de reproducción en Rive te dan un control fino sobre el comportamiento de las animaciones. Gracias a ellos puedes construir experiencias visuales más dinámicas, reactivas y conectadas a las acciones del usuario.

Sigue experimentando con `play()`, `pause()`, `stop()` y `scrub()` para dar vida a tus animaciones de una manera única y profesional. 🎯



