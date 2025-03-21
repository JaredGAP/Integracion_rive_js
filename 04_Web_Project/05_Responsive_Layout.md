# 📱 Diseño Responsive para Feature Points

Cuando se trata de animaciones con Rive y contenido dividido en secciones, es fundamental que el diseño funcione bien en **todas las resoluciones**, especialmente en dispositivos móviles.

En este ejemplo adaptamos el layout de la animación por puntos (Feature Points) para que sea **responsive y accesible** sin perder el impacto visual ni la sincronización con scroll.

---

## 🎨 Diseño original en desktop

```css
.feature {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 2rem;
  gap: 3rem;
}

.feature .content {
  display: flex;
  flex-direction: column;
  gap: 6rem;
  flex: 1;
}

.feature canvas {
  flex: 1;
  max-width: 500px;
  height: auto;
}
```

Este diseño coloca el contenido a la izquierda y la animación a la derecha, ideal para pantallas grandes.

---

## 📱 Versión responsive

```css
@media (max-width: 768px) {
  .feature {
    flex-direction: column-reverse;
    padding: 1rem;
    gap: 2rem;
  }

  .feature canvas {
    width: 100%;
    max-width: 100%;
    height: auto;
  }

  .feature .content {
    gap: 3rem;
  }
}
```

### 📌 ¿Qué estamos haciendo?

- Cambiamos `flex-direction` a `column-reverse` para que la animación quede **encima** del contenido.
- Ajustamos márgenes y separación entre secciones.
- Hacemos que el canvas se adapte al ancho completo del contenedor.

---

## ✅ Buenas prácticas para responsive + canvas

- ✔️ Usa `max-width: 100%` para que el canvas no se desborde en pantallas pequeñas.
- ✔️ Aplica `resizeDrawingSurfaceToCanvas()` al cargar la animación para que se ajuste correctamente.
- ✔️ Testea en móviles reales o emuladores para verificar el comportamiento del layout.
- ❌ No utilices valores fijos en `width` o `height` para el canvas cuando quieras responsividad.

---

## 🧩 Consejo adicional: adaptabilidad visual

Si tu animación depende de un input `scrollValue`, asegúrate de que los cambios en altura (por diseño responsive) **no afecten negativamente al cálculo del scroll**. Puedes usar `ScrollTrigger.refresh()` después de cambiar el DOM o cargar estilos condicionales.

```javascript
ScrollTrigger.refresh();
```

---

## 🏁 Conclusión

Adaptar tus secciones con Rive a dispositivos móviles es clave para ofrecer una experiencia profesional y completa. Un diseño responsive asegura que las animaciones y el contenido sean igual de impactantes y funcionales en cualquier pantalla. 📱✨

