# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

## [0.1.2] - 2026-08-05

### Fixed

- Org profile logo pointed at a hashed Astro asset that no longer exists, so the profile page rendered a broken image; now uses the stable `/assets/keller-solutions-logo.svg`
- ChronoMap link pointed at `evanrkeller.github.io`, which 404s since the repo moved to the org
- RouteCraft link pointed at `www.routecraft.app` instead of `flyroutecraft.com`
- Airport Code Quest was described as an "aviation trivia game"; it is a gamified logbook driven by real landings

### Changed

- Profile headline and intro reworded to lead with senior-led delivery
- KS Labs table now lists all five active products, with descriptions matching keller-solutions.com/labs
- Open source table now lists all five public repositories

## [0.1.1] - 2026-02-10

### Security

- Pin all 20 GitHub Actions references to commit SHAs to prevent supply chain attacks (#2)
- Move `${{ }}` expressions out of `run:` blocks into `env:` mappings to prevent template injection (#4)
- Add `persist-credentials: false` to all `actions/checkout` steps to prevent credential leakage (#5)

## [0.1.0] - 2026-02-10

### Added

- Reusable workflow: `ruby-ci.yml` — Brakeman, bundler-audit, importmap audit, RuboCop
- Reusable workflow: `rails-test.yml` — Rails test suite with PostgreSQL, optional Node.js, Playwright, and system tests
- Reusable workflow: `changelog-version-check.yml` — Enforces CHANGELOG version bump on PRs to main
- Reusable workflow: `release.yml` — Creates GitHub Releases from CHANGELOG with optional Sentry and New Relic markers
- Organization profile README

### Fixed

- Handle Brakeman exit code 5 (outdated version) as a warning instead of failure
- Guard against missing `bin/bundler-audit` and `package.json` in reusable workflows
- Default `.node-version` fallback when file does not exist

[Unreleased]: https://github.com/keller-solutions/.github/compare/v0.1.2...HEAD
[0.1.2]: https://github.com/keller-solutions/.github/compare/v0.1.1...v0.1.2
[0.1.1]: https://github.com/keller-solutions/.github/compare/v0.1.0...v0.1.1
[0.1.0]: https://github.com/keller-solutions/.github/releases/tag/v0.1.0
