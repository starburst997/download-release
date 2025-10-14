# Download Release Assets

A GitHub Action that intelligently downloads release assets with automatic version resolution.

## Features

- **Smart Version Resolution**: `v1` automatically resolves to the latest `v1.x.x` release
- **Pattern Matching**: Download specific files using glob patterns
- **Auto-Extraction**: Automatically extracts ZIP, TAR, and TAR.GZ archives
- **Authenticated**: Uses GitHub token for private repositories and rate limiting

## Usage

### Zero Configuration (uses defaults)

```yaml
# Downloads release.zip from current repository using current action ref
- name: Download release
  uses: starburst997/download-release@v1
```

### Basic Example

```yaml
- name: Download release
  uses: starburst997/download-release@v1
  with:
    repository: "owner/repo"
    tag: "v1.2.3"
    pattern: "*.zip"
```

### Smart Version Resolution

```yaml
- name: Download latest v1 release
  uses: starburst997/download-release@v1
  with:
    repository: "owner/repo"
    tag: "v1" # Resolves to latest v1.x.x
    pattern: "release.zip"
    extract-to: "./dist"
```

### Advanced Example

```yaml
- name: Download and extract
  id: download
  uses: starburst997/download-release@v1
  with:
    repository: "owner/repo"
    tag: "latest"
    pattern: "*.tar.gz"
    extract-to: "./build"
    token: ${{ secrets.GITHUB_TOKEN }}

- name: Use downloaded files
  run: |
    echo "Downloaded to: ${{ steps.download.outputs.download-path }}"
    echo "Resolved tag: ${{ steps.download.outputs.resolved-tag }}"
```

## Inputs

| Input        | Description                                     | Required | Default                      |
| ------------ | ----------------------------------------------- | -------- | ---------------------------- |
| `repository` | Repository in `owner/name` format               |          | `${{ github.repository }}`   |
| `tag`        | Release tag (supports `v1`, `v1.2.3`, `latest`) |          | `${{ github.action_ref }}`   |
| `pattern`    | File pattern to download                        |          | `release.zip`                |
| `extract-to` | Directory to extract files to                   |          | `${{ runner.temp }}/release` |
| `token`      | GitHub token for authentication                 |          | `${{ github.token }}`        |

## Outputs

| Output          | Description                        |
| --------------- | ---------------------------------- |
| `resolved-tag`  | The actual tag that was downloaded |
| `download-path` | Path where files were extracted    |

## Version Resolution

- `v1` → Latest `v1.x.x` release
- `v1.2.3` → Exact version `v1.2.3`
- `latest` → Latest release (any version)

## License

MIT
