# Opciones de Diseño en Rive

Rive ofrece diversas opciones de diseño (`layout`) que permiten ajustar cómo se muestra la animación dentro del `canvas`. Estas opciones nos ayudan a adaptar la animación al tamaño disponible y a alinear correctamente su contenido.

## Configuración del Diseño en Rive

El siguiente código muestra diferentes configuraciones de diseño en Rive:

```html
<script>
    const logo = new rive.Rive({
        src: "layout.riv",
        canvas: document.querySelector(".row:first-child canvas"),
        artboard: "logo",
        animations: "loop",
        autoplay: true,
        layout: new rive.Layout({
            fit: rive.Fit.Cover,
        }),
        onLoad: () => {
            logo.resizeDrawingSurfaceToCanvas();
        }
    });

    const shapes = new rive.Rive({
        src: "layout.riv",
        canvas: document.querySelector(".row:nth-child(2) canvas"),
        artboard: "shapes",
        animations: "loop",
        autoplay: true,
        layout: new rive.Layout({
            fit: rive.Fit.Contain,
            alignment: rive.Alignment.BottomCenter,
        }),
        onLoad: () => {
            shapes.resizeDrawingSurfaceToCanvas();
        }
    });

    const wide = new rive.Rive({
        src: "layout.riv",
        canvas: document.querySelector(".col canvas"),
        artboard: "Wide",
        animations: "loop",
        autoplay: true,
        layout: new rive.Layout({
            fit: rive.Fit.FitHeight,
            alignment: rive.Alignment.Center,
        }),
        onLoad: () => {
            wide.resizeDrawingSurfaceToCanvas();
        }
    });
</script>
```

## Propiedades del Layout

### `fit`
Define cómo se ajusta la animación dentro del `canvas`. Algunas opciones incluyen:
- `rive.Fit.Contain` (por defecto): Mantiene la proporción y ajusta la animación al espacio disponible sin recortar contenido.
- `rive.Fit.Cover`: Llena completamente el `canvas`, recortando el exceso si es necesario.
- `rive.Fit.Fill`: Deforma la animación para ajustarse completamente al `canvas`.
- `rive.Fit.FitWidth`: Ajusta la animación para que ocupe todo el ancho del `canvas`, manteniendo la proporción.
- `rive.Fit.FitHeight`: Ajusta la animación para que ocupe toda la altura del `canvas`, manteniendo la proporción.
- `rive.Fit.ScaleDown`: Solo escala la animación hacia abajo si es más grande que el `canvas`.
- `rive.Fit.None`: No ajusta el tamaño de la animación.

### `alignment`
Define la alineación de la animación dentro del `canvas`. Algunas opciones incluyen:
- `rive.Alignment.Center` (por defecto): Centra la animación dentro del `canvas`.
- `rive.Alignment.TopLeft`, `rive.Alignment.TopCenter`, `rive.Alignment.TopRight`: Alinea la animación en la parte superior.
- `rive.Alignment.CenterLeft`, `rive.Alignment.CenterRight`: Alinea la animación a los lados.
- `rive.Alignment.BottomLeft`, `rive.Alignment.BottomCenter`, `rive.Alignment.BottomRight`: Alinea la animación en la parte inferior.

## Ejemplos de Uso
- **Primer caso (`logo`)**: Usa `rive.Fit.Cover`, asegurando que la animación llene completamente el `canvas`, incluso si parte del contenido se recorta.
- **Segundo caso (`shapes`)**: Usa `rive.Fit.Contain` para ajustar la animación sin recortar contenido, alineándola en la parte inferior con `rive.Alignment.BottomCenter`.
- **Tercer caso (`wide`)**: Usa `rive.Fit.FitHeight` para que la animación ocupe toda la altura disponible y se mantenga centrada.

## Conclusión
El uso de `layout` en Rive permite un control preciso sobre cómo se muestran las animaciones dentro del `canvas`. Al utilizar las opciones de `fit` y `alignment`, podemos asegurarnos de que las animaciones se ajusten correctamente a distintos tamaños y alineaciones según nuestras necesidades.