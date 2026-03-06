# Reels System Deployment & Usage

Este sistema permite mostrar los últimos Reels de Instagram en tu web utilizando Vercel como hosting y para la automatización (cron).

## Estructura
- `/api/reels.js`: Función serverless que hace el scraping de Instagram.
- `/public/index.html`: Dashboard premium que consume los datos.
- `vercel.json`: Configura el cron job (una vez por hora) y las rutas.

## Cómo funciona la "Caché"
En lugar de escribir un archivo físico (que Vercel no permite en runtime), usamos **Edge Caching**. 
1. La API devuelve el JSON con el header `Cache-Control: s-maxage=3600`.
2. Vercel guarda este JSON en su red global durante 1 hora.
3. El frontend siempre recibe la versión rápida desde la caché.
4. El Cron job (`0 * * * *`) se asegura de disparar la función periódicamente para actualizar la caché.

## Pasos para Deploy en Vercel

1. **Subir a GitHub**: Sube esta carpeta a un nuevo repositorio.
2. **Importar en Vercel**: Importa el repo en el dashboard de Vercel.
3. **Variables de Entorno (Opcional)**: 
   - Define `INSTAGRAM_ACCOUNT` con el nombre de la cuenta (ej: `radiorafaela`). Si no se define, usará por defecto esta misma account.
4. **Deploy**: Pulsa Deploy.
5. **Configurar Cron**: Una vez desplegado, Vercel detectará el cron en `vercel.json` y lo ejecutará automáticamente cada hora.

---
© 2026 - Diseñado por Antigravity
