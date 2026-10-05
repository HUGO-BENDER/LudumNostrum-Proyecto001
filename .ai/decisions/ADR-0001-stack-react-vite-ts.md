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
- **ESLint**: el que trae la plantilla, sin reglas adicionales.
- **Vitest** como runner (comparte config y transformaciones con Vite), con **@testing-library/react** y **jsdom** para tests de componentes.
- **npm** como gestor de paquetes.
- Sin Prettier ni otras herramientas de formato por ahora (simplicidad).

## Consecuencias
- (+) Setup mínimo y estándar; documentación abundante.
- (+) Un único pipeline de transformación para dev, build y tests.
- (−) Sin formatter automático: el estilo depende de ESLint y de la disciplina; reconsiderar Prettier si aparecen inconsistencias.
- (−) Sin routing ni SSR de serie; si se necesitan, irán en issues/ADRs posteriores.
