---
id: 0001
title: Step001 · Proyecto React + Vite
status: done
type: chore
size: S
branch: issue/0001-step001-react-vite
created: 2026-10-05
---

# 0001 · Step001 · Proyecto React + Vite

## Contexto
El proyecto acaba de crearse desde el framework y no tiene código. El usuario ha decidido el stack (ver [ADR-0001](../decisions/ADR-0001-stack-react-vite-ts.md)): React + Vite + TypeScript, con Vitest para tests. Este issue crea el esqueleto sobre el que irán todos los issues de producto.

Entorno de desarrollo: Windows, Node 24.14, npm 11.12.

## Objetivo
Tener en la raíz del repo una app React + TypeScript generada con Vite que arranca en local, compila, pasa lint y tiene un test trivial en verde, con los comandos documentados en `AGENTS.md`.

## Fuera de alcance
- Cualquier funcionalidad de producto (la app queda con la pantalla por defecto de la plantilla).
- CI/CD y despliegue.
- Routing, librerías de estado y librerías de UI/estilos.
- Formatter adicional (Prettier) u otras reglas de ESLint más allá de las de la plantilla.
- Rellenar visión/alcance de `.ai/PROJECT.md` (lo hace el orquestador con el usuario).

## Criterios de aceptación
- [x] La app está generada con la plantilla `react-ts` de Vite **en la raíz del repo** (existen `package.json`, `index.html`, `vite.config.ts`, `src/main.tsx`, `src/App.tsx` en la raíz; no hay subcarpeta de proyecto).
- [x] Los archivos previos del repo (`.ai/`, `.claude/`, `AGENTS.md`, `CLAUDE.md`) siguen intactos: `git status` / `git diff` no muestra cambios en ellos salvo la sección *Comandos* de `AGENTS.md`.
- [x] `node_modules/` y `dist/` están en `.gitignore` (`git status` tras instalar y compilar no los lista).
- [x] `npm install` termina sin errores.
- [x] `npm run build` termina sin errores y genera `dist/`.
- [x] `npm run lint` termina sin errores (exit code 0).
- [x] `npm test` ejecuta `vitest run` y pasa al menos un test que renderiza `App` con `@testing-library/react` en entorno `jsdom` y comprueba un elemento visible (p. ej. el encabezado).
- [x] La sección *Comandos* de `AGENTS.md` documenta: instalar (`npm install`), dev (`npm run dev`), build (`npm run build`), tests (`npm test`), lint (`npm run lint`).
- [x] **Verificación manual del usuario:** con `npm run dev`, al abrir la URL que indica Vite (por defecto `http://localhost:5173`) el usuario confirma que la página de la plantilla se ve correctamente (logos de Vite y React, encabezado, botón contador que incrementa al pulsarlo) y sin errores en la consola del navegador.

## Plan técnico

**Archivos a crear/modificar**
- Generados por la plantilla (raíz): `package.json`, `package-lock.json`, `index.html`, `vite.config.ts`, `tsconfig.json`, `tsconfig.app.json`, `tsconfig.node.json`, `eslint.config.js`, `public/`, `src/` (`main.tsx`, `App.tsx`, `App.css`, `index.css`, `assets/`, `vite-env.d.ts` si lo trae).
- `.gitignore`: el de la plantilla, fusionado con el existente si lo hubiera (no perder entradas previas).
- `vite.config.ts`: añadir bloque `test` de Vitest (`environment: 'jsdom'`), con `/// <reference types="vitest/config" />` para el tipado.
- `package.json`: añadir script `"test": "vitest run"`.
- `src/App.test.tsx`: test trivial que renderiza `App` y busca el encabezado (`screen.getByRole('heading', ...)`). Importar `describe/it/expect` desde `vitest` explícitamente (sin `globals`), para no tocar tsconfig.
- `AGENTS.md`: solo la sección *Comandos*.

**Enfoque**
1. Generar la plantilla en una carpeta temporal fuera del repo (`npm create vite@latest <tmp> -- --template react-ts`) y copiar su contenido a la raíz, en lugar de generar directamente con `.`: el directorio no está vacío y el asistente de create-vite ofrece "Remove existing files", que borraría `.ai/`, `.claude/` y demás. Si se genera directamente en `.`, elegir **siempre** "Ignore files and continue".
2. No sobrescribir `README.md` si ya existe en el repo; si no existe, se puede conservar el de la plantilla.
3. `npm install`, luego añadir dependencias de test como `devDependencies`.
4. Configurar Vitest, escribir el test, añadir el script, ejecutar build/lint/test.
5. Documentar comandos en `AGENTS.md` y pedir al usuario la verificación visual con `npm run dev`.

**Dependencias nuevas (todas `devDependencies` salvo `react`/`react-dom` que trae la plantilla)**
- `vite`, `@vitejs/plugin-react`, `typescript`, `eslint` y plugins asociados: vienen con la plantilla `react-ts`; decisión del usuario (ADR-0001).
- `vitest`: runner de tests nativo de Vite, reutiliza su config y transformaciones; sin configuración extra de Babel/ts-jest.
- `@testing-library/react` (+ `@testing-library/dom`, peer dependency requerida en versiones recientes): renderizar componentes y consultarlos como lo haría el usuario.
- `jsdom`: entorno DOM para que Vitest pueda renderizar componentes en Node.
- No se añade `@testing-library/jest-dom` ni Prettier: no son necesarios para los criterios (simplicidad).

**Riesgos**
- Borrado accidental de archivos del repo al generar en directorio no vacío → mitigado con la carpeta temporal (paso 1) y el criterio de `git status`.
- `tsc -b` del build incluye `src/App.test.tsx`: si da error de tipos, revisar que los imports vienen de `vitest` y que `@testing-library/react` está instalado; no relajar `strict`.
- Desajuste de peer dependencies entre la versión de React de la plantilla y `@testing-library/react` → instalar la última versión compatible; no usar `--force` / `--legacy-peer-deps` sin anotarlo en *Implementación*.
- Saltos de línea CRLF en Windows: no se añade configuración; si ESLint protesta, anotarlo en *Notas*.

## Implementación
- Plantilla `react-ts` de create-vite 9.2.1 generada en carpeta temporal fuera del repo y copiada a la raíz (nada en `.ai/`, `.claude/`, `CLAUDE.md` tocado). `package.json` renombrado a `proyecto001`.
- Desviación respecto al plan: esta versión de la plantilla usa **oxlint** (`.oxlintrc.json`, script `"lint": "oxlint"`) en lugar de ESLint; no hay `eslint.config.js`. Se mantiene el linter de la plantilla.
- `.gitignore`: se conservó el existente y se añadieron `node_modules`, `dist`, `dist-ssr`, `*.local`. Se conserva el `README.md` de la plantilla (no existía).
- Añadidos como devDependencies: `vitest` 5.0.3, `@testing-library/react`, `@testing-library/dom`, `jsdom`. Instalación sin `--force` ni `--legacy-peer-deps`.
- `vite.config.ts`: bloque `test` con `environment: 'jsdom'` y `/// <reference types="vitest/config" />`. Script `"test": "vitest run"`.
- `src/App.test.tsx`: renderiza `App` y comprueba el heading "Get started" (sin `globals`, imports desde `vitest`).
- `AGENTS.md`: sección *Comandos* actualizada (instalar, dev, build, tests, lint).
- Resultados: `npm install` OK (0 vulnerabilidades); `npm run build` OK (genera `dist/`); `npm run lint` exit 0; `npm test` 1 test pasado; `npm run dev` responde HTTP 200 en http://localhost:5173/ (proceso detenido).
- Pendiente: verificación visual del usuario con `npm run dev`.

## Verificación
- [x] Plantilla react-ts en la raíz — evidencia: `package.json`, `index.html`, `vite.config.ts`, `src/main.tsx`, `src/App.tsx` en la raíz, sin subcarpeta de proyecto.
- [x] Archivos previos intactos — evidencia: `git diff --stat -- .claude CLAUDE.md .ai` solo muestra STATE.md y este issue; `git diff AGENTS.md .gitignore` solo toca *Comandos* y añade entradas al final de `.gitignore` (lo previo se conserva).
- [x] `node_modules/` y `dist/` ignorados — evidencia: `git status --short --ignored` los muestra como `!!` tras install y build; no aparecen como no rastreados.
- [x] `npm install` — evidencia: exit 0, 0 vulnerabilidades.
- [x] `npm run build` — evidencia: `tsc -b && vite build` exit 0, `dist/` generado.
- [x] `npm run lint` — evidencia: oxlint exit 0 sin avisos. Nota: la plantilla usa oxlint, no ESLint (desviación documentada en *Implementación*); el linter funciona.
- [x] `npm test` — evidencia: `vitest run` 1 test pasa; `src/App.test.tsx` renderiza `App` (jsdom en `vite.config.ts`) y comprueba el heading "Get started" por rol (comportamiento visible, sin globals).
- [x] *Comandos* de `AGENTS.md` — evidencia: instalar, dev, build, tests y lint documentados con sus comandos.
- [x] Verificación manual del usuario — CONFIRMADA por el usuario el 2026-10-05 con `npm run dev` (pidió cerrar el issue). Comprobación automática previa: `npm run dev` sirve `/` con HTTP 200 y HTML con `/@vite/client`; `/src/main.tsx` y `/src/App.tsx` respondieron 200 (la ruta pudo ser alterada por MSYS en el curl, así que el 200 puede ser el fallback SPA; no concluyente). Proceso detenido y puerto 5173 libre.
- Sin código muerto ni `TODO`/`FIXME` en `src/` y `vite.config.ts`; sin temporales (solo `.claude/settings.local.json` ignorado, preexistente).
- Observación menor (no bloqueante): `<title>` de `index.html` es "tpl" (resto de la plantilla).
Tests: 1 pasan / 0 fallan
Veredicto: OK (a falta de la verificación visual del usuario)

## Notas
- Sustituye al antiguo issue `0001-setup-inicial` (entrevista + elección de stack), ya resuelto por decisión directa del usuario.
