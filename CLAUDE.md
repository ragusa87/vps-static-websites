# CLAUDE.md

## Convention

Each top-level folder is a dedicated static application. The folder name is the
URL (hostname); its `index.html` is served statically at that host. Everything
inside is served as-is — no build step.

## Autodeploy

A hook autodeploys changes: any push to `main` triggers a deploy webhook
(`.github/workflows/deploy.yml`), which regenerates the Traefik routing config
via `upgrade.sh` and reloads the shared Caddy container. **Committing and
pushing to `main` is all that is needed to publish** — there is no manual deploy
step.

## Adding a new learning website

See the "how to add a new learning website" skill.
