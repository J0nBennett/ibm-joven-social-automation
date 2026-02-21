# Credenciales necesarias

Lista de credenciales que necesitas configurar para que los workflows funcionen. **Nunca guardes tokens ni passwords en archivos del repositorio.**

---

## Credenciales tipicas

| Servicio | Tipo de credencial | Donde obtenerla |
|----------|-------------------|-----------------|
| **Telegram Bot** | Bot Token | Crear bot con @BotFather en Telegram |
| **Telegram** | Chat ID del grupo | Ver instrucciones en `QUICKSTART.md` |
| **Google Sheets** | OAuth2 o Service Account | Google Cloud Console > APIs & Services > Credentials |
| **LLM (OpenAI)** | API Key | platform.openai.com > API Keys |
| **LLM (Gemini)** | API Key | aistudio.google.com > API Keys |

---

## Donde guardar las credenciales

### En n8n Cloud

1. Ir a **Settings > Credentials**.
2. Agregar una nueva credencial para cada servicio.
3. n8n las encripta y las guarda internamente. No necesitas hacer nada mas.

### En n8n Self-Host

Opcion A: Configurar directamente en la UI de n8n (igual que cloud).

Opcion B: Usar variables de entorno en el archivo `.env`:

```env
# Telegram
TELEGRAM_BOT_TOKEN=tu_token_aqui
TELEGRAM_CHAT_ID=tu_chat_id_aqui

# Google (Service Account)
GOOGLE_SERVICE_ACCOUNT_EMAIL=tu_email@proyecto.iam.gserviceaccount.com
GOOGLE_PRIVATE_KEY=tu_private_key_aqui
GOOGLE_SHEET_ID=id_de_la_sheet

# LLM
OPENAI_API_KEY=tu_api_key_aqui
# o
GEMINI_API_KEY=tu_api_key_aqui
```

> El archivo `.env` ya esta en `.gitignore`. Nunca lo subas al repositorio.

---

## Reglas de seguridad para credenciales

1. **Nunca commitear tokens, API keys ni passwords.** Si lo hiciste por accidente, rotalos inmediatamente.
2. **Usar variables de entorno** (`.env`) para self-host. No hardcodear valores en los workflows.
3. **Rotacion de emergencia**: si un token se filtra, revocarlo desde el servicio correspondiente y generar uno nuevo.
4. **Principio de minimo privilegio**: dar a cada credencial solo los permisos que necesita (ej: la cuenta de Google solo necesita acceso a la Sheet especifica).
5. **No compartir credenciales por chat o email.** Usar un gestor de passwords si es necesario.
6. **Revisar periodicamente** que las credenciales sigan activas y no hayan sido comprometidas.
