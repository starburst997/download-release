# Claude Code Configuration

This repository contains a GitHub Action for downloading release assets with smart version resolution.

## Project Structure

- `action.yml` - Main action configuration with composite steps
- `README.md` - User documentation and examples

## Development Notes

This action uses:
- **Composite action architecture** - Uses shell steps rather than JavaScript/Docker
- **Smart version resolution** - Major versions like `v1` resolve to latest `v1.x.x`
- **GitHub CLI** - Uses `gh` commands for authenticated API access
- **Auto-extraction** - Automatically extracts common archive formats

## Key Features

1. **Zero configuration** - Works with smart defaults for common use cases
2. **Version resolution** - `v1` → latest `v1.x.x`, `v1.2.3` → exact version
3. **Pattern matching** - Download specific files using glob patterns
4. **Authentication** - Uses GitHub token for private repos and rate limiting

## Common Commands

Since this is a pure GitHub Action without build steps:
- No compilation required
- No dependencies to install
- Direct testing via workflow runs

## Testing

Test the action by:
1. Creating a workflow in `.github/workflows/test.yml`
2. Using different version patterns (`v1`, `v1.2.3`, `latest`)
3. Testing with different repositories and file patterns

## Release Process

1. Test changes in a workflow
2. Tag a new version: `git tag v1.x.x`
3. Update major version tag: `git tag -f v1`
4. Push tags: `git push --tags --force`