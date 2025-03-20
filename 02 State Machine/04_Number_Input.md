# Uso de Number Inputs en Rive

Los *Number Inputs* en Rive permiten modificar estados de una *State Machine* utilizando valores numéricos. Esto es útil para representar múltiples estados dentro de una animación y cambiar entre ellos de manera dinámica.

## Configuración de un Number Input en Rive

El siguiente código muestra cómo configurar y manipular un *Number Input* dentro de una animación:

```html
<script>
    let iconState;
    
    const animation = new rive.Rive({
        src: "icon.riv",
        canvas: document.querySelector(".icon canvas"),
        autoplay: true,
        artboard: "menu",
        stateMachines: "state-machine",
        onLoad: () => {
            animation.resizeDrawingSurfaceToCanvas();

            // Obtener todos los inputs de la máquina de estados
            const inputs = animation.stateMachineInputs("state-machine");
            // Buscar el input numérico llamado "iconState"
            iconState = inputs.find(i => i.name == "iconState");
        }
    });

    const title = document.querySelector(".title");
    const pages = document.querySelectorAll(".content > *");

    function iconTap() {
        switch (title.textContent) {
            case "Details":
            case "Menu":
                goTo("home");
                break;
            
            case "Home":
                goTo("menu");
                break;
        }
    }

    function goTo(route) {
        switch (route) {
            case "menu":
                // Establecer valor del input numérico
                iconState.value = 3;
                title.innerText = "Menu";
                break;
                
            case "home":
                iconState.value = 0;
                title.innerText = "Home";
                break;
                
            case "details":
                iconState.value = 1;
                title.innerText = "Details";
                break;
        }

        pages.forEach(page => {
            if (page.classList.contains(route)) {
                page.classList.remove("hidden");
            } else {
                page.classList.add("hidden");
            }
        });
    }
</script>
```

## Explicación del Código

### `stateMachineInputs("state-machine")`
Obtiene un array con todos los inputs de la *State Machine* llamada `state-machine`.

### `find(i => i.name == "iconState")`
Busca dentro del array el input numérico con el nombre `iconState`.

### `iconState.value = X`
Establece el valor del *Number Input*, lo que permite cambiar el estado de la animación:
- `iconState.value = 0;` → Estado *Home*.
- `iconState.value = 1;` → Estado *Details*.
- `iconState.value = 3;` → Estado *Menu*.

### Interacción con el Usuario
El usuario puede cambiar de estado haciendo clic en el icono, lo que alterna entre las vistas *Home*, *Menu* y *Details* dependiendo del valor de `iconState`.

## Conclusión
Los *Number Inputs* en Rive permiten manejar múltiples estados dentro de una animación, brindando una mayor flexibilidad al controlar transiciones dinámicas en la interfaz de usuario.


