# 🔁 De la Animación a la Lógica: Rive como Motor de Eventos

Rive no solo sirve para **mostrar animaciones**: también puede convertirse en una fuente de **eventos lógicos** que controlen el flujo de tu aplicación. Gracias a los **eventos personalizados** emitidos desde máquinas de estado, puedes hacer que la animación influya directamente sobre el DOM, rutas, formularios, sonido, o cualquier parte de tu lógica de frontend.

---

## 🧠 ¿Por qué esto es importante?

Muchas veces vemos la animación como un resultado visual de lo que pasa en la app. Pero con Rive también puedes hacer lo contrario:

> 🧩 “Que sea la animación quien decida lo que ocurre.”

Esto abre posibilidades como:
- Navegar a otra vista cuando termina una animación.
- Lanzar efectos visuales o sonidos sincronizados.
- Ejecutar lógica de negocio cuando un estado llega a cierto punto.

---

## 📦 Estructura básica con Rive Events

```javascript
const animation = new rive.Rive({
  src: "animacion.riv",
  canvas: document.querySelector("canvas"),
  stateMachines: "machine",
  autoplay: true,
  onLoad: () => animation.resizeDrawingSurfaceToCanvas()
});

animation.on(rive.EventType.RiveEvent, (event) => {
  const data = event.data;

  if (data.name === "completo") {
    console.log("✅ Animación finalizada, redirigiendo...");
    window.location.href = "/gracias";
  }

  if (data.name === "jugarSonido") {
    const audio = new Audio("./click.mp3");
    audio.play();
  }
});
```

---

## 📖 ¿Qué está pasando aquí?

| Parte                         | Función                                                        |
|------------------------------|-----------------------------------------------------------------|
| `RiveEvent`                  | Escucha eventos emitidos desde la animación                    |
| `data.name === "completo"`   | Reacciona a un evento personalizado definido en Rive Studio     |
| `window.location.href`       | Lógica externa que se ejecuta al recibir el evento              |
| `audio.play()`               | Dispara una acción nativa del navegador (ej: sonido, DOM, etc.) |

---

## 🧩 ¿Cómo defino eventos en Rive Studio?

1. Abre tu máquina de estados.
2. Crea una transición entre dos estados.
3. Haz clic en la transición y añade un evento.
4. Ponle un nombre (ej: `completo`) y propiedades opcionales.
5. Exporta el archivo `.riv` normalmente.

---

## 🎯 Casos de uso comunes

- **Interacción por narrativa**: avanzar pasos al completar una transición.
- **Lógica condicional**: emitir eventos distintos según estados alcanzados.
- **Integración con UI**: mostrar/ocultar elementos del DOM según la animación.
- **Gamificación**: puntos, logros, feedback visual y sonoro sincronizados.

---

## ✅ Conclusión

Las animaciones en Rive no solo decoran tu interfaz. También pueden **dirigir el flujo de tu aplicación**, convirtiéndose en un motor visual que emite eventos clave. Usar `RiveEvent` te permite convertir interactividad visual en lógica real.

¡Y eso hace que tu UI cobre vida de verdad! ⚡🎯

