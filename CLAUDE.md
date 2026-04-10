# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Context

Finance Tracker is the starter project for the Code with Mosh Claude Code course. Per the README, it is **intentionally** shipped with a bug, poor UI, and messy code — all of which are fixed as course exercises. When you encounter smells, do not assume they are accidental; confirm with the user before "cleaning up" unrelated code.

Stack: React 19, Vite 7, plain CSS, JavaScript (no TypeScript, no tests, no backend).

## Commands

| Command | Purpose |
|---|---|
| `npm install` | Install dependencies |
| `npm run dev` | Start Vite dev server on http://localhost:5173 |
| `npm run build` | Production build to `dist/` |
| `npm run preview` | Serve the built `dist/` locally |
| `npm run lint` | Run ESLint across the repo |

There is no test script configured.

## Architecture

The entire app is one component. `src/main.jsx` mounts `<App />` inside React `StrictMode`; `src/App.jsx` owns all state, form handling, derived totals, filtering, and rendering. There is no router, no context, no external store, and no persistence — transactions are seeded in `useState` and disappear on reload.

Because everything lives in `App.jsx`, most tasks will involve editing that single file. If a task grows beyond cosmetic changes, consider whether the user wants the component split up before silently refactoring.

## Gotchas

- **Amounts are stored as strings** in both seed data and the add-transaction form. The `totalIncome`/`totalExpenses` reducers use `+`, which concatenates strings rather than summing. This is the intentional starter bug — don't "fix" it unless the task asks for it.
- **StrictMode** is enabled, so effects and some state updates run twice in dev. Keep this in mind when debugging.

## Lint Rules

ESLint flat config (`eslint.config.js`) extends `@eslint/js` recommended, `eslint-plugin-react-hooks`, and `eslint-plugin-react-refresh` (Vite preset). The `no-unused-vars` rule is configured with `varsIgnorePattern: '^[A-Z_]'`, so PascalCase and underscore-prefixed identifiers are allowed to go unused.
