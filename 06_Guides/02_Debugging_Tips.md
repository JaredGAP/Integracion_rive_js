# 🐞 Solución de Errores Comunes con Rive + JS

Trabajar con Rive y JavaScript abre muchas posibilidades, pero también puede traer errores sutiles que frustran a quienes están aprendiendo. Aquí tienes una lista de problemas frecuentes y cómo resolverlos de forma rápida y clara.

---

## 📱 1. El scroll deja de funcionar en móviles

**Síntoma:** En algunos móviles (sobre todo iOS), al integrar `GSAP + Rive` el scroll deja de responder o se congela.

**Solución:** Añade la opción `isTouchScrollEnabled: true` al crear la instancia de Rive.

```javascript
const animation = new rive.Rive({
  src: "file.riv",
  canvas: document.querySelector("canvas"),
  stateMachines: "scroll-machine",
  autoplay: true,
  isTouchScrollEnabled: true,
  onLoad: () => animation.resizeDrawingSurfaceToCanvas()
});
```

---

## 🕳️ 2. Inputs no se encuentran (`undefined` o `null`)

**Síntoma:** Al intentar acceder a un input con `.find(...)`, devuelve `undefined`.

**Causas posibles:**
- El nombre no coincide con el definido en Rive Studio (mayúsculas, espacios, etc).
- No esperaste a que cargara la animación (no usaste `onLoad`).

**Solución:**

```javascript
onLoad: () => {
  const inputs = animation.stateMachineInputs("machine");
  const input = inputs.find(i => i.name === "scrollValue");
  if (!input) console.warn("⚠️ Input no encontrado");
}
```

---

## 🔄 3. La animación no reacciona al scroll

**Síntoma:** La animación se muestra, pero no cambia con el scroll.

**Causas comunes:**
- El valor del scroll (`scrollY`) no se está calculando bien.
- El canvas no se ha ajustado con `resizeDrawingSurfaceToCanvas()`.
- El `input.value` no se está actualizando (por nombre incorrecto o no cargado).

**Solución mínima:**

```javascript
window.addEventListener("scroll", () => {
  const ratio = window.scrollY / (document.body.scrollHeight - window.innerHeight);
  const value = Math.min(Math.round(ratio * 10), 10);
  if (scrollInput) scrollInput.value = value;
});
```

---

## 🔁 4. Trigger no se vuelve a activar

**Síntoma:** Disparas una animación una vez, pero al hacer clic de nuevo no pasa nada.

**Motivo:** Un `Trigger Input` solo se dispara una vez por activación. Si tu lógica no “resetea” la animación, no volverá a ejecutarse.

**Solución:** Reestructura tu máquina de estados para que vuelva al estado inicial tras completarse. O usa otro trigger complementario para reiniciar.

---

## 🧩 5. Carga fallida del archivo `.riv`

**Síntoma:** No se ve nada en pantalla. No hay errores visibles.

**Causas posibles:**
- Ruta incorrecta (`src` mal escrito).
- No estás sirviendo los archivos desde un servidor local (necesario por WebAssembly).
- El archivo `.riv` está dañado o mal exportado.

**Solución rápida:** Usa VS Code + Live Server o un servidor local:
```bash
npx serve .
```

---

## 🔍 6. Eventos personalizados no se disparan

**Síntoma:** Usas `RiveEvent`, pero no ocurre nada en el navegador.

**Revisa:**
- Que estés escuchando `rive.EventType.RiveEvent`.
- Que hayas definido un evento correctamente en la transición dentro de Rive Studio.
- Que `automaticallyHandleEvents` no esté interfiriendo si lo tienes activado.

```javascript
animation.on(rive.EventType.RiveEvent, (event) => {
  console.log("Evento recibido:", event.data);
});
```

---

## ✅ Recomendaciones generales

- Usa `console.log()` para verificar si `onLoad` se ejecuta.
- Verifica que el archivo `.riv` esté actualizado (exporta de nuevo si hay dudas).
- Siempre revisa los nombres exactos de inputs, artboards y state machines.
- Si todo falla, crea un `.riv` mínimo solo con un cuadrado que cambia de color al hacer clic. Eso te ayudará a aislar el problema.

---

## 🏁 Conclusión

Estos errores son comunes en cualquier proyecto con Rive, especialmente cuando se combinan múltiples eventos, inputs o animaciones. Tener este archivo como referencia te permitirá **diagnosticar rápido y seguir creando sin frustraciones**.

¡Falla rápido, aprende más rápido! 🔧🧪

