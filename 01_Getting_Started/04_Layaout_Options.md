# 🧩 Opciones de Diseño (Layout) en Rive

Rive proporciona una poderosa configuración de diseño (`layout`) que permite controlar cómo se visualiza una animación dentro del elemento `<canvas>`. Gracias a las propiedades `fit` y `alignment`, podemos ajustar la escala y la posición de la animación según nuestras necesidades visuales y de responsividad.

---

## ⚙️ Configuración del Layout en Rive

A continuación se presentan tres ejemplos de animaciones con distintas configuraciones de layout:

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

// Ejemplo 2: Fit = Contain + alineación inferior
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

Controla cómo se escala la animación dentro del canvas:

| Valor      | Descripción |
| ---------- | ----------- |
| `Contain`  |             |

| *(default)* | Ajusta la animación sin recortes, manteniendo proporciones. |
| ----------- | ----------------------------------------------------------- |
| `Cover`     | Rellena todo el canvas, recortando lo necesario.            |
| `Fill`      | Deforma la animación para llenar el canvas completamente.   |
| `FitWidth`  | Ajusta al ancho del canvas, manteniendo la proporción.      |
| `FitHeight` | Ajusta a la altura del canvas, manteniendo la proporción.   |
| `ScaleDown` | Escala solo si es más grande que el canvas.                 |
| `None`      | No realiza ningún ajuste automático.                        |

### 🔹 `alignment`

Determina la posición de la animación dentro del canvas:

| Valor                                       | Descripción                             |
| ------------------------------------------- | --------------------------------------- |
| `Center` *(default)*                        | Centra la animación                     |
| `TopLeft`, `TopCenter`, `TopRight`          | Alinea en la parte superior             |
| `CenterLeft`, `CenterRight`                 | Alinea al centro a la izquierda/derecha |
| `BottomLeft`, `BottomCenter`, `BottomRight` | Alinea en la parte inferior             |

---

## 🧪 Ejemplos en contexto

- 🔸 **Logo** usa `Cover` para llenar completamente el canvas, ideal cuando el contenido puede recortarse ligeramente.
- 🔸 **Shapes** utiliza `Contain` y se alinea en la parte inferior con `BottomCenter`, manteniendo todo el contenido visible.
- 🔸 **Wide** aplica `FitHeight` para ajustar la altura completa y centrado visualmente en el canvas.

---

## ✅ Conclusión

El uso de `layout` en Rive te permite tener un control visual detallado sobre tus animaciones. Ajustando `fit` y `alignment`, puedes lograr que tus diseños se adapten perfectamente a distintos tamaños de canvas sin perder calidad ni estética.


