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

| Placeholder | Que poner | Ejemplo |
|---|---|---|
| `{{HOOK}}` | Frase gancho (del campo `hook`) | "Arrancas la semana sin fuerzas?" |
| `{{VERSE_REF}}` | Referencia biblica | "Filipenses 4:13" |
| `{{VERSE_TEXT}}` | Texto del versiculo | "Todo lo puedo en Cristo que me fortalece" |
| `{{CTA}}` | Llamado a la accion | "Compartilo con alguien que lo necesite" |
| `{{FOOTER}}` | Info fija | "@ibm_joven" |
| `{{TITULO}}` | Titulo del evento o seccion | "NOCHE DE JOVENES" |
| `{{SUBTITULO}}` | Fecha/hora/lugar (solo anuncios) | "Sabado 1 de marzo - 20:00 h" |
| `{{CUERPO}}` | Texto adicional (solo anuncios) | Frase clave o info extra |

> En Canva, crear cuadros de texto con estos nombres. Al usar el template, reemplazar con el contenido real de `bloques_canva`.

---

## Links a templates

Pegar aqui los links una vez creados (no commitear si contienen tokens de sesion):

```
TEMPLATE_POST_VERSICULO=https://www.canva.com/design/XXXXX/edit
TEMPLATE_STORY_VERSICULO=https://www.canva.com/design/XXXXX/edit
TEMPLATE_POST_ANUNCIO=https://www.canva.com/design/XXXXX/edit
TEMPLATE_STORY_ANUNCIO=https://www.canva.com/design/XXXXX/edit
TEMPLATE_CARRUSEL_FOTOS=https://www.canva.com/design/XXXXX/edit
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
