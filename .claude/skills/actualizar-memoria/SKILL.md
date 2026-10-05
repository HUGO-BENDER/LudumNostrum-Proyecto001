---
name: actualizar-memoria
description: Sincroniza la memoria .ai/ con la realidad del repositorio (STATE.md, LOG.md, estados de issues). Úsalo al final de una sesión, tras trabajo fuera del flujo o cuando el usuario sospeche que la memoria está desfasada.
---

# Actualizar memoria

1. Recoge la realidad: `git status`, `git branch --show-current`, `git log --oneline -15`, y el `status` de todos los archivos de `.ai/issues/`.
2. Detecta incoherencias:
   - Más de un issue `in-progress`.
   - Rama actual que no corresponde al issue activo.
   - Commits con `Refs: #NNNN` de issues que no están `done` (o al revés).
   - Cambios sin commitear sin issue asociado.
3. Corrige lo que sea objetivo (estados, `STATE.md`). Lo que requiera decisión, pregúntalo al usuario.
4. Reescribe `.ai/STATE.md` (≤ 40 líneas) y añade una línea a `.ai/LOG.md` si hubo cambios.
5. Informa al usuario de lo corregido en una lista breve.
