# Seal Canvas Development Notes

This project is now a browser-only static app. Do not reintroduce a backend, database, login system, account management, or server-side API proxy unless the user explicitly asks for a different product direction.

## Project Shape

- `src/StandaloneApp.tsx`: main app
- `src/StandaloneApp.css`: app styles
- `src/main.tsx`: React entry
- `index.html`: Vite HTML entry
- `vite.config.ts`: Vite config, with relative asset paths for static hosting
- `dist/`: generated static output from `npm run build`

## Commands

- `npm run dev`: start Vite dev server
- `npm run build`: type-check and build static output
- `npm run preview`: preview built output
- `npm run lint`: run ESLint

## Product Rules

- This is an infinite-canvas AI image generation workflow.
- The app is only for generating images.
- UI copy should stay primarily Chinese.
- The interface should remain compact and practical.
- Settings are stored in browser `localStorage`.
- localStorage key: `seal-canvas-settings`
- Do not add login, accounts, SQLite, Express, or API proxy code.
- Do not hardcode shared API keys or private service secrets into frontend code.
- The configured image API must support browser CORS requests.
- Keep the settings UI as a canvas overlay opened from the toolbar settings button.
- The default prompt node must be empty.
- Canvas state intentionally does not persist.
- Refreshing the page starts a new default canvas.
- Keep the `beforeunload` warning to prevent accidental exits.
- Prompt text is capped at 1000 characters.
- No negative prompt field is needed.
- Result node title should stay `结果`.
- Result thumbnails use a 3-column grid.
- Results should support large preview and download.
- Downloading images must not navigate the current page away.

## API Compatibility

Prefer OpenAI-compatible endpoints:

- Text-to-image: `/v1/images/generations`
- Image edit with references: `/v1/images/edits`
- Prompt optimization: `/v1/chat/completions`

Because the app is static, all requests are made directly from the browser. If a provider does not allow CORS, it will not work from this app without a separate user-managed proxy.

## Development Notes

- When changing node behavior, check both TypeScript and CSS impact.
- Keep generated build output out of commits unless the user asks to include it.
- Run `npm run build` after functional changes.
- Run `npm run lint` when changing React hooks, component names, or dependencies.
