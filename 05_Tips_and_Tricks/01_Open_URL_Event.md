# 🌐 Open URL Event en Rive

Rive permite que las animaciones generen **eventos personalizados** como abrir un enlace directamente desde una animación. Esto es posible gracias a los **Rive Events**, y específicamente al tipo `OpenUrlEvent`, diseñado para enlazar una animación con una URL.

---

## 🧠 ¿Qué es un OpenUrlEvent?

Un **OpenUrlEvent** es un evento que se puede emitir desde una máquina de estados en Rive. Incluye una propiedad `url` y, si se maneja correctamente en el navegador, puede **abrir una nueva pestaña o ventana** con ese enlace.

Este tipo de evento es útil para experiencias como:
- Animaciones de llamada a la acción.
- Banners interactivos que enlazan a promociones.
- Interfaces educativas o narrativas que enlazan con más contenido.

---

## ⚠️ Importante: comportamiento por defecto

Por razones de seguridad, Rive **NO activa automáticamente** eventos como `OpenUrlEvent`. Tienes dos formas de manejarlos:

### Opción 1: Gestión automática (modo fácil)

```javascript
const animation = new rive.Rive({
  src: "open-url-demo.riv",
  canvas: document.querySelector("canvas"),
  autoplay: true,
  stateMachines: "url-machine",
  automaticallyHandleEvents: true, // 🔓 Activa el modo automático
  onLoad: () => animation.resizeDrawingSurfaceToCanvas()
});
```

🟢 **Resultado:** cuando la animación dispare un evento que incluya la propiedad `url`, el navegador abrirá esa URL automáticamente.

---

### Opción 2: Manejo manual (modo recomendado)

```javascript
const animation = new rive.Rive({
  src: "open-url-demo.riv",
  canvas: document.querySelector("canvas"),
  autoplay: true,
  stateMachines: "url-machine",
  automaticallyHandleEvents: false, // por defecto está desactivado
  onLoad: () => animation.resizeDrawingSurfaceToCanvas()
});

animation.on(rive.EventType.RiveEvent, (event) => {
  const url = event.data.properties.url;
  if (url && isValidUrl(url)) {
    window.open(url, "_blank");
  }
});

function isValidUrl(url) {
  try {
    new URL(url);
    return true;
  } catch (_) {
    return false;
  }
}
```

🔒 **Ventajas del modo manual:**
- Validar la URL antes de abrirla.
- Personalizar cómo se abre (misma pestaña, nueva, popup...).
- Registrar métricas o estadísticas.
- Prevenir URLs maliciosas o mal formadas.

---

## 🔧 ¿Cómo emitir un OpenUrlEvent desde Rive Studio?

1. Abre tu máquina de estados.
2. Añade una transición.
3. En esa transición, añade un evento.
4. En el evento, crea una propiedad llamada `url`.
5. Escribe la URL como valor (por ejemplo, `https://tusitio.com`).

¡Y listo! Ya puedes emitir eventos desde la animación.

---

## ✅ Conclusión

`OpenUrlEvent` convierte tus animaciones de Rive en **puentes interactivos** hacia otras páginas, productos o contenidos. Puedes usarlos de forma segura y flexible, controlando exactamente qué se abre, cómo y cuándo.

Perfecto para experiencias ricas donde la animación no solo acompaña, sino que **invita a actuar**. 🚀

