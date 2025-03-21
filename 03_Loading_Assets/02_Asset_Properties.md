# 🧩 Propiedades de Asset en Rive

En Rive, un **Asset** es cualquier recurso embebido o referenciado en una animación: imágenes, fuentes, sonidos o datos. Cuando gestionas estos recursos desde JavaScript usando el parámetro `assetLoader`, puedes acceder a varias propiedades que te ayudan a identificar, personalizar o reemplazar dinámicamente ese asset.

---

## 🔍 Propiedades comunes del objeto Asset

Cuando defines una animación con un `assetLoader`, el objeto `asset` ofrece estas propiedades:

| Propiedad            | Tipo        | Descripción                                                             |
|----------------------|-------------|-------------------------------------------------------------------------|
| `id`                 | `number`    | Identificador único del asset.                                         |
| `name`               | `string`    | Nombre del asset definido en Rive Studio.                              |
| `type`               | `string`    | Tipo de recurso (`image`, `font`, etc.).                               |
| `isImage`            | `boolean`   | `true` si el asset es una imagen.                                      |
| `isFont`             | `boolean`   | `true` si el asset es una fuente.                                      |
| `renderImage`        | `object`    | Imagen actual vinculada al asset (si aplica).                          |
| `setRenderImage()`   | `function`  | Permite establecer una nueva imagen para el asset.                     |
| `setFont()`          | `function`  | Permite establecer una nueva fuente para el asset.                     |

---

## ⚙️ Ejemplo práctico

```javascript
const animation = new rive.Rive({
  src: "animacion-con-assets.riv",
  canvas: document.querySelector("canvas"),
  autoplay: true,
  assetLoader: (asset, bytes) => {
    console.log("Asset detectado:", asset.name);

    if (asset.isImage) {
      console.log("Es una imagen:", asset);
      // Aquí puedes cargar una imagen personalizada
    }

    if (asset.isFont) {
      console.log("Es una fuente:", asset);
      // Aquí podrías aplicar una fuente externa
    }

    return false; // Control total desde JS
  }
});
```

---

## 🧠 ¿Para qué sirve conocer estas propiedades?

- Para **reemplazar assets** (como imágenes o fuentes) de forma dinámica sin modificar el `.riv`.
- Para **inspeccionar y depurar** qué assets están embebidos en un archivo.
- Para crear sistemas de **personalización visual**, cargando contenido adaptado a cada usuario o situación.

---

## 🧰 Buenas prácticas

- ✔️ Utiliza nombres únicos y descriptivos en Rive Studio para identificar tus assets fácilmente.
- ✔️ Verifica que el tipo de asset coincida (`isImage`, `isFont`) antes de reemplazarlo.
- ✔️ Si cargas recursos externos (imágenes, fuentes), hazlo de forma asincrónica para evitar bloqueos.
- ❌ No asumas que todos los assets se cargarán automáticamente. Usa `return false` en `assetLoader` para gestionarlos tú mismo.

---

## ✅ Conclusión

Conocer las **propiedades de un Asset** en Rive te permite personalizar al máximo tu animación desde código. Ya sea para cambiar imágenes, añadir nuevas fuentes o analizar recursos embebidos, dominar estos detalles te ayudará a construir experiencias visuales ricas, flexibles y dinámicas. 🎨