# Guia de inicio rapido

## Requisitos minimos

- Cuenta de Google (para Google Sheets)
- Cuenta de Canva gratuita
- Cuenta de Telegram + un bot creado con @BotFather
- Acceso a n8n (cloud o self-host)
- Opcional: clave de API de un LLM (OpenAI, Gemini, etc.)

---

## Opcion 1: n8n Cloud (mas simple)

1. Crear cuenta gratuita en [n8n.io](https://n8n.io).
2. Ir a **Settings > Import Workflow**.
3. Subir los archivos JSON de `01-n8n/workflows/`.
4. Configurar las credenciales en **Settings > Credentials** (ver `01-n8n/credentials/credentials.example.md`).
5. Activar los workflows.

> Con el plan gratuito de n8n cloud tenes un limite de ejecuciones. Para IBM Joven deberia ser suficiente (pocas publicaciones diarias).

## Opcion 2: Self-host con Docker (mas control)

Si preferis tener n8n corriendo en tu propia maquina o servidor:

```bash
# 1. Crear carpeta de datos
mkdir -p ~/n8n-data

# 2. Levantar n8n con Docker
docker run -d \
  --name n8n \
  -p 5678:5678 \
  -v ~/n8n-data:/home/node/.n8n \
  --env-file .env \
  n8nio/n8n

# 3. Abrir http://localhost:5678 en el navegador
```

Crear un archivo `.env` en la raiz (ver `.env.example` si existe) con las variables necesarias:

```
N8N_BASIC_AUTH_ACTIVE=true
N8N_BASIC_AUTH_USER=admin
N8N_BASIC_AUTH_PASSWORD=tu_password_seguro
```

> Nunca commitear el archivo `.env`. Ya esta en `.gitignore`.

---

## Importar workflows JSON

1. Abrir n8n en el navegador.
2. Click en **"+"** para crear un nuevo workflow.
3. Click en los **3 puntos** (menu) > **Import from file**.
4. Seleccionar el JSON correspondiente de `01-n8n/workflows/`:
   - `versiculo-diario.json` - Flujo de versiculo del dia
   - `anuncio-evento.json` - Flujo de anuncios de eventos
   - `fotos-culto-pack.json` - Flujo de pack de fotos del culto
5. Revisar que los nodos esten correctos y conectar las credenciales.

---

## Preparar Google Sheet / CSV

1. Crear una Google Sheet nueva o importar el archivo `02-content/sheets/content_db_template.csv`.
2. Respetar las columnas exactas del template (no renombrar ni reordenar).
3. Compartir la Sheet con la cuenta de servicio de Google que uses en n8n (si aplica).
4. Copiar el ID de la Sheet (esta en la URL: `docs.google.com/spreadsheets/d/{SHEET_ID}/edit`).
5. Usar ese ID en los nodos de Google Sheets dentro de n8n.

> Si preferis trabajar solo con CSV, podes usarlo directamente con nodos de lectura de archivo en n8n.

---

## Configurar Telegram (bot + chat_id)

### Crear el bot

1. Abrir Telegram y buscar **@BotFather**.
2. Enviar `/newbot` y seguir los pasos.
3. Copiar el **token** que te da BotFather (formato: `123456:ABC-DEF1234ghIkl-zyx57W2v1u123ew11`).
4. **No pegar el token en ningun archivo del repo.** Guardarlo en las credenciales de n8n o en variables de entorno.

### Obtener el chat_id

1. Crear un grupo de Telegram para aprobaciones (ej: "IBM Joven - Aprobaciones").
2. Agregar el bot al grupo.
3. Enviar un mensaje en el grupo.
4. Visitar `https://api.telegram.org/bot{TU_TOKEN}/getUpdates` (reemplazar `{TU_TOKEN}`).
5. Buscar el campo `"chat": {"id": -100XXXXXXXXXX}`. Ese numero negativo es el `chat_id`.
6. Guardar el `chat_id` en n8n junto con el token del bot.

### Uso en los workflows

Los workflows envian un mensaje al grupo de Telegram con el contenido generado. El aprobador responde "ok" o sugiere cambios. Solo despues de la aprobacion el flujo continua hacia la publicacion.

---

## Siguiente paso

Leete `OPERACION.md` para entender el flujo diario de trabajo.
