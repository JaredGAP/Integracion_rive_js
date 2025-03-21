# ✅ Uso de Boolean Inputs en Rive

Los **Boolean Inputs** en Rive son variables de tipo verdadero o falso que controlan el estado dentro de una *State Machine*. Son especialmente útiles para alternar animaciones o comportamientos de forma reactiva según interacciones del usuario, condiciones lógicas o cambios en el entorno de la app.

---

## ⚙️ Ejemplo de configuración con Boolean Input

```html
<canvas id="location-pin-icon" width="500" height="500"></canvas>
<input type="text" placeholder="Escribe un destino..." />
<p class="result"></p>

<script>
  let searching;

  const pinIcon = new rive.Rive({
    src: "icon.riv",
    canvas: document.getElementById("location-pin-icon"),
    artboard: "location-pin",
    autoplay: true,
    stateMachines: "state-machine",
    onLoad: () => {
      pinIcon.resizeDrawingSurfaceToCanvas();
      const inputs = pinIcon.stateMachineInputs("state-machine");
      searching = inputs.find(i => i.name === "searching");
    }
  });

  const result = document.querySelector(".result");
  const textField = document.querySelector("input");

  textField.addEventListener("keydown", e => {
    if (e.key === "Enter") {
      findDestination();
    }
  });

  function findDestination() {
    if (!searching) return;

    // Activar estado de "buscando"
    searching.value = true;
    result.innerText = "Buscando...";

    // Simular una búsqueda
    setTimeout(() => {
      searching.value = false;
      result.innerText = `${textField.value} ¿es este el destino?`;
    }, 4000);
  }
</script>
```

---

## 🔍 Explicación de los elementos clave

| Elemento | Descripción |
|---------|-------------|
| `stateMachineInputs()` | Devuelve todos los inputs definidos en la State Machine. |
| `searching.value = true` | Activa el input booleano para cambiar el estado de la animación. |
| `value = false` | Desactiva el input, lo que puede revertir o detener la animación. |
| `keydown` + `Enter` | Detecta la acción del usuario e inicia el flujo de búsqueda. |

---

## 🧠 Casos de uso típicos con Boolean Inputs

### 🔄 Toggle visual
- Mostrar o ocultar una animación de carga.
- Cambiar entre dos estados visuales: encendido/apagado, abierto/cerrado, etc.

### 🖱️ Respuesta a eventos del usuario
- Activar un estado "hover" cuando el ratón pasa por encima.
- Encender un modo "activo" al hacer clic en un botón.

### 🧩 Comportamiento de componentes interactivos
- Expandir o contraer una sección animada.
- Activar el seguimiento de ubicación en un mapa animado.
- Mostrar confirmaciones visuales (p. ej., "correcto" o "fallido").

### 🎮 Aplicaciones en juegos
- Iniciar una acción como correr, defender o esconderse.
- Entrar en modo "alerta" o "dañado" visualmente.

---

## 🚦 Buenas prácticas

- ✅ Verifica que el input exista antes de modificarlo.
- ✅ Usa nombres claros y descriptivos para los inputs, como `isOpen`, `searching`, `isActive`, etc.
- ❌ No utilices triggers para estados persistentes. Usa booleanos si el estado debe mantenerse.
- ✅ Mantén el control del cambio de valor desde JS o desde la propia State Machine según convenga.

---

## ✅ Conclusión

Los **Boolean Inputs** son ideales para representar estados binarios dentro de una animación. Su uso permite que las animaciones respondan de forma más natural y contextual a eventos del usuario o lógica de aplicación.

Combinados con otras entradas como triggers o números, puedes construir flujos de interacción complejos sin perder claridad ni control.


