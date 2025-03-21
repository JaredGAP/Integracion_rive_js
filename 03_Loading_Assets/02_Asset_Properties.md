# 🧩 Propiedades de Asset en Rive

En Rive, un **Asset** es cualquier recurso adicional embebido o referenciado en una animación: imágenes, fuentes, sonidos u otros datos. Cuando trabajas con animaciones que utilizan assets dinámicos desde JavaScript (por ejemplo, mediante `assetLoader`), es importante conocer las propiedades disponibles para inspeccionarlos y manipularlos.

---

## 🔍 Propiedades comunes de un Asset

Cuando usas el método `assetLoader(asset, bytes)` en la instancia de `rive.Rive`, puedes acceder a las siguientes propiedades del objeto `asset`:

| Propiedad | Tipo | Descripción |
|----------|------|-------------|
| `id` | `number` | Identificador único del asset. |
| `name` | `string` | Nombre del asset definido en Rive Studio. |
| `type` | `string` | Tipo de asset (por ejemplo, `image`, `font`, etc.). |
| `isImage` | `boolean` | Verdadero si el asset es una imagen. |
| `isFont` | `boolean` | Verdadero si el asset es una fuente. |
| `renderImage` | `object/null` | Imagen cargada asociada al asset (si aplica). |
| `setRenderImage(img)` | `function` | Permite establecer una imagen nueva para el asset. |
| `setFont(font)` | `function` | Permite establecer una nueva fuente para el asset. |

---

## 🧪 Ejemplo práctico

```javascript
const animation = new rive.Rive({
  src: "animacion-con-assets.riv",
  canvas: document.querySelector("canvas"),
  autoplay: true,
  assetLoader: (asset, bytes) => {
    console.log("Asset detectado:", asset.name);

    if (asset.isImage) {
      console.log("Es una imagen:", asset);
      // Aquí puedes cargar una imagen personalizada con setRenderImage()
    }

    if (asset.isFont) {
      console.log("Es una fuente:", asset);
      // Aquí puedes cargar una fuente personalizada con setFont()
    }

    return false; // Indica que el asset no se cargó automáticamente
  }
});
```

---

## 🔧 Consideraciones útiles

- Puedes acceder a los assets definidos en Rive Studio al exportar un archivo `.riv` con imágenes o fuentes embebidas.
- Si quieres reemplazar un asset, guarda la referencia y luego utiliza `.setRenderImage()` o `.setFont()` según el tipo.
- Los assets no se cargan automáticamente si devuelves `false` en el `assetLoader`, lo que te da control total sobre su gestión.

---

## ✅ Conclusión

Conocer las propiedades de los **Asset** en Rive te permite personalizar tus animaciones dinámicamente desde JavaScript. Ya sea para reemplazar imágenes, tipografías u otros recursos visuales, este sistema te brinda flexibilidad para crear experiencias interactivas y adaptables sin modificar el archivo `.riv` original.