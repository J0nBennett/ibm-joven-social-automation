# Guia de operacion

Paso a paso de cada flujo, desde la carga de contenido hasta la publicacion.

---

## Flujo 1: Versiculo diario

**Trigger:** Cron a las 7:00 AM (o ejecucion manual).

| Paso | Quien | Que hace |
|------|-------|----------|
| 1 | **Editor** | Carga una fila en la Sheet con `tipo=versiculo`, datos del versiculo y `estado=pendiente` |
| 2 | n8n (auto) | Lee la fila, envia datos a Gemini, genera copy |
| 3 | n8n (auto) | Arma el PACK_LISTO y lo envia por Telegram |
| 4 | n8n (auto) | Actualiza la Sheet a `estado=listo` |
| 5 | **Editor** | Recibe el pack en Telegram, abre template Canva |
| 6 | **Editor** | Pega los `bloques_canva` (titulo, versiculo, footer) |
| 7 | **Editor** | Exporta PNG (post 1080x1080 + story 1080x1920) |
| 8 | **Editor** | Publica en IG + FB con el `copy_post` y `hashtags` |
| 9 | **Editor** | Marca `estado=publicado` en la Sheet |

**Que llega por Telegram:**
- Hook + Copy post + Copy story
- Hashtags y CTA
- Links a templates Canva (post y story)
- Checklist rapido de publicacion

---

## Flujo 2: Anuncio de evento

**Trigger:** Manual (el editor ejecuta cuando hay un evento nuevo).

| Paso | Quien | Que hace |
|------|-------|----------|
| 1 | **Editor** | Carga fila en Sheet con `tipo=anuncio`, datos del evento y `estado=pendiente` |
| 2 | **Editor** | Ejecuta el workflow manualmente en n8n |
| 3 | n8n | Lee la fila, genera copy + bloques_canva con Gemini |
| 4 | n8n | Envia PACK_LISTO por Telegram |
| 5 | n8n | Actualiza Sheet a `estado=listo` |
| 6 | **Editor** | Abre template Canva de anuncio, pega titulo/subtitulo/cuerpo/footer |
| 7 | **Editor** | Verifica fecha, hora y lugar en el diseño |
| 8 | **Editor** | Exporta PNG y publica |
| 9 | **Editor** | Marca `estado=publicado` en la Sheet |

**Que llega por Telegram:**
- Hook + Copy post + Copy story
- Bloques Canva (titulo, subtitulo, cuerpo, footer)
- Links a templates Canva (post y story)
- Checklist rapido

---

## Flujo 3: Fotos del culto

**Trigger:** Manual (despues de seleccionar las fotos del servicio).

| Paso | Quien | Que hace |
|------|-------|----------|
| 1 | **Editor** | Selecciona las mejores fotos y las sube a la carpeta de Drive |
| 2 | **Editor** | Carga fila en Sheet con `tipo=fotos`, titulo del culto y `estado=pendiente` |
| 3 | **Editor** | Ejecuta el workflow en n8n |
| 4 | n8n | Lee la fila, genera caption + versiculo sugerido con Gemini |
| 5 | n8n | Envia PACK_LISTO por Telegram |
| 6 | n8n | Actualiza Sheet a `estado=listo` |
| 7 | **Editor** | Abre template carrusel en Canva, inserta fotos |
| 8 | **Editor** | Verifica que el versiculo sugerido sea correcto |
| 9 | **Editor** | Exporta cada slide como PNG |
| 10 | **Editor** | Publica carrusel en IG + FB con el caption |
| 11 | **Editor** | Marca `estado=publicado` en la Sheet |

**Que llega por Telegram:**
- Hook + Caption del carrusel
- Versiculo sugerido (verificar que sea real)
- Hashtags y CTA
- Link a template carrusel Canva
- Link a carpeta de fotos en Drive
- Checklist rapido

---

## Output estandar

Los 3 flujos producen un JSON con formato comun. Ver detalle completo en `02-content/OUTPUT_ESTANDAR.md`.

Campos principales: `hook`, `copy_post`, `copy_story`, `hashtags`, `cta`, `bloques_canva`, `links_templates`.

---

## Estados en la Sheet

```
pendiente  →  listo  →  publicado
   ↑            ↑          ↑
 Editor     n8n (auto)   Editor
```

| Estado | Significado | Quien lo cambia |
|--------|------------|-----------------|
| `pendiente` | Fila cargada, esperando procesamiento | Editor |
| `listo` | Pack generado y enviado por Telegram | n8n (automatico) |
| `publicado` | Contenido publicado en redes | Editor/Publicador |

---

## Notas importantes

- **No se publica nada sin revision humana.** El pack se entrega por Telegram, pero la publicacion es manual.
- **Canva es manual.** No usamos API de Canva; el diseño lo hace una persona con templates.
- **El LLM es una ayuda, no un reemplazo.** El copy se revisa y puede editarse.
- **Verificar versiculos.** Especialmente en el flujo de fotos, donde el LLM sugiere el versiculo.
- **Registrar todo en la Sheet.** Cada publicacion queda con estado, timestamp y quien aprobo.
