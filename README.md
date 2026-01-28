# ci-test-semantic-release

A test project demonstrating automated semantic versioning, changelog generation, and npm publishing using semantic-release.

## Features

- ✅ Automated semantic versioning based on conventional commits
- ✅ Automatic changelog generation
- ✅ Git tags for each release
- ✅ GitHub releases with release notes
- ✅ NPM publishing
- ✅ Manual release trigger (workflow_dispatch)

## Installation

```bash
npm install ci-test-semantic-release
```

## Development

```bash
# Install dependencies
npm install

# Start dev server
npm run dev

# Build for production
npm run build

# Run TypeScript type checking
npm run typecheck
```

## Release Process

Releases are triggered manually via GitHub Actions:

1. Go to the "Actions" tab
2. Select the "Release" workflow
3. Click "Run workflow" on the main branch
4. The workflow will:
   - Analyze commits and determine version
   - Update CHANGELOG.md
   - Create a git tag
   - Create a GitHub release
   - Publish to npm

## Commit Convention

Use conventional commits for proper versioning:

- `feat: description` - Minor version bump (0.X.0)
- `fix: description` - Patch version bump (0.0.X)
- `BREAKING CHANGE:` - Major version bump (X.0.0)

## License

MIT
