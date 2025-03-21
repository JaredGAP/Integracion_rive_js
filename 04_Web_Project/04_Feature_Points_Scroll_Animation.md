# 🎯 Feature Point Animation con Scroll Sync

En esta sección aprenderás cómo crear una animación con Rive que se sincroniza con diferentes **puntos clave (feature points)** de tu layout, activados mediante scroll. Cada punto activa una parte diferente de la animación, permitiendo contar una historia visual paso a paso mientras el usuario navega por la página.

---

## 🧠 ¿Qué haremos?

- Utilizaremos **ScrollTrigger de GSAP** para detectar cuándo el usuario llega a distintas secciones del layout.
- Cada sección o paso actualizará el estado de la animación Rive mediante un **Number Input** o **Trigger Input**.
- La animación responderá en tiempo real, destacando o activando partes específicas según la sección visible.

---

## 🧱 Estructura HTML sugerida

```html
<section class="feature">
  <div class="feature-rive">
    <canvas width="640" height="640"></canvas>
  </div>
  <div class="steps">
    <div class="step" data-step="0">Paso 1: Introducción</div>
    <div class="step" data-step="1">Paso 2: Seguridad</div>
    <div class="step" data-step="2">Paso 3: Integración</div>
    <div class="step" data-step="3">Paso 4: Final</div>
  </div>
</section>
```

---

## ⚙️ Lógica en JavaScript

```javascript
// Requiere: GSAP + ScrollTrigger + Rive

document.addEventListener("DOMContentLoaded", () => {
  gsap.registerPlugin(ScrollTrigger);

  let featureInput;

  const animation = new rive.Rive({
    src: "features.riv",
    canvas: document.querySelector(".feature-rive canvas"),
    stateMachines: "FeatureMachine",
    autoplay: true,
    onLoad: () => {
      animation.resizeDrawingSurfaceToCanvas();
      const inputs = animation.stateMachineInputs("FeatureMachine");
      featureInput = inputs.find(i => i.name === "step");
    }
  });

  // Crear un ScrollTrigger por cada paso
  document.querySelectorAll(".step").forEach((stepEl) => {
    ScrollTrigger.create({
      trigger: stepEl,
      start: "top center",
      end: "bottom center",
      onEnter: () => {
        const stepValue = parseInt(stepEl.dataset.step);
        if (featureInput) featureInput.value = stepValue;
      },
      onEnterBack: () => {
        const stepValue = parseInt(stepEl.dataset.step);
        if (featureInput) featureInput.value = stepValue;
      }
    });
  });
});
```

---

## 🔍 ¿Cómo funciona?

- Cada `.step` representa una sección del contenido.
- Cuando esa sección entra en el viewport, ScrollTrigger lanza un evento.
- El valor de `featureInput` (Number Input en Rive) cambia según el `data-step` del elemento.
- En Rive, cada número puede representar una animación o highlight diferente.

---

## 🧪 Casos de uso comunes

- 🎓 Explicar una funcionalidad paso a paso.
- 🧬 Mostrar un proceso dividido en fases.
- 💡 Desplegar beneficios o características en scroll.
- 🛠️ Guiar al usuario a través de diferentes componentes de un producto.

---

## 🧰 Sugerencias y mejoras

- Agrega animaciones suaves entre pasos con GSAP para el contenido textual.
- Usa `opacity` o `clip-path` para revelar elementos gradualmente.
- Puedes usar triggers en lugar de números si cada sección es muy distinta visualmente.
- Asegúrate de que la animación sea clara y no demasiado distractora.

---

## ✅ Conclusión

Con esta técnica, puedes transformar el scroll del usuario en una guía visual que le ayuda a entender tu contenido paso a paso. Es perfecta para explicar funcionalidades, productos o conceptos complejos de forma interactiva y atractiva.

