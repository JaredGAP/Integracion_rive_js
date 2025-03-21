# 🔢 Uso de Number Inputs en Rive

Los **Number Inputs** en Rive te permiten controlar el comportamiento de una *State Machine* mediante valores numéricos. Son útiles para representar diferentes **estados, niveles o fases** dentro de una animación, especialmente cuando hay más de dos opciones posibles (a diferencia de un booleano).

---

## ⚙️ Ejemplo de uso con Number Input

```html
<canvas class="icon" width="500" height="500"></canvas>
<h2 class="title">Home</h2>

<script>
  let iconState;

  const animation = new rive.Rive({
    src: "icon.riv",
    canvas: document.querySelector(".icon"),
    artboard: "menu",
    autoplay: true,
    stateMachines: "state-machine",
    onLoad: () => {
      animation.resizeDrawingSurfaceToCanvas();
      const inputs = animation.stateMachineInputs("state-machine");
      iconState = inputs.find(i => i.name === "iconState");
    }
  });

  const title = document.querySelector(".title");
  const pages = document.querySelectorAll(".content > *");

  function goTo(route) {
    switch (route) {
      case "menu":
        iconState.value = 3;
        title.innerText = "Menu";
        break;
      case "home":
        iconState.value = 0;
        title.innerText = "Home";
        break;
      case "details":
        iconState.value = 1;
        title.innerText = "Details";
        break;
    }

    pages.forEach(page => {
      page.classList.toggle("hidden", !page.classList.contains(route));
    });
  }
</script>
```

---

## 🧠 ¿Qué hace este código?

| Elemento                | Función                                                                 |
|------------------------|-------------------------------------------------------------------------|
| `iconState.value = N`  | Cambia el valor numérico para modificar el estado animado.             |
| `goTo("home")`         | Cambia la vista y actualiza la animación según la sección.              |
| `.classList.toggle()`  | Muestra u oculta páginas según el valor actual del estado.             |

---

## 🎯 ¿Cuándo usar Number Inputs?

### 🧭 Navegación entre vistas
- Cambiar entre diferentes pantallas (Home, Menú, Detalles, Perfil, etc.).

### 🎚️ Ajustes progresivos
- Control de volumen, zoom o brillo con niveles.
- Representar progreso o escalas visuales.

### 🎞️ Múltiples animaciones en una sola lógica
- Ciclos de personaje (ej. caminar, correr, saltar).
- Estados de carga: 0 = inactivo, 1 = cargando, 2 = completo, 3 = error.

### 🎮 Interfaces de juegos
- Mostrar reacciones diferentes según el nivel o el puntaje del jugador.

---

## 🖱️ Controlar la animación con scroll

También puedes usar un Number Input para **sincronizar la animación con el desplazamiento** del usuario:

```html
<script>
  let scrollInput;
  const maxValue = 10;

  const animation = new rive.Rive({
    src: "scroll-animation.riv",
    canvas: document.querySelector("canvas"),
    stateMachines: "ScrollMachine",
    autoplay: true,
    onLoad: () => {
      animation.resizeDrawingSurfaceToCanvas();
      const inputs = animation.stateMachineInputs("ScrollMachine");
      scrollInput = inputs.find(input => input.name === "scrollValue");
    }
  });

  window.addEventListener("scroll", () => {
    const scrollRatio = window.scrollY / (document.body.scrollHeight - window.innerHeight);
    const value = Math.min(Math.round(scrollRatio * maxValue), maxValue);
    if (scrollInput) scrollInput.value = value;
  });
</script>
```

### 📌 ¿Cómo funciona?
- `scrollY` mide cuánto se ha desplazado el usuario.
- Se calcula un valor proporcional al total del scroll disponible.
- Se actualiza el valor del input `scrollValue` para animar en función del desplazamiento.

✅ Este patrón es muy útil para animaciones de tipo presentación o efectos de parallax avanzados.

---

## ✅ Conclusión

Los **Number Inputs** te permiten representar múltiples estados y crear transiciones visuales suaves y progresivas. Son ideales cuando tienes más de dos opciones, o cuando la animación debe responder a una variable continua como el scroll, una barra de progreso o un selector numérico.

Combinados con triggers y booleanos, completan el conjunto de herramientas para construir interfaces animadas ricas y adaptables. 🔢✨

