# 🎛️ Propiedades para Animaciones Rive en JavaScript

Cuando trabajamos con animaciones de Rive en JavaScript, existen varias propiedades clave que nos permiten controlar la carga, reproducción e interacción de una animación dentro de un elemento `<canvas>`. Conocer estas propiedades te ayudará a aprovechar al máximo las capacidades del runtime de Rive.

En esta guía exploraremos las propiedades más comunes que puedes usar al crear una instancia de `rive.Rive()`.

---

## ⚙️ Ejemplo completo de inicialización

Aquí tienes un ejemplo práctico que utiliza varias propiedades para personalizar el comportamiento de una animación:

```javascript
new rive.Rive({
    src: "icon.riv", // Ruta al archivo .riv exportado desde Rive
    canvas: document.querySelector("canvas"), // Canvas donde se mostrará la animación
    artboard: "location-pin", // Artboard específico dentro del archivo .riv
    animations: ["rotate", "float"], // Lista de animaciones a reproducir
    autoplay: true, // Iniciar automáticamente

    // Callback cuando la animación ha cargado correctamente
    onLoad: () => {
        console.log("✅ Animación cargada exitosamente.");
    },

    // Callback si ocurre un error al cargar
    onLoadError: () => {
        console.error("❌ Error al cargar la animación.");
    }
});
```

---

## 🧾 Explicación de propiedades clave

### 🔹 `src`
Ruta al archivo `.riv`. Este archivo debe haber sido exportado desde el editor de Rive.

### 🔹 `canvas`
Referencia al elemento HTML `<canvas>` donde se dibujará la animación. Es esencial para renderizar la animación visualmente.

### 🔹 `artboard`
Permite seleccionar un artboard específico dentro del archivo `.riv`. Útil si el archivo contiene múltiples ilustraciones o escenas.

### 🔹 `animations`
Nombre(s) de las animaciones que deseas reproducir. Puede ser una cadena (`"idle"`) o un array (`["rotate", "float"]`).

### 🔹 `autoplay`
Define si la animación debe comenzar automáticamente al cargar. Si es `false`, puedes iniciar manualmente usando `play()`.

### 🔹 `onLoad`
Función que se ejecuta una vez la animación ha sido cargada exitosamente. Puedes usarla para inicializar otras acciones en tu app.

### 🔹 `onLoadError`
Función que se dispara si ocurre un error durante la carga. Ideal para mostrar mensajes al usuario o reintentar.

---

## 🎯 ¿Por qué son importantes estas propiedades?

Estas propiedades te permiten:

- Tener control total sobre cómo se comporta la animación.
- Mejorar la experiencia de usuario (UX) gestionando bien el estado de carga.
- Preparar tu proyecto para integraciones más avanzadas (por ejemplo, diferentes artboards según contexto, reproducción condicional, etc.).

---

A medida que avances, verás cómo estas propiedades se combinan con otras técnicas como las máquinas de estados (State Machines) para lograr animaciones aún más dinámicas e interactivas.




