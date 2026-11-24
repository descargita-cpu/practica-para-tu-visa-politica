# Política de privacidad publicada (GitHub Pages)

Archivo fuente: `playstore\privacidad\index.html` (HTML autocontenido: CSS dentro, sin imágenes
externas ni JavaScript). Es la misma información que la pantalla **Ajustes → Privacidad y datos**
de la app, pero en versión web para Google Play.

## 1. Crear el repositorio

1. Entra a <https://github.com> con tu cuenta (la misma que usas para las otras apps).
2. Botón **+** (arriba a la derecha) → **New repository**.
3. Nombre: `practica-para-tu-visa-politica`
   - Visible: **Public** (obligatorio para GitHub Pages gratis y para que Play pueda abrirlo).
   - No marques «Add a README file».
4. **Create repository**.

## 2. Subir el archivo

1. En el repo vacío, clic en **uploading an existing file**.
2. Arrastra `playstore\privacidad\index.html` (o usa *choose your files*).
3. Abajo, **Commit changes**.

> El archivo debe llamarse exactamente `index.html` y estar en la raíz del repo: GitHub Pages lo
> usa como página de inicio.

## 3. Activar GitHub Pages

1. En el repo: **Settings** (arriba) → menú izquierdo **Pages**.
2. En *Build and deployment* → *Source*: **Deploy from a branch**.
3. *Branch*: **main** y carpeta **/ (root)** → **Save**.
4. Espera 1 o 2 minutos y recarga la página: aparece el aviso verde con la dirección.

URL final (con tu usuario de GitHub):

```
https://TU-USUARIO.github.io/practica-para-tu-visa-politica/
```

Ejemplo si el usuario es `descargita-cpu`:

```
https://descargita-cpu.github.io/practica-para-tu-visa-politica/
```

## 4. Pegarla en Google Play

Play Console → tu app → **Contenido de la app** → **Política de privacidad** → pegar la URL →
**Guardar**. Requisitos que ya cumple:

- Es pública, sin inicio de sesión y en español.
- Es una página web (no un PDF ni un archivo descargable).
- Menciona la app, el desarrollador y un correo de contacto.
- Explica el permiso de micrófono, el reconocimiento de voz y cómo borrar los datos.

## 5. Actualizarla en el futuro

- Edita `playstore\privacidad\index.html` en el proyecto, cambia la fecha del encabezado y súbelo
  otra vez al repo (**Add file → Upload files**, sobrescribe) o edítalo en GitHub con el lápiz.
- Si agregas otro servicio (respaldo en la nube, analítica, etc.), actualiza también la pantalla
  «Privacidad y datos» de la app y la sección **Seguridad de los datos** del Play Console.
## Respuestas para «Seguridad de los datos» (Play Console)

Desde la versión 0.7.0 la app muestra anuncios de Google AdMob (banner al pie de todas las pantallas), así que la declaración **ya no es
«No se recogen datos»**. Responde así:

| Pregunta | Respuesta |
|---|---|
| ¿La app recoge o comparte datos del usuario? | **Sí** |
| ¿Se recogen datos cifrados en tránsito? | Sí (HTTPS; lo gestiona el SDK de Google) |
| ¿Se permite solicitar la eliminación de datos? | No aplica; se borran desde Ajustes o al desinstalar |
| Datos tratados solo en el dispositivo | Perfil (país, visa, duración), preferencia de voz e historial de prácticas |
| **Identificadores del dispositivo u otros** | **Recogido y compartido** · Fin: **publicidad o marketing** · Obligatorio · No se puede desactivar dentro de la app (sí desde Ajustes de Android) |
| Permisos sensibles | Micrófono (`RECORD_AUDIO`), solo al tocar el botón |
| Publicidad | **Sí**: Google AdMob (banner al pie de todas las pantallas + anuncio a pantalla completa al abrir) |
| Compras dentro de la app | No |
| Cuentas / inicio de sesión | No |
| Menores | App no dirigida a menores de 13 |

Declaraciones cortas para el formulario:

- **Datos del usuario:** «La app no pide datos personales. El perfil y el historial de prácticas se
guardan solo en el dispositivo. El micrófono se usa únicamente cuando el usuario lo activa.»
- **Identificadores del dispositivo:** «La app usa el SDK de Google AdMob. Google puede tratar el
identificador de publicidad del dispositivo con fines publicitarios. El desarrollador no recibe ni
almacena esos datos.»

## 6. Anuncios (AdMob) — pasos en la cuenta

La app ya trae el SDK y un interruptor por compilación. Para pasar de las unidades de **prueba** a
las reales:

1. En <https://admob.google.com> → **Apps** → **Añadir app** → Android → «¿Ya está publicada en
   Google Play?»: sí (o «No» si aún no) → nombre `Práctica para tu Visa`.
2. Copia el **App ID** (`ca-app-pub-6578097612016179~XXXXXXXXXX`) y pégalo en
   `android\app\src\main\AndroidManifest.xml` (meta-data `com.google.android.gms.ads.APPLICATION_ID`).
3. En la app de AdMob → **Unidades de anuncio** → crear dos:
   - **Banner** → pegar el ID en `lib\core\ads\anuncios.dart` → `_bannerReal`.
   - **Anuncio de apertura de app** (App open) → pegar el ID en `_cargaReal`.
4. Compilar con `--dart-define=ANUNCIOS_PRUEBA=false` (o cambiar el `defaultValue` de
   `kAnunciosDePrueba` a `false`). Mientras los IDs digan `PENDIENTE`, la app usa las unidades de
   prueba y no genera ingresos ni riesgo de cuenta.
5. **Nunca** toques tus propios anuncios reales en el teléfono: se considera fraude. Para probar,
   usa el dispositivo configurado como *test device* en AdMob.

