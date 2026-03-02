# Guia de inicio rapido

## Requisitos

- Cuenta de Google (para Google Sheets)
- Cuenta de Canva gratuita
- Cuenta de Telegram + bot creado con @BotFather
- Acceso a n8n (cloud o self-host)
- API Key de Gemini (gratis en aistudio.google.com)

---

## Paso 1: Configurar variables de entorno

Copiar `.env.example` a `.env` y completar los valores:

```bash
cp .env.example .env
```

Variables necesarias:

| Variable | Donde obtenerla |
|----------|----------------|
| `TELEGRAM_BOT_TOKEN` | @BotFather en Telegram |
| `TELEGRAM_CHAT_ID` | Ver seccion "Configurar Telegram" abajo |
| `GOOGLE_SHEETS_ID` | URL de tu Sheet: `docs.google.com/spreadsheets/d/{ID}/edit` |
| `GOOGLE_SHEETS_TAB` | Nombre de la hoja (ej: "Hoja 1") |
| `GEMINI_API_KEY` | aistudio.google.com > Get API Key |

---

## Paso 2: Preparar Google Sheet

1. Crear una Google Sheet nueva.
2. Importar `02-content/sheets/content_db_template.csv` (Archivo > Importar > Subir).
3. Verificar que las columnas coincidan exactamente (ver `02-content/sheets/SHEETS_SETUP.md`).
4. Copiar el ID de la Sheet desde la URL.
5. En n8n, la Sheet se conecta via OAuth2 (te pedira login de Google al configurar la credencial).

### Columnas de la Sheet

```
id | tipo | fecha_publicacion | titulo | texto_base | verse_ref | verse_text |
copy_generado | hashtags | cta | hook | canva_template_post | canva_template_story |
imagen_export_link | estado | aprobado_por | timestamp
```

### Estados validos

| Estado | Significado |
|--------|------------|
| `pendiente` | Fila cargada, esperando procesamiento |
| `listo` | n8n genero el copy y envio el pack por Telegram |
| `publicado` | Contenido publicado en redes |

---

## Paso 3: Configurar Telegram

### Crear el bot

1. Abrir Telegram y buscar **@BotFather**.
2. Enviar `/newbot` y seguir los pasos.
3. Copiar el **token** (formato: `123456:ABC-DEF1234ghIkl-zyx57W2v1u123ew11`).

### Obtener el chat_id

1. Crear un grupo de Telegram (ej: "IBM Joven – Packs").
2. Agregar el bot al grupo.
3. Enviar un mensaje en el grupo.
4. Visitar: `https://api.telegram.org/bot{TU_TOKEN}/getUpdates`
5. Buscar `"chat": {"id": -100XXXXXXXXXX}`. Ese numero es el `chat_id`.

---

## Paso 4: Configurar n8n

### Opcion A: n8n Cloud

1. Crear cuenta en [n8n.io](https://n8n.io).
2. Importar los 3 workflows JSON desde `01-n8n/workflows/`.
3. Configurar credenciales en **Settings > Credentials**:
   - **Google Sheets OAuth2**: login con tu cuenta de Google.
   - **Gemini API Key**: crear credencial tipo "Query Auth" con `name=key`, `value=tu_api_key`.
   - **Telegram Bot**: pegar el bot token.

### Opcion B: Self-host con Docker Compose (recomendado)

```bash
docker-compose up -d
```

Esto levanta n8n con las variables de `.env`, timezone de Argentina y volumen persistente.

> Alternativa sin Docker Compose:
> ```bash
> mkdir -p ~/n8n-data
> docker run -d \
>   --name n8n \
>   -p 5678:5678 \
>   -v ~/n8n-data:/home/node/.n8n \
>   --env-file .env \
>   n8nio/n8n:1.76.1
> ```

Abrir `http://localhost:5678` e importar los workflows.

> **Importante:** Cambiar `N8N_BASIC_AUTH_PASSWORD` en `.env` antes de deployar. No usar el valor por defecto.

---

## Paso 5: Importar workflows

1. Abrir n8n en el navegador.
2. Click en **"+"** > **Import from file**.
3. Importar cada JSON:
   - `versiculo-diario.json` – Versiculo del dia (cron 7am + manual)
   - `anuncio-evento.json` – Anuncios de eventos (manual)
   - `fotos-culto-pack.json` – Fotos del culto (manual)
4. En cada workflow, abrir los nodos y conectar las credenciales:
   - Nodos "Leer Sheet" y "Actualizar Sheet" → Google Sheets OAuth2
   - Nodo "Gemini" → Query Auth (name=key, value=API key)
   - Nodo "Enviar Pack Telegram" → Telegram Bot Token
5. Activar el workflow de versiculo (tiene cron). Los otros 2 son manuales.

---

## Paso 6: Crear templates en Canva

1. Crear 3 templates en Canva (ver `03-design/canva/templates.md`):
   - Post 1080x1080 (versiculo, anuncio)
   - Story 1080x1920 (versiculo, anuncio)
   - Carrusel 1080x1080 multi-pagina (fotos)
2. Copiar los links de edicion de cada template.
3. Actualizar los links en el nodo PACK_LISTO de cada workflow.

---

## Paso 7: Probar

1. Cargar una fila de prueba en la Sheet con `tipo=versiculo`, `estado=pendiente`.
2. Ejecutar el workflow manualmente desde n8n (boton "Execute Workflow").
3. Verificar que llega el pack a Telegram.
4. Verificar que la Sheet se actualizo a `estado=listo`.

---

## Siguiente paso

Lee `OPERACION.md` para entender el flujo diario de trabajo.
