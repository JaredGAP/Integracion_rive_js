# Uso de Trigger Inputs en Rive

Los *Trigger Inputs* en Rive permiten activar eventos dentro de una *State Machine*, desencadenando acciones específicas en respuesta a interacciones del usuario o cambios en el estado de la aplicación.

## Configuración de un Trigger Input en Rive

El siguiente código muestra cómo configurar y activar un *Trigger Input* en una animación:

```html
<main class="center">
    <div class="container" onclick="notifyTrigger.fire()">
        <canvas width="500" height="500"></canvas>
    </div>
</main>

<script>
    let notifyTrigger;

    const animation = new rive.Rive({
        src: "icon.riv",
        canvas: document.querySelector("canvas"),
        artboard: "bell",
        autoplay: true,
        stateMachines: "state-machine",
        onLoad: () => {
            animation.resizeDrawingSurfaceToCanvas();
            
            // Obtener todos los inputs de la máquina de estados
            const inputs = animation.stateMachineInputs("state-machine");
            // Buscar el input específico llamado "notify"
            notifyTrigger = inputs.find(i => i.name == "notify");
            
            // Activar el trigger
            notifyTrigger.fire();
        }
    });
</script>
```

## Explicación del Código

### `stateMachineInputs("state-machine")`
Obtiene un array con todos los inputs definidos en la *State Machine* llamada `state-machine`.

### `find(i => i.name == "notify")`
Busca dentro del array el input con el nombre `notify`, que en este caso es un *Trigger*.

### `fire()`
Dispara el *Trigger Input*, activando el estado correspondiente en la animación.

### Interacción con el Usuario
El evento `onclick` en el `<div>` que contiene el `canvas` permite activar la animación manualmente al hacer clic.

## Conclusión
Los *Trigger Inputs* son una herramienta poderosa en Rive para manejar interacciones dentro de las *State Machines*. Permiten que la animación reaccione a eventos en tiempo real, haciendo que la experiencia de usuario sea más dinámica e interactiva.
