# Configuracion de Google Sheets

La Google Sheet es la base de datos central. Cada fila es un contenido a publicar.

## Como crear la Sheet

1. Ir a [sheets.google.com](https://sheets.google.com) y crear una nueva.
2. Importar `content_db_template.csv` (Archivo > Importar > Subir > Reemplazar hoja).
3. Renombrar la hoja a "Hoja 1" (o el nombre que pongas en `GOOGLE_SHEETS_TAB`).
4. Copiar el ID de la URL: `docs.google.com/spreadsheets/d/{ESTE_ES_EL_ID}/edit`.

## Columnas

| Columna | Tipo | Quien la llena | Descripcion |
|---------|------|----------------|-------------|
| `id` | numero | Editor | Identificador unico (1, 2, 3...) |
| `tipo` | texto | Editor | `versiculo`, `anuncio` o `fotos` |
| `fecha_publicacion` | fecha | Editor | Fecha objetivo de publicacion (YYYY-MM-DD) |
| `titulo` | texto | Editor | Titulo descriptivo del contenido |
| `texto_base` | texto | Editor | Contexto o descripcion para el LLM |
| `verse_ref` | texto | Editor | Referencia biblica (ej: Filipenses 4:13). Opcional para fotos |
| `verse_text` | texto | Editor | Texto del versiculo. Opcional para fotos |
| `copy_generado` | texto | n8n | Copy generado por el LLM |
| `hashtags` | texto | n8n | Hashtags generados |
| `cta` | texto | n8n | Call to action generado |
| `hook` | texto | n8n | Frase gancho generada |
| `canva_template_post` | texto | Editor | Link al template Canva del post (opcional) |
| `canva_template_story` | texto | Editor | Link al template Canva de la story (opcional) |
| `imagen_export_link` | texto | Editor | Link al PNG exportado (opcional) |
| `estado` | texto | Editor/n8n | `pendiente` → `listo` → `publicado` |
| `aprobado_por` | texto | Editor | Nombre de quien reviso/aprobo |
| `timestamp` | fecha-hora | n8n/Editor | Fecha-hora de la ultima actualizacion |

## Estados

```
pendiente  ──n8n──>  listo  ──humano──>  publicado
```

- **pendiente**: el editor cargo la fila, n8n aun no la proceso.
- **listo**: n8n genero el copy y envio el pack por Telegram.
- **publicado**: el contenido fue publicado en redes sociales.

## Tipos validos

| Tipo | Workflow que lo lee | Trigger |
|------|-------------------|---------|
| `versiculo` | versiculo-diario.json | Cron 7am o manual |
| `anuncio` | anuncio-evento.json | Manual |
| `fotos` | fotos-culto-pack.json | Manual |

## Ejemplo de filas

| id | tipo | fecha_publicacion | titulo | texto_base | verse_ref | verse_text | estado |
|----|------|-------------------|--------|------------|-----------|------------|--------|
| 1 | versiculo | 2026-02-24 | Versiculo del lunes | Empezar la semana con fe | Filipenses 4:13 | Todo lo puedo en Cristo que me fortalece. | pendiente |
| 2 | anuncio | 2026-03-01 | Noche de jovenes | Encuentro primer sabado de marzo. Salon principal, 20hs. | Salmos 133:1 | Miren que bueno es que los hermanos convivan en armonia. | pendiente |
| 3 | fotos | 2026-02-23 | Fotos culto dominical | Resumen del culto de alabanza del domingo. | | | pendiente |

## Notas

- No renombrar ni reordenar las columnas.
- Las columnas que llena n8n (`copy_generado`, `hashtags`, etc.) se dejan vacias al cargar la fila.
- El campo `verse_ref` y `verse_text` son opcionales para tipo `fotos` (el LLM sugiere uno).
- Mantener el ID unico y secuencial.
