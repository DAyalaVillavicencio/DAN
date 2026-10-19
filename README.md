# Informe de visita técnica – App Android (APK)

Este proyecto envuelve la app web en una app de Android con Capacitor.
Al descargar el informe (Word o PDF) se abre el menú de compartir de Android, desde donde puedes guardarlo en Archivos/Drive o enviarlo por WhatsApp o correo.

> Importante: este proyecto no fue compilado ni probado por quien lo preparó (no había herramientas de Android disponibles). Si algún paso falla, revisa la sección «Problemas comunes».

## Requisitos (en tu computadora)
1. **Node.js 20 o superior** (https://nodejs.org).
2. **Android Studio** (https://developer.android.com/studio). Incluye el JDK y el SDK de Android necesarios; ábrelo una vez y deja que termine de descargar los componentes.
3. Conexión a internet solo para esta preparación.

## Pasos
Abre una terminal dentro de esta carpeta y ejecuta:

```
npm install
npx cap add android
npm run sync
```

`npm run sync` copia los archivos de la app, registra los plugins y agrega el permiso de cámara.

### Opción A: compilar con Android Studio (la más fácil)
```
npx cap open android
```
En Android Studio espera a que termine «Gradle sync» y ve a **Build > Build Bundle(s) / APK(s) > Build APK(s)**. Al terminar, pulsa «locate» en el aviso.
El archivo queda en `android/app/build/outputs/apk/debug/app-debug.apk`.

### Opción B: desde la terminal
- Mac/Linux: `cd android && ./gradlew assembleDebug`
- Windows: `cd android` y luego `gradlew.bat assembleDebug`

El APK queda en la misma ruta de la opción A.


### Opción C: compilar en la nube, sin Android Studio
1. Crea una cuenta gratuita en https://github.com y un repositorio nuevo (puede ser privado).
2. Sube todo el contenido de esta carpeta al repositorio, incluida la carpeta oculta `.github`. Si la subes desde la web, usa «Add file > Upload files» y arrastra la carpeta completa.
3. En el repositorio, entra a la pestaña **Actions**, elige **Compilar APK** y pulsa **Run workflow**.
4. Cuando termine (unos minutos), abre la ejecución y descarga **app-debug** en la sección «Artifacts». Es un zip que contiene `app-debug.apk`.
5. Instálalo en el celular como se explica abajo.

## Instalar en el celular
1. Pasa `app-debug.apk` al celular (cable, Drive, WhatsApp…).
2. Ábrelo desde el celular. Android pedirá permitir «instalar apps desconocidas» para esa aplicación; acéptalo.
3. Abre «Informe Visita Técnica».

Este es un APK de prueba (firmado con la clave de depuración). No sirve para publicar en Google Play.

## Cambiar la app más adelante
Edita `www/index.html`, luego ejecuta `npm run sync` y vuelve a compilar.

## Problemas comunes
- **`npx cap add android` falla:** revisa que Node sea 20 o superior (`node -v`).
- **El PDF no se genera:** comprueba que exista `www/lib/html2pdf.bundle.min.js`. Si no, ejecuta `npm run prep`.
- **El título queda tapado por la barra de estado del celular:** es un ajuste de márgenes de pantalla; avísame y lo corregimos en `www/index.html`.
- **Las fotos no se pueden tomar con la cámara:** vuelve a ejecutar `npm run sync` y verifica que `AndroidManifest.xml` tenga el permiso `android.permission.CAMERA`. Elegir fotos de la galería no necesita ese permiso.
- **Los datos se guardan solo dentro de la app:** al desinstalarla se pierden los informes sin exportar.
