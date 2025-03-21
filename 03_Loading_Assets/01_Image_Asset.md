# 🖼️ Uso de Image Assets en Rive

Rive permite integrar imágenes dentro de tus animaciones mediante el sistema de **Image Assets**. Lo más interesante es que puedes **cambiar esas imágenes dinámicamente desde JavaScript**, permitiendo experiencias personalizadas, contenido en tiempo real y animaciones contextuales.

---

## ⚙️ Ejemplo práctico en JavaScript

```html
<canvas width="500" height="500"></canvas>
<button onclick="changeImage()">Cambiar imagen</button>

<script>
  let imgAsset;

  const animation = new rive.Rive({
    src: "mockup.riv",
    canvas: document.querySelector("canvas"),
    autoplay: true,
    onLoad: () => animation.resizeDrawingSurfaceToCanvas(),

    assetLoader: (asset, bytes) => {
      if (asset.isImage) {
        imgAsset = asset;
      }
      return false; // Indicamos que gestionaremos el asset manualmente
    }
  });

  async function changeImage() {
    console.log("Cargando nueva imagen...");

    const response = await fetch("https://picsum.photos/800");
    const buffer = await response.arrayBuffer();
    const img = await rive.decodeImage(new Uint8Array(buffer));

    if (imgAsset) {
      imgAsset.setRenderImage(img);
      console.log("✅ Imagen reemplazada!");
    }

    img.unref(); // Libera memoria usada por la imagen anterior
  }
</script>
```

---

## 🔍 ¿Qué hace este código?

| Elemento                       | Función                                                                 |
|-------------------------------|-------------------------------------------------------------------------|
| `assetLoader(asset, bytes)`   | Detecta cuando Rive intenta cargar un recurso embebido.                |
| `asset.isImage`               | Verifica si el asset es una imagen.                                    |
| `setRenderImage(img)`         | Reemplaza visualmente la imagen en la animación.                       |
| `decodeImage(bytes)`          | Convierte un archivo en bytes a una imagen válida para Rive.          |
| `unref()`                     | Libera recursos de memoria al dejar de usar una imagen.                |

---

## 🧩 Casos de uso interesantes

### 🎨 Personalización visual
- Cargar una foto de perfil en un avatar animado.
- Cambiar fondos, texturas o ilustraciones según preferencias del usuario.

### 🛍️ Visualización de productos
- Mostrar un producto en distintas versiones o colores.
- Aplicar imágenes personalizadas sobre maquetas (mockups).

### 🧰 Herramientas creativas
- Crear una app que combine imágenes arrastradas con animaciones predefinidas.
- Mostrar presentaciones animadas con contenido generado en tiempo real.

### 🌐 Integración dinámica con APIs
- Mostrar contenido visual proveniente de servicios externos.
- Conectar datos de usuario con elementos gráficos en la interfaz.

---

## ✅ Buenas prácticas

- ✔️ Asegúrate de que `imgAsset` esté definido antes de llamar a `setRenderImage()`.
- ✔️ Usa imágenes optimizadas para reducir el tiempo de carga y uso de memoria.
- ✔️ Considera mostrar una animación de carga mientras se descarga la nueva imagen.
- ❌ No reutilices imágenes sin llamar a `unref()` para liberar memoria correctamente.

---

## 🎯 Conclusión

Los **Image Assets** hacen posible que tus animaciones de Rive sean dinámicas y personalizadas. Al permitir reemplazar imágenes en tiempo real desde JavaScript, abres la puerta a experiencias interactivas únicas: desde productos personalizables hasta presentaciones con contenido generado en vivo.

Una herramienta poderosa para crear interfaces modernas, flexibles y centradas en el usuario. 🖼️✨

