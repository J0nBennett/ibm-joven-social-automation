# Guia de operacion

Documento que describe los flujos operativos diarios y los roles involucrados.

---

## Flujo 1: Versiculo diario

Frecuencia: todos los dias (automatico con cron o manual).

| Paso | Quien | Que hace | Tiempo estimado |
|------|-------|----------|-----------------|
| 1 | n8n (auto) | Lee la fila del dia desde Google Sheet/CSV | - |
| 2 | n8n (auto) | Envia el versiculo + datos al LLM con el prompt de `prompt_versiculo.md` | - |
| 3 | n8n (auto) | Recibe el copy generado (hook, reflexion, CTA, hashtags) | - |
| 4 | n8n (auto) | Envia preview al grupo de Telegram para aprobacion | - |
| 5 | **Aprobador** | Revisa el copy en Telegram. Responde "ok" o pide cambios | 2-3 min |
| 6 | **Editor** | Abre el template de Canva, pega los textos en los placeholders | 5-10 min |
| 7 | **Editor** | Exporta la imagen (PNG 1080x1080 para post, 1080x1920 para story) | 1-2 min |
| 8 | **Publicador** | Sube la imagen a Instagram/Facebook con el copy generado | 3-5 min |
| 9 | **Publicador** | Marca la fila como "publicado" en la Sheet y anota la fecha/hora | 1 min |

**Tiempo total estimado por persona**: 10-20 minutos.

---

## Flujo 2: Anuncio de evento

Frecuencia: segun necesidad (cuando hay actividades programadas).

| Paso | Quien | Que hace | Tiempo estimado |
|------|-------|----------|-----------------|
| 1 | **Editor** | Carga los datos del evento en la Sheet (titulo, fecha, lugar, descripcion) | 5 min |
| 2 | n8n (manual) | Se ejecuta el workflow de anuncio. Envia datos al LLM con `prompt_anuncio.md` | - |
| 3 | n8n (auto) | Genera copy para post y story, CTA, hashtags y sugerencias para Canva | - |
| 4 | n8n (auto) | Envia preview al grupo de Telegram | - |
| 5 | **Aprobador** | Revisa y aprueba o pide ajustes | 3-5 min |
| 6 | **Editor** | Diseña en Canva usando el template de anuncio | 10-15 min |
| 7 | **Publicador** | Publica en redes y marca como "publicado" | 3-5 min |

**Tiempo total estimado**: 20-30 minutos.

---

## Flujo 3: Fotos del culto

Frecuencia: despues de cada servicio/culto (1-2 veces por semana).

| Paso | Quien | Que hace | Tiempo estimado |
|------|-------|----------|-----------------|
| 1 | **Editor** | Selecciona las mejores fotos (5-10 fotos) y las sube a una carpeta compartida | 10-15 min |
| 2 | **Editor** | Carga una fila en la Sheet con tipo "fotos", titulo del culto y fecha | 3 min |
| 3 | n8n (manual) | Se ejecuta el workflow. Envia datos al LLM con `prompt_caption_fotos.md` | - |
| 4 | n8n (auto) | Genera caption, hashtags y versiculo sugerido | - |
| 5 | n8n (auto) | Envia preview al grupo de Telegram | - |
| 6 | **Aprobador** | Revisa el caption y el versiculo sugerido | 2-3 min |
| 7 | **Editor** | Arma el carrusel o album en Canva (opcional) o sube directo | 5-10 min |
| 8 | **Publicador** | Publica el pack de fotos con el caption aprobado | 3-5 min |
| 9 | **Publicador** | Marca como "publicado" en la Sheet | 1 min |

**Tiempo total estimado**: 25-35 minutos.

---

## Roles sugeridos

| Rol | Responsabilidad | Puede ser |
|-----|----------------|-----------|
| **Editor** | Carga contenido en la Sheet, diseña en Canva, ajusta textos | Lider de comunicacion o voluntario de diseño |
| **Aprobador** | Revisa contenido en Telegram antes de publicar. Tiene la ultima palabra | Lider de jovenes o pastor |
| **Publicador** | Publica el contenido aprobado en las redes sociales | Editor u otra persona con acceso a las cuentas |

> Una misma persona puede cumplir varios roles, pero se recomienda que **al menos la aprobacion sea de alguien distinto** al que genero el contenido.

---

## Notas importantes

- **No se publica nada sin aprobacion.** Si el aprobador no responde, el contenido queda en estado "pendiente".
- **Los tiempos son estimados.** Dependen de la experiencia del equipo y la complejidad del contenido.
- **Canva es manual.** No usamos API de Canva; el diseño lo hace una persona con los templates pre-armados.
- **El LLM es una ayuda, no un reemplazo.** El copy generado siempre se revisa y puede editarse antes de publicar.
- **Registrar todo.** Cada publicacion queda marcada en la Sheet con fecha, estado y quien aprobo.
