# Contributing — Klaapp engineering standard

This document is the org-wide default. It applies to every KlaappInc repository
unless a repo overrides it with its own `CONTRIBUTING.md`.

## Branching model — Git Flow

| Branch        | Role                                              |
|---------------|---------------------------------------------------|
| `develop`     | Default & integration branch. All work targets it.|
| `main`        | Production. Tagged. Only `release/*` and `hotfix/*` merge here. |
| `feature/*`   | New work. Branch from `develop`, PR back to `develop`. |
| `fix/*`       | Bug fixes. Branch from `develop`, PR back to `develop`. |
| `release/*`   | Optional stabilization. Branch from `develop`, PR to `main`. |
| `hotfix/*`    | Urgent prod fix. Branch from `main`, PR to `main`, then back-merge to `develop`. |

Both `develop` and `main` are protected: PRs only, ≥1 approval, conversation
resolution required, no force-push, no deletion. Org admins can bypass for
break-glass situations.

## Commits — Conventional Commits (required)

Every PR is checked by `commitlint`. Use the Conventional Commits format:

```
<type>(<optional scope>): <subject>

feat:     a new feature            → minor version bump
fix:      a bug fix                → patch version bump
feat!: / BREAKING CHANGE:          → major version bump
chore:, docs:, ci:, refactor:, test:, build:, perf:, style:  → no release
```

This is what lets release-please compute versions and changelogs automatically.

## Releases — release-please

1. Land `feat`/`fix` PRs into `develop`.
2. Promote to `main` (directly, or via a `release/x.y` stabilization branch).
3. On push to `main`, **release-please** opens/updates a release PR that bumps the
   version and updates `CHANGELOG.md`.
4. Merging that release PR creates the **git tag + GitHub Release**, which triggers
   the repo's deploy/publish workflow (wrangler / EAS / npm / docker).
5. Back-merge `main` → `develop`.

Do not hand-edit version numbers or tags — release-please owns them.

## Dependencies — Dependabot

Dependabot is configured per repo to open PRs against `develop` on a weekly
schedule, using `build(deps)` / `ci(deps)` commit prefixes so they pass commitlint.
