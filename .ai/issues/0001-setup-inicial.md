---
id: 0001
title: Setup inicial del proyecto
status: draft
type: chore
size: S
branch: issue/0001-setup-inicial
created: 2026-10-05
---

# 0001 · Setup inicial del proyecto

## Contexto
El proyecto acaba de crearse desde el framework. No hay visión detallada, stack ni estructura de código.

## Objetivo
Dejar el proyecto listo para el primer issue de funcionalidad: visión y alcance definidos, stack decidido, esqueleto que compila y un test que pasa.

## Fuera de alcance
- Cualquier funcionalidad de producto.
- CI/CD y despliegue (issue posterior si se necesita).

## Criterios de aceptación
- [ ] `.ai/PROJECT.md` tiene visión, objetivo actual, alcance y stack completados con el usuario.
- [ ] Existe `ADR-0001` en `.ai/decisions/` con la elección de stack y su motivo.
- [ ] Estructura base creada (`src/`, `tests/`) según el stack.
- [ ] La sección *Comandos* de `AGENTS.md` tiene instalar, build, tests y lint, y cada comando se ejecuta sin errores.
- [ ] Existe al menos un test trivial que pasa con el comando de tests.

## Plan técnico
1. Orquestador: entrevista breve al usuario (visión, público, restricciones) → `PROJECT.md`.
2. Explorer: comparar 2–3 opciones de stack según las restricciones → `knowledge/stack.md`.
3. Planificador: ADR-0001 con la decisión aprobada por el usuario.
4. Developer: esqueleto, formatter/linter, test trivial, comandos.

## Implementación

## Verificación

## Notas
