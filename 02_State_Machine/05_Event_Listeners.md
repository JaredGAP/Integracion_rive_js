# 📡 Uso de Event Listeners en Rive

Rive permite escuchar eventos personalizados emitidos desde una *State Machine* mediante los **Event Listeners**. Esto te permite ejecutar funciones específicas en JavaScript en el momento exacto en que ocurre algo dentro de la animación.

Esta funcionalidad es ideal para crear interfaces altamente interactivas, reactivas y sincronizadas con el estado visual.

---

## ⚙️ Ejemplo básico en JavaScript

```html
<canvas width="500" height="500"></canvas>
<p class="label">Esperando evento...</p>

<script>
  const animation = new rive.Rive({
    src: "menu.riv",
    canvas: document.querySelector("canvas"),
    stateMachines: "state-machine",
    autoplay: true,
    onLoad: () => {
      animation.resizeDrawingSurfaceToCanvas();
    }
  });

  const label = document.querySelector(".label");

  // Escuchar eventos enviados desde la State Machine
  animation.on(rive.EventType.RiveEvent, (event) => {
    console.log("Evento recibido:", event);
    console.log("Nombre:", event.data.name);
    console.log("Propiedades:", event.data.properties);

    // Mostrar texto en pantalla según la propiedad del evento
    label.innerText = event.data.properties.label || "Evento sin nombre";
  });
</script>
```

---

## 🧠 ¿Qué son los eventos de Rive?

Desde el editor de Rive Studio, puedes definir eventos dentro de las transiciones de una *State Machine*. Estos eventos pueden llevar:

- Un **nombre** personalizado (como `onComplete`, `onError`, `nextStep`).
- Un **conjunto de propiedades** dinámicas (por ejemplo: `label: "¡Enviado!"`, `step: 3`).

Estos eventos pueden ser escuchados en tu código para **sincronizar otras partes de la interfaz**.

---

## 🔍 Explicación del código

| Línea clave                  | Función                                                         |
|-----------------------------|------------------------------------------------------------------|
| `rive.EventType.RiveEvent`  | Tipo de evento personalizado generado desde Rive.               |
| `event.data.name`           | Nombre del evento emitido.                                      |
| `event.data.properties`     | Propiedades adjuntas al evento como un objeto clave-valor.      |
| `label.innerText = ...`     | Muestra la propiedad `label` del evento en pantalla.            |

---

## 🧪 Casos de uso reales

### 🛎️ Notificaciones
- Mostrar un mensaje al completar una animación.
- Confirmar que un paso visual se ha completado correctamente.

### 🧩 Comunicación entre componentes
- Activar clases CSS o mostrar elementos del DOM cuando ocurre un evento.

### 📊 Analítica y métricas
- Contabilizar cuántas veces se lanza un estado animado.
- Lanzar eventos de seguimiento o log personalizados.

### 🎮 Juegos y simulaciones
- Detectar cuándo termina un ataque para habilitar el siguiente.
- Sincronizar efectos sonoros con la animación visual.

### 🖼️ Storytelling visual
- Mostrar texto o imágenes dinámicas al avanzar entre estados narrativos.

---

## ✅ Buenas prácticas

- ✔️ Usa nombres y propiedades claras en los eventos de Rive Studio.
- ✔️ Siempre valida que `event.data.properties` exista antes de acceder.
- ❌ No delegues toda la lógica de tu aplicación a eventos de animación.
- ✔️ Úsalos como *disparadores visuales* para complementar tu UI.

---

## 🎯 Conclusión

Los **Event Listeners** en Rive son el puente perfecto entre lo visual y la lógica de tu interfaz. Te permiten detectar en tiempo real lo que ocurre dentro de tus animaciones y sincronizarlo con otros elementos del DOM.

Al usarlos correctamente, puedes crear experiencias ricas, interactivas y perfectamente coordinadas. 🚀

