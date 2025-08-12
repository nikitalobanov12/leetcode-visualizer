# AGENTS.md

- Project: Next.js 15 + React 19 + TypeScript; ESLint flat config extends next/core-web-vitals and next/typescript; Tailwind v4; shadcn/ui is the main design library.
- Why this guide: give agents exact run commands and consistent style to keep edits safe and CI-friendly.

- Install:
  - bun install (preferred; bun.lock present)
  - or: npm ci

- Run:
  - Dev: bun run dev
  - Build: bun run build
  - Start: bun run start
  - Lint: bun run lint

- Tests:
  - No test framework configured yet. If adding tests, prefer Vitest + @testing-library/react + jsdom.
  - After setup: bun run test; single test: bun run test path/to/file.test.ts -t "case name"

- Imports:
  - ESM only; no require. Relative imports unless tsconfig paths are added.
  - Order: node builtins > external (react, next, shadcn/ui) > internal (src/*); blank line between groups; alphabetize within groups.

- Formatting:
  - Prettier conventions (2 spaces, semicolons, single quotes ok); UTF-8 LF; final newline.
  - Keep files small and cohesive; colocate component, styles, and tests.

- Types:
  - Prefer strict typing; avoid any. Exported functions/components have explicit return types.
  - Use discriminated unions for algorithm steps to power visualizations.

- Naming:
  - Components: PascalCase; files match component name.
  - Functions/vars: camelCase; module-level constants UPPER_SNAKE_CASE.
  - Next app router conventions in src/app; avoid unnamed default exports.

- React/Next:
  - Server Components by default; add "use client" only when needed (state/effects/shadcn interactivity).
  - Async data with error.tsx/loading.tsx when applicable; no secrets client-side.

- Error handling:
  - Don’t swallow errors; try/catch with typed narrowing. Log details server-side; show user-safe messages.

- State and visualization:
  - Algorithms are pure, deterministic functions; emit step-by-step states for the visualizer.
  - Keep visualization state local or Context; avoid prop drilling.

- CSS/UI:
  - Tailwind v4 utilities first; compose with shadcn/ui primitives (Button, Card, Dialog).
  - Avoid inline styles except dynamic visuals; prefer class-variance-authority patterns when needed.

- Linting rules source:
  - ESLint: eslint.config.mjs extends next/core-web-vitals and next/typescript.
  - No Cursor/Copilot rules found (.cursor/rules, .cursorrules, .github/copilot-instructions.md absent).

- Quick checks:
  - Typecheck: bunx tsc --noEmit
  - Lint single file: bunx eslint src/path/to/file.tsx
