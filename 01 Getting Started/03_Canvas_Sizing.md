# Tamaño del Canvas en Rive

Al trabajar con Rive en la web, es importante entender la diferencia entre el tamaño de renderizado del `canvas` y el tamaño de visualización en la página. Esto garantiza que la animación conserve su calidad óptima en diferentes dispositivos y resoluciones.

## Configuración del Tamaño del Canvas

En el siguiente código definimos un `canvas` con un tamaño de renderizado y otro de visualización:

```html
<div class="container">
    <!-- Tamaño de renderizado -->
    <canvas width="500" height="500"></canvas>
</div>

<style>
    /* Tamaño de visualización */
    canvas {
        width: 750px;
        height: 750px;
    }
</style>
```

### Explicación:
- **Tamaño de renderizado (`width` y `height` en la etiqueta `<canvas>`)**: Define la resolución interna de la animación.
- **Tamaño de visualización (`width` y `height` en CSS)**: Define el tamaño al que se muestra el `canvas` en la página.
- Si el tamaño de visualización es mayor que el de renderizado, la imagen puede verse pixelada o borrosa.

## Ajuste Dinámico del Tamaño del Canvas

Para mantener la calidad de la animación sin importar el tamaño del `canvas`, Rive proporciona el método `resizeDrawingSurfaceToCanvas()`, que ajusta dinámicamente la superficie de dibujo al tamaño del `canvas`:

```html
<script>
    const animation = new rive.Rive({
        ...
        onLoad: () => {
            // Ajustar el tamaño de renderizado del canvas al tamaño de visualización
            animation.resizeDrawingSurfaceToCanvas();
        }
    });
</script>
```

### Explicación:
- `onLoad`: Se ejecuta cuando la animación ha terminado de cargar.
- `resizeDrawingSurfaceToCanvas()`: Ajusta la superficie de dibujo del `canvas` al tamaño real en la página, asegurando que la animación se vea con la mejor calidad posible.

## Conclusión
Configurar correctamente el tamaño del `canvas` es fundamental para obtener animaciones de alta calidad en Rive. Usar `resizeDrawingSurfaceToCanvas()` permite ajustar automáticamente la superficie de dibujo y evitar problemas de pixelación o distorsión en diferentes dispositivos.