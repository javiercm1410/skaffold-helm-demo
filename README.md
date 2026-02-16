# skaffold-test

Sample Next.js (TypeScript) app for testing deployment methods.

## Commands

- `npm run dev` - Run local development server
- `npm run build` - Create production build artifacts
- `npm run start` - Run the production build
- `npm run lint` - Run ESLint checks

## Quick Test

```bash
npm install
npm run build
npm run start
```

## Skaffold + Taskfile

This project has two Skaffold modules:

- `skaffold-test-app` (local chart in `.helm`)
- `skaffold-test-db` (Bitnami `postgresql` remote chart with `.helm-db/values.yaml`)

Use `Taskfile.yml` helpers:

```bash
# Build + deploy app module (recommended for app)
task app:run

# Deploy db module only
task db:deploy

# Build + deploy app + db
task all:run

# Override environment/profile and repo
task app:run PROFILE=production DEFAULT_REPO=docker.io/jamaca1410
task db:deploy PROFILE=uat DEFAULT_REPO=docker.io/jamaca1410
```

If you really want `deploy` for the app module, you must provide prebuilt image tags:

```bash
task app:deploy PROFILE=stage DEFAULT_REPO=docker.io/jamaca1410 IMAGES=docker.io/jamaca1410/skaffold-test:my-tag
```

Why your command failed:

- `skaffold deploy -m skaffold-test-app` does not build images.
- The app chart expects a tagged image (`skaffold-test`) but none was provided.
- Use `skaffold run` (or `task app:run`) to build + tag + deploy in one step.

## TODO

- Add cache configs
- See multiple helm chart declaration
