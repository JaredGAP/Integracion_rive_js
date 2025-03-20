# Uso de Font Assets en Rive

Rive permite cargar y cambiar fuentes tipográficas en tiempo real dentro de una animación. Esto facilita la personalización del texto dentro de la animación sin necesidad de modificar el archivo `.riv`.

## Configuración de un Font Asset en Rive

El siguiente código muestra cómo manejar fuentes en Rive y cambiarlas dinámicamente:

```html
<script>
    let fontAsset;

    const animation = new rive.Rive({
        src: "shimmer.riv",
        canvas: document.querySelector("canvas"),
        autoplay: true,
        onLoad: () => animation.resizeDrawingSurfaceToCanvas(),
        
        // Manejo de carga de assets
        assetLoader: (asset, bytes) => {
            if (asset.isFont) {
                // Guardar referencia al asset de fuente
                fontAsset = asset;
                changeFont("Boska");

                // Indicar que el asset fue manejado manualmente
                return true;
            }
            return false;
        }
    });

    async function changeFont(fontName) {
        console.log("Cargando fuente...", fontName);

        // Obtener la fuente desde una carpeta local
        const response = await fetch(`fonts/${fontName}.ttf`);
        // Convertir la fuente a un formato compatible con Rive
        const font = await rive.decodeFont(
            new Uint8Array(
                await response.arrayBuffer()
            )
        );
        
        // Asignar la nueva fuente al asset
        fontAsset.setFont(font);

        console.log("Fuente cargada!");
        
        // Liberar memoria de la fuente anterior
        font.unref();
    }
</script>
```

## Explicación del Código

### `assetLoader(asset, bytes)`
Este callback maneja la carga de assets en la animación:
- Si el *asset* es una fuente (`asset.isFont`), se guarda en `fontAsset` y se carga una fuente predeterminada (`Boska`).
- Se retorna `true` si el asset se maneja manualmente, y `false` en caso contrario.

### `changeFont(fontName)`
Esta función permite cambiar la fuente en tiempo real:
1. Descarga la fuente desde la carpeta `fonts/`.
2. La convierte a un formato compatible con Rive usando `rive.decodeFont()`.
3. Asigna la fuente al asset con `fontAsset.setFont(font)`.
4. Libera memoria de la fuente anterior con `font.unref()`.

### Interacción con el Usuario
El usuario puede hacer clic en `Array Font` para cambiar la fuente de la animación dinámicamente.

## Conclusión
El uso de *Font Assets* en Rive permite modificar fuentes en tiempo real, brindando flexibilidad y personalización en animaciones interactivas.
