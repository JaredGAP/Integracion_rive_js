# 💸 Transaction Status Animation con Rive

Este módulo muestra cómo implementar una animación de estado de transacción usando **Rive**, integrándola a un flujo de envío de dinero. La animación se activa con un trigger y muestra un resultado (éxito o fallo) mediante un input numérico.

---

## 🧠 ¿Qué aprenderás aquí?

- Usar **Trigger Inputs** y **Number Inputs** en una State Machine.
- Escuchar eventos del usuario (botón "Send").
- Simular un proceso de envío y actualizar el resultado con una animación.

---

## 🧱 Estructura HTML relevante

```html
<main>
  <div class="container">
    <div class="topbar">
      <span>←</span>
      <span>Send Money</span>
      <span>•••</span>
    </div>

    <div class="rive-wrapper">
      <canvas></canvas>
    </div>

    <div class="input-wrapper">
      <input type="text" placeholder="$0">
      <h2>In Transit</h2>
    </div>

    <p>sending money to</p>
    <div class="avatar"><p>🐵</p></div>
    <p>Jacob</p>
    <span class="amt"></span>

    <a class="send" onclick="sendMoney()">Send</a>
  </div>
</main>
```

---

## ⚙️ Lógica de la animación con Rive y JS

```javascript
let startTrigger;   // Trigger para iniciar animación
let resultNumber;   // Number Input para definir resultado

const animation = new rive.Rive({
  src: "send.riv",
  canvas: document.querySelector("canvas"),
  autoplay: true,
  stateMachines: "state-machine",
  onLoad: () => {
    animation.resizeDrawingSurfaceToCanvas();

    const inputs = animation.stateMachineInputs("state-machine");
    startTrigger = inputs.find(i => i.name === "load");
    resultNumber = inputs.find(i => i.name === "result");
  }
});

function sendMoney() {
  startTrigger.fire(); // Inicia la animación

  initiateTransaction((isSuccess) => {
    resultNumber.value = isSuccess ? 1 : 0; // 1 = éxito, 0 = fallo
  });
}
```

---

## 📦 Simulación de envío y resultado

```javascript
function initiateTransaction(onFinished) {
  document.querySelector(".input-wrapper").classList.add("show-status");
  document.querySelector(".amt").innerText = document.querySelector("input").value;

  setTimeout(() => {
    const isSuccess = Math.random() < 0.5; // Resultado aleatorio
    onFinished(isSuccess);

    const statusLabel = document.querySelector(".input-wrapper > h2");
    statusLabel.innerText = isSuccess ? "Successful" : "Transaction Failed";
  }, 4000);
}
```

---

## 🔍 ¿Qué hace cada input en Rive?

- `load` (Trigger): Inicia la animación de carga o envío.
- `result` (Number): Define visualmente el estado final:
  - 1: Éxito
  - 0: Fallo

En **Rive Studio**, estos inputs se vinculan a transiciones dentro de una *State Machine*.

---

## 🎨 Resultado visual esperado

1. El usuario introduce una cantidad y pulsa "Send".
2. Se dispara la animación `load`.
3. Tras unos segundos, la animación muestra un resultado (éxito o error).
4. El texto debajo del campo cambia dinámicamente.

---

## ✅ Conclusión

Esta técnica combina inputs de Rive con lógica de frontend para simular flujos reales de una app financiera. Es perfecta para mejorar la experiencia del usuario con retroalimentación visual elegante y dinámica.

