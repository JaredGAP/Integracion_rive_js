# 🧩 Opciones de Diseño (Layout) en Rive

Cuando integras animaciones en Rive dentro de tu página web, es muy útil saber cómo controlar **la forma en que se escalan y alinean** dentro del elemento `<canvas>`. Para ello, Rive ofrece la clase `Layout`, que te permite definir dos propiedades clave: `fit` y `alignment`.

Estas propiedades ayudan a que tu animación luzca bien sin importar el tamaño del canvas o el dispositivo.

---

## ⚙️ ¿Cómo se configura un Layout en Rive?

Aquí tienes tres ejemplos prácticos de cómo aplicar distintos layouts:

```javascript
// Ejemplo 1: Fit = Cover
const logo = new rive.Rive({
  src: "layout.riv",
  canvas: document.querySelector(".row:first-child canvas"),
  artboard: "logo",
  animations: "loop",
  autoplay: true,
  layout: new rive.Layout({
    fit: rive.Fit.Cover
  }),
  onLoad: () => logo.resizeDrawingSurfaceToCanvas()
});

// Ejemplo 2: Contain + alineación inferior
const shapes = new rive.Rive({
  src: "layout.riv",
  canvas: document.querySelector(".row:nth-child(2) canvas"),
  artboard: "shapes",
  animations: "loop",
  autoplay: true,
  layout: new rive.Layout({
    fit: rive.Fit.Contain,
    alignment: rive.Alignment.BottomCenter
  }),
  onLoad: () => shapes.resizeDrawingSurfaceToCanvas()
});

// Ejemplo 3: FitHeight centrado
const wide = new rive.Rive({
  src: "layout.riv",
  canvas: document.querySelector(".col canvas"),
  artboard: "Wide",
  animations: "loop",
  autoplay: true,
  layout: new rive.Layout({
    fit: rive.Fit.FitHeight,
    alignment: rive.Alignment.Center
  }),
  onLoad: () => wide.resizeDrawingSurfaceToCanvas()
});
```

---

## 🔧 Propiedades del Layout

### 🔹 `fit`
Determina cómo la animación se escala dentro del canvas. Los valores posibles son:

| Valor        | Descripción                                                                 |
|-------------|-----------------------------------------------------------------------------|
| `Contain`   | (por defecto) Escala la animación para que quepa entera sin recortes.      |
| `Cover`     | Escala para cubrir todo el canvas, aunque se recorte parte.                |
| `Fill`      | Deforma la animación para llenar el canvas completamente.                  |
| `FitWidth`  | Ajusta al ancho del canvas, manteniendo proporción.                        |
| `FitHeight` | Ajusta a la altura del canvas, manteniendo proporción.                     |
| `ScaleDown` | Solo escala si la animación es más grande que el canvas.                   |
| `None`      | No ajusta automáticamente; mantiene el tamaño original.                    |

### 🔹 `alignment`
Controla la posición de la animación dentro del canvas:

| Valor                                        | Descripción                             |
|---------------------------------------------|-----------------------------------------|
| `Center` *(por defecto)*                    | Centra la animación                     |
| `TopLeft`, `TopCenter`, `TopRight`          | Alinea en la parte superior             |
| `CenterLeft`, `CenterRight`                 | Alinea verticalmente al centro          |
| `BottomLeft`, `BottomCenter`, `BottomRight` | Alinea en la parte inferior             |

---

## 🧪 ¿Cuándo usar cada configuración?

- 🔸 **Logo con `Cover`**: ideal para llenar todo el espacio del canvas, aunque se recorte parte de la animación.
- 🔸 **Shapes con `Contain` + `BottomCenter`**: mantiene todo el contenido visible y lo posiciona en la parte inferior.
- 🔸 **Wide con `FitHeight` + centrado**: útil cuando quieres que la animación siempre se ajuste en altura sin perder proporción.

---

## ✅ Conclusión

El sistema de `layout` de Rive te permite lograr un control visual preciso para que tus animaciones se adapten a distintos tamaños de canvas sin perder calidad ni coherencia visual.

👉 Experimenta combinando diferentes valores de `fit` y `alignment` para conseguir el efecto deseado en cada proyecto.

Con un buen uso del layout, tus animaciones se verán **perfectamente integradas y profesionales** en cualquier dispositivo. ✨

