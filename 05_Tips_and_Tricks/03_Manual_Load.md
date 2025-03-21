# 📦 Manual Load: Cargar archivos `.riv` manualmente en tiempo de ejecución

Por lo general, para mostrar una animación en Rive usamos la propiedad `src` para indicar el archivo `.riv`. Sin embargo, también es posible **cargar un archivo `.riv` manualmente desde JavaScript**, lo que puede ser útil si necesitas:

- Cargar animaciones desde una API o backend.
- Usar lógica personalizada de carga (por ejemplo, con autorización).
- Manipular el buffer del archivo antes de pasarlo al runtime.

---

## 🧠 ¿Cuándo usar carga manual?

- Si quieres mantener tus animaciones protegidas detrás de autenticación.
- Si deseas cargar archivos `.riv` desde URLs externas o CDN de terceros.
- Si necesitas cargar `.riv` en tiempo de ejecución tras alguna acción específica.

---

## ⚙️ Código JavaScript para carga manual

```html
<script>
  // Definimos una función asincrónica para cargar la animación
  async function loadRive() {
    // 1. Hacemos la solicitud al archivo .riv
    const response = await fetch("https://path.to/file.riv");
    const buffer = await response.arrayBuffer();

    // 2. Creamos la instancia de Rive con el buffer cargado
    new rive.Rive({
      buffer: buffer,
      canvas: document.querySelector("canvas"),
      autoplay: true,
      stateMachines: "state-machine",
      onLoad: () => {
        console.log("Animación cargada desde buffer correctamente");
      },
    });
  }

  // No olvides llamar la función
  loadRive();
</script>
```

---

## 📄 HTML mínimo necesario

```html
<canvas width="500" height="500"></canvas>
```

---

## 🔍 ¿Qué es `buffer`?

El `buffer` es una representación en memoria del archivo `.riv`. Al usar `fetch()` seguido de `.arrayBuffer()`, obtenemos esa representación y la pasamos directamente al constructor de Rive en lugar de usar una URL en `src`.

---

## 🔧 Alternativas y mejoras

- Puedes usar esta técnica junto con loaders personalizados para múltiples animaciones.
- Úsalo para pre-cargar animaciones antes de mostrarlas.
- También es posible usarla con almacenamiento local (`localStorage`, IndexedDB, etc.).

---

## ✅ Conclusión

Cargar archivos `.riv` manualmente es una forma avanzada de controlar cómo y cuándo se usan tus animaciones. Aunque en la mayoría de casos no es necesario, te da mayor flexibilidad cuando trabajas con datos protegidos, lógica condicional o cargas dinámicas.

