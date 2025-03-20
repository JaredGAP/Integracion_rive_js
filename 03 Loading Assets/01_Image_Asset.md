# Uso de Image Assets en Rive

Rive permite el uso de imágenes como *assets* dentro de una animación. Con esta funcionalidad, podemos cargar imágenes de manera dinámica y utilizarlas dentro de la animación en tiempo real.

## Configuración de un Image Asset en Rive

El siguiente código muestra cómo manejar imágenes en una animación de Rive:

```html
<script>
    let imgAsset;

    const animation = new rive.Rive({
        src: "mockup.riv",
        canvas: document.querySelector("canvas"),
        autoplay: true,
        onLoad: () => animation.resizeDrawingSurfaceToCanvas(),
        
        // Manejo de carga de assets
        assetLoader: (
            asset, // Asset handle a cargar
            bytes // Bytes del asset si está embebido
        ) => {
            if (asset.isImage) {
                imgAsset = asset;
            }

            // Retornar false si el asset no se ha cargado
            return false;

            // Retornar true si el asset se ha cargado manualmente
            return true;
        }
    });

    async function changeImage() {
        console.log("Cargando imagen...");
    
        // Obtener una imagen externa
        const response = await fetch("https://picsum.photos/800");
        // Convertir la imagen a un formato compatible con Rive
        const img = await rive.decodeImage(
            new Uint8Array(await response.arrayBuffer())
        );
        
        // Asignar la imagen cargada al asset en la animación
        imgAsset.setRenderImage(img);
        
        console.log("Imagen cargada!");
        
        // Liberar memoria de la imagen anterior
        img.unref();
    }
</script>
```

## Explicación del Código

### `assetLoader(asset, bytes)`
Este callback se ejecuta cuando Rive intenta cargar un *asset* dentro de la animación.
- Si el *asset* es una imagen (`asset.isImage`), se almacena en la variable `imgAsset`.
- Se retorna `false` si el asset no se carga automáticamente y `true` si se maneja manualmente.

### `changeImage()`
Esta función permite cambiar la imagen en tiempo real:
1. Obtiene una nueva imagen desde una URL externa.
2. Convierte la imagen a un formato compatible con Rive usando `rive.decodeImage()`.
3. Usa `imgAsset.setRenderImage(img)` para actualizar la imagen en la animación.
4. Libera memoria de la imagen anterior con `img.unref()`.

### Interacción con el Usuario
El usuario puede hacer clic en el botón `Change Image` para cargar una nueva imagen en la animación en tiempo real.

## Conclusión
El uso de *Image Assets* en Rive permite crear animaciones dinámicas con imágenes que pueden cambiarse en tiempo real, lo que es ideal para aplicaciones interactivas y personalizadas.