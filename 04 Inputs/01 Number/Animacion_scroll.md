# Uso de Inputs Numéricos para ejecutar animacions de RIVE con Scroll

## Introducción

Rive es una herramienta poderosa para crear animaciones interactivas basadas en una **State Machine**, lo que permite manejar distintos estados de una animación de manera programática. En esta sección, vamos a aprender cómo utilizar **inputs numéricos** en Rive para modificar dinámicamente el estado de una animación mediante eventos de desplazamiento (**scroll**) en una página web.

En este caso, trabajaremos con un input numérico llamado `Number`, que se actualizará en función del movimiento del scroll del usuario. Este enfoque se puede aplicar en múltiples situaciones, como controlar la velocidad de una animación, cambiar su posición o modificar atributos visuales en tiempo real.

## Inicialización del Input Numérico en Rive

El siguiente fragmento de código inicializa la animación en Rive y configura la interacción con un input numérico dentro de una **State Machine**.

```javascript
let scrollValue;

const animation = new rive.Rive({
    src: "https://cristalplant.relevancia.net/prueba.riv", // Archivo con la animación
    canvas: document.getElementById("scroll-animation"),
    autoplay: true,
    isTouchScrollEnabled: true,
    stateMachines: "State Machine 1",
    onLoad: () => {
        animation.resizeDrawingSurfaceToCanvas();
        console.log("Animación cargada correctamente");

        // Obtener inputs de la State Machine
        const inputs = animation.stateMachineInputs("State Machine 1");
        scrollValue = inputs.find(i => i.name == "Number");

        if (!scrollValue) {
            console.error("No se encontró el input 'Number'. Verifica el archivo .riv");
        }
    }
});
```

### Explicación del código
- **`rive.Rive({})`**: Crea una nueva instancia de la animación en Rive.
- **`src`**: Especifica la URL del archivo `.riv` con la animación.
- **`canvas`**: Hace referencia al elemento `<canvas>` en el que se renderiza la animación.
- **`autoplay`**: Activa la animación de forma automática al cargar la página.
- **`stateMachines`**: Define el nombre de la máquina de estados utilizada en la animación.
- **`onLoad`**: Función que se ejecuta cuando la animación se ha cargado correctamente. Aquí obtenemos los inputs de la **State Machine**.
- **`animation.stateMachineInputs("State Machine 1")`**: Devuelve un arreglo con los inputs de la máquina de estados.
- **`inputs.find(i => i.name == "Number")`**: Busca el input numérico llamado `Number`.
- **Si el input no se encuentra**, se muestra un mensaje de error en la consola.

## Modificación del Input Numérico con Scroll

Ahora agregamos un evento de **scroll** para modificar el valor del input `Number` y actualizar la animación en consecuencia.

```javascript
window.addEventListener("wheel", (event) => {
    if (!scrollValue) return;
    let newValue = scrollValue.value + (event.deltaY > 0 ? 5 : -5);
    scrollValue.value = Math.max(0, Math.min(100, newValue));
    animation.drawFrame();
    console.log("Nuevo valor de 'Number':", scrollValue.value);
});
```

### Explicación del código
- **`window.addEventListener("wheel", callback)`**: Escucha eventos de desplazamiento vertical del ratón.
- **`event.deltaY > 0`**: Indica un desplazamiento hacia abajo, aumentando el valor del input.
- **`event.deltaY < 0`**: Indica un desplazamiento hacia arriba, disminuyendo el valor del input.
- **`Math.max(0, Math.min(100, newValue))`**: Asegura que el valor del input se mantenga entre 0 y 100.
- **`animation.drawFrame()`**: Redibuja la animación en el lienzo con el nuevo valor.

## Código Completo

```html
<body>
    <!-- Canvas de 500px x 500px donde se renderiza la animación -->
    <canvas id="scroll-animation" width="500" height="500"></canvas>

    <script src="https://unpkg.com/@rive-app/canvas@latest"></script>
    <script>
        // Variable para almacenar el número de estado del input
        let scrollValue;
        
        // Inicialización de la animación con Rive
        const animation = new rive.Rive({
            src: "https://cristalplant.relevancia.net/prueba.riv", // Archivo Rive con la animación
            canvas: document.getElementById("scroll-animation"), // Canvas donde se renderiza la animación
            autoplay: true, // Activar reproducción automática para probar
            isTouchScrollEnabled: true, // Hacer que el Scroll de la web siga funcionando en versión Movil
            stateMachines: "State Machine 1", // Nombre de la State Machine
            onLoad: () => {
                animation.resizeDrawingSurfaceToCanvas(); // Ajusta el tamaño del canvas al contenedor
                
                // Verificar que la animación se está ejecutando
                console.log("Animación cargada correctamente");

                // Obtiene los inputs de la State Machine
                const inputs = animation.stateMachineInputs("State Machine 1");
                
                // Encuentra el input numérico llamado "Number" y lo almacena
                scrollValue = inputs.find(i => i.name == "Number");

                if (!scrollValue) {
                    console.error("No se encontró el input 'Number'. Verifica el archivo .riv");
                
                }
            }
        });

        // Manejo del evento de scroll para actualizar la animación
        window.addEventListener("wheel", (event) => {
            if (!scrollValue) return;

            // Ajusta el valor basado en la dirección del scroll
            let newValue = scrollValue.value + (event.deltaY > 0 ? 5 : -5);
            
            // Restringe el valor entre 0 y 100
            scrollValue.value = Math.max(0, Math.min(100, newValue));

            // Redibujar la animación con el nuevo valor
            animation.drawFrame();
            console.log("Nuevo valor de 'Number':", scrollValue.value);
        });
    </script>
</body>
</html>
```

## Conclusión

Este ejemplo muestra cómo **controlar una animación en Rive utilizando un input numérico modificado con eventos de scroll**. Este método puede aplicarse a muchas otras interacciones en interfaces web, como cambios de color, velocidad o desplazamiento de elementos animados.

