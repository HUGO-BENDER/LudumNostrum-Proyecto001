---
name: nuevo-issue
description: Crea un nuevo issue en .ai/issues/ a partir de una necesidad del usuario, delegando en el planificador, y lo presenta para aprobación. Úsalo cuando el usuario pida algo nuevo (funcionalidad, corrección, investigación).
---

# Nuevo issue

1. Aclara la necesidad con el usuario si es ambigua (máximo 3 preguntas).
2. ¿Falta contexto técnico? → lanza al **explorer** con una pregunta concreta.
3. Lanza al **planificador** con: la necesidad, lo que queda fuera de alcance, los hallazgos del explorer y la instrucción de crear el issue en `draft` desde `.ai/issues/_TEMPLATE.md` con el siguiente número libre.
4. Lee el issue creado y presenta al usuario en 5–10 líneas: número y título, objetivo, criterios de aceptación, tamaño.
5. Pide aprobación:
   - Aprobado → `status: ready`, añade una línea en `.ai/LOG.md` y actualiza `.ai/STATE.md`.
   - Cambios → reenvíalos al planificador y repite el paso 4.
6. Pregunta si se ejecuta ya (skill `ejecutar-issue`).
