# Proyecto001

_Pendiente de definir con el usuario._

> Proyecto gestionado con el framework **LudumNostrum IA** (`../IA`). Visión y alcance en [.ai/PROJECT.md](.ai/PROJECT.md).

## Cómo se trabaja aquí

- **Solo se habla con el orquestador.** Él delega en `planificador`, `explorer`, `developer` y `tester` (`.claude/agents/`).
- **Siempre por issues**, pequeños (S/M) y uno a la vez. Flujo: `draft → ready → in-progress → in-review → done`. Detalle en `../IA/docs/flujo-issues.md`.
- **Nunca se planifica más allá** de los próximos 3–5 issues (`.ai/ROADMAP.md`).

## Memoria y fuentes de verdad: `.ai/`

| Archivo | Para qué | Dueño |
|---|---|---|
| `.ai/STATE.md` | Dónde estamos ahora. **Léelo siempre primero.** | orquestador |
| `.ai/PROJECT.md` | Visión, alcance, stack | orquestador |
| `.ai/ROADMAP.md` | Próximos issues | planificador |
| `.ai/LOG.md` | Diario append-only | orquestador |
| `.ai/issues/` | Un archivo por issue | por secciones |
| `.ai/decisions/` | ADRs | planificador |
| `.ai/knowledge/` | Hallazgos | explorer |

Reglas: cada archivo tiene un único dueño que escribe; si no está en `.ai/`, no se decidió; lee solo lo necesario.

## Comandos

<!-- Se completan en el issue de setup. Mantener actualizados. -->
- Instalar: `npm install`
- Dev: `npm run dev` (http://localhost:5173)
- Build: `npm run build`
- Tests: `npm test` (Vitest)
- Lint: `npm run lint` (oxlint)

## Estándares comunes

- Código: `../IA/standards/coding.md`
- Git: `../IA/standards/git.md`
- Definition of Done: `../IA/standards/definition-of-done.md`

## Particularidades de este proyecto

<!-- Reglas específicas que no estén en los estándares comunes. -->
_Ninguna todavía._
