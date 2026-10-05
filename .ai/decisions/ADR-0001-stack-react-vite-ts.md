# ADR-0001: Stack base React + Vite + TypeScript, con Vitest para tests

- **Fecha:** 2026-10-05
- **Estado:** Aceptado
- **Issue:** #0001

## Contexto
Proyecto001 arranca sin código. Hace falta un stack de frontend para empezar a construir, con build, lint y tests desde el primer issue. Entorno de desarrollo: Windows, Node 24.14, npm 11.12. El usuario ha elegido el stack directamente.

## Opciones consideradas
1. React + Vite + TypeScript (plantilla `react-ts`), Vitest + Testing Library + jsdom para tests.
2. React + Vite + JavaScript (plantilla `react`).
3. Framework con más opinión (p. ej. Next.js) o Jest como runner.

## Decisión
Opción 1, por decisión del usuario:
- **Vite** con plantilla oficial `react-ts`, generada en la raíz del repo: arranque y HMR rápidos, configuración mínima.
- **TypeScript**: tipado estático desde el principio.
- **oxlint** como linter: es el que trae de serie la plantilla actual (create-vite 9.2.1 `react-ts`), configurado en `.oxlintrc.json` y ejecutado con `npm run lint` (→ `oxlint`). Se usa sin reglas adicionales. Motivo: viene incluido con la plantilla, es mucho más rápido que ESLint y no requiere configuración extra.
- **Vitest** como runner (comparte config y transformaciones con Vite), con **@testing-library/react** y **jsdom** para tests de componentes.
- **npm** como gestor de paquetes.
- Sin Prettier ni otras herramientas de formato por ahora (simplicidad).

## Consecuencias
- (+) Setup mínimo y estándar; documentación abundante.
- (+) Un único pipeline de transformación para dev, build y tests.
- (+) Lint muy rápido y sin configuración que mantener más allá de `.oxlintrc.json`.
- (−) oxlint cubre menos reglas y tiene un ecosistema de plugins más pequeño que ESLint; si se echan en falta reglas concretas, reconsiderar ESLint en un ADR posterior.
- (−) Sin formatter automático: el estilo depende de oxlint y de la disciplina; reconsiderar Prettier si aparecen inconsistencias.
- (−) Sin routing ni SSR de serie; si se necesitan, irán en issues/ADRs posteriores.

## Modificaciones
- **2026-10-05:** el linter pasa de ESLint a **oxlint**, porque la plantilla actual de create-vite (9.2.1, `react-ts`) ya trae oxlint en lugar de ESLint. Aprobado explícitamente por el usuario.
