# 🖼️ Uso de Image Assets en Rive

Rive permite integrar imágenes dinámicas dentro de tus animaciones mediante el sistema de **Image Assets**. Esta funcionalidad te permite reemplazar imágenes en tiempo real desde código, algo muy útil para crear experiencias visuales personalizadas, animaciones adaptables o contenido generado dinámicamente.

---

## ⚙️ Ejemplo básico de configuración

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
      return false; // Indicamos que lo gestionaremos manualmente
    }
  });

  async function changeImage() {
    console.log("Cargando imagen...");

    const response = await fetch("https://picsum.photos/800");
    const buffer = await response.arrayBuffer();
    const img = await rive.decodeImage(new Uint8Array(buffer));

    imgAsset.setRenderImage(img);
    console.log("Imagen cambiada!");

    img.unref(); // Libera memoria de la imagen previa
  }
</script>
```

---

## 📖 Explicación técnica

| Función | Descripción |
|--------|-------------|
| `assetLoader(asset, bytes)` | Se ejecuta cuando Rive detecta un asset embebido en el archivo `.riv`. |
| `asset.isImage` | Permite identificar si el asset es una imagen. |
| `setRenderImage(img)` | Reemplaza la imagen en la animación con una nueva. |
| `decodeImage(bytes)` | Convierte un archivo de imagen (en bytes) en un formato válido para Rive. |
| `unref()` | Libera memoria cuando una imagen ya no se necesita. |

---

## 🧠 Casos de uso avanzados

### 🎨 Personalización de interfaces
- Permitir al usuario cargar su propia foto de perfil y verla animada en tiempo real.
- Cambiar el fondo o texturas de una animación según el tema del sitio.

### 📦 Visualización de productos
- Mostrar un mockup que cambia según la imagen de producto seleccionada.
- Probar distintas combinaciones de materiales o colores en una animación.

### 📸 Herramientas de diseño
- Arrastrar una imagen y verla integrada en una animación tipo collage o mockup animado.
- Crear un sistema de vista previa animada para presentaciones, flyers, etc.

### 🧩 Integraciones dinámicas
- Actualizar contenido visual desde una API externa.
- Vincular imágenes de perfiles sociales a avatares animados.

### 📱 Apps móviles o kioscos
- Permitir al usuario hacerse una foto y verla animada en una postal digital o tarjeta.
- Mostrar animaciones personalizadas por usuario según sus elecciones.

---

## 🧰 Buenas prácticas y consideraciones

- ✅ Verifica que `imgAsset` esté definido antes de aplicar `setRenderImage()`.
- ✅ Usa imágenes optimizadas para no saturar la memoria o afectar el rendimiento.
- ✅ Maneja errores de carga para evitar fallos si la imagen no está disponible.
- ✅ Considera agregar una animación de carga mientras se descarga y decodifica la imagen.
- ❌ No reutilices el mismo objeto `img` sin llamar a `unref()` para liberar memoria.

---

## ✅ Conclusión

Los **Image Assets** permiten llevar tus animaciones a otro nivel de dinamismo. Ya no estás limitado a lo que exportas desde Rive Studio: puedes modificar el contenido visual en tiempo real, generando experiencias únicas, personalizadas y contextualmente relevantes.

Ideal para apps interactivas, experiencias personalizadas y animaciones que se adaptan a cada usuario o situación.

