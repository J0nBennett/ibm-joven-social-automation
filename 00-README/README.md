# IBM Joven – Automatizacion de Redes Sociales

Repositorio de automatizaciones para las redes sociales de **IBM Joven** (Iglesia Bautista Maranata – Ministerio Joven).

## Vision

Generar un **pack listo para publicar** (imagen + copy) para Instagram/Facebook con el minimo esfuerzo manual. La IA genera los textos, n8n orquesta el flujo, y Telegram entrega el pack al equipo.

## Que resuelve

| Flujo | Frecuencia | Output |
|-------|-----------|--------|
| Versiculo diario | Diario (cron 7am) | Post + Story |
| Anuncio de evento | Segun necesidad (manual) | Post + Story |
| Fotos del culto | Post-servicio (manual) | Carrusel + Caption |

## Filosofia: 90% automatico + revision humana

Nada se publica sin que una persona lo revise. La automatizacion genera textos, arma plantillas y entrega el pack por Telegram. El humano abre Canva, pega los textos, revisa, exporta y publica.

## Stack

| Herramienta | Funcion | Costo |
|---|---|---|
| **n8n** | Orquestador de flujos | Gratis (self-host) o plan free cloud |
| **Canva** | Diseño con templates (sin API) | Gratis (plan basico) |
| **Google Sheets** | Base de contenidos + log de estados | Gratis |
| **Telegram** | Entrega del pack listo al equipo | Gratis |
| **Gemini Flash** | Generacion de copy y hashtags | Gratis (tier gratuito) |

## Mapa de carpetas

```
ibm-joven-social-automation/
├── .env.example              # Variables de entorno (plantilla)
├── .gitignore
├── 00-README/
│   ├── README.md             # Este archivo
│   ├── QUICKSTART.md         # Como empezar desde cero
│   └── OPERACION.md          # Paso a paso por cada flujo
├── 01-n8n/
│   ├── workflows/
│   │   ├── versiculo-diario.json
│   │   ├── anuncio-evento.json
│   │   └── fotos-culto-pack.json
│   └── credentials/
│       └── credentials.example.md
├── 02-content/
│   ├── OUTPUT_ESTANDAR.md    # Formato JSON comun de los 3 flujos
│   ├── sheets/
│   │   ├── content_db_template.csv
│   │   └── SHEETS_SETUP.md   # Como configurar la Google Sheet
│   └── prompts/
│       ├── prompt_versiculo.md
│       ├── prompt_anuncio.md
│       └── prompt_caption_fotos.md
├── 03-design/
│   └── canva/
│       ├── templates.md      # Specs de templates Canva
│       ├── brand-kit.md      # Identidad visual
│       └── exports/          # PNGs exportados (no versionados)
├── 04-ops/
│   └── checklists/
│       ├── checklist_publicacion.md
│       └── checklist_aprobacion.md
└── 05-security/
    └── safe_ai_rules.md
```

## Como funciona cada flujo

Todos los flujos siguen el mismo patron:

```
Sheet (pendiente) → n8n → Gemini (genera copy) → PACK_LISTO → Telegram → Sheet (listo)
```

El output es un JSON estandarizado (ver `02-content/OUTPUT_ESTANDAR.md`) con:
- `hook`, `copy_post`, `copy_story`, `hashtags`, `cta`
- `bloques_canva` (textos exactos para pegar en Canva)
- `links_templates` (URLs a los templates de Canva)

## Reglas del repositorio

- **Nunca commitear tokens, passwords ni claves de API.** Usar `.env`.
- Los workflows de n8n se exportan como JSON y se versionan normalmente.
- Los exports de Canva (PNG/JPG) no se versionan (ver `.gitignore`).
- Si modificas un prompt, probalo al menos 3 veces antes de commitear.
- Toda publicacion pasa por revision humana. Sin excepciones.

## Empezar

1. Lee `QUICKSTART.md` para configurar todo desde cero.
2. Lee `OPERACION.md` para entender el flujo diario.
3. Lee `OUTPUT_ESTANDAR.md` para entender el formato de salida.
