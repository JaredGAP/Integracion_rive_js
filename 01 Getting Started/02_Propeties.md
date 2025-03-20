# Propiedades en Rive con JavaScript

Cuando trabajamos con Rive en JavaScript, podemos configurar diversas propiedades para personalizar cómo se carga y se ejecuta una animación en un elemento `<canvas>`. En este documento, exploraremos las principales propiedades disponibles al instanciar un objeto `rive.Rive`.

## Configuración de la animación

El siguiente código define una animación de Rive con múltiples propiedades:

```html
<script>
    new rive.Rive({
        // Archivo de animación de Rive (.riv)
        src: "icon.riv",
        
        // Canvas donde se mostrará la animación
        canvas: document.querySelector("canvas"),
        
        // Tablero de arte dentro del archivo Rive
        artboard: "location-pin",
        
        // Animaciones a reproducir dentro del archivo
        animations: ["rotate", "float"],
        
        // Iniciar la animación automáticamente al cargar
        autoplay: true,
        
        // Callback cuando el archivo Rive se ha cargado
        onLoad: () => {
            console.log("Cargado correctamente");
        },
        
        // Callback cuando hay un error al cargar el archivo
        onLoadError: () => {
            console.log("Error al cargar el archivo");
        }
    });
</script>
```

## Explicación de las propiedades

### `src`
Especifica la ruta del archivo `.riv` que contiene la animación. En este caso, se usa `"icon.riv"`.

### `canvas`
Selecciona el elemento `<canvas>` en el que se renderizará la animación.

### `artboard`
Permite seleccionar un tablero de arte específico dentro del archivo `.riv`. En este caso, el tablero de arte se llama `"location-pin"`.

### `animations`
Define las animaciones que se reproducirán dentro del archivo Rive. Aquí se han seleccionado `"rotate"` y `"float"`.

### `autoplay`
Si está configurado como `true`, la animación se iniciará automáticamente al cargarse.

### `onLoad`
Es un callback que se ejecuta cuando el archivo Rive se ha cargado correctamente. En este ejemplo, imprime `"Cargado correctamente"` en la consola.

### `onLoadError`
Es un callback que se ejecuta si ocurre un error al cargar el archivo Rive. En este ejemplo, imprime `"Error al cargar el archivo"` en la consola.

## Conclusión
Las propiedades de Rive permiten un alto grado de personalización en la integración de animaciones dentro de una página web. Con estas opciones, podemos controlar cómo se renderizan y reproducen las animaciones, además de manejar eventos de carga y errores.