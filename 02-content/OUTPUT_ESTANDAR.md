# Output Estándar – Pack Listo para Publicar

Todos los flujos (versículo, anuncio, fotos) producen un JSON con la misma
estructura base. Esto garantiza que el mensaje de Telegram y los textos para
Canva siempre sean predecibles.

## Campos comunes

| Campo              | Tipo     | Descripción                                     | Ejemplo                                  |
|--------------------|----------|-------------------------------------------------|------------------------------------------|
| `hook`             | string   | Frase gancho para captar atención (max 15 palabras) | "Dios pelea tus batallas, solo confía"   |
| `copy_post`        | string   | Texto completo para el caption de Instagram/FB  | Reflexión + versículo + CTA              |
| `copy_story`       | string   | Texto corto para la story (max 40 palabras)     | Hook resumido + CTA rápido               |
| `hashtags`         | string   | Hashtags separados por espacio                  | "#IBMJoven #Devocional #Fe"              |
| `cta`              | string   | Llamada a la acción (max 15 palabras)           | "Comparte con alguien que lo necesita"   |
| `bloques_canva`    | object   | Textos exactos para pegar en template Canva     | Ver detalle abajo                        |
| `links_templates`  | object   | URLs a templates Canva (post / story / carrusel)| Ver detalle abajo                        |
| `assets_links`     | object   | Links a carpeta Drive / fotos / exports         | Ver detalle abajo                        |

## `bloques_canva` (textos para pegar en Canva)

```json
{
  "titulo":    "NOCHE DE JÓVENES",
  "subtitulo": "Viernes 7 de marzo · 20:00 h",
  "cuerpo":    "Ven a compartir una noche de alabanza...",
  "footer":    "Iglesia Bautista Maranata · @ibm_joven",
  "verse_ref": "Filipenses 4:13",
  "verse_text": "Todo lo puedo en Cristo que me fortalece."
}
```

> No todos los campos aplican a todos los flujos.
> - **Versículo:** usa `verse_ref`, `verse_text`, `titulo` (hook), `footer`.
> - **Anuncio:** usa `titulo`, `subtitulo`, `cuerpo`, `footer`.
> - **Fotos:** usa `titulo`, `footer` (el carrusel es visual).

## `links_templates`

```json
{
  "post":     "https://www.canva.com/design/XXXXX/edit",
  "story":    "https://www.canva.com/design/YYYYY/edit",
  "carrusel": "https://www.canva.com/design/ZZZZZ/edit"
}
```

Estos links se configuran una vez en el nodo Set de cada workflow y apuntan a
los templates base de Canva. El operador abre el link, duplica el diseño y
pega los textos de `bloques_canva`.

## `assets_links`

```json
{
  "drive_folder": "https://drive.google.com/drive/folders/XXXXX",
  "fotos":        ["url_foto_1", "url_foto_2"],
  "export_link":  ""
}
```

- `drive_folder`: Carpeta compartida donde se guardan las fotos originales.
- `fotos`: Array de URLs (solo aplica al flujo de fotos-culto).
- `export_link`: Se llena manualmente después de exportar de Canva.

## Ejemplo completo (flujo versículo)

```json
{
  "hook": "Dios pelea tus batallas, solo confía",
  "copy_post": "\"Todo lo puedo en Cristo que me fortalece.\" — Filipenses 4:13\n\nA veces sentimos que no podemos más...",
  "copy_story": "Todo lo puedo en Cristo 💪 ¿Ya leíste el versículo de hoy?",
  "hashtags": "#IBMJoven #VersículoDelDía #Fe #Cristo",
  "cta": "Guarda este post y compártelo con alguien que lo necesita",
  "bloques_canva": {
    "titulo": "VERSÍCULO DEL DÍA",
    "verse_ref": "Filipenses 4:13",
    "verse_text": "Todo lo puedo en Cristo que me fortalece.",
    "footer": "@ibm_joven"
  },
  "links_templates": {
    "post": "https://www.canva.com/design/XXXXX/edit",
    "story": "https://www.canva.com/design/YYYYY/edit"
  },
  "assets_links": {
    "drive_folder": "",
    "fotos": [],
    "export_link": ""
  }
}
```

## Cómo se usa en cada flujo

1. **n8n genera** el JSON con los campos de arriba.
2. **Nodo Set** agrega los `links_templates` (fijos por flujo).
3. **Nodo Telegram** envía un mensaje formateado con el `copy_post`, `hook`,
   links a templates y un checklist rápido.
4. El operador **abre Canva**, duplica el template, pega los `bloques_canva`.
5. Exporta, sube el PNG, y publica con el `copy_post` + `hashtags`.
