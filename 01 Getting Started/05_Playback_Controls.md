# Controles de Reproducción en Rive

Rive proporciona métodos para controlar la reproducción de las animaciones, lo que nos permite iniciar, pausar, detener y manipular la reproducción de forma dinámica.

## Configuración de la Animación con Controles

En el siguiente código se inicializa una animación con controles interactivos:

```html
<main class="center">
    <div class="container">
        <canvas width="500" height="500"></canvas>
    </div>
    <a onclick="toggleRotate()">Play Rotate</a>
</main>

<script>
    const animation = new rive.Rive({
        src: "icon.riv",
        canvas: document.querySelector("canvas"),
        animations: ["rotate", "float"],
        onLoad: () => {
            animation.resizeDrawingSurfaceToCanvas();
        }
    });

    // Reproducir una animación específica
    animation.play("float");

    let isRotating = false;
    const btn = document.querySelector("a");

    function toggleRotate() {
        if (isRotating) {
            // Pausar la animación "rotate"
            animation.pause("rotate");
            btn.innerText = "Play Rotate";
        } else {
            // Reanudar la animación "rotate"
            animation.play("rotate");
            btn.innerText = "Pause Rotate";
        }
        isRotating = !isRotating;
    }
</script>
```

## Métodos de Control de Reproducción

### `play()`
Inicia la reproducción de una o varias animaciones:
- `animation.play()`: Reproduce todas las animaciones.
- `animation.play("rotate")`: Reproduce solo la animación llamada `rotate`.

### `pause()`
Pausa la animación en el fotograma actual:
- `animation.pause()`: Pausa todas las animaciones.
- `animation.pause("rotate")`: Pausa solo la animación `rotate`.

### `stop()`
Detiene completamente la animación y la reinicia al principio:
- `animation.stop()`: Detiene todas las animaciones.
- `animation.stop("float")`: Detiene solo `float`.

### `scrub()`
Permite posicionar la animación en un punto específico:
- `animation.scrub("rotate", 0.5)`: Mueve la animación `rotate` al 50% de su duración.

## Ejemplo Interactivo
En el código anterior, el botón alterna la reproducción de la animación `rotate`. Cuando está en reproducción, el botón cambia a “Pause Rotate”, y cuando está en pausa, cambia a “Play Rotate”.

## Conclusión
Los controles de reproducción en Rive permiten un manejo preciso de las animaciones, ideal para crear experiencias interactivas y dinámicas en aplicaciones web.