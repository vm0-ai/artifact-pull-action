# VM0 Artifact Pull Action

Pull VM0 cloud artifacts to your GitHub Actions workflow.

## Usage

```yaml
- uses: vm0-ai/artifact-pull-action@v1
  with:
    artifact-name: "my-artifact"
    vm0-token: ${{ secrets.VM0_TOKEN }}
```

## Inputs

| Input | Description | Required | Default |
|-------|-------------|----------|---------|
| `artifact-name` | Artifact name to pull | Yes | - |
| `path` | Destination path for the artifact | No | `.` |
| `version-id` | Version ID to pull | No | `latest` |
| `vm0-token` | VM0 authentication token | Yes | - |
| `vm0-api-url` | VM0 API URL | No | `https://www.vm0.ai` |
| `cli-version` | @vm0/cli version to install | No | `latest` |

## Outputs

| Output | Description |
|--------|-------------|
| `success` | Whether the pull completed successfully |

## Examples

### Basic Usage

```yaml
name: Pull Artifact

on: [workflow_dispatch]

jobs:
  pull:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4

      - name: Pull VM0 Artifact
        uses: vm0-ai/artifact-pull-action@v1
        with:
          artifact-name: "my-data"
          path: "./data"
          vm0-token: ${{ secrets.VM0_TOKEN }}

      - name: Use artifact
        run: ls -la ./data
```

### With GitHub Artifacts

Pull VM0 artifact and upload to GitHub Artifacts for use in other jobs or workflows:

```yaml
name: Sync VM0 to GitHub Artifact

on: [workflow_dispatch]

jobs:
  sync:
    runs-on: ubuntu-latest
    steps:
      - name: Pull VM0 Artifact
        uses: vm0-ai/artifact-pull-action@v1
        with:
          artifact-name: "my-data"
          path: "./data"
          vm0-token: ${{ secrets.VM0_TOKEN }}

      - name: Upload to GitHub Artifacts
        uses: actions/upload-artifact@v4
        with:
          name: my-data
          path: ./data
```

## License

MIT
