# TasaFlexi v2.1 · Guía de despliegue

## Qué contiene este pack

- `index.html` — la aplicación completa (demo lista para enseñar)
- `manifest.webmanifest` — hace la app instalable (PWA)
- `sw.js` — service worker: funciona sin conexión y gestiona notificaciones
- `icons/` — iconos de la app (Android, iPhone y escritorio)
- `LEEME-DESPLIEGUE.md` — este documento

## Subir a GitHub Pages (repo `tasaflexi`)

1. Entra en tu repositorio → botón **Add file → Upload files**.
2. Arrastra **TODOS** los archivos del pack a la raíz del repo: `index.html`, `manifest.webmanifest`, `sw.js` y la carpeta `icons` con sus 4 imágenes.
3. **Importante**: el archivo principal debe llamarse exactamente `index.html`. Si tu navegador lo descargó como `index (1).html` o `index_1.html`, renómbralo antes de subirlo.
4. Commit changes. En 1–2 minutos estará en:
   `https://cristianfernandez-sudo.github.io/tasaflexi/`
5. Si ves la versión antigua, fuerza recarga con **Ctrl + F5** (en móvil: borrar datos del sitio o abrir en incógnito).

> Los dispositivos que ya usaron la demo antigua se actualizan solos: al abrir, la app detecta la nueva versión de ejemplos y los carga sin perder las tasaciones creadas por el usuario. Si algo se ve raro, en **Ajustes → Reiniciar datos demo**.

## La demo para la central

- **Entrar como captador**: escribe un nombre, elige *Captador* y entra. Verás la cuenta de "Tienda Sevilla" ya con actividad: una tasación **con horquilla** (Golf), una **pendiente** (Tucson) y un **borrador** a medio rellenar (Sportage) para enseñar el flujo PC → móvil → PC.
- **Entrar como tasador**: cualquier nombre con el rol *Tasador*. La bandeja llega con **13 tasaciones reales con foto**, 4 pendientes, tiempos de respuesta y horquillas.
- **Matrícula duplicada**: abre el Golf `1234 BCD` — hay dos tasaciones de ese coche (Sevilla hoy y Córdoba hace 3 meses). El captador ve el historial **sin precios** («El precio solo lo ve el tasador»); el tasador lo ve todo.
- **Fotos**: son imágenes de coches alojadas en tu Cloudinary (`ti57iccy/tasaflexi/demo`), cargan desde cualquier dispositivo.

## Instalar como app

- **Android (Chrome)**: botón *Instalar app* en la barra superior, o menú ⋮ → *Añadir a pantalla de inicio*.
- **iPhone (Safari)**: Compartir → *Añadir a pantalla de inicio*.
- **PC (Chrome/Edge)**: icono de instalación en la barra de direcciones.

Una vez instalada abre a pantalla completa, con su icono naranja, e incluye acceso directo "Nueva tasación".

## Cámara, galería y notificaciones

- **Cámara**: en el formulario, *Hacer foto* abre la cámara real (trasera en móvil, con cambio de cámara). Requiere HTTPS — GitHub Pages ya lo es.
- **Galería**: *Subir fotos* permite selección múltiple; las imágenes se comprimen en el dispositivo antes de guardar.
- **Notificaciones**: al activarlas, el tasador recibe aviso de tasaciones nuevas y mensajes; el captador, cuando le ponen precio o le escriben. Con la app abierta o en segundo plano funcionan ya; para push con la app **cerrada** hace falta Firebase Cloud Messaging (el service worker ya está preparado).

## Pasar de demo a versión real

La app funciona en modo demo (datos en cada dispositivo) hasta que se configura Firebase:

1. En `index.html`, busca `firebaseConfig` y sustituye los valores `PEGA_AQUI_...` por los de tu proyecto (Consola Firebase → Configuración del proyecto → Tus apps → Web).
2. En Firebase: **Authentication → Google** activado, y en dominios autorizados añade `cristianfernandez-sudo.github.io`.
3. **Firestore**: crea la base de datos y aplica las reglas restringidas a `@flexicar.es` (documento CONFIGURAR-FIREBASE).
4. Al detectar la configuración, la app cambia sola: login con Google (solo cuentas `@flexicar.es`), datos compartidos en tiempo real entre todas las tiendas.

Las **fotos y Carfax** ya suben a tu Cloudinary (`cloudName: ti57iccy`, preset `TasaFlexi`) — no requiere tarjeta ni cambios.

## Tasadores

Los correos con rol tasador están al principio del script en `index.html` (`TASADORES`):
cristian.fernandez, carlos.infante, kevin.yanez, daniel.gesali, jhiguera — todos `@flexicar.es`.
Para añadir o quitar, edita esa lista y vuelve a subir el archivo.
