# Reglas de seguridad y uso de IA

Reglas que todo el equipo debe conocer y respetar al usar herramientas de IA y automatizacion en este proyecto.

---

## 1. Aprobacion humana obligatoria

- **Ningun contenido generado por IA se publica sin revision humana.**
- El aprobador debe verificar que el texto sea correcto, respetuoso y fiel a la Biblia.
- Si hay dudas, no se publica. Mejor consultar que publicar algo incorrecto.

## 2. Proteccion de credenciales

- **Nunca subir tokens, API keys, passwords ni credenciales al repositorio.**
- Usar variables de entorno (`.env`) para manejar secretos.
- Si un token se filtra por accidente:
  1. Revocarlo inmediatamente desde el servicio correspondiente.
  2. Generar uno nuevo.
  3. Limpiar el historial de git si es necesario (`git filter-branch` o `BFG Repo-Cleaner`).
  4. Notificar al equipo.

## 3. Anti prompt-injection

Los prompts que enviamos al LLM pueden ser manipulados si los datos de entrada contienen instrucciones maliciosas. Para prevenir esto:

- **No incluir en la Sheet textos que no hayan sido escritos por el equipo.** No copiar/pegar texto de fuentes no confiables directamente en los campos que van al LLM.
- **Revisar siempre la salida del LLM.** Si el modelo genera algo inesperado (links, codigo, instrucciones raras), no publicarlo y reportarlo.
- **No usar prompts que le pidan al LLM acceder a URLs, ejecutar codigo o interactuar con sistemas externos.**
- **Los prompts del repo son los unicos autorizados.** No modificarlos sin revision del equipo.

## 4. No descargar ni ejecutar archivos no verificados

- No descargar ejecutables, scripts ni archivos adjuntos de fuentes desconocidas.
- No instalar plugins de n8n de fuentes no oficiales.
- No ejecutar comandos que alguien comparta por chat sin entender que hacen.
- Si un workflow de n8n hace algo que no entendes, pregunta antes de activarlo.

## 5. Proteccion de datos personales

- No incluir datos personales de miembros de la iglesia (nombres completos, telefonos, direcciones) en la Sheet ni en los prompts.
- Las fotos del culto deben publicarse solo con consentimiento de las personas que aparecen.
- No usar la IA para procesar o analizar datos personales de miembros.

## 6. Registro de cambios (audit simple)

Mantener un registro basico de las acciones importantes:

| Que registrar | Donde | Quien |
|---|---|---|
| Contenido aprobado | Columna `aprobado_por` en la Sheet | Aprobador |
| Contenido publicado | Columna `estado` y `timestamp` en la Sheet | Publicador |
| Cambios en prompts | Commits en git con mensaje descriptivo | Editor |
| Cambios en workflows | Commits en git con el JSON actualizado | Editor |
| Incidentes de seguridad | Notificar al lider del equipo | Quien lo detecte |

## 7. Principio de minimo privilegio

- Cada persona tiene acceso solo a lo que necesita.
- El bot de Telegram solo tiene acceso al grupo de aprobaciones.
- La cuenta de Google solo tiene acceso a la Sheet del proyecto.
- Las API keys del LLM se configuran con los limites mas bajos posibles.

## 8. Revisiones periodicas

- **Mensualmente**: verificar que las credenciales sigan activas y no comprometidas.
- **Ante cualquier sospecha**: cambiar credenciales inmediatamente.
- **Al salir alguien del equipo**: revocar sus accesos y rotar credenciales compartidas.

---

## Resumen

> Si algo parece raro, no lo publiques. Si un token se filtro, revocalo ya. Si no entendes un cambio, pregunta. La seguridad es responsabilidad de todo el equipo.
