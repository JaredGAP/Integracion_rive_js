# 🚀 Introducción a la Integración de Rive con JavaScript

Rive es una herramienta poderosa que permite crear animaciones interactivas y de alto rendimiento para aplicaciones web. En esta guía aprenderás paso a paso cómo integrar una animación básica creada en Rive en tu página web utilizando JavaScript.

---

## 📌 Configuración del HTML

Primero, necesitamos configurar un archivo HTML que incluya un elemento `<canvas>` donde se mostrará nuestra animación:

```html
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Animación Rive</title>
    <link rel="stylesheet" href="styles.css">
</head>
<body>
    <canvas width="500" height="500"></canvas>

    <!-- Cargar la librería Rive desde CDN -->
    <script src="https://unpkg.com/@rive-app/canvas@latest"></script>

    <!-- Nuestro script para inicializar la animación -->
    <script src="script.js"></script>
</body>
</html>
```

### 📖 Explicación:

- Colocamos un `<canvas>` directamente en el `body` con dimensiones establecidas (500x500px), donde se renderizará la animación.
- Cargamos la librería Rive desde CDN para asegurarnos siempre de utilizar la última versión.
- Finalmente, añadimos nuestro archivo JavaScript personalizado (`script.js`) para inicializar la animación.

---

## ⚙️ Inicialización de la Animación con JavaScript

En el archivo `script.js` inicializaremos la animación utilizando el siguiente código:

```javascript
// Inicializar la animación de Rive
const animacion = new rive.Rive({
    src: "shapes.riv", // Archivo .riv generado en Rive
    canvas: document.querySelector("canvas"), // Seleccionamos el canvas
    autoplay: true, // Inicia automáticamente
    animations: "loop" // Nombre de la animación a reproducir
});
```

### 📖 Explicación:

- Creamos una nueva instancia `rive.Rive`.
- El parámetro `src` indica la ruta al archivo `.riv` que creaste previamente en Rive.
- `canvas` apunta al elemento HTML `<canvas>` que definimos anteriormente.
- Configuramos `autoplay: true` para que la animación inicie automáticamente al cargar la página.
- La opción `animations` permite elegir qué animación reproducir. Aquí usamos un ejemplo llamado "loop".

---

## 🎉 Resultado esperado

Siguiendo estos pasos, tendrás una animación funcional integrada en tu web que se reproducirá automáticamente y estará lista para interactuar.

---

## ✅ Resumen

Con estos pasos sencillos ya sabes cómo integrar fácilmente animaciones dinámicas creadas en Rive dentro de cualquier página web usando JavaScript. Explora los siguientes capítulos para profundizar en funcionalidades avanzadas, como interactividad y manejo de estados con State Machines.

---

¡Disfruta creando experiencias web increíbles con Rive! 🚀✨

