# oraculodelpulpo
Pulpo con poderes para predecir el futuro

# 🔮 El Oráculo del Pulpo — Deploy en GitHub Pages

## Estructura de archivos requerida
```
tu-repo/
├── index.html          ✅ (el archivo principal)
├── sw.js               ✅ (service worker)
├── manifest.json       ✅ (manifiesto PWA)
├── icon-192x192.png    ⚠️  (generar desde icon-source.svg)
├── icon-512x512.png    ⚠️  (generar desde icon-source.svg)
└── icon-source.svg     (solo referencia, no requerido en producción)
```

---

## PASO 1: Generar los íconos PNG

### Opción A — Inkscape (gratis)
1. Abre `icon-source.svg` en Inkscape
2. Archivo → Exportar PNG
3. Exportar en 192×192 px → guardar como `icon-192x192.png`
4. Repetir en 512×512 px → guardar como `icon-512x512.png`

### Opción B — Online (más rápido)
1. Ve a https://svgtopng.com o https://cloudconvert.com/svg-to-png
2. Sube `icon-source.svg`
3. Configura dimensión 192×192 → descarga como `icon-192x192.png`
4. Repite con 512×512 → descarga como `icon-512x512.png`

### Opción C — Node.js (si tienes npm)
```bash
npm install sharp
node -e "
  const sharp = require('sharp');
  const fs = require('fs');
  const svg = fs.readFileSync('icon-source.svg');
  sharp(svg).resize(192,192).png().toFile('icon-192x192.png', ()=>console.log('192 listo'));
  sharp(svg).resize(512,512).png().toFile('icon-512x512.png', ()=>console.log('512 listo'));
"
```

---

## PASO 2: Crear el repositorio en GitHub

```bash
# Si ya tienes git instalado:
git init
git add .
git commit -m "feat: El Oráculo del Pulpo PWA v1.0"
git branch -M main
git remote add origin https://github.com/TU-USUARIO/TU-REPO.git
git push -u origin main
```

---

## PASO 3: Activar GitHub Pages

1. Ve a tu repositorio en GitHub
2. Entra a **Settings → Pages**
3. En **Source** selecciona: `Deploy from a branch`
4. En **Branch** selecciona: `main` y carpeta `/root`
5. Haz clic en **Save**

Tu app estará disponible en:
`https://TU-USUARIO.github.io/TU-REPO/`

---

## PASO 4: Instalar como PWA en móvil

### Android (Chrome)
- Abre la URL en Chrome
- Toca el menú (⋮) → **"Agregar a pantalla de inicio"**

### iOS (Safari)
- Abre la URL en Safari
- Toca el botón compartir (□↑) → **"Agregar a pantalla de inicio"**

---

## Notas técnicas

| Característica | Detalle |
|---|---|
| Modelo predictivo | ELO rating + Distribución de Poisson |
| Offline | ✅ Service Worker cache-first |
| Instalable | ✅ PWA compliant |
| Framework | React 18 (UMD, sin bundler) |
| Fuentes | Cinzel Decorative + Cinzel + Inter |
| Banderas | FlagCDN (con cache offline) |

---

## Actualizar el Service Worker

Cada vez que actualices la app, cambia el número de versión en `sw.js`:
```js
const CACHE_NAME = 'oraculo-pulpo-v1.0.1'; // incrementar versión
```
Esto forzará a los usuarios a recibir la versión nueva.
