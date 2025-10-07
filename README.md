GitHub Actions for Ideogrow

This repository centralizes automations for the Ideogrow projects (including Winclo). Workflows live in `.github/workflows/` and are designed to be org-wide and repo-agnostic.

Workflows

1) Daily Process APIs

- File: `.github/workflows/daily-cron.yml`
- Schedule: daily at 00:00 UTC
- Action: POSTs to configured process endpoints with an `x-cron-secret` header
- Secret required:
  - `CRON_SECRET`: shared secret your API validates

2) Keep Render Service Awake

- File: `.github/workflows/render-keepalive.yml`
- Schedule: every 5 minutes
- Action: GET `https://api.winclo.ai/` and fail on non-200 to surface issues

Project Scope

- IdeoGrow organization-wide workflows
- Winclo API keepalive and scheduled processing
- Extend by adding more per-project workflows under `.github/workflows/`

Managing Secrets

1) Go to: Repository Settings → Secrets and variables → Actions
2) Add secret `CRON_SECRET` with the value your API expects

Manual Runs

All workflows support manual triggers:

- GitHub → Actions → select workflow → Run workflow

Modifying Endpoints

- Edit the URLS array in `daily-cron.yml` to add/remove process endpoints
- Keepalive target can be changed by editing the `url` variable in `render-keepalive.yml`

Notes

- Backend scheduler and Firebase-based locks were removed; scheduling is handled entirely here
- Schedules use UTC; adjust cron expressions if you need a different cadence
