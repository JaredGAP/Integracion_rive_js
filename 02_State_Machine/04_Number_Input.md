# 🔢 Uso de Number Inputs en Rive

Los **Number Inputs** en Rive permiten gestionar múltiples estados dentro de una *State Machine* utilizando valores numéricos. Son ideales para animaciones donde cada valor representa un estado, una etapa o una opción distinta dentro de la misma lógica visual.

---

## ⚙️ Configuración básica con Number Input

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

## 📖 Explicación clave

| Elemento | Descripción |
|---------|-------------|
| `iconState.value = N` | Cambia el valor del input numérico para activar un estado. |
| `goTo("home")` | Ejecuta una transición visual y lógica hacia una sección específica. |
| `.classList.toggle()` | Muestra u oculta páginas dependiendo del estado. |

---

## 🧠 Casos de uso útiles para Number Inputs

### 🧭 Navegación entre vistas
- Menú → Home → Detalles → Perfil: cada valor representa una vista diferente.

### 🎚️ Ajustes progresivos
- Niveles de zoom, volumen o brillo.
- Escalado visual de una animación o ilustración.

### 🎞️ Animaciones con múltiples escenas
- Ciclos de personajes (caminar, correr, saltar).
- Estados de carga: inactivo → cargando → completo → error.

### 🎮 Interfaz de juego o gamificación
- Nivel de vida, progreso o puntuación.
- Reacciones del avatar según puntuación (0 = triste, 3 = feliz).

---

## 🖱️ Controlar una animación con scroll del ratón

También puedes utilizar un **Number Input** para controlar una animación progresiva según el movimiento del scroll del usuario:

```html
<script>
  let scrollInput;
  const maxValue = 10; // Valor máximo del input numérico

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

### 📝 ¿Cómo funciona?
- `scrollY` mide el desplazamiento actual.
- Se calcula una proporción (`scrollRatio`) con respecto a toda la página.
- Se multiplica por un valor máximo para limitar el número.
- El input numérico de la *State Machine* se actualiza para reflejar ese valor en tiempo real.

✅ Este patrón es ideal para animaciones que reaccionan al desplazamiento, como presentaciones interactivas o efectos visuales progresivos.

---

## ✅ Conclusión

Los **Number Inputs** permiten un nivel elevado de control sobre la lógica visual de tus animaciones. Al representar valores dinámicos, te permiten crear interfaces altamente interactivas, con múltiples estados animados que responden tanto a eventos discretos como a entradas continuas (como el scroll).






