# AGENTS.md

## Cursor Cloud specific instructions

### Project overview
React 17 SPA using Feature-Sliced Design architecture, TypeScript, Webpack 5, Redux Toolkit, and i18next. Mock backend via json-server.

### Node.js version
CI uses Node 20.x. Use `nvm use 20` (already set as default alias).

### Running the application
Two services must run for full development:
- **Frontend**: `npx webpack serve --env port=3000 --no-open` (port 3000). The `npm start` script will fail in headless environments because `webpack.config.ts` hardcodes `browser: 'google chrome'` in the `open` config. Use `--no-open` to bypass.
- **Mock API**: `npm run start:dev:server` (port 8000). Uses json-server with an 800ms artificial delay. Test credentials: username `admin`, password `123`.

### Available npm scripts
See `package.json` for the full list. Key commands:
- `npm run lint:ts` — ESLint for TypeScript
- `npm run lint:scss` — Stylelint for SCSS
- `npm run test:unit` — Jest unit tests
- `npm run build:prod` — Production webpack build
- `npm run storybook` — Storybook (also has the `google chrome` issue; use `BROWSER=none npm run storybook` or run `npx storybook dev -p 6006 -c ./config/storybook`)

### Pre-commit hooks
Husky runs: `build:prod`, `lint:ts`, `lint:scss`, `test:unit`. All must pass before commits.

### Gotchas
- The `open.app.name` in webpack dev server config is hardcoded to `'google chrome'` (macOS name). On Linux/headless, always use `--no-open` flag or the direct `npx webpack serve` command above.
- `npm run storybook` sets `BROWSER='google chrome'` — override with `BROWSER=none` in headless environments.
- Chromatic visual tests (`npm run test:ui`) require `CHROMATIC_PROJECT_TOKEN` env var.
