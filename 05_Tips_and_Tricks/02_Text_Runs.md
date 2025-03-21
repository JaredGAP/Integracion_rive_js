# ✍️ Text Runs en Rive: Texto Dinámico desde Código

**Text Runs** es una característica experimental de Rive que permite **reemplazar texto desde JavaScript**, ideal para crear componentes como tarjetas animadas, presentaciones, estadísticas, mensajes o interfaces con contenido que cambia dinámicamente.

---

## 🧠 ¿Qué es un Text Run?

Un **Text Run** es una línea de texto en un artboard que puede ser detectada y modificada desde JavaScript usando el método `textRun()` del runtime de Rive.

Esto permite cambiar el contenido del texto **sin necesidad de editar el archivo `.riv` en Rive Studio**.

---

## ⚙️ Ejemplo práctico

```html
<canvas width="500" height="500"></canvas>
<input type="text" placeholder="Escribe algo..." />
```

```javascript
let textRun;

const animation = new rive.Rive({
  src: "text-run.riv",
  canvas: document.querySelector("canvas"),
  autoplay: true,
  onLoad: () => {
    animation.resizeDrawingSurfaceToCanvas();
    textRun = animation.textRun("mensaje"); // nombre del Text Run en Rive Studio
  }
});

const input = document.querySelector("input");
input.addEventListener("input", () => {
  if (textRun) textRun.text = input.value;
});
```

---

## 📖 ¿Qué hace este código?

| Elemento                  | Función                                                                 |
|---------------------------|-------------------------------------------------------------------------|
| `textRun("mensaje")`      | Accede al Text Run definido en Rive con el nombre "mensaje".            |
| `textRun.text = valor`    | Cambia el contenido del texto en tiempo real.                           |
| `input.addEventListener`  | Detecta entrada del usuario y actualiza la animación.                   |

---

## 🎯 Casos de uso recomendados

- **Tarjetas personalizadas**: texto que cambia según el usuario.
- **Formularios con animación**: donde el contenido aparece escrito en tiempo real.
- **Sistemas de notificación**: donde el mensaje cambia según el resultado (éxito, error, etc.).
- **Interfaces educativas o narrativas** con texto interactivo.

---

## 🧪 Consideraciones importantes

- Actualmente, **solo es compatible con ciertas fuentes** (por ahora fuentes integradas por Rive).
- Asegúrate de que el objeto de texto en Rive esté preparado como **Text Run**.
- El texto puede no responder a salto de línea (`\n`), según el render.
- Esta característica aún está evolucionando, por lo que su soporte puede cambiar.

---

## ✅ Conclusión

`Text Runs` abre la puerta a crear animaciones con texto adaptable y vivo, directamente desde código JavaScript. Es perfecto para interfaces donde el contenido textual **responde a la interacción del usuario o cambia en tiempo real**, sin tener que reexportar la animación.

Ideal para mensajes personalizados, presentaciones, formularios animados y mucho más. 🧠💬

