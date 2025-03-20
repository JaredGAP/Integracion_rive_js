# Instalación y Configuración de Rive en JavaScript

Para integrar animaciones de Rive en tu proyecto web utilizando JavaScript, sigue los pasos que se detallan a continuación.

## 1. Incluir la Librería de Rive

Existen dos métodos principales para agregar la librería de Rive a tu proyecto:

### a) Uso de una etiqueta `<script>` con CDN

Puedes incluir la librería directamente desde un CDN en tu archivo HTML:

```html
<!-- Incluye la última versión del runtime de Rive -->
<script src="https://unpkg.com/@rive-app/canvas@latest"></script>
```

Esto cargará el paquete `@rive-app/canvas` desde un CDN, exponiendo un objeto global llamado `rive` que contiene la API de Rive. Es recomendable usar siempre la última versión disponible de la librería; el ejemplo anterior carga la versión más reciente automáticamente, pero también podrías fijar una versión específica en la URL.

### b) Uso de un gestor de paquetes (NPM)

Si tu proyecto utiliza un empaquetador de módulos como Webpack o Vite, puedes instalar la librería mediante NPM:

```bash
npm install @rive-app/canvas
```

Luego, impórtala en tu código JavaScript o TypeScript:

```javascript
import * as rive from '@rive-app/canvas';
```

La API será la misma que usando el objeto global. Por ejemplo, podrías crear una instancia con `new rive.Rive({...})` de igual manera. Alternativamente, puedes importar solo la clase `Rive`:

```javascript
import { Rive } from '@rive-app/canvas';
```

Y luego instanciarla:

```javascript
const animacion = new Rive({
    // Configuración
});
```

## 2. Preparar el Elemento `<canvas>`

Rive renderiza las animaciones en un elemento `<canvas>`. Añade uno en tu HTML con un identificador y tamaño deseado:

```html
<canvas id="canvas" width="500" height="500"></canvas>
```

Este elemento servirá como lienzo donde se dibujará la animación.

## 3. Crear una Instancia de Rive

Con la librería incluida y el canvas en el DOM, puedes crear una instancia de Rive en tu código JavaScript para cargar y reproducir una animación:

```javascript
const animacion = new rive.Rive({
    src: 'ruta/al/archivo.riv',
    canvas: document.getElementById('canvas'),
    autoplay: true, // Inicia la animación automáticamente
    onLoad: () => {
        console.log('Animación cargada y lista para usarse.');
    }
});
```

En este ejemplo:

- `src`: Especifica la ruta o URL del archivo `.riv` que contiene la animación.
- `canvas`: Hace referencia al elemento `<canvas>` donde se renderizará la animación.
- `autoplay`: Si se establece en `true`, la animación comenzará a reproducirse automáticamente una vez cargada.
- `onLoad`: Es una función de callback que se ejecuta cuando la animación se ha cargado correctamente.

## 4. Consideraciones Adicionales

- **Elección del Paquete Adecuado:** Rive ofrece varios paquetes de runtime; en la mayoría de los casos se recomienda `@rive-app/canvas`, que utiliza el renderizado Canvas 2D nativo del navegador. Existe también `@rive-app/webgl` para usar WebGL y un paquete ligero `@rive-app/canvas-lite` (que omite funciones de texto y audio) útil si deseas un tamaño menor de librería cuando no necesitas esas funcionalidades.

- **Compatibilidad:** Asegúrate de que el navegador donde se ejecutará la animación soporte las características necesarias para el runtime elegido. La mayoría de los navegadores modernos son compatibles con `@rive-app/canvas`.

Siguiendo estos pasos, tendrás Rive integrado en tu proyecto web y listo para cargar y controlar animaciones.

---

Este archivo proporciona una guía paso a paso sobre cómo instalar y configurar Rive en un entorno JavaScript, incluyendo ejemplos de código que ilustran cada paso del proceso.
