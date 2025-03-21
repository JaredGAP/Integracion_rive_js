# 🖱️ Hero Hover Interaction con Rive y Eventos Personalizados

Finalizamos la sección *hero* añadiendo interactividad basada en **hover** sobre los íconos que forman parte de la animación de Rive. Esto se logra escuchando eventos personalizados emitidos desde la *State Machine* y animando el texto del título de la sección cuando el usuario pasa el ratón por diferentes áreas.

---

## 🧠 ¿Qué estamos haciendo?

- Escuchamos los eventos personalizados enviados desde la animación de Rive (definidos en la *State Machine*).
- Extraemos el texto desde la propiedad `event.data.properties.text`.
- Cambiamos dinámicamente el texto del encabezado (`<h1>`) dentro del hero para que coincida con la acción.

Esto permite que los íconos dentro de la animación generen reacciones en la interfaz web, como si "hablaran" con el usuario.

---

## ✨ Código JavaScript explicado

```javascript
// :: Hero Icon Hover Interaction ::
heroAnimation.on(
  rive.EventType.RiveEvent,
  (event) => {
    animateHeading(event.data.properties.text);
  }
);

// utils
const heading = document.querySelector(".hero h1");

function animateHeading(text) {
  if (heading.innerText === text) return;

  heading.classList.add("fade-out");
  setTimeout(() => {
    heading.innerText = text;
    heading.classList.remove("fade-out");
  }, 200);
}
```

---

## 🧱 HTML relevante

Asegúrate de tener un encabezado dentro del hero:

```html
<section class="hero">
  <h1>Payments Done Right!</h1>
</section>
```

Y añade algo de estilo para la animación:

```css
.hero h1.fade-out {
  opacity: 0;
  transition: opacity 0.2s ease;
}
```

---

## 📦 ¿Qué debe incluir tu archivo `.riv`?

Desde **Rive Studio**, en la máquina de estados de tu artboard:

- Crea transiciones (por ejemplo, entre íconos al pasar el cursor).
- En esas transiciones, **emite un evento** con un nombre como `icon-hover`.
- Añade una propiedad `text` al evento, con el mensaje que quieras mostrar.

---

## ✅ Resultado esperado

- Al pasar el cursor sobre un ícono dentro de la animación:
  - Se activa un evento en Rive.
  - Se captura desde JavaScript.
  - Se anima el texto `<h1>` para mostrar el nombre o mensaje correspondiente.

Esta interacción refuerza la sensación de que el contenido reacciona al usuario, haciendo que la animación cobre vida.

---

## 🧰 Sugerencias y mejoras

- Puedes añadir más propiedades a los eventos (por ejemplo, color, subtítulo, etc.).
- Usa una animación más larga o una transición suave con GSAP si deseas más impacto.
- Si usas múltiples idiomas, puedes traducir dinámicamente el contenido recibido.

---

## 🏁 Conclusión

Esta técnica convierte tu animación en un **componente interactivo real**, donde los elementos dentro de Rive informan a la interfaz web de lo que está ocurriendo. Es una forma elegante de conectar el mundo gráfico con la lógica de la experiencia de usuario.

