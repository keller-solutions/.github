# Contributing to Keller Solutions Projects

## Development Workflow

1. **Prepare**: Orient to the project and update dependencies
2. **Plan**: Create a story and GitHub issue with acceptance criteria
3. **Produce**: Implement using Test-Driven Development (red-green-refactor)
4. **Present**: Self-review and create PR

## Branch Strategy

- `main` - Production-ready code, tagged releases only
- `develop` - Integration branch (where applicable)
- `feature/*` - Feature branches
- `fix/*` or `bugfix/*` - Bug fix branches
- `hotfix/*` - Urgent production fixes

## Code Style

Follow the conventions of the project's language and framework. Run linters before committing.

## Testing

All code changes require tests. We practice TDD:

1. **Red**: Write a failing test
2. **Green**: Write minimal code to pass
3. **Refactor**: Clean up while tests stay green

## Commit Messages

Use [Conventional Commits](https://www.conventionalcommits.org/) format:

```
<type>(scope): description
```

Types: `feat`, `fix`, `docs`, `style`, `refactor`, `test`, `chore`

Include AI co-authorship when applicable:

```
Co-Authored-By: Claude Opus 4.6 <noreply@anthropic.com>
```

## Changelog

We follow [Keep a Changelog](https://keepachangelog.com/) and [Semantic Versioning](https://semver.org/).

### During Development

Add changes to the `[Unreleased]` section of `CHANGELOG.md`:

```markdown
## [Unreleased]

### Added
- Your new feature description ([#PR_NUMBER])
```

Categories: **Added**, **Changed**, **Deprecated**, **Removed**, **Fixed**, **Security**

### Before Merging to Main

1. Move `[Unreleased]` changes to a new version section with today's date
2. Update comparison links at the bottom of CHANGELOG.md
3. Add PR reference links

### CI Validation

PRs to main must bump the CHANGELOG version. CI will fail if:
- The version is unchanged from main
- The new version is not greater than the current version

## PR Feedback

Every review comment gets a response:

- **If you agree**: Make the change, commit, then reply with the commit SHA
- **If you disagree**: Reply with a clear rationale referencing relevant patterns or guidelines

Never ignore feedback.
