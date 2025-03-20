# Uso de Event Listeners en Rive

Rive permite escuchar eventos generados dentro de una *State Machine* y responder a ellos mediante *Event Listeners*. Esto permite ejecutar funciones personalizadas cuando ocurren ciertos eventos en la animación.

## Configuración de un Event Listener en Rive

El siguiente código muestra cómo configurar un *Event Listener* en Rive para capturar eventos generados en la animación:

```html
<script>
    const animation = new rive.Rive({
        src: "menu.riv",
        canvas: document.querySelector("canvas"),
        stateMachines: "state-machine",
        autoplay: true,
        onLoad: () => {
            animation.resizeDrawingSurfaceToCanvas();
        }
    });

    const label = document.querySelector(".label");

    // Agregar un Event Listener
    animation.on(
        // Escuchar eventos de Rive
        rive.EventType.RiveEvent,
        (event) => {
            console.log({
                event: event,
                name: event.data.name,
                properties: event.data.properties,
            });

            // Actualizar el texto del label con la propiedad recibida
            label.innerText = event.data.properties.label;
        }
    );
</script>
```

## Explicación del Código

### `animation.on(rive.EventType.RiveEvent, callback)`
Escucha eventos de tipo `RiveEvent` y ejecuta la función `callback` cuando un evento ocurre.

### `event.data.name`
Contiene el nombre del evento generado dentro de la *State Machine*.

### `event.data.properties`
Contiene un objeto con las propiedades enviadas desde Rive, permitiendo personalizar la respuesta.

### `label.innerText = event.data.properties.label`
Modifica dinámicamente el contenido del `label`, actualizándolo con el valor recibido desde la animación.

## Uso de Event Listeners en Rive

Los eventos en Rive permiten:
- Ejecutar código en respuesta a cambios en la animación.
- Sincronizar la animación con otros elementos en la página.
- Personalizar la interacción del usuario con la animación.

## Conclusión
Los *Event Listeners* en Rive proporcionan una forma poderosa de hacer que las animaciones sean interactivas y dinámicas, permitiendo la comunicación entre la animación y el resto de la interfaz web.
