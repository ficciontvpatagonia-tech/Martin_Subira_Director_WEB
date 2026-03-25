# CLAUDE.md — Proyecto martin-subira-web

Archivo de contexto permanente. Claude Code lo lee automáticamente al iniciar cada sesión.

---

## Proyecto

Sitio web personal de **Martín Subirá** — director de cine, documentalista y director de fotografía argentino.

- **Repo principal:** https://github.com/ficciontvpatagonia-tech/Martin_Subira_Director_WEB
- **Repo secundario:** https://github.com/martinsubira/cine
- **URL principal:** https://ficciontvpatagonia-tech.github.io/Martin_Subira_Director_WEB/
- **URL secundaria:** https://martinsubira.github.io/cine/
- **Archivos:** un solo `index.html` con todo el CSS y JS inline. Carpeta `images/` para imágenes.

## Cuentas GitHub

- `ficciontvpatagonia-tech` — cuenta de la productora (repo original)
- `martinsubira` — cuenta nueva para URL más limpia

Para pushear a los dos repos usar tokens explícitos (las credenciales no comparten bien entre cuentas):
```bash
TOKEN=$(gh auth token --user ficciontvpatagonia-tech)
git push https://ficciontvpatagonia-tech:${TOKEN}@github.com/ficciontvpatagonia-tech/Martin_Subira_Director_WEB.git main

TOKEN2=$(gh auth token --user martinsubira)
git push https://martinsubira:${TOKEN2}@github.com/martinsubira/cine.git main
```

## Auto-deploy configurado

Hook en `.claude/settings.json` del proyecto: después de cada Edit/Write, hace commit y push automático. **Solo activo desde la segunda sesión en adelante** (el watcher no toma archivos nuevos en la sesma sesión que se crean).

## Estructura del sitio

- Nav fija con scroll: logo, links, botones de idioma (ES/EN/PT/中文)
- Secciones: Hero, About, Films (con modal de video/playlist), Galería BioAnimal, Press, Blog, Contact
- Paleta: arena/piedra patagónica (`--bg: #dbd3c6`), acento verde bosque (`--accent: #2c4a1e`)
- Fuentes: Syne (títulos), Manrope (texto), Instrument Serif (itálicas)

## Sistema de traducción

Usa Google Translate JS widget con botones custom (ES/EN/PT/中文).
- **No usar** `translate="no"` en el tag `<html>` — bloquea la traducción
- CSS y MutationObserver ocultan el banner nativo de Google Translate
- La función `setLang()` activa la traducción via `.goog-te-combo`

## Modal de video

- `data-video="URL"` → reproduce video único
- `data-playlist='[{...}]'` → muestra grilla de episodios
  - `{"title":"Ep. 01","id":"YOUTUBE_ID"}` → episodio activo
  - `{"title":"Ep. 02","coming":true}` → próximamente
  - `{"title":"Trailer","url":"https://player.vimeo.com/video/ID","thumb":"images/..."}` → Vimeo con thumb custom
- `data-gallery='["images/foto1.jpg",...]'` → galería de fotos debajo de la playlist en el modal

## Filmografía — estado actual

### Rescatistas: Brigada de montaña
- Trailer: Vimeo 50413399
- Ep. 01: YouTube `6f69bJf4FzU`
- Ep. 02: YouTube `DMLBCPbrCZw`
- Ep. 03: YouTube `szMUMhy7HVg`
- Eps. 04-08: coming soon

### Bio Animal (Canal Encuentro)
- 12 capítulos — todos coming soon (agregar IDs de YouTube cuando estén disponibles)
- Galería de 20 fotos integrada en el modal

### La dignidad de los nadies
- Imagen: `images/lerner-dignidad-nadies.jpg`
- Sin video (Martín fue editor, no director)

## Imágenes

- Hero: `images/patagonia-nevada-atardecer.jpg` (mejorada con ImageMagick desde `_MG_5826.JPG`)
- Para mejorar imágenes: `magick input.jpg -auto-gamma -sigmoidal-contrast 4,50% -modulate 100,125,100 -unsharp 0x0.8+1.2+0.02 -quality 88 output.jpg`

## Personas

- **Martín Subirá** — dueño del sitio, director de cine
- **Tincho (Tincho76880)** — colaborador del proyecto, tiene acceso por Telegram. Reporta bugs mobile. Vinculado a ficciontvpatagonia@gmail.com.
