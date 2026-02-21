# IBM Joven - Automatizacion de Redes Sociales

Repositorio de automatizaciones para las redes sociales de **IBM Joven** (Iglesia Bautista Maranata - Ministerio Joven).

## Que resuelve

Este proyecto automatiza las tareas repetitivas de publicacion en redes sociales:

- **Versiculo diario**: genera copy, hashtags y diseño listo para publicar cada dia.
- **Anuncios de eventos**: prepara las piezas graficas y textos para actividades de la iglesia.
- **Fotos del culto**: arma packs de publicacion a partir de las fotos tomadas en los servicios.

## Filosofia: 90% automatico + aprobacion humana

Nada se publica sin que una persona lo revise y apruebe. La automatizacion se encarga del trabajo pesado (generar textos, armar plantillas, recordar fechas), pero **siempre hay un paso de aprobacion humana** antes de que el contenido llegue a las redes.

Esto garantiza que el mensaje sea fiel, respetuoso y alineado con los valores de la iglesia.

## Stack recomendado

| Herramienta | Funcion | Costo |
|---|---|---|
| **n8n** | Orquestador de flujos (workflows) | Gratis (self-host) o plan free en cloud |
| **Canva** | Diseño grafico con templates | Gratis (plan basico) |
| **Google Sheets / CSV** | Base de datos de contenido | Gratis |
| **Telegram** | Canal de aprobacion y notificaciones | Gratis |
| **LLM (OpenAI / Gemini / local)** | Generacion de copy y hashtags | Segun proveedor |

## Mapa de carpetas

```
ibm-joven-social-automation/
  00-README/          -> Documentacion general, quickstart y operacion
  01-n8n/
    workflows/        -> Exports JSON de los flujos de n8n
    credentials/      -> Guia de credenciales (sin secretos)
  02-content/
    sheets/           -> Template CSV de la base de contenido
    prompts/          -> Prompts para IA (versiculo, anuncio, fotos)
  03-design/
    canva/            -> Guias de templates Canva y brand kit
    canva/exports/    -> Carpeta para guardar exports PNG (no versionados)
  04-ops/
    checklists/       -> Checklists de aprobacion y publicacion
  05-security/        -> Reglas de seguridad y uso de IA
```

## Reglas del repositorio

- **Nunca commitear tokens, passwords ni claves de API.** Usar variables de entorno.
- Los archivos `.example` muestran la estructura esperada sin datos sensibles.
- Los exports de Canva (PNG/JPG) no se versionan en git (ver `.gitignore`).
- Los workflows de n8n se exportan como JSON y se versionan normalmente.

## Contribuir

1. Leete el `QUICKSTART.md` y `OPERACION.md` en esta carpeta.
2. Si modificas un workflow de n8n, exportalo como JSON y reemplaza el archivo en `01-n8n/workflows/`.
3. Si cambias un prompt, probalo al menos 3 veces antes de commitear.
4. Toda publicacion pasa por aprobacion humana. Sin excepciones.
