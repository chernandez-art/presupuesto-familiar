# Presupuesto Familiar

App de presupuesto familiar (React, una sola página) con **sincronización en tiempo real** entre dispositivos vía Firebase.

- **Sitio publicado:** https://presupuesto-familiar-hernandez.netlify.app
- **Hosting:** Netlify (deploy manual con `netlify deploy --prod --dir .`)
- **Datos:** Firestore (proyecto `santins-c0d82`), documento único `presupuesto/familia`.
- **Acceso:** login obligatorio (Firebase Auth, correo/clave). Comparten Christian y Ruth.

## Cómo funciona la sincronización
- Cada cambio local (debounce 500 ms) escribe el documento `presupuesto/familia`.
- `onSnapshot` aplica los cambios remotos al instante en el otro dispositivo.
- Anti-eco por `session` para que no se pisen entre ellos. Última escritura gana.

## Configuración en la consola de Firebase (santins-c0d82)
1. **Firestore → Reglas:** agregar el bloque de [`firestore-presupuesto.rules`](firestore-presupuesto.rules) dentro de `match /databases/{database}/documents { … }` (sin borrar las reglas de SANTINS).
2. **Authentication → Users:** crear el usuario de Ruth (`ggruthie92@gmail.com` + clave).
3. **Authentication → Settings → Authorized domains:** agregar `presupuesto-familiar-hernandez.netlify.app`.

## Volver a desplegar tras cambios
```
netlify deploy --prod --dir . --site 5f0f487c-4f9d-4a0f-98ae-33ed05e7e936
```
