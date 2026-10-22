# Respaldo íntegro de `jza172001-netizen/bodega-inventario`

Hecho el 22-oct-2026, desde el repo original, solo leyéndolo: el original no se tocó.

## Qué hay en esta copia, y dónde

| Qué | Dónde | Comprobado |
|---|---|---|
| Código e historial completo (344 commits de `main`, desde el 27-nov-2025) | rama `main` | Mismo commit que el original: `8cb835c` |
| Las 21 ramas del original | mismas ramas | Comparadas una por una: mismo commit |
| El código de los 110 PR, incluidos los commits que se borraron al mezclar (447 commits en PR) | ramas `respaldo/pr-1` … `respaldo/pr-110` | Cada una tiene el mismo commit que el PR original |
| Los 110 PR: título, estado, autor, fechas, ramas, commit de merge, descripción y lista de commits | `PULL-REQUESTS.md` (índice) y `prs/NNN.md`, en esta rama | 110 de 110 |
| Los 330 comentarios de los PR, con autor y fecha | dentro de cada `prs/NNN.md` | 330 de 330 |
| Los 9 rótulos (labels) | recreados en la copia y en `datos/etiquetas.json` | 9 de 9 |
| Los 615 despliegues de Vercel (metadatos) | `datos/despliegues.json` | {'Preview': 150, 'Production': 155, 'Production – bodega-inventario-z941': 104, 'Production – bodega-inventario': 104, 'Preview – bodega-inventario-z941': 51, 'Preview – bodega-inventario': 51}, del 2025-11-30 al 2026-10-19 |
| Todo en bruto, tal como lo devuelve GitHub | `datos/*.json` | — |

**En el original no había:** issues (0), releases (0), tags (0), revisiones de PR (0), comentarios en líneas de código (0), wiki ni GitHub Actions. No faltó nada de eso: no existía.

## Lo que NO se copió, y por qué

| Qué | Por qué no se puede | Qué hacer |
|---|---|---|
| **Los PR como PR de verdad**, con su estado «mezclado» y su página | GitHub no deja crear un PR ya mezclado ni con otro autor y otra fecha | Están como archivo (`prs/`) y como ramas (`respaldo/pr-N`) |
| **La visibilidad: la copia quedó PÚBLICA** | Esta sesión no puede cambiar la configuración del repo | Juli: Settings → Danger Zone → Change visibility → Private |
| **La descripción y la página del repo** (original: «bodega», https://bodega-inventario.vercel.app) | Lo mismo | Juli: en la página del repo, ⚙ junto a «About» |
| **Colaboradores, permisos y protección de ramas** | No son parte del contenido; son configuración de cuenta | Invitar de nuevo en Settings → Collaborators |
| **Las conexiones**: la app de Claude, Vercel y webhooks | Pertenecen al repo original | Conectarlas de nuevo si la copia se va a desplegar |
| **Los secretos**: llaves de Supabase y token de la API | Viven en Vercel y Supabase, nunca en GitHub | Siguen donde estaban; la copia no los necesita para existir |
| **La base de datos** (Supabase) y **los despliegues** (Vercel) | No son GitHub | La estructura está en `supabase/migrations/`; los datos, en Supabase |
| **Estrellas, seguidores, tráfico y reacciones** | No se pueden transferir | — |

## Advertencia

El historial trae datos que quedaron expuestos en el original: una clave de Google en `migrated_prompt_history/` y contraseñas viejas. **Revocá la clave** en console.cloud.google.com → Credenciales, y dejá esta copia **privada**.
