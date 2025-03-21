# 🔤 Test Runs: Control de Texto en Rive desde JavaScript

**Text Runs** (también llamados "Text Input" o "Text Runs" en el contexto de Rive) permiten modificar dinámicamente el texto de una animación Rive desde JavaScript. Esto es ideal para personalizar títulos, botones, mensajes o cualquier contenido textual embebido en una animación.

---

## 🧠 ¿Qué aprenderás?

- Cómo leer el texto actual de una animación Rive.
- Cómo cambiar ese texto desde tu código JS.
- Cómo hacer que una animación reaccione a un clic modificando el texto en tiempo real.

---

## 📄 HTML de ejemplo

```html
<main class="center">
  <div class="container" onclick="changeText()">
    <canvas></canvas>
  </div>
</main>
```

Este HTML define un canvas que renderiza una animación de Rive. Cuando el usuario hace clic en el contenedor, se llama a `changeText()` para cambiar el texto.

---

## ⚙️ JavaScript: lectura y modificación de texto

```javascript
const animation = new rive.Rive({
  src: "button.riv",
  canvas: document.querySelector("canvas"),
  autoplay: true,
  artboard: "Label",
  stateMachines: "state-machine",
  onLoad: () => {
    animation.resizeDrawingSurfaceToCanvas();

    // Leer valor de texto actual
    console.log(animation.getTextRunValue("label"));
  },
});

function changeText() {
  // Cambiar el texto de forma dinámica
  animation.setTextRunValue("label", "Get Started Here");
}
```

---

## 📌 Explicación de métodos clave

| Método | Descripción |
|--------|-------------|
| `getTextRunValue("nombre")` | Devuelve el texto actual del elemento de texto nombrado. |
| `setTextRunValue("nombre", "nuevo texto")` | Cambia el valor del texto visualizado en tiempo real. |

---

## 🎯 Requisitos en Rive Studio

Para usar Text Runs correctamente:
1. Crea un **Text Run** en tu artboard (desde la barra de herramientas).
2. Asígnale un **nombre** único (por ejemplo: `label`).
3. Asegúrate de que el artboard y el nombre del texto coincidan con los usados en JS.

---

## 🧪 Casos de uso comunes

- Botones dinámicos: cambia el texto al pasar el cursor o hacer clic.
- Mensajes personalizados en onboarding.
- Etiquetas contextuales (como nombre del usuario, idioma, etc.).
- Títulos animados que cambian con la sección o scroll.

---

## ✅ Conclusión

**Text Runs** en Rive son una herramienta poderosa para hacer tus animaciones más flexibles y personalizables. Combinados con interacciones JS, puedes ofrecer contenido textual dinámico con una presentación visual impactante.