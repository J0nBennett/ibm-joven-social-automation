# Templates de Canva

Guia para crear y usar los templates de diseño en Canva.

---

## Templates a crear

### 1. Post de Instagram (1080 x 1080 px)

Usar para: versiculos diarios, anuncios de eventos.

**Estructura sugerida:**

```
+----------------------------------+
|          {{HOOK}}                 |  <- Frase gancho (grande, bold)
|                                  |
|       {{VERSE_TEXT}}             |  <- Texto del versiculo (italica)
|       - {{VERSE_REF}}           |  <- Referencia biblica
|                                  |
|          {{CTA}}                 |  <- Llamado a la accion
|                                  |
|  [Logo IBM Joven]  {{FOOTER}}   |  <- Pie con redes/info
+----------------------------------+
```

### 2. Story de Instagram (1080 x 1920 px)

Usar para: version vertical de versiculos y anuncios.

```
+------------------+
|                  |
|    {{HOOK}}      |  <- Frase gancho
|                  |
|  {{VERSE_TEXT}}  |  <- Versiculo
|  - {{VERSE_REF}} |
|                  |
|    {{CTA}}       |  <- CTA
|                  |
| [Logo] {{FOOTER}}|
+------------------+
```

### 3. Carrusel de fotos (1080 x 1080 px, multi-pagina)

Usar para: fotos del culto/servicio.

**Slide 1 (portada):**

```
+----------------------------------+
|                                  |
|         {{TITULO}}               |  <- Titulo del culto
|                                  |
|  [Foto de portada]               |
|                                  |
|         {{FOOTER}}               |
+----------------------------------+
```

**Slides 2-9 (fotos):**

```
+----------------------------------+
|                                  |
|  [Foto a pantalla completa]      |
|                                  |
|                                  |
+----------------------------------+
```

**Slide final (cierre):**

```
+----------------------------------+
|                                  |
|  {{VERSE_TEXT}}                  |  <- Versiculo sugerido
|  - {{VERSE_REF}}                |
|                                  |
|  {{CTA}}                        |
|                                  |
|  [Logo] {{FOOTER}}              |
+----------------------------------+
```

---

## Placeholders

Campos de texto editables en cada template:

| Placeholder | Que poner | Fuente en el pack | Ejemplo |
|---|---|---|---|
| `{{HOOK}}` | Frase gancho | campo `hook` (del mensaje Telegram) | "Arrancas la semana sin fuerzas?" |
| `{{VERSE_REF}}` | Referencia biblica | `bloques_canva.verse_ref` | "Filipenses 4:13" |
| `{{VERSE_TEXT}}` | Texto del versiculo | `bloques_canva.verse_text` | "Todo lo puedo en Cristo que me fortalece" |
| `{{CTA}}` | Llamado a la accion | campo `cta` (del mensaje Telegram) | "Compartilo con alguien que lo necesite" |
| `{{FOOTER}}` | Info fija | `bloques_canva.footer` | "@ibm_joven" |
| `{{TITULO}}` | Titulo del evento o seccion | `bloques_canva.titulo` | "NOCHE DE JOVENES" |
| `{{SUBTITULO}}` | Fecha/hora/lugar (solo anuncios) | `bloques_canva.subtitulo` | "Sabado 1 de marzo - 20:00 h" |
| `{{CUERPO}}` | Texto adicional (solo anuncios) | `bloques_canva.cuerpo` | Frase clave o info extra |

> En Canva, crear cuadros de texto con estos nombres. Los campos de `bloques_canva` se pegan directamente. Para `{{HOOK}}` y `{{CTA}}`, copiarlos del mensaje de Telegram (son campos separados del pack).

---

## Links a templates

Pegar aqui los links una vez creados (no commitear si contienen tokens de sesion):

```
TEMPLATE_POST_VERSICULO=https://www.canva.com/design/DAHCbkkduC4/ACvj4_ioO4mR7JOAQPHsjA/edit
TEMPLATE_STORY_VERSICULO=https://www.canva.com/design/DAHCb8S17NY/S-doVdGwryMCO8aqwRTblQ/edit
TEMPLATE_POST_ANUNCIO=https://www.canva.com/design/DAHCb1_SdU4/Aa2WuLc9uVUjMJMXbiu1oA/edit
TEMPLATE_STORY_ANUNCIO=https://www.canva.com/design/DAHCdAzm_cw/6qJV2qENs5MUNdS26QNX1w/edit
TEMPLATE_CARRUSEL_FOTOS=https://www.canva.com/design/DAHCdIrkgZM/DanL_9kdQGPnMSZnD_AXng/edit
```

> Estos links se ponen tambien en el nodo PACK_LISTO de cada workflow.

---

## Checklist de diseño

Antes de exportar una pieza, verificar:

- [ ] **Tipografias**: usar las definidas en `brand-kit.md` (maximo 2 fuentes).
- [ ] **Contraste**: el texto se lee claramente sobre el fondo.
- [ ] **Logo IBM Joven**: presente en la pieza.
- [ ] **Margenes**: al menos 60px en todos los bordes (evitar cortes en stories).
- [ ] **Tamaño correcto**: Post = 1080x1080, Story = 1080x1920.
- [ ] **Export PNG**: formato PNG, calidad alta.
- [ ] **Nombre del archivo**: `tipo_fecha.png` (ej: `versiculo_2026-02-24.png`).
- [ ] **Sin errores de ortografia**: revisar antes de exportar.
