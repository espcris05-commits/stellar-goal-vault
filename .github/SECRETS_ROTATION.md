# Secrets Rotation Guide

## Environment Variables Required

| Variable | Description | Rotation |
|----------|-------------|----------|
| `STELLAR_SECRET_KEY` | Stellar secret key for campaign operations | Every 90 days |
| `GITHUB_TOKEN` | GitHub API token for issue creation | Every 90 days |
| `DATABASE_URL` | PostgreSQL connection string | On credential change |

## Rotating Secrets in GitHub Actions

1. Go to Settings → Secrets and variables → Actions
2. Update the secret value
3. Restart the deployment to pick up the new value

## Rotation Automation

This can be automated with a scheduled workflow:

```yaml
name: Rotate Secrets
on:
  schedule:
    - cron: "0 0 1 */3 *"  # First day of every 3rd month
  workflow_dispatch:
jobs:
  rotate:
    runs-on: ubuntu-latest
    steps:
      - name: Check rotation due
        run: echo "Trigger manual rotation via Secrets page"
```

## Local Development

For local development, copy `.env.example` to `.env` and fill in values.
Never commit `.env` files to the repository.
