# 🌐 Open URL Event en Rive

Rive permite que las animaciones generen **eventos especiales**, como abrir un enlace directamente desde la propia animación. Esto se logra mediante los **Rive Events** y específicamente el tipo de evento llamado `OpenUrlEvent`. Sin embargo, por razones de seguridad y control, estos eventos **no se activan automáticamente** a menos que tú lo configures explícitamente.

---

## 🧠 ¿Qué es un OpenUrlEvent?

Un **OpenUrlEvent** es un tipo especial de evento que puedes emitir desde Rive Studio y que contiene una URL como propiedad. Si se gestiona correctamente en el navegador, abrirá esa URL en una nueva pestaña o ventana.

---

## ⚠️ Comportamiento por defecto

Por seguridad, Rive **NO ejecuta automáticamente** los eventos especiales como OpenUrlEvent. Esto significa que:

- Necesitas **escucharlos manualmente** usando un listener de tipo `EventType.RiveEvent`, o bien...
- Puedes activar el modo automático con `automaticallyHandleEvents: true`.

---

## ✅ Activar OpenUrlEvent automáticamente

```javascript
const animation = new rive.Rive({
  src: "open-url-demo.riv",
  canvas: document.querySelector("canvas"),
  autoplay: true,
  stateMachines: "url-machine",
  automaticallyHandleEvents: true, // Activa la gestión automática
  onLoad: () => animation.resizeDrawingSurfaceToCanvas()
});
```

### 🔐 ¿Qué pasa con esto?

- Si la animación emite un evento con una propiedad `url`, Rive abrirá esa URL automáticamente cuando se active el evento.
- Esta funcionalidad puede ser útil en experiencias interactivas tipo "click para visitar".

---

## 👂 Manejo manual (modo recomendado)

Si quieres tener más control sobre qué se abre y cómo:

```javascript
const animation = new rive.Rive({
  src: "open-url-demo.riv",
  canvas: document.querySelector("canvas"),
  autoplay: true,
  stateMachines: "url-machine",
  automaticallyHandleEvents: false, // por defecto es false
  onLoad: () => animation.resizeDrawingSurfaceToCanvas()
});

animation.on(rive.EventType.RiveEvent, (event) => {
  const url = event.data.properties.url;
  if (url) {
    window.open(url, "_blank"); // Puedes validarlo antes de abrir
  }
});
```

### 🔒 Ventajas de manejarlo manualmente
- ✅ Puedes validar la URL antes de abrirla.
- ✅ Puedes registrar el evento (para analítica).
- ✅ Puedes abrir en la misma pestaña, en otra o con condiciones.
- ✅ Evitas comportamiento no deseado o inesperado en tu aplicación.

---

## 🔧 ¿Cómo configurar un OpenUrlEvent en Rive Studio?

1. Abre tu *State Machine*.
2. Crea una transición.
3. Añade un **evento** desde esa transición.
4. Nómbralo (opcional).
5. Añade una propiedad llamada `url` con el enlace deseado.

---

## ✅ Conclusión

El uso de **OpenUrlEvent** en Rive es una forma poderosa de enlazar tu animación con el contenido externo. Ya sea automáticamente o de forma controlada, te permite convertir animaciones en componentes interactivos reales que guían al usuario hacia acciones claras.

