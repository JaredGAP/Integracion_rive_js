# 🔠 Uso de Font Assets en Rive

Rive permite cargar fuentes tipográficas de forma dinámica, lo que habilita un altísimo nivel de personalización en animaciones que contienen texto. Gracias a los **Font Assets**, puedes cambiar el tipo de letra de tu animación en tiempo real desde JavaScript, sin tener que modificar ni reexportar el archivo `.riv`.

---

## ⚙️ Ejemplo básico de configuración

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
        return true;
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
      font.unref();

      console.log("Fuente cambiada con éxito a:", fontName);
    } catch (error) {
      console.error("Error al cargar fuente:", error);
    }
  }
</script>
```

---

## 📖 Explicación técnica

| Función | Descripción |
|--------|-------------|
| `asset.isFont` | Detecta si el asset es una fuente. |
| `decodeFont(bytes)` | Convierte el archivo `.ttf` a un formato válido para Rive. |
| `setFont(font)` | Asigna una nueva fuente al asset dentro de la animación. |
| `unref()` | Libera la memoria de fuentes anteriores. |

---

## 🧠 Casos de uso prácticos

### ✏️ Personalización en vivo
- Permitir al usuario elegir entre múltiples estilos tipográficos.
- Adaptar fuentes según idioma (por ejemplo, fuentes que soporten caracteres especiales).

### 💼 Branding adaptable
- Cambiar la fuente en tiempo real según el cliente o marca seleccionada.
- Personalizar la fuente en presentaciones animadas para adaptarlas a distintos públicos.

### 🧩 Integraciones inteligentes
- Cargar una fuente específica según preferencias del usuario.
- Cambiar la tipografía en función de la hora del día o de eventos contextuales.

### 🖼️ Herramientas visuales
- Crear generadores de banners, tarjetas o contenidos con fuentes intercambiables.
- Permitir a los usuarios visualizar distintos estilos antes de exportar una imagen o vídeo animado.

---

## 🧰 Buenas prácticas

- ✅ Usa archivos `.ttf` bien optimizados y con licencia apropiada.
- ✅ Asegúrate de que el asset exista antes de aplicar `setFont()`.
- ✅ Carga las fuentes desde una ruta segura y confiable.
- ✅ Maneja errores de red para evitar fallos si el archivo no se encuentra.
- ❌ No recargues fuentes innecesariamente si ya están aplicadas.

---

## ✅ Conclusión

Los **Font Assets** amplían enormemente la capacidad expresiva de tus animaciones en Rive. Te permiten integrar lógica de personalización, adaptar el diseño a cada contexto y ofrecer experiencias únicas al usuario con tan solo cambiar una fuente.

Una herramienta clave para interfaces personalizables, branding animado y experiencias donde el texto también se anima.


