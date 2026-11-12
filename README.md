# Feedback del equipo

App web de feedback anónimo entre compañeros: por cada persona, **2 × «Sigue haciendo»**, **1 × «Te propondría probar»** y un **«Gracias por…»** opcional.

- **Frontend:** `index.html` estático, publicado en GitHub Pages.
- **Backend:** Supabase (proyecto `tablero-equipo`), tablas con prefijo `fb_`.
  Las tablas no se pueden leer directamente: RLS está activado sin políticas y se han revocado los permisos. Todo pasa por funciones RPC `fb_*` (security definer) que comprueban el token de sesión.

## Anonimato
- `fb_comentarios` no guarda ni el autor ni la fecha.
- `fb_enviados` solo registra que «X ya escribió a Y», para evitar duplicados, sin enlazarlo con el texto.
- Los comentarios se publican todos a la vez (estado `publicada`) y solo a quien tenga al menos `min_feedbacks` (por defecto 3).
- El administrador solo ve cifras, nunca el contenido.

## Acceso
1. El admin añade los nombres en «Administración» y copia el enlace personal de cada uno (`?i=<código>`).
2. La primera vez, cada persona elige su contraseña desde ese enlace.
3. Después entra eligiendo su nombre y poniendo la contraseña.
4. Si alguien olvida la contraseña, «Reiniciar» genera un enlace nuevo.
