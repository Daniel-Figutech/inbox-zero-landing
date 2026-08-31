# Inbox Zero — waitlist landing

Landing de una sola pantalla, réplica exacta del mockup: titular en cromado con
caracteres bitmap intercalados, sobre metálico con badge "0" y barra de waitlist.

- `index.html` — todo dentro (CSS + SVG del sobre + JS del formulario). Sin build, sin dependencias.
- Tipografías: Space Grotesk, Pixelify Sans, Space Mono (Google Fonts).
- Escala proporcional: todo se mide en `--k` (1% del ancho de referencia de 1993px), bloqueado a partir de esa anchura.

**Live:** https://daniel-figutech.github.io/inbox-zero-landing/

El botón *Join waitlist* valida el email y muestra la confirmación en la propia barra.
No hay backend: para capturar de verdad, apuntar el `submit` a un endpoint (FormSubmit, Klaviyo, GHL...).
