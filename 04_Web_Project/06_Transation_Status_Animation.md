# 💸 Animación de Estado de Transacción con Rive

En este ejemplo vamos a simular una animación de **envío de dinero** usando Rive. Se utilizará una combinación de:

- `Trigger Input` para activar la animación.
- `Number Input` para reflejar el resultado (`0 = fail`, `1 = success`).

Esta animación puede usarse para representar procesos como pagos, confirmaciones, envíos o notificaciones.

---

## 🧱 Estructura del HTML

```html
<canvas class="transaction" width="500" height="500"></canvas>
<p class="result"></p>
<div class="controls">
  <button onclick="send(true)">Simular éxito</button>
  <button onclick="send(false)">Simular error</button>
</div>
```

---

## 🎬 Script en `app.js`

```javascript
let triggerInput, resultInput;

const animation = new rive.Rive({
  src: "transaction.riv",
  canvas: document.querySelector(".transaction"),
  stateMachines: "TransactionMachine",
  autoplay: true,
  onLoad: () => {
    animation.resizeDrawingSurfaceToCanvas();
    const inputs = animation.stateMachineInputs("TransactionMachine");
    triggerInput = inputs.find(i => i.name === "send");
    resultInput = inputs.find(i => i.name === "result");
  }
});

function send(isSuccess) {
  if (!triggerInput || !resultInput) return;

  resultInput.value = isSuccess ? 1 : 0;
  triggerInput.fire();

  const resultText = document.querySelector(".result");
  resultText.innerText = isSuccess ? "✅ Transacción exitosa" : "❌ Transacción fallida";
}
```

---

## 🔍 Explicación del flujo

| Elemento                | Función                                                                  |
|-------------------------|---------------------------------------------------------------------------|
| `resultInput.value = n` | Define si el estado es exitoso (1) o fallido (0).                         |
| `triggerInput.fire()`   | Lanza la animación que responde al resultado definido.                   |
| `.result.innerText`     | Actualiza el texto visible según el resultado simulado.                  |

---

## 🎯 ¿Cuándo usar este patrón?

- Confirmaciones de acciones (envíos, compras, formularios).
- Feedback visual inmediato tras una acción.
- Interacción simple pero expresiva con el usuario.

---

## ✅ Buenas prácticas

- ✔️ Nombra bien tus inputs (`send`, `result`) y asegúrate de que coincidan con los definidos en Rive.
- ✔️ Muestra un resultado textual o visual que acompañe la animación.
- ❌ No uses triggers sin establecer antes el valor del resultado.
- ✔️ Usa `resizeDrawingSurfaceToCanvas()` para que el canvas se ajuste correctamente.

---

## 🏁 Conclusión

Esta integración demuestra cómo **Rive puede usarse para representar procesos lógicos** dentro de una app, añadiendo feedback visual atractivo a interacciones cotidianas. Combinar triggers y valores numéricos es una forma simple pero potente de **darle vida a la interfaz**. 🔁✅

