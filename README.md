# Mi Bolsillo 💜

App personal de gastos y ahorro. Funciona en el navegador, se instala en el móvil como una app y guarda los datos solo en tu dispositivo.

## Archivos
`index.html` (la app), `manifest.json`, `sw.js`, `icon.svg`, `icon-192.png`, `icon-512.png`. Tienen que estar todos en la misma carpeta.

## 1. Subirla a GitHub y ponerla en el móvil

1. Crea una cuenta en github.com y un repositorio nuevo (por ejemplo `mi-bolsillo`). Puede ser **privado** si tu cuenta lo permite con Pages; si no, público (los datos no van en el repo, se quedan en tu móvil).
2. Sube los 6 archivos (botón *Add file → Upload files*), o desde terminal:
   ```bash
   git init
   git add .
   git commit -m "Mi Bolsillo"
   git branch -M main
   git remote add origin https://github.com/TU_USUARIO/mi-bolsillo.git
   git push -u origin main
   ```
3. En el repo: *Settings → Pages → Build and deployment → Deploy from a branch → main / (root) → Save*.
4. En un minuto tendrás una URL tipo `https://TU_USUARIO.github.io/mi-bolsillo/`.
5. Ábrela en el móvil:
   - **Android (Chrome):** menú ⋮ → *Instalar aplicación* / *Añadir a pantalla de inicio*.
   - **iPhone (Safari):** botón compartir → *Añadir a pantalla de inicio*.
6. Ya la tienes como una app más, y funciona sin conexión.

> Los datos se guardan en el navegador de cada dispositivo. Si cambias de móvil o borras datos del navegador, usa *Ajustes → Exportar datos* antes y *Importar* después. Haz una copia de vez en cuando.

## 2. Cómo se calcula tu plan (todo editable en Ajustes)

- Ingreso mensual = beca / pagos al año (+ otros ingresos si los añades).
- Fijos: piso, gastos, transporte y gimnasio se apartan primero.
- Lo que sobra se reparte entre **compra / salidas / ahorro** (por defecto 55 / 27 / 18 %).
- **Agosto**: sin piso ni gastos, todo ese dinero va a tu **cuenta de caprichos**.
- Lo que no gastes de compra y salidas se suma a tu ahorro; lo que te pases se resta.
- Cuentan como "gasto" solo las categorías compra, salidas y caprichos; los fijos ya están apartados.

## 3. Conectar con Abanca

**Importante:** Abanca no ofrece una API pública para particulares. La única vía "oficial" es la banca abierta (PSD2), que se usa a través de proveedores intermedios. Para un proyecto personal tienes tres niveles:

### Nivel 1: importar el CSV (ya incluido, recomendado para empezar)
1. En la banca online de Abanca descarga tus movimientos (normalmente hay opción de Excel o CSV; si es Excel, guárdalo como CSV).
2. En la app: *Gastos → Importar de Abanca*, sube el archivo.
3. Revisa las categorías propuestas (supermercados → compra, bares → salidas...) y confirma.

Tarda 2 minutos a la semana y nunca duplica movimientos. El formato exacto del archivo de Abanca puede variar; la app detecta separador, fecha e importe automáticamente, pero si algún archivo no se lee, pásamelo (con datos de ejemplo, sin tus números reales) y lo ajusto.

### Nivel 2: banca abierta con un agregador (automático)
Proveedores a revisar (comprueba qué admiten cuentas personales y si Abanca está soportada ahora mismo): **Enable Banking**, **GoCardless Bank Account Data**, **Tink**, **TrueLayer**.
- Necesitas una pequeña función en servidor (Cloudflare Workers, Vercel, etc.) que guarde las claves en secreto y llame al proveedor. **Nunca pongas claves en `index.html`.**
- Hay que renovar el consentimiento del banco periódicamente (por PSD2, cada pocos meses).
- La función devolvería los movimientos y la app los pasaría por el mismo importador que ya existe.

### Nivel 3: otras alternativas
- Apps de terceros con sincronización bancaria (p. ej. Fintonic, Finanzas de Abanca si tu banco la ofrece) como fuente de exportación.
- Notificaciones del banco + registro manual rápido con el botón ＋ (10 segundos por gasto).

## 4. Ideas para seguir
- Gráfico de evolución del ahorro mes a mes.
- Notificación semanal "¿has apuntado tus gastos?".
- Gastos recurrentes automáticos y objetivos concretos (viaje de agosto, etc.).
- Sincronización entre dispositivos con una base de datos gratuita (Supabase/Firebase).
