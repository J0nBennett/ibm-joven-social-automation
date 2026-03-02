# Troubleshooting – Problemas comunes

Guia rapida para resolver los errores mas frecuentes en los workflows.

---

## 1. "No hay [versiculos/anuncios/fotos] pendientes"

**Mensaje en Telegram**: "Info: No hay versiculos pendientes en la Sheet..."

**Causa**: No hay filas con `tipo=versiculo` (o anuncio/fotos) y `estado=pendiente`.

**Solucion**:
- Abrir la Google Sheet.
- Verificar que exista una fila con el `tipo` correcto y `estado=pendiente`.
- Verificar que la columna `id` tenga un valor (n8n la usa para identificar la fila).

---

## 2. Error de credenciales / autenticacion

**Mensaje**: "401 Unauthorized" o "INVALID_API_KEY" o "insufficient permissions"

**Solucion**:
- **Gemini**: Verificar que la API key sea valida en aistudio.google.com. Verificar que la credencial HTTP Query Auth tenga `name=key` y `value=TU_API_KEY`.
- **Google Sheets**: Verificar que la cuenta OAuth2 tenga acceso a la Sheet. Reautorizar si expiro.
- **Telegram**: Verificar el bot token con `https://api.telegram.org/botTU_TOKEN/getMe`. Si devuelve error, regenerar el token con @BotFather.

---

## 3. "No se pudo parsear respuesta LLM"

**Causa**: Gemini devolvio texto que no es JSON valido.

**Solucion**:
- Revisar la ejecucion fallida en n8n (ir al historial de ejecuciones).
- Ver el output del nodo "Gemini – Generar Copy" para ver que devolvio.
- Si pasa frecuentemente, verificar que el prompt no haya sido modificado.
- Intentar ejecutar de nuevo (a veces el LLM falla una vez y al reintentar funciona).

---

## 4. "Campos faltantes en respuesta LLM"

**Causa**: Gemini no genero todos los campos requeridos (hook, copy_post, cta, etc.).

**Solucion**:
- Reejecutar el workflow (suele resolverse al reintentar).
- Si persiste, verificar que los datos de entrada en la Sheet esten completos (titulo, texto_base, etc.).
- Revisar que el prompt no haya sido alterado.

---

## 5. "Contenido sospechoso detectado en respuesta LLM"

**Causa**: La respuesta del LLM contiene URLs externas o patrones de codigo que podrian ser resultado de prompt injection.

**Solucion**:
- **No publicar el contenido.**
- Revisar la fila de la Sheet: verificar que los campos `titulo`, `texto_base`, `verse_text` no contengan instrucciones ocultas o texto sospechoso.
- Si los datos de la Sheet estan bien, reejecutar. Si persiste, reportar al lider del equipo.

---

## 6. Error de timeout en Gemini

**Mensaje**: "ETIMEDOUT" o "Request timed out"

**Causa**: La API de Gemini tardo mas de 30 segundos en responder.

**Solucion**:
- Reejecutar el workflow.
- Verificar el estado de la API de Gemini en status.cloud.google.com.
- Si el problema persiste, el servicio puede estar experimentando alta demanda.

---

## 7. El workflow del versiculo no se ejecuto automaticamente

**Causa posible**: El cron no esta activo.

**Solucion**:
- Verificar que el workflow este **activado** (toggle verde en n8n).
- Verificar la zona horaria de n8n (el cron esta configurado a las 7:00 AM).
- En n8n Cloud: Settings > General > Timezone.
- En self-host: variable de entorno `GENERIC_TIMEZONE`.

---

## 8. Telegram no envia el mensaje

**Causa**: Bot no es admin del grupo, chat ID incorrecto, o bot baneado.

**Solucion**:
- Verificar que el bot sea miembro del grupo/canal.
- Verificar el chat ID (puede cambiar si se recreo el grupo).
- Probar enviar un mensaje manual: `https://api.telegram.org/botTU_TOKEN/sendMessage?chat_id=TU_CHAT_ID&text=test`

---

## 9. Google Sheets no actualiza la fila

**Causa**: El `id` de la fila no coincide o la Sheet cambio de estructura.

**Solucion**:
- Verificar que la columna `id` exista y tenga valores unicos.
- Verificar que el nombre de la hoja coincida con `GOOGLE_SHEETS_TAB`.
- Verificar que las columnas de la Sheet no hayan sido renombradas.

---

## Donde ver los logs

| Plataforma | Como ver logs |
|---|---|
| n8n Cloud | Ir al workflow > Executions (historial) |
| n8n Self-Host | Misma UI, o `docker logs n8n` si usas Docker |
| Telegram | Los errores se envian al mismo chat como notificaciones |

---

## Regla general

> Si algo falla: revisar la ejecucion en n8n, ver en que nodo fallo, leer el mensaje de error. La mayoria de problemas se resuelven verificando credenciales, datos de la Sheet, o reejecutando.
