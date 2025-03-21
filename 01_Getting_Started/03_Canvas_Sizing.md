# 📐 Tamaño del Canvas en Rive

Cuando integras animaciones de Rive en tu web, es esencial comprender la diferencia entre el **tamaño de renderizado** y el **tamaño de visualización** del elemento `<canvas>`. Esta comprensión garantiza que tus animaciones se vean nítidas y con buena calidad en todos los dispositivos y resoluciones.

---

## 🧱 Tamaño de Canvas: Renderizado vs Visualización

```html
<canvas width="500" height="500"></canvas>

<style>
  canvas {
    width: 750px;
    height: 750px;
  }
</style>
```

### 📖 Explicación:
- **Renderizado (`width` y `height` en HTML):** Determina la resolución interna del `canvas`. Afecta la calidad de la animación.
- **Visualización (`width` y `height` en CSS):** Define el tamaño visible en la pantalla.
- Si el tamaño visual es mayor que el de renderizado, la animación puede verse borrosa o pixelada.

---

## 🔄 Ajuste Dinámico del Canvas con Rive

Para garantizar una buena calidad visual en cualquier tamaño, Rive proporciona el método `resizeDrawingSurfaceToCanvas()`, que ajusta automáticamente la superficie de dibujo:

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

### 📖 Detalles:
- `onLoad`: Se ejecuta una vez que el archivo `.riv` se ha cargado correctamente.
- `resizeDrawingSurfaceToCanvas()`: Ajusta la resolución del `canvas` a su tamaño CSS, asegurando una visualización clara y precisa sin importar el dispositivo.

---

## ✅ Conclusión

Un `canvas` mal configurado puede afectar la calidad de tu animación. Usar correctamente los atributos de tamaño y el método `resizeDrawingSurfaceToCanvas()` de Rive permite mantener tus animaciones nítidas y optimizadas para cualquier pantalla.

