# hotel-reservation

hotel-reservation — created with Alpha.

One repository with a frontend and a backend. Each app is a complete project with its own
`package.json`, lockfile, tests and README, and builds and deploys on its own.

| Folder | App | Stack | Runs locally at |
| ------ | --- | ----- | --------------- |
| `apps/web` | Frontend | React | http://localhost:5173 |
| `apps/api` | Backend | Node.js API | http://localhost:3000 |

## Getting started

```bash
cp apps/api/.env.example apps/api/.env
cp apps/web/.env.example apps/web/.env
npm install      # installs both apps
npm run dev      # starts both apps
```

The frontend calls the backend at the URL in its `.env`, and the backend allows the frontend in
`CORS_ORIGINS`; the defaults already point at each other.

## Scripts

Run from the repository root; each runs the same script in both apps, backend first.

| Command | Does |
| ------- | ---- |
| `npm run dev` | Run both apps in watch mode (`dev:api` and `dev:web` run one) |
| `npm run build` | Build both apps |
| `npm test` | Test both apps |
| `npm run typecheck` | Type-check both apps |
| `npm run lint` | Lint both apps |

To work on one app, run its own scripts from its folder, e.g. `cd apps/web && npm test`.

## CI/CD

`.github/workflows/ci-api.yml` (API CI, from `Capstone-Agentic-AI-Orchestration/alphaorch-workflow@v1:workflow-templates/product/monorepo/api-nodejs.yml`) and `.github/workflows/ci-web.yml` (Web CI, from `Capstone-Agentic-AI-Orchestration/alphaorch-workflow@v1:workflow-templates/product/monorepo/web-react.yml`) run each app's unit tests with coverage, lint and security scan, in its own folder, on every push and pull request to `dev`, `uat` and `main`. Both run on every change, so a pull request is always checked against both apps.

Work lands on `dev`, is promoted to `uat`, then to `main`, by pull request only.

Hosting is set up automatically by Alpha: the API on **Render** from `apps/api`, the frontend on **Vercel** from `apps/web`, each pointed at the other. See status, URLs and deploys from this repository’s project in Alpha.
