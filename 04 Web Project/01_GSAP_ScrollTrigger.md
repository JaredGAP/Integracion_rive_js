# Uso de GSAP ScrollTrigger

GSAP (*GreenSock Animation Platform*) junto con *ScrollTrigger* permite crear animaciones que reaccionan al desplazamiento de la página. Esto permite efectos dinámicos como cambios de opacidad, transformaciones y disparadores basados en la posición del usuario en el documento.

## Configuración de GSAP y ScrollTrigger

El siguiente código muestra cómo estructurar la página y enlazar las librerías necesarias:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>GSAP ScrollTrigger</title>
    <link rel="stylesheet" href="css/style.css">
</head>
<body>
    <main>
        <section></section>
        <section>
            <div class="label"></div>
            <div class="container"></div>
        </section>
        <section></section>
    </main>

    <!-- Cargar las librerías de GSAP y ScrollTrigger -->
    <script src="https://cdn.jsdelivr.net/npm/gsap@3.12.5/dist/gsap.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/gsap@3.12.5/dist/ScrollTrigger.min.js"></script>
    <script src="app.js"></script>
</body>
</html>
```

### Explicación:
- Se incluyen las librerías `gsap.min.js` y `ScrollTrigger.min.js` para manejar las animaciones con el desplazamiento.
- Se definen tres secciones dentro de `<main>`, donde una de ellas contiene elementos que serán animados.

## Implementación de ScrollTrigger

En `app.js`, podemos definir una animación usando `ScrollTrigger`:

```javascript
// Registrar ScrollTrigger en GSAP
gsap.registerPlugin(ScrollTrigger);

// Animación al hacer scroll
gsap.from(".container", {
    opacity: 0,
    y: 50,
    duration: 1.5,
    scrollTrigger: {
        trigger: ".container", // Elemento que activa la animación
        start: "top 80%", // Inicia cuando el elemento está en el 80% de la ventana
        end: "top 30%", // Termina cuando llega al 30%
        scrub: true // Hace que la animación sea más fluida
    }
});
```

### Explicación:
- `gsap.registerPlugin(ScrollTrigger)`: Habilita ScrollTrigger dentro de GSAP.
- `gsap.from()` anima la `.container` desde `opacity: 0` y `y: 50px` hasta su estado original.
- `trigger`: Especifica el elemento que activa la animación.
- `start`: Indica cuándo debe comenzar la animación (`top 80%` significa cuando el `top` del elemento está en el 80% de la ventana).
- `end`: Define cuándo termina la animación (`top 30%`).
- `scrub: true`: Sincroniza la animación con el desplazamiento para un efecto más suave.

## Conclusión
El uso de *GSAP ScrollTrigger* permite crear efectos avanzados de animación que reaccionan al desplazamiento de la página, mejorando la experiencia del usuario y agregando dinamismo a las interfaces web.