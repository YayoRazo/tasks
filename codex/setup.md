# Codex Setup

Use this guide to configure a ChatGPT Codex (custom GPT) to safely run the bootstrap and maintenance workflows for this repository.

## Repository layout
```
/codex
  AGENTS.md
  bootstrap_runbook.md
  postgresql_schema_reviewer.md
  setup.md
/scripts
  bootstrap.sh
  maintenance.sh
/flyway/sql
  000_base/001__create_db.sql
  ...
```

## Secrets to define in Codex (Environment)
- `POSTGRES_DB`
- `POSTGRES_USER`
- `POSTGRES_PASSWORD`
- `POSTGRES_HOST`
- `POSTGRES_PORT`

Do not store secrets in the repository or prompts.

## Typical sequence (Codex)
1. `./scripts/bootstrap.sh`  (provisions local PG in Codex if host is localhost and runs migrations)
2. `./scripts/maintenance.sh health`
3. `./scripts/maintenance.sh flyway-info`