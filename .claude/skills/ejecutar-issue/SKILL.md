---
name: ejecutar-issue
description: Ejecuta un issue en estado ready - crea la rama, delega la implementación en el developer y la verificación en el tester, con un máximo de 2 reintentos. Úsalo cuando el usuario diga "ejecuta/implementa el issue NNNN" o apruebe empezar.
---

# Ejecutar issue

Precondición: el issue está en `ready` y no hay otro `in-progress`. Si no se cumple, avisa y para.

1. **Rama:** `git switch main` y `git switch -c issue/NNNN-slug` (o cámbiate a ella si ya existe). Anota la rama en el frontmatter (`branch`).
2. **Implementación:** `status: in-progress`, actualiza `.ai/STATE.md`. Lanza al **developer** con la ruta del issue.
   - `BLOQUEADO` → marca `blocked`, explica al usuario y para.
3. **Verificación:** `status: in-review`. Lanza al **tester** con la ruta del issue.
4. **Resultado:**
   - `OK` → continúa con la skill `cerrar-issue`.
   - `FALLO` → reenvía el informe al developer y vuelve al paso 3. Máximo **2 reintentos**; después `blocked` y escala al usuario con opciones.
5. Informa al usuario en cada transición en una sola línea.
