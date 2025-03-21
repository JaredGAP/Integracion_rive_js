# 🎨 Patrones Comunes de Animación con Rive

Una vez que conoces las bases de Rive y cómo integrarlo con JavaScript, es útil identificar **patrones reutilizables** que puedes aplicar en cualquier proyecto. Estos patrones no solo te ahorran tiempo, sino que también te ayudan a estructurar tu código de forma escalable y coherente.

Este documento resume los **patrones más comunes** que has aplicado (o podrías aplicar) usando Rive + JS.

---

## 📍 1. Scroll-Driven Animation (Animación basada en scroll)

**Descripción:** La animación avanza progresivamente a medida que el usuario hace scroll.

- Se conecta el progreso del scroll con un `Number Input` en Rive.
- Ideal para banners, storytelling, o efectos de presentación.

📂 Implementado en: `04_Web_Project/01_GSAP_ScrollTrigger.md`, `02_Hero_Scroll_Animation.md`

---

## 🧠 2. Scroll-Step Navigation (Cambio de estado por secciones)

**Descripción:** Cada sección del scroll actualiza un estado visual.

- Se usa `ScrollTrigger` para detectar el paso por secciones.
- Se asigna un valor a un `Number Input` según el índice.

📂 Implementado en: `04_Web_Project/04_Feature_Points_Scroll_Animation.md`

---

## 🖱️ 3. Hover-Based Interactions

**Descripción:** La animación responde cuando el usuario pasa el cursor por encima.

- Se activa un `Trigger Input` desde JS (`mouseenter`, `mouseleave`).
- Ideal para botones, personajes, o elementos destacados.

📂 Implementado en: `04_Web_Project/03_Hero_Hover_Interaction.md`

---

## 🧩 4. Evento → Lógica en JS

**Descripción:** La animación emite un evento (`RiveEvent`) que desencadena una acción en tu lógica JS.

- Útil para lanzar rutas, sonidos, mostrar u ocultar elementos, etc.

📂 Implementado en: `02_State_Machine/06_Animation_to_Logic.md`

---

## 🔄 5. Trigger + Resultado (Feedback visual por acción)

**Descripción:** Se dispara un `Trigger` para iniciar una animación, y se define el resultado con un `Number`.

- Ideal para simular procesos (enviar formulario, pagar, validar...).

📂 Implementado en: `04_Web_Project/06_Transaction_Status_Animation.md`

---

## 🧰 6. Reemplazo dinámico de contenido visual

**Descripción:** Cambiar imágenes o fuentes dentro de la animación desde JS.

- Se usan métodos como `setRenderImage()` o `setFont()` sobre los assets.

📂 Implementado en: `03_Loading_Assets/01_Image_Asset.md`, `03_Font_Asset.md`

---

## 💬 7. Texto dinámico desde inputs

**Descripción:** El texto en la animación cambia en tiempo real con `textRun()`.

- Se vincula a inputs o eventos del usuario.

📂 Implementado en: `05_Tips_and_Tricks/02_Text_Runs.md`

---

## ✅ Conclusión

Estos patrones aparecen una y otra vez en proyectos reales, y puedes combinarlos entre sí para construir **interfaces sofisticadas y personalizadas**. Tenerlos como referencia te ayudará a:

- Elegir el enfoque correcto para cada situación.
- Comunicar mejor tu lógica visual con tu equipo.
- Reutilizar estructuras ya probadas.

**Consejo:** Crea tus propios patrones y documenta su uso. Rive es tan flexible como lo seas tú. 💡

