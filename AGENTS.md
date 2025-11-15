# Repository Guidelines

## Project Structure & Module Organization
Keep the app inside `src/`: `main.tsx` mounts `App.tsx`, assets sit in `src/assets/`, and component styles live next to each view so Vite HMR reloads instantly. Static files that must remain untouched belong in `public/`, long-form specs live in `docs/`, and AI-DLC steering plus specs stay under `.kiro/`. Tooling configs (`vite.config.ts`, `tsconfig*.json`, `eslint.config.js`, `prettier.config.mjs`, `stylelint.config.mjs`) live at the root—mirror that layout when introducing new modules.

## Build, Test, and Development Commands
Install the pinned toolchain with `mise install` (Node 25.2.0 + pnpm 10.21.0), then `pnpm install`. Use `pnpm dev` for the HMR server, `pnpm build` for type checking plus bundling, `pnpm preview` to serve `dist/`, and `pnpm lint` for the flat ESLint stack. For one-off utilities (Prettier, Vitest, Storybook, Secretlint), prefer `pnpm exec <tool>` so the catalog-locked versions are reused.

## Coding Style & Naming Conventions
Author all code in TypeScript; components/providers use PascalCase filenames, hooks/utilities stay camelCase, and environment helpers end with `.config.ts`. ESLint combines React, Hooks, Functional, and Vite presets, so default to pure functions, respect exhaustive-deps, and avoid shared mutable state. Prettier enforces LF endings, 100-character lines, single quotes, and sorted imports; run `pnpm exec prettier --write "src/**/*.{ts,tsx,css}"` before reviews. Stylelint (standard + tailwindcss + strict-value) blocks unsupported CSS and magic values, so keep tokens in dedicated modules instead of inline literals.

## Testing Guidelines
Vitest with `@testing-library/react` drives automated tests; co-locate specs (`Component.test.tsx`) with the feature. Run `pnpm exec vitest` while iterating and `pnpm exec vitest run --coverage` ahead of a PR to feed the V8 coverage report. Mock network edges with MSW handlers and capture edge cases via mutation-minded assertions. When a component is reusable, add a Storybook story and publish a Chromatic snapshot for asynchronous visual review.

## Commit & Pull Request Guidelines
Commit messages follow Conventional Commits (`feat:`, `fix:`, `chore:`) as already in the log, and commitlint will reject anything else. Pull requests should summarize the user impact, link the `.kiro` specification they fulfill, and list the commands you ran (`pnpm build && pnpm exec vitest run --coverage && pnpm lint`). Attach screenshots or Chromatic URLs for UI changes and ensure checks pass before requesting review.

## Security & Configuration Tips
Run `pnpm exec secretlint "**/*"` before pushing to guard credentials, and keep sensitive values in untracked `.env.local` files; document any required keys in `docs/configuration.md`. Respect the strict pnpm catalog to avoid drifting dependency versions.
