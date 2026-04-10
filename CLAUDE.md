# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Finance Tracker — a React expense/income tracker app. Course starter project that intentionally contains bugs, poor UI, and messy code to be fixed as exercises.

## Commands

- `npm run dev` — start Vite dev server (http://localhost:5173)
- `npm run build` — production build to `dist/`
- `npm run lint` — ESLint across all JS/JSX files
- `npm run preview` — preview production build

No test framework is configured.

## Architecture

Single-component React app (React 19, Vite 7, plain CSS, no TypeScript).

All application logic lives in `src/App.jsx` — state, form handling, filtering, and rendering are co-located in one component. There is no routing, no backend, and no external state management.

Transaction data is hardcoded in component state (no persistence). Amounts are stored as strings, which causes arithmetic bugs in the summary calculations (string concatenation instead of numeric addition).

## Known Issues

- `amount` values are strings — `totalIncome`/`totalExpenses` use `reduce` with `+` which concatenates instead of summing
- "Freelance Work" seed data is marked as `type: "expense"` but is logically income
- No delete functionality despite `.delete-btn` styles existing in CSS

## Lint Configuration

ESLint uses flat config (`eslint.config.js`) with `react-hooks` and `react-refresh` plugins. The `no-unused-vars` rule ignores variables starting with uppercase or underscore (`varsIgnorePattern: '^[A-Z_]'`).
