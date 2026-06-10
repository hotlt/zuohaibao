# Seal Canvas

Seal Canvas is a browser-only AI image generation canvas. It uses React Flow-style nodes to connect prompts, reference images, generation settings, and result previews into a lightweight image workflow.

The app has no backend, no database, and no login system. Model API settings are saved in the current browser's `localStorage`.

## Features

- Infinite canvas workflow for AI image generation
- Prompt, reference image, generation, and result nodes
- Multiple image providers and models
- OpenAI-compatible image generation and image edit endpoints
- Prompt optimization through an OpenAI-compatible chat completions endpoint
- Local browser settings with no server-side storage
- Static build output suitable for GitHub Pages, Netlify, Vercel, nginx, or any static hosting service

## Requirements

- Node.js 22 or newer
- npm 10 or newer
- An image generation API compatible with:
  - `POST /v1/images/generations`
  - `POST /v1/images/edits`
- Optional prompt optimization API compatible with:
  - `POST /v1/chat/completions`

The API must support browser CORS requests because Seal Canvas calls it directly from the browser.

## Getting Started

```bash
npm install
npm run dev
```

Open the local Vite URL, then use the settings button in the canvas toolbar to configure your API base URL, API key, and models.

## Build

```bash
npm run build
```

The static site is generated into `dist/`.

To test the production build locally:

```bash
npm run preview
```

## Privacy And Security

Seal Canvas is a static web app. API keys are stored in the browser's `localStorage` under `seal-canvas-settings` and are sent directly from the browser to the configured API provider.

Do not deploy this app with shared API keys embedded in the source code. For public deployments, each user should configure their own API credentials.

## License

MIT
