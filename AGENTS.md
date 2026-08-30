# AGENTS.md

## Project architecture

This project is a single static file: `index.html`. All markup, styles, and behavior live in that one file — there is no build system, bundler, framework, or package.json. This was a deliberate choice per the original request (a portable, self-contained SPA).

## Key structure within `index.html`

- `<style>` block: CSS custom properties define the dark theme palette (`--bg`, `--card`, `--accent`, etc.). Layout is a centered card using flexbox on `body` and a CSS grid for the from/swap/to currency row.
- `<body>` markup: a single `<main class="card">` containing the amount input, currency selectors, swap button, result display, and status line.
- `<script>` block (IIFE): all JavaScript is scoped inside a single immediately-invoked function to avoid polluting the global namespace.

## Data flow

- `CURRENCIES` is a static list of `[code, name]` pairs used to populate both `<select>` elements.
- `fetchRates(base)` calls `https://open.er-api.com/v6/latest/{base}` and caches the response per base currency in `rateCache` (a `Map`) to avoid redundant network calls when the user only changes the amount or target currency.
- Changing the "From" currency triggers a new fetch (`loadAndRender`); changing the amount or "To" currency only recalculates from already-fetched rates (`renderResult`), keeping the UI fast and reducing API calls.
- An `AbortController` cancels an in-flight fetch if the user changes the base currency again before the previous request resolves.

## Conventions

- No external dependencies — do not introduce npm packages, CDNs, or frameworks without discussing the tradeoff first, since the single-file portability is intentional.
- Keep formatting logic (currency display, rate display, timestamps) using built-in `Intl` APIs rather than manual string manipulation.
