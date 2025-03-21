# 📦 Carga Manual de Archivos `.riv` desde JavaScript

En algunos casos, puede que necesites **cargar una animación `.riv` de forma manual** en lugar de usar la propiedad `src` con una URL. Esto te permite:

- Obtener el archivo desde una API, base de datos o sistema de archivos local.
- Modificar el contenido antes de cargarlo.
- Evitar rutas públicas o dependencias externas.

---

## ⚙️ Ejemplo práctico: carga manual

```html
<canvas width="500" height="500"></canvas>
<input type="file" />
```

```javascript
let manualAnimation;

const fileInput = document.querySelector("input[type=file]");

fileInput.addEventListener("change", async (event) => {
  const file = event.target.files[0];
  if (!file) return;

  const buffer = await file.arrayBuffer();
  const bytes = new Uint8Array(buffer);

  manualAnimation = new rive.Rive({
    buffer: bytes, // aquí va el contenido binario
    canvas: document.querySelector("canvas"),
    autoplay: true,
    onLoad: () => {
      manualAnimation.resizeDrawingSurfaceToCanvas();
      console.log("✅ Animación cargada desde archivo local");
    }
  });
});
```

---

## 📖 Explicación de claves

| Elemento               | Función                                                                 |
|------------------------|-------------------------------------------------------------------------|
| `input type="file"`    | Permite seleccionar un archivo `.riv` desde el dispositivo.             |
| `arrayBuffer()`        | Convierte el archivo a una secuencia de bytes.                          |
| `new Uint8Array(...)`  | Lo transforma al formato requerido por el runtime de Rive.              |
| `buffer:`              | Se usa en lugar de `src:` para cargar la animación.                    |

---

## 🧩 Casos de uso recomendados

- **Herramientas de edición** que permiten al usuario cargar sus propias animaciones.
- **Apps offline o desktop** con archivos `.riv` locales.
- **Pruebas rápidas** de animaciones sin subirlas a un servidor.

---

## ⚠️ Consideraciones

- La animación debe ser un archivo `.riv` válido y exportado desde Rive Studio.
- No puedes usar `buffer` y `src` al mismo tiempo.
- Si tu app permite cargar archivos, valida su tipo (`.riv`) antes de instanciar Rive.

---

## ✅ Conclusión

Cargar archivos `.riv` manualmente desde código te da total control sobre **cómo y cuándo** se insertan animaciones en tu app. Esto habilita flujos más dinámicos, seguros y personalizados en tus proyectos con Rive.

Una técnica especialmente útil para aplicaciones que usan contenido generado por el usuario o requieren mayor flexibilidad en la carga de recursos. 🗃️✨

