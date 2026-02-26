# Credenciales necesarias

Lista de credenciales que necesitas configurar para que los workflows funcionen. **Nunca guardes tokens ni passwords en archivos del repositorio.**

---

## Credenciales del proyecto

| Servicio | Tipo en n8n | Donde obtenerla | Nodos que la usan |
|----------|------------|-----------------|-------------------|
| **Telegram Bot** | Telegram API | @BotFather en Telegram | Enviar Pack Telegram, Aviso Sin Pendientes, Notificar Error |
| **Google Sheets** | Google Sheets OAuth2 | Google Cloud Console > APIs & Services > Credentials | Leer Sheet, Actualizar Sheet |
| **Gemini (LLM)** | HTTP Query Auth | aistudio.google.com > API Keys | Gemini – Generar Copy/Caption |

### Configuracion de la credencial Gemini en n8n

La credencial para Gemini se configura como **HTTP Query Auth** con estos valores:

| Campo | Valor |
|-------|-------|
| **Name** | `key` |
| **Value** | Tu API key de Gemini (empieza con `AIza...`) |

Esto agrega `?key=TU_API_KEY` a la URL de la API automaticamente.

---

## Donde guardar las credenciales

### En n8n Cloud

1. Ir a **Settings > Credentials**.
2. Agregar una nueva credencial para cada servicio (3 en total).
3. n8n las encripta y las guarda internamente.

### En n8n Self-Host

Opcion A: Configurar directamente en la UI de n8n (igual que cloud).

Opcion B: Usar variables de entorno en el archivo `.env`:

```env
# Telegram
TELEGRAM_BOT_TOKEN=tu_token_aqui
TELEGRAM_CHAT_ID=tu_chat_id_aqui

# Google Sheets
GOOGLE_SHEETS_ID=id_de_la_sheet
GOOGLE_SHEETS_TAB=Hoja 1

# Gemini
GEMINI_API_KEY=tu_api_key_aqui
```

> El archivo `.env` ya esta en `.gitignore`. Nunca lo subas al repositorio.

---

## Como conectar credenciales en los workflows

Despues de importar los JSONs en n8n, los nodos aparecen con credenciales marcadas como `"CONFIGURAR"`. Para cada workflow:

1. Abrir el workflow en el editor de n8n.
2. Hacer clic en cada nodo que tenga un icono de advertencia (credencial faltante).
3. En el campo de credencial, seleccionar la credencial que creaste.
4. Guardar el workflow.

Cada workflow usa 3 credenciales:
- **Google Sheets OAuth2** (en nodos "Leer Sheet" y "Actualizar Sheet")
- **Gemini API Key** (en nodo "Gemini – Generar Copy/Caption")
- **Telegram Bot** (en nodos de envio de mensajes)

---

## Reglas de seguridad para credenciales

1. **Nunca commitear tokens, API keys ni passwords.** Si lo hiciste por accidente, rotalos inmediatamente.
2. **Usar variables de entorno** (`.env`) para self-host. No hardcodear valores en los workflows.
3. **Rotacion de emergencia**: si un token se filtra, revocarlo desde el servicio correspondiente y generar uno nuevo.
4. **Principio de minimo privilegio**: dar a cada credencial solo los permisos que necesita (ej: la cuenta de Google solo necesita acceso a la Sheet especifica).
5. **No compartir credenciales por chat o email.** Usar un gestor de passwords si es necesario.
6. **Revisar periodicamente** que las credenciales sigan activas y no hayan sido comprometidas.
7. **Gemini API Key**: configurar limites de uso en Google AI Studio para evitar gastos inesperados.
