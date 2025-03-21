# 🚀 Introducción a la Integración de Rive con JavaScript

**Rive** es una herramienta moderna para crear animaciones vectoriales **interactivas y ligeras**, ideales para páginas web, apps y juegos. A diferencia de otras soluciones como GIFs o animaciones CSS, Rive permite definir la lógica de animación (por ejemplo, respuestas a clics o movimientos) directamente desde su editor visual, y luego controlar esa animación fácilmente con JavaScript.

En esta guía aprenderás paso a paso cómo integrar una animación básica de Rive en tu sitio web usando JavaScript. No necesitas experiencia avanzada: solo conocer HTML básico y un poco de JavaScript.

---

## 🧱 Paso 1: Estructura básica en HTML

Primero, creamos una estructura HTML que incluya un `<canvas>`, donde se dibujará la animación:

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

### 🧠 ¿Qué hace este código?

- Crea un `<canvas>` de 500x500 píxeles donde se mostrará la animación.
- Incluye la librería oficial de Rive desde su CDN.
- Ejecuta un archivo `script.js` donde controlaremos la animación.

---

## ⚙️ Paso 2: Inicializar la animación en JavaScript

Ahora vamos al archivo `script.js`, donde escribimos el código necesario para mostrar la animación en el canvas.

```javascript
// Crear una nueva instancia de Rive
const animacion = new rive.Rive({
    src: "shapes.riv", // Archivo .riv exportado desde Rive
    canvas: document.querySelector("canvas"), // Seleccionamos el canvas del HTML
    autoplay: true, // Inicia automáticamente
    animations: "loop" // Nombre de la animación a reproducir
});
```

### 📌 Detalles importantes:

- `src`: es la ruta al archivo `.riv` exportado desde el editor de Rive.
- `canvas`: es el elemento HTML donde se dibujará la animación.
- `autoplay`: si está en `true`, la animación se reproduce al cargar.
- `animations`: nombre exacto de la animación que quieres reproducir (debe coincidir con el nombre en el archivo `.riv`).

---

## ✅ Resultado esperado

Si seguiste los pasos correctamente, deberías ver tu animación de Rive reproducirse automáticamente dentro del canvas al cargar la página.

---

## 📦 ¿Y ahora qué?

¡Ya tienes tu primera animación Rive integrada! En los siguientes capítulos aprenderás cómo:

- Hacer que tus animaciones reaccionen a eventos (como clics, scroll o formularios).
- Usar **State Machines** para controlar comportamientos más complejos.
- Cargar animaciones más avanzadas con imágenes, fuentes o animaciones condicionales.

---

¡Bienvenido al mundo de Rive! 🚀  
Prepárate para crear experiencias web modernas, interactivas y sorprendentes ✨

