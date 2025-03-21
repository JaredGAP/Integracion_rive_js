# 🌀 Hero Scroll Animation con Rive y ScrollTrigger

Esta animación implementa un efecto dinámico en el *hero* de la landing de **Paybyte**, donde una animación de Rive reacciona al desplazamiento del usuario utilizando **GSAP ScrollTrigger**. A medida que se hace scroll, la animación se actualiza en tiempo real.

---

## 🧠 ¿Qué es todo esto?

Para entender cómo funciona esta integración, primero aclaremos los conceptos principales:

### 🔹 ¿Qué es Rive?
Rive es una herramienta que permite crear animaciones interactivas y exportarlas como archivos `.riv`. Estas animaciones pueden ser manipuladas desde código, reaccionando a entradas como clics, valores numéricos, triggers y más.

### 🔹 ¿Qué es GSAP?
**GSAP** (GreenSock Animation Platform) es una librería de animaciones en JavaScript que permite animar cualquier elemento del DOM con un control preciso y fluido.

### 🔹 ¿Qué es ScrollTrigger?
Es un plugin de GSAP que permite vincular animaciones al scroll del usuario. Puedes decirle a GSAP: "Cuando el usuario haga scroll hasta cierto punto, anima este elemento".

### 🔹 ¿Qué estamos haciendo aquí?
Estamos combinando Rive (para la animación gráfica) y ScrollTrigger (para detectar el scroll) para que, al hacer scroll en la web, una animación creada en Rive avance en sincronía con el desplazamiento.

---

## 🎯 Objetivo

Controlar un **Number Input** de una *State Machine* en Rive (llamado `rotate`) para que varíe proporcionalmente al avance del scroll sobre el contenedor `.hero-rive-container`.

---

## 🧱 Estructura HTML clave

```html
<section class="hero">
  <div class="hero-rive-container">
    <canvas width="1080" height="640"></canvas>
  </div>
  <div class="content">
    <h1>Payments Done Right!</h1>
    <p>Texto de ejemplo...</p>
    <a class="btn">Link Wallet</a>
  </div>
</section>
```

Este bloque define la sección *hero* que incluye el canvas de Rive y contenido textual.

---

## ⚙️ Lógica de integración en `app.js`

```javascript
document.addEventListener("DOMContentLoaded", () => {
  gsap.registerPlugin(ScrollTrigger);

  const heroAnimation = new rive.Rive({
    src: "app.riv",
    canvas: document.querySelector(".hero-rive-container > canvas"),
    artboard: "hero",
    stateMachines: "state-machine",
    autoplay: true,
    onLoad: () => {
      heroAnimation.resizeDrawingSurfaceToCanvas();

      const inputs = heroAnimation.stateMachineInputs("state-machine");
      const rotateInput = inputs.find(i => i.name === "rotate");

      ScrollTrigger.create({
        trigger: ".hero-rive-container",
        start: "top top",
        onUpdate: (self) => {
          rotateInput.value = self.progress * 100;
        }
      });
    }
  });
});
```

---

## 🔍 ¿Cómo funciona?

| Parte | Descripción |
|-------|-------------|
| `stateMachineInputs("state-machine")` | Accede a los inputs definidos en la State Machine del artboard `hero`. |
| `rotateInput.value = self.progress * 100` | Se asigna un valor entre 0 y 100 en función del progreso del scroll dentro del trigger. |
| `ScrollTrigger.create({...})` | Establece una zona de observación para detectar desplazamiento y vincularlo a la animación. |

---

## 🎨 Resultado visual

- Al llegar al *hero*, la animación comienza.
- A medida que el usuario hace scroll, la propiedad `rotate` se modifica, creando un efecto reactivo fluido.
- El input puede estar vinculado a una rotación, deformación, opacidad o cualquier parámetro en Rive que reaccione a ese valor numérico.

---

## 🧪 Ideas de mejora y casos de uso

- ✅ Agregar `scrub: true` para controlar más suavemente la progresión.
- 🔁 Enlazar otros inputs de Rive (por ejemplo, `opacity`, `scale`, etc.) al scroll.
- 🔀 Combinar con `GSAP timelines` para coordinar otros elementos visuales junto con el canvas.
- 🎬 Iniciar una segunda animación al llegar al final del hero (por ejemplo, transición de color).

---

## ✅ Conclusión

Con esta técnica, se puede **sincronizar perfectamente una animación de Rive con el desplazamiento** del usuario, generando una experiencia más inmersiva y fluida. 

Ideal para *hero sections*, presentaciones visuales de producto o storytelling interactivo.

