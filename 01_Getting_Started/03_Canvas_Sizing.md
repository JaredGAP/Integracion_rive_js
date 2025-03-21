# 📐 Tamaño del Canvas en Rive

Cuando integras animaciones de Rive en tu página web, es fundamental entender la diferencia entre el **tamaño de renderizado** y el **tamaño visual** del elemento `<canvas>`. Esta comprensión te ayudará a garantizar que las animaciones se vean **nítidas y bien proporcionadas** en todo tipo de pantallas, desde móviles hasta monitores de alta resolución.

---

## 🧱 Renderizado vs Visualización

```html
<canvas width="500" height="500"></canvas>

<style>
  canvas {
    width: 750px;
    height: 750px;
  }
</style>
```

### 📖 ¿Qué significa esto?

- **Tamaño de renderizado (HTML):** Se define con los atributos `width` y `height` directamente en la etiqueta `<canvas>`. Esto determina la resolución interna del lienzo.
- **Tamaño de visualización (CSS):** Se establece con `width` y `height` en CSS, y controla cuánto espacio ocupa el canvas en la pantalla.
- Si el tamaño visual es mayor que el de renderizado, la imagen puede verse **pixelada o borrosa**, especialmente en pantallas con alta densidad de píxeles.

🔍 **Consejo:** Intenta siempre que el tamaño de renderizado sea igual o superior al de visualización.

---

## 🔄 Ajuste automático con Rive

Rive nos facilita este trabajo con el método `resizeDrawingSurfaceToCanvas()`, que ajusta automáticamente el tamaño de renderizado al tamaño CSS del canvas.

```javascript
const animacion = new rive.Rive({
  src: "animacion.riv",
  canvas: document.querySelector("canvas"),
  autoplay: true,
  animations: "loop",
  onLoad: () => {
    animacion.resizeDrawingSurfaceToCanvas();
  }
});
```

### 🧠 ¿Qué hace este método?

- `resizeDrawingSurfaceToCanvas()`: Alinea la resolución interna del canvas con su tamaño visual, asegurando que se vea **claro y sin distorsiones**.
- Se recomienda ejecutarlo dentro del callback `onLoad`, una vez que la animación esté lista.

📱 **Importante para dispositivos móviles:** Muchos móviles tienen pantallas con mayor densidad de píxeles. Este ajuste garantiza que las animaciones mantengan su nitidez también allí.

---

## ✅ Conclusión

Para que tus animaciones se vean espectaculares en todos los dispositivos:

- Asegúrate de comprender la diferencia entre el tamaño HTML y CSS del canvas.
- Usa `resizeDrawingSurfaceToCanvas()` para adaptar automáticamente el lienzo a su contenedor.

Con esta buena práctica, tus animaciones hechas en Rive se verán siempre **nítidas, profesionales y adaptadas a cada pantalla**. 📲✨

