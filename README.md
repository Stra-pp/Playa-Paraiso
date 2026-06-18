# Playa Paraíso · App operativa (ILD + Compras + Sistemas + Mantenimiento)

Aplicación web de una sola página (`index.html`) que unifica:

- **ILD** (Inspección de Lista Diaria): formularios por área y turno, fotos, aprobación, dashboard de cumplimiento y configuración (checklists, usuarios, aprobadores, días esperados, nuevos ILD).
- **Compras**, **Sistemas** y **Mantenimiento**: solicitudes/tickets con flujo de aprobación, seguimiento por jefatura y tablero Kanban.

El histórico se guarda en **SharePoint (sitio Prueba7)** vía Microsoft Graph (MSAL), así que se abre desde cualquier dispositivo iniciando sesión.

---

## Publicar GRATIS con GitHub Pages

1. Crea un repositorio **público** en GitHub (ej. `playa-paraiso-app`).
   - Debe ser público para que GitHub Pages sea gratis. (Privado requiere plan de pago.)
2. Sube **`index.html`** (y este `README.md`) a la raíz: botón **Add file → Upload files**, arrastra, **Commit changes**.
3. Activa Pages: **Settings → Pages → Source: Deploy from a branch → Branch: `main` / `/ (root)` → Save**.
4. Espera ~1 minuto. Arriba aparecerá tu URL:
   `https://TU-USUARIO.github.io/playa-paraiso-app/`
5. Cada vez que actualices `index.html` y hagas commit, la página se vuelve a publicar sola.

## Conectar con SharePoint (Azure) — paso único

La app usa el **mismo App Registration** que tu ILD actual.

1. Abre la app publicada, ingresa con PIN **9999** (Desarrollador) → **Configuración**.
2. Copia el valor que muestra **"Redirect URI (regístralo en Azure)"**
   (será algo como `https://TU-USUARIO.github.io/playa-paraiso-app/`).
3. En Azure → **App Registrations** → tu app → **Authentication** →
   en la plataforma **Single-page application**, pulsa **Add URI**, pega esa URL y **Save**.
4. Permisos delegados ya consentidos para el ILD: `Files.ReadWrite.All` y `User.Read`.

> Mientras no registres la URL, el inicio de sesión de Microsoft dará error de *redirect_uri*.
> Es un único registro; después funciona desde cualquier dispositivo.

## Importar tus ILD reales

Desarrollador → **Configuración → 📥 Importar desde 12-jun**: lee `ILD_Registros.json`
de Prueba7 y trae los registros del 12 de junio en adelante (sin duplicar).

## Datos en SharePoint (no tocan los del ILD actual)

`NEXO_ILD.json`, `NEXO_Compras.json`, `NEXO_Sistemas.json`, `NEXO_Mantenimiento.json`, `NEXO_Config.json`.

## PINs

`9999` Desarrollador · `0000` Gerencia · `1001` Operaciones · `1002` Comercial ·
`1003` Mantenimiento · `1004` Ama de Llaves · `1005` Compras · `1006` Sistemas.
Los colaboradores ingresan sin PIN.

## Modo demo (sin SharePoint)

*Configuración → Cambiar a demo local* (o `APP.useGraph = false` en el código).
Los datos quedan solo en el navegador.

---

### Nota de seguridad

Como el repo es público, el código (incluidos los PINs de jefatura) queda visible.
Para un uso interno suele ser aceptable; si prefieres ocultarlo, opciones: usar un repo privado
con un plan que permita Pages, otro hosting estático gratuito sin tarjeta (Cloudflare Pages),
o cambiar los PINs por valores nuevos. El `clientId`/`tenantId` no son secretos.
