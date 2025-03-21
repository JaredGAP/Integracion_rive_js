# 🚀 Guía Completa de Integración Rive + JavaScript

Bienvenido a este repositorio donde aprenderás a integrar **animaciones Rive** en proyectos web reales usando **JavaScript**. A través de ejemplos claros y prácticos, descubrirás cómo llevar tus interfaces al siguiente nivel con animaciones interactivas, reactivas y modernas.

---

## 🎯 Objetivos

- ✅ Aprender a cargar y mostrar animaciones `.riv` en un `<canvas>`.
- ✅ Conectar animaciones con eventos como scroll, hover o clic.
- ✅ Usar **State Machines** con inputs tipo `trigger`, `boolean` y `number`.
- ✅ Cargar dinámicamente imágenes, fuentes o animaciones desde archivos o URLs.
- ✅ Crear un proyecto web completo y responsive usando GSAP + Rive.

---

## 🛠️ Requisitos para empezar

- Una cuenta en [Rive](https://rive.app/) para crear/exportar tus animaciones.
- Editor de código (recomendado: VS Code).
- Navegador moderno (Chrome, Firefox, Edge).

Instala la librería de Rive si usas bundlers:
```bash
npm install @rive-app/canvas
```

O usa la CDN para proyectos simples:
```html
<script src="https://unpkg.com/@rive-app/canvas@2.8.3"></script>
```

---

## 📚 Estructura del Proyecto

| Carpeta | Descripción |
|--------|-------------|
| `01_Getting_Started/` | Carga básica de una animación Rive en HTML y control desde JS. |
| `02_State_Machine/`   | Uso de máquinas de estados con triggers, booleanos y valores numéricos. |
| `03_Loading_Assets/`  | Cómo reemplazar imágenes y fuentes dinámicamente desde JS. |
| `04_Web_Project/`     | Proyecto web real con scroll, interacciones, eventos y diseño responsive. |
| `05_Tips_and_Tricks/` | Funcionalidades avanzadas: abrir enlaces, actualizar texto, cargar manualmente. |

---

## ▶️ ¿Cómo usar este repositorio?

1. Revisa cada carpeta en orden para construir tu aprendizaje paso a paso.
2. Ejecuta los ejemplos con Live Server (VS Code) para evitar errores con WebAssembly.
3. Usa tus propias animaciones o edita las existentes para practicar.
4. Modifica los ejemplos y prueba nuevas combinaciones de inputs y animaciones.

---

## 💡 Consejos útiles

- ✔️ Nombra bien los inputs en Rive Studio para encontrarlos fácilmente desde JS.
- ✔️ Siempre usa `resizeDrawingSurfaceToCanvas()` al cargar la animación.
- ✔️ Valida URLs o datos antes de usarlos con `setRenderImage`, `setFont` o `textRun()`.

---

## 🔗 Recursos adicionales

- 🌐 [Sitio oficial de Rive](https://rive.app/)
- 📚 [Documentación oficial](https://help.rive.app/)
- 💬 [Comunidad de Discord](https://discord.gg/rive)
- 🛠️ [Runtime JS en GitHub](https://github.com/rive-app/rive-wasm)

---

## 🙌 Contribuciones

¡Toda mejora es bienvenida! Si tienes sugerencias, ideas o encuentras errores:

- Abre un Issue 🐞
- Envía un Pull Request 🔧

---

Hecho con ❤️ para que tus interfaces cobren vida.

**¡Anima tu web con Rive!** 🎨⚡

