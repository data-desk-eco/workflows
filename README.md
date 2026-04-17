# Data Desk shared workflows

Reusable GitHub Actions workflows for Data Desk notebook repos.

This repo is **public** so that public notebook repos can call the workflows. Private notebook repos call them too — same workflow, both visibility tiers.

## `notebook-deploy.yml`

Builds an Observable Notebook Kit site and deploys to GitHub Pages.

```yaml
jobs:
  deploy:
    uses: data-desk-eco/workflows/.github/workflows/notebook-deploy.yml@main
    permissions:
      contents: write
      pages: write
      id-token: write
    secrets: inherit
```

### Inputs

| Input | Default | Notes |
|-------|---------|-------|
| `skip_data` | `false` | Skip the `make data` step |
| `install_uv` | `false` | Install [uv](https://github.com/astral-sh/uv) before `make data` (for repos whose Makefile shells out to `uv run …`) |

### Required secrets

- `GH_PAT` — personal access token with `repo:read` on `data-desk-eco/.github` (used to fetch shared `.claude/` skills and `template.html`).
- `CLAUDE_CODE_OAUTH_TOKEN` *(optional)* — installs `@anthropic-ai/claude-code` if set so `make data` can shell out to `claude`.

Both are configured at the org level; `secrets: inherit` passes them through.
