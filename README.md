# 🏅 Olimpiadas AR — WebAR con MindAR.js

Aplicación de Realidad Aumentada que detecta markers y muestra videos olímpicos de YouTube.

---

## 📁 Estructura del proyecto

```
olimpiadas-ar/
├── index.html          ← App principal
├── targets.mind        ← Archivo de markers compilado (lo generás vos)
└── README.md
```

---

## 🖼️ Paso 1 — Crear los markers

Los markers son imágenes que la cámara va a reconocer.
Necesitás compilarlos en un archivo `.mind` con la herramienta oficial de MindAR.

### ¿Qué imagen usar como marker?
- Imágenes con **muchos detalles, bordes y contraste** funcionan mejor
- Evitá logos simples, fondos planos o patrones repetitivos
- Ejemplo: fotos de atletas olímpicos, el logo de tu evento, imágenes de disciplinas

### Cómo compilar los markers:

1. Ir a: **https://hiukim.github.io/mind-ar-js-doc/tools/compile**
2. Subir las 3 imágenes (una por marker, en orden: 0, 1, 2)
3. Hacer clic en **"Start"**
4. Descargar el archivo `targets.mind`
5. Colocarlo en la raíz del proyecto (junto a `index.html`)

> ⚠️ El orden de las imágenes importa: la primera = marker 0, segunda = marker 1, etc.

---

## 🎬 Paso 2 — Configurar los videos

En `index.html`, buscá la sección `VIDEOS CONFIG` y editá los IDs de YouTube:

```javascript
const VIDEOS = [
  {
    label: "Nombre descriptivo del video",
    youtubeId: "XXXXXXXXXX"   // ← ID que aparece en youtube.com/watch?v=ESTE_ID
  },
  // ...
];
```

Para obtener el ID de un video de YouTube:
- URL: `https://www.youtube.com/watch?v=dQw4w9WgXcQ`
- ID: `dQw4w9WgXcQ`

---

## 🚀 Paso 3 — Deploy (opciones)

### Opción A: GitHub Pages (gratuito, público)

1. Crear repositorio en GitHub
2. Subir `index.html` y `targets.mind`
3. Ir a Settings → Pages → Source: `main` branch
4. Tu app estará en: `https://TU_USUARIO.github.io/NOMBRE_REPO/`

> ⚠️ HTTPS es **obligatorio** para que la cámara funcione en móviles.
> GitHub Pages lo provee automáticamente.

---

### Opción B: Netlify (gratuito, con protección por contraseña en plan Pro)

1. Crear cuenta en https://netlify.com
2. Arrastrar la carpeta del proyecto a la zona de deploy
3. Tu app estará en: `https://nombre-random.netlify.app`

**Para acceso controlado (requiere plan Pro ~$19/mes):**
- Site settings → Access control → Password protection

**Alternativa gratuita para acceso controlado:**
- Compartir la URL solo por WhatsApp/email (URL no indexada = acceso de facto controlado)
- O agregar un PIN en JavaScript (ver abajo)

---

### Opción C: Vercel (gratuito, muy rápido)

1. Instalar Vercel CLI: `npm i -g vercel`
2. Ejecutar `vercel` en la carpeta del proyecto
3. Seguir las instrucciones

---

## 🔒 Acceso controlado con PIN (sin costo)

Si querés que solo usuarios con un código puedan acceder, agregá esto al inicio
del `<script>` en `index.html`:

```javascript
const ACCESS_PIN = "1924";  // Año de los primeros JJ.OO. modernos

const entered = prompt("Ingresá el código de acceso:");
if (entered !== ACCESS_PIN) {
  document.body.innerHTML = "<h2 style='color:white;text-align:center;padding:2rem'>Acceso no autorizado</h2>";
}
```

---

## 📱 Cómo usar la app

1. Abrir la URL en el celular (Chrome en Android, Safari en iOS)
2. Tocar **"Activar cámara AR"**
3. Aceptar el permiso de cámara
4. Apuntar a uno de los markers impresos o en pantalla
5. Cuando aparezca el overlay azul, **tocar la pantalla**
6. El video de YouTube se reproduce encima de la cámara

---

## 🛠️ Agregar más markers

1. Añadir más imágenes al compilar `targets.mind`
2. En `index.html`:
   - Agregar entrada al array `VIDEOS`
   - Copiar y pegar un bloque `<a-entity mindar-image-target>` con el índice correcto

---

## ⚠️ Notas técnicas importantes

- **HTTPS obligatorio**: la API de cámara solo funciona en HTTPS (o localhost)
- **Primer carga lenta**: MindAR tarda 3-8 segundos en inicializar
- **YouTube en AR**: los videos se reproducen en un overlay 2D, no pegados al marker en 3D (limitación de YouTube iframe en WebGL)
- **iOS**: Safari 14.5+ es compatible; en versiones anteriores puede fallar
- **targets.mind**: sin este archivo la app no funciona; es el más importante

---

## 📚 Recursos

- MindAR.js docs: https://hiukim.github.io/mind-ar-js-doc/
- Compilador de markers: https://hiukim.github.io/mind-ar-js-doc/tools/compile
- A-Frame docs: https://aframe.io/docs/
