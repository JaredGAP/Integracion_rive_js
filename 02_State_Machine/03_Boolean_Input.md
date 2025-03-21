# ✅ Uso de Boolean Inputs en Rive

Los **Boolean Inputs** en Rive son entradas que representan un estado binario: verdadero (`true`) o falso (`false`). Son perfectas para controlar **transiciones entre estados**, como mostrar/ocultar, encender/apagar o iniciar/detener una animación, según la lógica de tu aplicación o interacciones del usuario.

---

## ⚙️ Ejemplo de uso en JavaScript

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

    // Activar el estado "buscando"
    searching.value = true;
    result.innerText = "Buscando...";

    // Simular búsqueda
    setTimeout(() => {
      searching.value = false;
      result.innerText = `${textField.value} ¿es este el destino?`;
    }, 4000);
  }
</script>
```

---

## 🧠 ¿Qué está pasando aquí?

| Elemento                    | Función                                                                 |
|----------------------------|-------------------------------------------------------------------------|
| `stateMachineInputs()`     | Devuelve los inputs de la máquina de estados.                          |
| `searching.value = true`   | Activa la animación de búsqueda.                                       |
| `searching.value = false`  | La desactiva (regresa a su estado anterior).                           |
| Evento `keydown` + Enter   | Detecta cuando el usuario presiona Enter en el input de texto.         |

---

## 🔍 ¿Para qué usar Boolean Inputs?

### ✅ Casos comunes:

- Cambiar visualmente entre dos estados (p. ej. interruptores on/off).
- Mostrar una animación de carga mientras se espera una respuesta.
- Cambiar de "modo activo" a "modo inactivo".
- Indicar si un elemento está seleccionado, visible, enfocado, etc.

### 🎮 En juegos o apps interactivas:

- Mostrar si un personaje está corriendo, saltando o herido.
- Entrar o salir de un estado especial (modo escudo, invisibilidad, etc.).

---

## ⚠️ Buenas prácticas

- ✔️ Asegúrate de que el input existe (`if (input) input.value = true;`).
- ✔️ Usa nombres de inputs claros como `isActive`, `searching`, `showDetails`, etc.
- ❌ No uses triggers para representar estados persistentes.
- ✔️ Decide si el cambio de valor ocurre desde JS o desde la lógica visual en Rive.

---

## ✅ Conclusión

Los **Boolean Inputs** son ideales para manejar animaciones que representan un estado que puede estar activo o inactivo. Son simples, potentes y muy útiles cuando quieres que tu animación reaccione de forma continua a una condición.

Combinados con triggers y valores numéricos, te permiten construir experiencias visuales interactivas con una lógica clara y mantenible. 💡

