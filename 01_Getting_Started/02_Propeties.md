# 🎛️ Propiedades para Animaciones Rive en JavaScript

Cuando trabajamos con animaciones Rive en JavaScript, podemos utilizar diversas propiedades que nos permiten controlar detalladamente la carga, visualización e interacción de nuestras animaciones en un elemento `<canvas>`. Este documento explora las propiedades principales que puedes usar al instanciar un objeto `rive.Rive`.

---

## ⚙️ Ejemplo práctico de configuración

Aquí tienes un ejemplo completo de cómo inicializar una animación de Rive con múltiples propiedades:

```javascript
new rive.Rive({
    src: "icon.riv", // Archivo .riv que contiene la animación
    canvas: document.querySelector("canvas"), // Elemento canvas donde se muestra la animación
    artboard: "location-pin", // Nombre específico del artboard dentro del archivo
    animations: ["rotate", "float"], // Animaciones a reproducir
    autoplay: true, // Comienza automáticamente la reproducción

    // Callback al cargar correctamente la animación
    onLoad: () => {
        console.log("✅ Animación cargada exitosamente.");
    },

    // Callback al ocurrir un error durante la carga
    onLoadError: () => {
        console.error("❌ Error al cargar la animación.");
    }
});
```

---

## 📌 Explicación detallada de propiedades

### 🔸 `src`
Define la ruta al archivo `.riv` que contiene tu animación creada en Rive.

### 🔸 `canvas`
Permite seleccionar el elemento `<canvas>` de tu página web en donde será renderizada la animación.

### 🔸 `artboard`
Especifica el nombre de un artboard concreto dentro de tu archivo `.riv`, útil cuando tienes múltiples animaciones o ilustraciones en un mismo archivo.

### 🔸 `animations`
Determina qué animaciones dentro del archivo `.riv` se reproducirán. Puedes proporcionar una sola animación (como cadena) o varias animaciones simultáneamente (como array).

### 🔸 `autoplay`
Establece si la animación comenzará automáticamente cuando el archivo esté listo (`true`) o si se controlará manualmente (`false`).

### 🔸 `onLoad`
Callback que se ejecuta cuando la animación se ha cargado completamente, útil para ejecutar acciones posteriores, como mostrar mensajes de éxito o activar otras funciones.

### 🔸 `onLoadError`
Callback que se dispara cuando ocurre algún problema al cargar el archivo `.riv`, permitiéndote manejar el error, por ejemplo, notificando al usuario o intentando nuevamente la carga.

---

## 🎯 Ventajas de usar estas propiedades

Utilizando estas propiedades avanzadas puedes:

- Controlar precisamente cómo y cuándo se ejecutan tus animaciones.
- Mejorar la experiencia de usuario al gestionar correctamente eventos de carga y errores.
- Realizar integraciones más complejas y sofisticadas con facilidad.

---



