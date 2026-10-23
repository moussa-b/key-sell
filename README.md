# key-sell

Monorepo (npm workspaces) :

- [`apps/api`](apps/api/README.md) — API NestJS (`@key-sell/api`), image Docker `bdzapps/key-sell-services`
- [`apps/web`](apps/web/README.md) — front Angular (`@key-sell/web`)

```bash
npm install        # à la racine uniquement (un seul package-lock.json / node_modules)
npm run dev:api    # API en watch (http://localhost:3000), lit apps/api/.env
npm run dev:web    # front (http://localhost:4300), proxy /api -> localhost:3000
npm run build      # build des deux apps
npm test           # tests unitaires du front (Karma)
```

Docker (API + MySQL), depuis la racine :

```bash
docker compose up -d
docker build -f apps/api/Dockerfile -t key-sell-services .
```

CI : `.github/workflows/api.yml` (bump version, tag `v<version>`, push Docker Hub, redeploy Coolify) ne se déclenche que sur `apps/api/**` et les fichiers npm racine ; `.github/workflows/web.yml` (bump version, tag `web-v<version>`) uniquement sur `apps/web/**`.
