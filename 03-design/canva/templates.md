# Templates de Canva

Guia para crear y usar los templates de diseño en Canva.

---

## Templates a crear

### 1. Post de Instagram (1080 x 1080 px)

Usar para: versiculos diarios, anuncios de eventos, fotos del culto.

**Estructura sugerida del template:**

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

Usar para: version vertical de los mismos contenidos.

**Estructura sugerida del template:**

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

---

## Placeholders

Estos son los campos de texto editables que debes crear en cada template de Canva:

| Placeholder | Que poner | Ejemplo |
|---|---|---|
| `{{HOOK}}` | Frase gancho generada por el LLM | "Arrancas la semana sin fuerzas?" |
| `{{VERSE_REF}}` | Referencia biblica | "Filipenses 4:13" |
| `{{VERSE_TEXT}}` | Texto del versiculo | "Todo lo puedo en Cristo que me fortalece" |
| `{{CTA}}` | Llamado a la accion | "Compartilo con alguien que lo necesite" |
| `{{FOOTER}}` | Info fija (redes, horarios) | "@ibmjoven - Domingos 10hs" |

> En Canva, simplemente crear cuadros de texto con estos nombres como placeholder. Al usar el template, reemplazar el texto con el contenido real.

---

## Links a templates

Pegar aqui los links de los templates creados en Canva (no commitear si contienen tokens de sesion):

```
TEMPLATE_POST_URL=https://www.canva.com/design/XXXXX/edit
TEMPLATE_STORY_URL=https://www.canva.com/design/XXXXX/edit
```

> Estos links son de edicion. Solo compartirlos con el equipo de diseño.

---

## Checklist de diseño

Antes de exportar una pieza, verificar:

- [ ] **Tipografias**: usar las definidas en `brand-kit.md` (maximo 2 fuentes).
- [ ] **Contraste**: el texto debe leerse claramente sobre el fondo.
- [ ] **Logo IBM Joven**: presente en la pieza (tamaño discreto, esquina inferior).
- [ ] **Margenes**: dejar al menos 60px de margen en todos los bordes (evitar cortes en stories).
- [ ] **Tamaño correcto**: Post = 1080x1080, Story = 1080x1920.
- [ ] **Export PNG**: exportar en formato PNG, calidad alta.
- [ ] **Nombre del archivo**: usar formato `tipo_fecha.png` (ej: `versiculo_2026-02-24.png`).
- [ ] **Sin errores de ortografia**: revisar antes de exportar.
