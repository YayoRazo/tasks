# Codex Bootstrap Runbook

A practical runbook to bring up the environment inside a ChatGPT Codex runner.

## 1) Validate environment
- Ensure `.env` exists or environment variables are set.
- Confirm `POSTGRES_HOST` is `localhost` for local provisioning.

## 2) Bootstrap
Run:
```
./scripts/bootstrap.sh
```

## 3) Verify
```
./scripts/maintenance.sh health
./scripts/maintenance.sh flyway-info
```

## 4) Troubleshoot
- If `psql` not found, install client or rerun bootstrap.
- If Flyway auth fails, ensure the role password was set by bootstrap.
- If DB host is remote, bootstrap will skip PG install and only run migrations.