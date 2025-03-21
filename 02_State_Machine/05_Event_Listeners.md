# 📡 Uso de Event Listeners en Rive

Rive permite escuchar eventos personalizados emitidos desde una *State Machine* mediante los **Event Listeners**. Estos eventos pueden contener datos dinámicos y te permiten ejecutar funciones JavaScript específicas en el momento exacto en que ocurre algo dentro de la animación.

Esto abre un mundo de posibilidades para crear interfaces reactivas, sincronizadas y altamente interactivas.

---

## ⚙️ Ejemplo básico de uso

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

  // Escuchar eventos emitidos desde Rive
  animation.on(rive.EventType.RiveEvent, (event) => {
    console.log("Evento recibido:", event);
    console.log("Nombre:", event.data.name);
    console.log("Propiedades:", event.data.properties);

    // Mostrar texto dinámico proveniente de la animación
    label.innerText = event.data.properties.label || "Evento sin nombre";
  });
</script>
```

---

## 🧠 ¿Qué son los eventos de Rive?

Desde la interfaz de Rive Studio, puedes definir un **evento** dentro de una transición de una *State Machine*. Este evento puede llevar un nombre personalizado y un conjunto de propiedades clave-valor. Al activarse, ese evento puede ser capturado por tu código JavaScript mediante un listener.

---

## 📖 Explicación clave del código

| Línea clave | Descripción |
|-------------|-------------|
| `rive.EventType.RiveEvent` | Tipo de evento que escucha el listener (los generados en la animación). |
| `event.data.name` | Nombre del evento que se definió en Rive Studio. |
| `event.data.properties` | Objeto con los datos asociados al evento (pueden ser dinámicos). |
| `label.innerText = ...` | Actualiza el contenido visible de un elemento según el evento recibido. |

---

## 🧪 Casos de uso reales

### 🛎️ Notificaciones visuales
- Activar un aviso cuando se completa una animación.
- Mostrar una confirmación cuando se finaliza una interacción (por ejemplo, un formulario animado).

### 🧩 Comunicación con otros componentes
- Sincronizar otros elementos del DOM cuando ocurre un evento animado.
- Cambiar la clase de un botón cuando la animación indica "activo", "error", etc.

### 📊 Captura de métricas y analítica
- Registrar cuántas veces se activó cierto estado animado.
- Lanzar una acción de seguimiento (analytics, logs) cuando una animación reporta una acción específica.

### 🎮 Integración en juegos o simulaciones
- Detectar cuándo una animación de golpe ha terminado para habilitar el siguiente movimiento.
- Lanzar efectos sonoros sincronizados con estados visuales.

### 🖼️ Experiencias narrativas y UI storytelling
- Mostrar texto dinámico relacionado con la animación (por ejemplo, etiquetas, títulos, descripciones que cambian al avanzar en la animación).

---

## 🧰 Buenas prácticas

- ✅ Define nombres de eventos y propiedades claros y coherentes en Rive Studio.
- ✅ Valida que `event.data.properties` no sea `undefined` antes de acceder a valores.
- ✅ Usa los eventos para comunicar estados, no para lógica compleja que debería gestionarse desde JS.
- ❌ No dependas exclusivamente de los eventos para el flujo principal de una app.

---

## ✅ Conclusión

Los **Event Listeners** de Rive son el puente entre tus animaciones y la lógica de tu aplicación. Gracias a ellos, puedes reaccionar en tiempo real a lo que ocurre visualmente, sincronizar elementos del DOM, actualizar interfaces y potenciar la interactividad de forma profesional.
