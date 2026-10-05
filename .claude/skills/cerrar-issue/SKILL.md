---
name: cerrar-issue
description: Cierra un issue verificado - comprueba la Definition of Done, hace los commits, propone el merge a main, marca done y actualiza STATE, LOG y ROADMAP. Úsalo cuando el tester devuelva OK.
---

# Cerrar issue

1. Comprueba `../IA/standards/definition-of-done.md` punto por punto. Si algo falla, resuélvelo delegando o informa al usuario.
2. Si el developer reportó comandos nuevos de build/test, actualiza la sección *Comandos* de `AGENTS.md`.
3. Marca el issue `status: done`.
4. Actualiza la memoria:
   - `.ai/LOG.md` → añade `- YYYY-MM-DD · #NNNN <título> · done · <una línea de resumen>`.
   - `.ai/STATE.md` → reescríbelo (sin issue activo, último hecho, siguiente paso).
   - Pide al **planificador** que actualice `.ai/ROADMAP.md` (quitar el cerrado, reordenar candidatos).
5. Commit en la rama del issue siguiendo `../IA/standards/git.md` (`Refs: #NNNN`).
6. Pide aprobación al usuario para hacer merge a `main` (`git switch main && git merge --no-ff issue/NNNN-slug`). Sin aprobación, deja la rama lista.
7. Resume al usuario: qué se hizo, cómo se verificó y el siguiente issue propuesto.
