# GitHub Actions Reference

Composite actions and reusable workflows provided by the kit.

## Security Scan Action

**Path:** `Nturdsh27/Cloud-IaC/.github/actions/security-scan@v1`

### Usage

```yaml
- uses: Nturdsh27/Cloud-IaC/.github/actions/security-scan@v1
  with:
    scan_type: "all"
    severity_threshold: "HIGH"
```

### Inputs

| Input | Required | Default | Description |
|-------|----------|---------|-------------|
| `scan_type` | No | `all` | `all`, `container`, `iac`, `secrets` |
| `severity_threshold` | No | `HIGH` | Fail on this severity: `CRITICAL`, `HIGH`, `MEDIUM`, `LOW` |
| `image` | No | — | Container image (required when `scan_type` is `container`) |

### Outputs

| Output | Description |
|--------|-------------|
| `sarif_files` | Comma-separated list of generated SARIF files |
| `findings_count` | Total number of findings |
| `critical_count` | Number of CRITICAL findings |
| `high_count` | Number of HIGH findings |

### Required Permissions

```yaml
permissions:
  security-events: write  # upload SARIF to Security tab
  contents: read          # checkout code
```

### What Runs

1. **TruffleHog** → `trufflehog.sarif`
2. **Trivy** (IaC + container) → `trivy.sarif`
3. **Checkov** (Terraform + Dockerfile) → `checkov.sarif`
4. All SARIF files uploaded to GitHub Security tab via `github/codeql-action/upload-sarif`

### Scanner Versions

Scanners are pulled at their latest stable version on each run. To pin versions, use the paid tier's `.dsk-scan.yml` configuration.
