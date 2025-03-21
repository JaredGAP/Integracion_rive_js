# 🔠 Uso de Font Assets en Rive

Rive permite integrar fuentes personalizadas dentro de tus animaciones y lo mejor es que puedes **reemplazarlas en tiempo real desde JavaScript**, sin necesidad de reexportar el archivo `.riv`. Esto ofrece un alto grado de flexibilidad y personalización en cualquier animación que utilice texto.

---

## ⚙️ Ejemplo práctico con cambio de fuente

```html
<canvas width="500" height="500"></canvas>
<button onclick="changeFont('Boska')">Cambiar a Boska</button>
<button onclick="changeFont('Orbitron')">Cambiar a Orbitron</button>

<script>
  let fontAsset;

  const animation = new rive.Rive({
    src: "shimmer.riv",
    canvas: document.querySelector("canvas"),
    autoplay: true,
    onLoad: () => animation.resizeDrawingSurfaceToCanvas(),

    assetLoader: (asset, bytes) => {
      if (asset.isFont) {
        fontAsset = asset;
        changeFont("Boska");
        return true; // Ya manejamos la carga
      }
      return false;
    }
  });

  async function changeFont(fontName) {
    console.log("Cargando fuente:", fontName);

    try {
      const response = await fetch(`fonts/${fontName}.ttf`);
      const fontBytes = new Uint8Array(await response.arrayBuffer());
      const font = await rive.decodeFont(fontBytes);

      fontAsset.setFont(font);
      font.unref(); // Liberar memoria anterior

      console.log("✅ Fuente cambiada a:", fontName);
    } catch (error) {
      console.error("❌ Error al cargar la fuente:", error);
    }
  }
</script>
```

---

## 🔍 Explicación del código

| Elemento                   | Función                                                               |
|----------------------------|-----------------------------------------------------------------------|
| `asset.isFont`             | Detecta si el asset es una fuente.                                   |
| `decodeFont(bytes)`        | Convierte una fuente `.ttf` en un formato legible por Rive.          |
| `setFont(font)`            | Reemplaza la fuente actual con una nueva.                            |
| `unref()`                  | Libera recursos asociados a la fuente anterior.                      |

---

## 🧠 ¿Cuándo usar Font Assets?

### ✏️ Personalización tipográfica
- Permitir al usuario elegir entre varios estilos tipográficos.
- Cambiar fuentes según idioma o región (soporte para caracteres especiales).

### 💼 Branding dinámico
- Mostrar diferentes fuentes según la marca o cliente seleccionado.
- Personalizar presentaciones animadas con la identidad visual del usuario.

### 🧰 Herramientas creativas
- Generadores de tarjetas, banners o contenido animado con tipografía intercambiable.
- Aplicaciones de diseño interactivo con vistas previas animadas.

### 🤖 Integraciones inteligentes
- Cargar fuentes según configuración de usuario, perfil o contexto (día/noche).

---

## 🧰 Buenas prácticas

- ✔️ Usa fuentes `.ttf` optimizadas y con licencia adecuada.
- ✔️ Asegúrate de que el asset exista antes de aplicar `setFont()`.
- ✔️ Carga fuentes desde rutas seguras y maneja errores de red.
- ❌ No reapliques fuentes ya cargadas innecesariamente.

---

## ✅ Conclusión

Los **Font Assets** de Rive te permiten añadir un nivel extra de personalización a tus animaciones con texto. Puedes adaptar la experiencia visual según el contexto, el usuario o la marca, todo sin tocar el archivo original de animación.

Ideal para interfaces personalizables, branding flexible y experiencias donde el texto también es protagonista. ✨