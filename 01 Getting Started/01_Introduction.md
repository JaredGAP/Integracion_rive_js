# Introducción a la Integración de Rive con JavaScript

Rive es una herramienta poderosa de animación que permite a los desarrolladores crear animaciones interactivas y de alto rendimiento para la web. En esta introducción, mostraremos cómo integrar una animación básica de Rive en una página web utilizando JavaScript.

## Configuración de la Estructura HTML

Para renderizar la animación de Rive, necesitamos definir una estructura HTML que incluya un elemento `<canvas>` donde se dibujará la animación. Aquí está la configuración básica:

```html
<main class="center">
    <div class="container">
        <!-- Agregar canvas -->
        <canvas width="500" height="500"></canvas>
    </div>
</main>
```

### Explicación:
- El elemento `<main>` contiene la animación y está centrado para una mejor presentación.
- Dentro de un `<div class="container">`, agregamos un elemento `<canvas>` con un ancho y alto de 500px.
- Este `canvas` sirve como la superficie de renderizado para la animación de Rive.

## Cargando la Librería JavaScript de Rive

Para utilizar animaciones de Rive en nuestra página web, necesitamos incluir la última versión de la dependencia de Rive. Podemos hacer esto agregando la siguiente etiqueta `<script>` antes de nuestro código JavaScript:

```html
<script src="https://unpkg.com/@rive-app/canvas@latest"></script>
```

Este script carga la biblioteca de Rive directamente desde un CDN, asegurando que siempre tengamos la última versión disponible.

## Inicialización de la Animación de Rive

Ahora, inicialicemos la animación de Rive usando JavaScript:

```html
<script>
    // Inicializar la animación de Rive
    new rive.Rive({
        src: "shapes.riv", // Ruta del archivo de animación Rive
        canvas: document.querySelector("canvas"), // Selecciona el elemento canvas
        autoplay: true, // La animación se reproduce automáticamente
        animations: "loop", // Especifica la animación a reproducir
    });
</script>
```

### Explicación:
- Creamos una nueva instancia de `rive.Rive`.
- La propiedad `src` especifica la ruta del archivo de animación de Rive (por ejemplo, `shapes.riv`).
- La propiedad `canvas` selecciona el elemento `<canvas>` donde se renderizará la animación.
- La propiedad `autoplay` está configurada en `true`, lo que significa que la animación comenzará a reproducirse automáticamente al cargarse.
- La propiedad `animations` permite especificar qué animación se debe reproducir (en este caso, `loop`).

## Resumen
Esta configuración básica nos permite renderizar una animación de Rive dentro de un elemento `<canvas>` en una página web. Al incluir la biblioteca JavaScript de Rive e inicializar una animación con `rive.Rive`, podemos integrar fácilmente animaciones dinámicas e interactivas en nuestras aplicaciones web.
