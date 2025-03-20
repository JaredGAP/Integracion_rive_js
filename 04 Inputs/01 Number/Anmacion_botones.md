# Uso de Inputs Numéricos en RIVE con Botones de Incremento y Decremento

## Introducción

En este ejemplo, aprenderemos a controlar una animación en **Rive** utilizando un **input numérico modificado con botones de incremento y decremento**. Este enfoque permite a los usuarios ajustar valores de forma precisa y controlada sin depender de sliders o el scroll.

Esta técnica es útil para cambiar estados, ajustar parámetros de animaciones o modificar efectos visuales en una aplicación interactiva.

## Inicialización del Input Numérico en Rive

Primero, cargamos la animación y obtenemos el input numérico dentro de la **State Machine**:

```javascript
let numberInput;

const animation = new rive.Rive({
    src: "https://cristalplant.relevancia.net/prueba.riv", // Archivo con la animación
    canvas: document.getElementById("button-animation"),
    autoplay: true,
    stateMachines: "State Machine 1",
    onLoad: () => {
        animation.resizeDrawingSurfaceToCanvas();
        console.log("Animación cargada correctamente");

        // Obtener inputs de la State Machine
        const inputs = animation.stateMachineInputs("State Machine 1");
        numberInput = inputs.find(i => i.name == "Number");

        if (!numberInput) {
            console.error("No se encontró el input 'Number'. Verifica el archivo .riv");
        }
    }
});
```

### Explicación del código
- **`rive.Rive({})`**: Crea una nueva instancia de la animación.
- **`src`**: Define la URL del archivo `.riv`.
- **`canvas`**: Define dónde se renderiza la animación.
- **`autoplay`**: Activa la animación automáticamente.
- **`stateMachines`**: Especifica el nombre de la **State Machine** que maneja la animación.
- **`animation.stateMachineInputs("State Machine 1")`**: Obtiene los inputs de la animación.
- **`inputs.find(i => i.name == "Number")`**: Busca el input numérico `Number`.

## Modificación del Input Numérico con Botones

Ahora añadimos la funcionalidad para que los botones **incrementen o decrementen** el valor del input numérico:

```javascript
document.getElementById("increase-btn").addEventListener("click", () => {
    if (!numberInput) return;
    
    numberInput.value = Math.min(100, numberInput.value + 5);
    animation.drawFrame();
    console.log("Nuevo valor de 'Number':", numberInput.value);
});


document.getElementById("decrease-btn").addEventListener("click", () => {
    if (!numberInput) return;
    
    numberInput.value = Math.max(0, numberInput.value - 5);
    animation.drawFrame();
    console.log("Nuevo valor de 'Number':", numberInput.value);
});
```

### Explicación del código
- **`document.getElementById("increase-btn")`**: Obtiene el botón de incremento.
- **`addEventListener("click", callback)`**: Escucha el evento de clic.
- **`numberInput.value = Math.min(100, numberInput.value + 5)`**: Aumenta el valor hasta un máximo de 100.
- **`numberInput.value = Math.max(0, numberInput.value - 5)`**: Disminuye el valor hasta un mínimo de 0.
- **`animation.drawFrame()`**: Redibuja la animación con el nuevo valor.

## Código Completo

```html
<body>
    <!-- Canvas donde se renderiza la animación -->
    <canvas id="button-animation" width="500" height="500"></canvas>
    
    <!-- Botones para modificar el input numérico -->
    <button id="decrease-btn">-</button>
    <button id="increase-btn">+</button>

    <script src="https://unpkg.com/@rive-app/canvas@latest"></script>
    <script>
        let numberInput;
        
        const animation = new rive.Rive({
            src: "https://cristalplant.relevancia.net/prueba.riv",
            canvas: document.getElementById("button-animation"),
            autoplay: true,
            stateMachines: "State Machine 1",
            onLoad: () => {
                animation.resizeDrawingSurfaceToCanvas();
                console.log("Animación cargada correctamente");

                const inputs = animation.stateMachineInputs("State Machine 1");
                numberInput = inputs.find(i => i.name == "Number");

                if (!numberInput) {
                    console.error("No se encontró el input 'Number'. Verifica el archivo .riv");
                }
            }
        });

        document.getElementById("increase-btn").addEventListener("click", () => {
            if (!numberInput) return;
            numberInput.value = Math.min(100, numberInput.value + 5);
            animation.drawFrame();
            console.log("Nuevo valor de 'Number':", numberInput.value);
        });

        document.getElementById("decrease-btn").addEventListener("click", () => {
            if (!numberInput) return;
            numberInput.value = Math.max(0, numberInput.value - 5);
            animation.drawFrame();
            console.log("Nuevo valor de 'Number':", numberInput.value);
        });
    </script>
</body>
```

## Conclusión

Este ejemplo muestra cómo **controlar una animación en Rive utilizando botones para incrementar o disminuir el valor de un input numérico**.

Este método es ideal para ajustes precisos y puede aplicarse a múltiples escenarios, como **cambiar el tamaño de un objeto, ajustar la velocidad o modificar parámetros de animación**. 🚀

