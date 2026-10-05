---
name: estado
description: Resumen breve para el usuario de dónde está el proyecto - issue activo, último trabajo hecho, bloqueos y siguiente paso. Úsalo cuando el usuario pregunte "¿dónde estamos?", "¿qué falta?" o al retomar el trabajo.
---

# Estado

1. Lee `.ai/STATE.md`, `.ai/ROADMAP.md` y las 5 últimas entradas de `.ai/LOG.md`.
2. Comprueba `git branch --show-current` y `git status --short`.
3. Responde en ≤ 10 líneas:
   - **Ahora:** issue activo y su estado (o "ninguno").
   - **Último hecho:** 1–3 líneas.
   - **Bloqueos:** si los hay.
   - **Siguiente:** el paso concreto que propones.
4. Si `STATE.md` no coincide con git, avisa y ofrece ejecutar `actualizar-memoria`.
