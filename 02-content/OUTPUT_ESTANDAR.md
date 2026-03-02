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
| `link_template_post` | string | URL al template Canva de post                 | `https://www.canva.com/design/XXX/edit`  |
| `link_template_story`| string | URL al template Canva de story                | `https://www.canva.com/design/YYY/edit`  |
| `link_template_carrusel`| string | URL al template Canva de carrusel (solo fotos)| `https://www.canva.com/design/ZZZ/edit`|
| `drive_folder`     | string   | URL a carpeta Drive con fotos (solo fotos)      | `https://drive.google.com/drive/folders/XXX` |

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

## Links a templates (campos planos)

En el nodo PACK_LISTO, los links se configuran como campos planos (no anidados):

```
link_template_post      → URL del template de post en Canva
link_template_story     → URL del template de story en Canva
link_template_carrusel  → URL del template de carrusel en Canva (solo flujo fotos)
drive_folder            → URL de carpeta Google Drive con fotos (solo flujo fotos)
```

Estos links se configuran una vez en el nodo Set de cada workflow y apuntan a
los templates base de Canva. El operador abre el link, duplica el diseño y
pega los textos de `bloques_canva`.

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
  "link_template_post": "https://www.canva.com/design/XXXXX/edit",
  "link_template_story": "https://www.canva.com/design/YYYYY/edit"
}
```

## Cómo se usa en cada flujo

1. **n8n genera** el JSON con los campos de arriba.
2. **Nodo Set** agrega los `link_template_post`/`link_template_story` (fijos por flujo).
3. **Nodo Telegram** envía un mensaje formateado con el `copy_post`, `hook`,
   links a templates y un checklist rápido.
4. El operador **abre Canva**, duplica el template, pega los `bloques_canva`.
5. Exporta, sube el PNG, y publica con el `copy_post` + `hashtags`.
