# keller-solutions/.github

Organization-wide defaults and reusable GitHub Actions workflows for Keller Solutions and client repositories. The organization profile page lives in [`profile/README.md`](profile/README.md).

Pin every call to a release tag (see [Releases](https://github.com/keller-solutions/.github/releases)) so a change here never reaches your repository until you choose to adopt it.

## Reusable workflows

| Workflow | What it does |
|----------|--------------|
| [`bundle-audit.yml`](.github/workflows/bundle-audit.yml) | Fails the build on any open advisory in `Gemfile.lock` |
| [`ruby-ci.yml`](.github/workflows/ruby-ci.yml) | Brakeman, bundler-audit (through `bundle-audit.yml`), importmap audit, RuboCop |
| [`rails-test.yml`](.github/workflows/rails-test.yml) | Rails test suite with PostgreSQL, optional Node.js, Playwright, and system tests |
| [`changelog-version-check.yml`](.github/workflows/changelog-version-check.yml) | Requires a `CHANGELOG.md` version bump on pull requests to `main` |
| [`release.yml`](.github/workflows/release.yml) | Creates a GitHub Release from `CHANGELOG.md` when that version is not yet tagged, with optional Sentry and New Relic markers |

## bundle-audit

```yaml
name: CI

on:
  pull_request:
  push:
    branches: [main]

jobs:
  bundle-audit:
    uses: keller-solutions/.github/.github/workflows/bundle-audit.yml@v0.2.1
```

It installs bundler-audit itself and never runs `bundle install`. Your project does not need bundler-audit in its Gemfile, a `bin/bundler-audit`, or credentials for private gem sources. Ruby comes from your `.ruby-version`. The advisory database is updated on every run.

| Input | Default | Purpose |
|-------|---------|---------|
| `working-directory` | `.` | Directory holding `Gemfile.lock` and `.ruby-version`, for monorepos |
| `runs-on` | `ubuntu-latest` | Runner label, or a JSON array of labels such as `'["self-hosted", "linux"]'` |
| `honor-ignore-list` | `false` | Apply the ignore list in `config-file` |
| `config-file` | `.bundler-audit.yml` | Ignore list location, relative to `working-directory`. Rails 8 apps use `config/bundler-audit.yml` |
| `bundler-audit-version` | `0.9.3` | bundler-audit gem version to install |

**Any open advisory fails the build by default.** bundler-audit normally applies `.bundler-audit.yml` on its own whenever the file exists, so this workflow points it at an empty ignore list instead. Set `honor-ignore-list: true` to accept the risks your ignore list records. The workflow then fails if `config-file` does not exist, so a misplaced file cannot silently disable the check.

Self-hosted runners need Ruby available to [`ruby/setup-ruby`](https://github.com/ruby/setup-ruby#using-self-hosted-runners).

## ruby-ci

`ruby-ci.yml` runs its gem scan through `bundle-audit.yml`, so both workflows apply the same rules. Pass `bundler-audit-honor-ignore-list` and `bundler-audit-config-file` to opt in to an ignore list. `bin/bundler-audit` is no longer required.

## Releasing this repository

Every pull request to `main` must bump the top version in `CHANGELOG.md`. Merging to `main` tags and publishes that version automatically. See [CONTRIBUTING.md](CONTRIBUTING.md).
