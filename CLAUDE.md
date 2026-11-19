# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

An unmodified Create React App (react-scripts 5.0.1) scaffold running React 19. Plain JavaScript (no TypeScript), no router, no state library, and no backend. The build, lint, and test configuration lives inside `react-scripts`; there are no webpack, Babel, or Jest config files in the repo.

## Commands

- `npm start`: dev server at http://localhost:3000 with hot reload. Lint errors appear in the console and browser overlay.
- `npm run build`: production build into `build/`.
- `npm test`: Jest in interactive watch mode.
  - Run once without watch (for CI or non-interactive shells): `CI=true npm test`
  - Run a single test file: `CI=true npm test -- src/App.test.js`
  - Run tests by name: `CI=true npm test -- -t "renders learn react link"`
- Linting: there is no separate lint script. ESLint runs during `start` and `build` with the `react-app` and `react-app/jest` configs (set in `package.json` under `eslintConfig`). To lint directly, run `npx eslint src`.
- Do not run `npm run eject`. It is one-way and copies all the hidden build config into the repo.

## Architecture

- `public/index.html` provides the `#root` element. `src/index.js` mounts `<App />` there with `ReactDOM.createRoot` inside `React.StrictMode`, so effects run twice in development.
- `src/App.js` is the top-level component, and new UI should hang off it. Components import their CSS files directly (for example, `import './App.css'`). CRA bundles these as global CSS, not CSS modules, unless a file is named `*.module.css`.
- Tests sit next to source files as `*.test.js` and use React Testing Library. `src/setupTests.js` loads the `@testing-library/jest-dom` matchers automatically before every test.
- `src/reportWebVitals.js` is an optional performance hook. It does nothing unless a callback is passed in `index.js`.
- Only environment variables prefixed with `REACT_APP_` reach client code (a CRA rule).
