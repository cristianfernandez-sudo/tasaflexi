# TasaFlexi v2 · Web app instalable (PWA)

## Qué hay en el pack
- `index.html` — la app completa (diseño, lógica, catálogo de vehículos).
- `manifest.webmanifest` — hace que se pueda **instalar** como app (icono, nombre, pantalla completa).
- `sw.js` — service worker: modo **offline** del armazón y soporte de **notificaciones**.
- `icons/` — iconos de la app (Android, iPhone y maskable).

## Publicar en GitHub Pages (repo `tasaflexi`)
1. Sube **todos** los archivos a la raíz del repositorio (reemplaza el `index.html` anterior). Respeta la carpeta `icons/`.
2. Commit. En ~1 minuto: `https://cristianfernandez-sudo.github.io/tasaflexi/`
3. Si ves la versión antigua, recarga con Ctrl+F5 (o cierra y abre la app instalada).

## Instalar en el móvil / PC
- **Android / Chrome:** botón "Instalar" en la cabecera o menú ⋮ → "Instalar app".
- **iPhone:** Safari → Compartir → "Añadir a pantalla de inicio".
- **PC (Chrome/Edge):** icono de instalar en la barra de direcciones.

## Cámara, galería y notificaciones
- **Hacer foto** abre la cámara en vivo (trasera en móvil, con botón para girar); si el navegador no lo permite, usa la cámara del sistema.
- **Elegir de la galería** permite varias fotos a la vez. Todas se **comprimen** (máx. 1600 px) antes de subir.
- **Notificaciones:** al activarlas (banner de Inicio o Ajustes), el captador recibe aviso cuando el tasador pone precio o escribe, y el tasador cuando llega una tasación nueva o un mensaje. Funcionan con la app abierta o instalada en segundo plano.
  *Para avisos con la app totalmente cerrada hace falta "push" de servidor (Firebase Cloud Messaging); el service worker ya está preparado para ello.*

## Modo demo → modo real
Ahora mismo la app arranca en **modo demo**: cada dispositivo guarda sus propios datos (persisten al recargar) y se entra con nombre + rol. Para el **modo real** (datos compartidos entre las 50 tiendas y login con Google solo @flexicar.es):
1. En `index.html`, busca `const firebaseConfig = {` y pega los 6 valores de tu proyecto Firebase (Consola → Configuración del proyecto → Tus apps).
2. Asegúrate de tener en Firebase: Authentication → Google activado; Authorized domains con `cristianfernandez-sudo.github.io`; Firestore creado con las reglas del documento `CONFIGURAR-FIREBASE.md`.
3. Sube el `index.html`. La app detecta la configuración y cambia sola a modo real (aparece "Iniciar sesión con Google").

Las fotos y PDFs ya van a **vuestro Cloudinary** (cloud `ti57iccy`, preset `TasaFlexi`), también en modo demo.

## Tasadores
La lista de correos de tasadores está en `index.html` (`const TASADORES`). Cualquier otro correo @flexicar.es entra como captador.
