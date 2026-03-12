# Multi-Scanner CI/CD

One GitHub Action. Four security scanners. Every PR scanned automatically.

## What It Does

A composite GitHub Action that runs:

1. **TruffleHog** — detect leaked secrets, API keys, passwords
2. **Trivy** — container image CVEs and IaC misconfigurations
3. **Checkov** — Terraform and Dockerfile security checks
4. **tfsec** — Terraform-specific security rules

All output as **SARIF** and uploaded to GitHub's Security tab.

## Usage

```yaml
# .github/workflows/security.yml
name: Security Scan
on: [pull_request]

jobs:
  scan:
    runs-on: ubuntu-latest
    permissions:
      security-events: write
    steps:
      - uses: actions/checkout@v4
      - uses: Nturdsh27/Cloud-IaC/.github/actions/security-scan@v1
        with:
          scan_type: "all"
```

That's it. One step, four scanners, SARIF results on the Security tab.

## Configuration

| Input | Default | Description |
|-------|---------|-------------|
| `scan_type` | `"all"` | `all`, `container`, `iac`, or `secrets` |
| `severity_threshold` | `"HIGH"` | Fail on this severity or above |
| `image` | — | Container image to scan (for `container` type) |

## Scan Types

=== "All"

    ```yaml
    - uses: Nturdsh27/Cloud-IaC/.github/actions/security-scan@v1
      with:
        scan_type: "all"
    ```

=== "IaC Only"

    ```yaml
    - uses: Nturdsh27/Cloud-IaC/.github/actions/security-scan@v1
      with:
        scan_type: "iac"
    ```

=== "Container"

    ```yaml
    - uses: Nturdsh27/Cloud-IaC/.github/actions/security-scan@v1
      with:
        scan_type: "container"
        image: "myapp:latest"
    ```

=== "Secrets"

    ```yaml
    - uses: Nturdsh27/Cloud-IaC/.github/actions/security-scan@v1
      with:
        scan_type: "secrets"
    ```

## What the Paid Tier Adds

- **Per-repo config file** (`.dsk-scan.yml`) — enable/disable scanners, set severity thresholds
- **PR comment summaries** — inline findings with fix suggestions
- **Parallel scanning** — matrix strategy for speed
- **Unified JSON output** — aggregated results for dashboard ingestion
- **Scanner DB caching** — faster runs via cached vulnerability databases
