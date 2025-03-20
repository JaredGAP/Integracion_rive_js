# Uso de State Machines en Rive

Las *State Machines* en Rive permiten manejar transiciones y estados dentro de una animación, lo que nos da un mayor control sobre el comportamiento de la animación en función de eventos o interacciones.

## Configuración de una State Machine en Rive

Para inicializar una animación con una *State Machine*, usamos la propiedad `stateMachines` al instanciar `rive.Rive`:

```html
<script>
    const animation = new rive.Rive({
        ...,
        stateMachines: "state-machine",
    });
</script>
```

### Explicación:
- **`stateMachines`**: Especifica el nombre de la *State Machine* dentro del archivo `.riv`.
- **Las *State Machines* permiten:**
  - Controlar estados dentro de la animación.
  - Hacer transiciones entre diferentes estados según condiciones.
  - Activar cambios basados en eventos del usuario o variables dentro de la animación.

## Beneficios del Uso de *State Machines*
- **Interactividad**: Se pueden cambiar estados en respuesta a clics, teclas, o eventos del sistema.
- **Fluidez**: Permiten crear animaciones más naturales sin necesidad de gestionar cada cambio manualmente.
- **Modularidad**: Se pueden reutilizar estados y transiciones sin reescribir código.

## Conclusión
El uso de *State Machines* en Rive es una poderosa herramienta para manejar la lógica de animación de manera dinámica. Es especialmente útil en interfaces interactivas donde las animaciones deben responder a eventos del usuario o a cambios en el estado de la aplicación.
