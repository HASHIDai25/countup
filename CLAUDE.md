# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project status

This repository is newly initialized: it contains only the dev container configuration (`.devcontainer/`) and has no application code, build scripts, or tests yet. Update this file with build/test/lint commands and architecture notes once code is added.

## Development environment

The project runs in a Dev Container based on the "Go & PostgreSQL" template:

- **app** service: `mcr.microsoft.com/devcontainers/go` image (Go 1.27, Debian trixie), with Node.js and Claude Code added as features. The repo is mounted at `/workspaces/countup`.
- **db** service: `postgres:latest`, data persisted in the `postgres-data` volume.
- The app container uses `network_mode: service:db`, so PostgreSQL is reachable from the app at `localhost:5432`.
- Database credentials come from `.devcontainer/.env` (`POSTGRES_USER`, `POSTGRES_PASSWORD`, `POSTGRES_DB`, `POSTGRES_HOSTNAME`), which is loaded as environment variables into both containers. Read connection settings from these env vars rather than hardcoding them.

## Git

The workspace is mounted with root ownership, so git may fail with "detected dubious ownership". Fix with:

```
git config --global --add safe.directory /workspaces/countup
```
