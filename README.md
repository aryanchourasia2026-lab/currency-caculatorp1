# Currency Calculator

A single-page currency converter built with plain HTML, CSS, and JavaScript — no frameworks, no build step.

## Features

- Live exchange rates fetched from [open.er-api.com](https://open.er-api.com)
- Real-time recalculation as the amount changes
- "From" / "To" dropdowns pre-populated with major currencies (USD, EUR, GBP, JPY, INR, CAD, AUD, and more)
- Swap button to flip base and target currencies
- Converted amount formatted with `Intl.NumberFormat`, plus the unit exchange rate and a "last updated" UTC timestamp
- Dark theme, responsive layout, and a loading indicator while rates are fetched

## Technology

- Semantic HTML5
- CSS3 (no preprocessors, no frameworks)
- Vanilla JavaScript using `async`/`await` and the Fetch API

## Running locally

This is a static file with no dependencies or build process. Either:

- Open `index.html` directly in a browser, or
- Serve it with any static file server, e.g.:

  ```bash
  npx serve .
  ```

  or with the Netlify CLI:

  ```bash
  netlify dev
  ```
