# 🚀 Uso Avanzado de Trigger Inputs en Rive

Los **Trigger Inputs** en Rive son una poderosa herramienta para ejecutar eventos específicos dentro de una *State Machine*. Funcionan como botones de acción: no almacenan estado, pero permiten *disparar* animaciones o transiciones en respuesta a una acción del usuario, a lógica de tu app o a cualquier evento del entorno.

---

## ⚙️ ¿Qué es un Trigger Input?

Un **Trigger** es un tipo de input dentro de una *State Machine* en Rive que se activa de forma puntual. A diferencia de los booleanos o numéricos, no mantiene valor alguno, sino que provoca una transición inmediata o ejecuta una acción específica cuando se dispara.

---

## 🔧 Configuración básica de un Trigger en JavaScript

```html
<canvas width="500" height="500"></canvas>

<script>
  let notifyTrigger;

  const animation = new rive.Rive({
    src: "icon.riv",
    canvas: document.querySelector("canvas"),
    autoplay: true,
    stateMachines: "state-machine",
    onLoad: () => {
      animation.resizeDrawingSurfaceToCanvas();

      // Obtener todos los inputs de la máquina de estados
      const inputs = animation.stateMachineInputs("state-machine");

      // Buscar el trigger por nombre
      notifyTrigger = inputs.find(input => input.name === "notify");

      // Activar el trigger inmediatamente (solo como ejemplo)
      notifyTrigger.fire();
    }
  });

  // Activar el trigger manualmente al hacer clic
  document.querySelector("canvas").addEventListener("click", () => {
    notifyTrigger.fire();
  });
</script>
```

---

## 📖 Explicación de cada parte

| Elemento | Descripción |
|---------|-------------|
| `stateMachineInputs()` | Devuelve los inputs definidos en la máquina de estados. |
| `input.name === "notify"` | Identifica el input tipo Trigger que creaste en Rive. |
| `fire()` | Dispara el trigger: lanza la transición o evento asociado. |

---

## 🧠 ¿Para qué sirven los Trigger Inputs?

Los triggers se utilizan para lanzar acciones específicas **una sola vez**, sin necesidad de cambiar o mantener valores. Por ejemplo:

- 🔔 Hacer sonar una campana cuando llega una notificación.
- 💥 Mostrar una explosión tras una colisión.
- 🧤 Ejecutar una animación de "apretón de manos" al hacer clic en un botón.
- 🧼 Lanzar una secuencia de limpieza cuando se detecta una acción de usuario.
- 📬 Reproducir una animación de "enviar mensaje" al hacer clic en un formulario.

---

## 🧪 Casos de uso interesantes

### 🎮 Interacciones en juegos
- Disparar una animación de golpe al pulsar un botón de ataque.
- Activar un power-up visual cuando se recoge un ítem.

### 💼 Aplicaciones empresariales o dashboards
- Mostrar una animación de validación exitosa al completar un formulario.
- Reproducir una animación sutil cuando cambia el estado de un KPI (por ejemplo, sube una métrica).

### 📱 Apps móviles o SPA (Single Page Applications)
- Animaciones de respuesta táctil (por ejemplo, ripple effects).
- Transiciones suaves entre secciones al navegar en la app.

### 🖼️ Elementos decorativos o microinteracciones
- Disparar partículas al pasar el mouse sobre un elemento.
- Mostrar un pulso luminoso en una notificación nueva.
- Lanzar una reacción (emoji, fuego, etc.) al pulsar un botón de "like".

---

## 🚦 Buenas prácticas al usar Trigger Inputs

- ✅ Verifica siempre que el trigger exista (`if (trigger) trigger.fire()`).
- ✅ Usa nombres descriptivos en Rive como `onClick`, `explode`, `submitForm`, etc.
- ✅ Combina triggers con lógica visual en Rive para crear experiencias sin lógica extra en JS.
- ❌ No intentes asignarles valores. No son booleanos ni contadores.

---

## ✅ Conclusión

Los **Trigger Inputs** son el mecanismo perfecto para conectar tus animaciones con acciones reales del usuario o de tu aplicación. Permiten reacciones inmediatas y elegantes, haciendo que la interfaz cobre vida.

Explora su potencial, experimenta con varios triggers en la misma *State Machine* y diseña flujos visuales ricos sin complicar tu lógica de programación.



