# CHANGELOG — Kibonsai · v1.8 — 2026-06-29

## v1.8 — PWA: app instalable + recordatorios con notificación

Kibonsai pasa de "página web" a **app instalable en el teléfono**.

### Añadido
- **Instalable (PWA)**: manifest + ícono propio (bonsái moyogi sobre fondo volcánico) +
  service worker. El usuario hace “Agregar a inicio” y queda con ícono, pantalla completa
  (sin barra del navegador) y color de marca.
- **Funciona offline**: el service worker cachea la app; abre sin internet.
- **Recordatorios con notificación del sistema**: botón “Activar recordatorios” en Ajustes.
  Al abrir la app, si hay árboles que toca revisar, dispara una notificación
  (“Tenés N árboles que toca revisar”). Lleva a observar — nunca ordena trabajo.
- Botón **“Instalar app”** en Ajustes (Android prompt nativo; iPhone muestra instrucciones).
- Soporte de **safe-area** para el notch del iPhone en modo standalone.

### Nota honesta sobre el push
- Esto es **Nivel 1**: notificación local cuando abrís la app (sin backend, gratis).
- El push que llega con la **app cerrada** (Nivel 2) requiere un servidor con llaves VAPID;
  se agrega cuando quieras avisos masivos a tu comunidad. En iPhone, además, exige que el
  usuario haya hecho “Agregar a inicio”.

### Validación
0 errores. manifest JSON válido, sw.js sin errores de sintaxis, head con manifest/icons/
theme-color, botones de instalar y notificaciones, y todo lo previo intacto.

---

# Cómo subir la v1.8 a Vercel (ahora son varios archivos)

La PWA necesita **7 archivos en la raíz del repo** (antes era solo `index.html`):

1. `index.html`  (reemplaza el actual)
2. `manifest.webmanifest`
3. `sw.js`
4. `icon-192.png`
5. `icon-512.png`
6. `icon-maskable-512.png`
7. `apple-touch-icon.png`

Pasos en GitHub (repo `kibonsai`):
1. **Add file → Upload files**
2. Arrastrá los **7 archivos** juntos (reemplazá el index.html viejo)
3. **Commit changes** (ej. mensaje: “v1.8 — PWA instalable + recordatorios”)
4. Vercel redeploya solo (~30s). Misma URL: kibonsai.vercel.app

Probar en el celular:
- Abrí kibonsai.vercel.app → **Compartir → Agregar a inicio** (iPhone) o menú → **Instalar app** (Android).
- Abrí Kibonsai desde el ícono nuevo (ya sin barra del navegador).
- En Ajustes → **Activar recordatorios** y aceptá el permiso.
