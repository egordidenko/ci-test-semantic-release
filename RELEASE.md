# Release Process Documentation

## Overview
This repository now has a fully automated release process using semantic-release. The process is designed to only trigger manually and will automatically:
1. Create git tags
2. Update the CHANGELOG.md file
3. Create GitHub releases
4. Publish to npm

## How to Trigger a Release

Releases can only be triggered manually by:
1. Going to the "Actions" tab in GitHub
2. Selecting the "Release" workflow
3. Clicking "Run workflow"
4. Selecting the branch (typically `main`)
5. Clicking "Run workflow"

## What Happens During a Release

When the release workflow runs, it will:

1. **Analyze Commits**: Examines commit messages since the last release to determine the version bump type (major, minor, patch)
2. **Generate Release Notes**: Creates release notes from conventional commits
3. **Update CHANGELOG.md**: Adds the new version and release notes to the changelog
4. **Update package.json**: Bumps the version number
5. **Publish to npm**: Publishes the package to npm registry
6. **Create Git Tag**: Creates a git tag for the new version
7. **Commit Changes**: Commits the updated CHANGELOG.md, package.json, and package-lock.json with message `chore(release): X.Y.Z [skip ci]`
8. **Create GitHub Release**: Creates a release in GitHub with the release notes

## Commit Message Convention

To ensure proper versioning, use conventional commit messages:

- `feat: description` - Triggers a minor version bump (0.X.0)
- `fix: description` - Triggers a patch version bump (0.0.X)
- `BREAKING CHANGE:` in commit body - Triggers a major version bump (X.0.0)

Example:
```
feat: add new user authentication

This commit adds JWT-based authentication for users.
```

## Configuration Files

- `.releaserc.json` - Semantic-release configuration
- `CHANGELOG.md` - Automatically updated changelog
- `.github/workflows/release.yml` - GitHub Actions workflow for releases

## Requirements

- All commits must be pushed to the `main` branch before triggering a release
- The workflow requires a GITHUB_TOKEN (automatically provided by GitHub Actions)
- The workflow requires an NPM_AUTH_TOKEN secret (configured in repository settings) for publishing to npm
- Releases will only work from the `main` branch

## NPM Token Setup

To publish to npm, you need to set up an NPM_AUTH_TOKEN secret:

1. Go to npmjs.com and create an access token (Automation or Publish type)
2. In your GitHub repository, go to Settings → Secrets and variables → Actions
3. Add a new secret named `NPM_AUTH_TOKEN` with your npm token
4. The workflow maps this secret to the NPM_TOKEN environment variable used by semantic-release for npm authentication

## Testing Locally

You can test the release configuration locally (dry-run mode):

```bash
npm install
npx semantic-release --dry-run --no-ci
```

This will show what would happen during a release without actually performing it.
