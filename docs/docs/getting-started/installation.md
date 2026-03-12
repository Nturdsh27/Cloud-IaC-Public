# Installation

Detailed installation for each component of the DevSecOps Starter Kit.

## Terraform Modules

No installation required — reference modules directly from GitHub:

```hcl
module "landing_zone" {
  source = "github.com/Nturdsh27/Cloud-IaC//modules/foundation/landing-zone?ref=v1.0.0"
  # ...
}
```

!!! tip "Pin to a release tag"
    Always use `?ref=vX.Y.Z` in production. Never reference `main` — it may contain breaking changes.

## DSK CLI

=== "macOS (Homebrew)"

    ```bash
    brew install Nturdsh27/tap/dsk
    ```

=== "Linux"

    ```bash
    curl -sSL https://github.com/Nturdsh27/Cloud-IaC/releases/latest/download/dsk_linux_amd64.tar.gz | tar xz
    sudo mv dsk /usr/local/bin/
    ```

=== "Windows"

    ```powershell
    # Download from GitHub Releases
    Invoke-WebRequest -Uri "https://github.com/Nturdsh27/Cloud-IaC/releases/latest/download/dsk_windows_amd64.zip" -OutFile dsk.zip
    Expand-Archive dsk.zip -DestinationPath "$env:LOCALAPPDATA\dsk"
    # Add to PATH
    ```

Verify installation:

```bash
dsk version
```

## GCP Prerequisites

### Required APIs

Enable the APIs used by foundation modules:

```bash
gcloud services enable \
  compute.googleapis.com \
  container.googleapis.com \
  iam.googleapis.com \
  iamcredentials.googleapis.com \
  cloudresourcemanager.googleapis.com \
  secretmanager.googleapis.com \
  logging.googleapis.com \
  monitoring.googleapis.com
```

### Authentication

For local development:

```bash
gcloud auth application-default login
```

For CI/CD, use [Workload Identity Federation](../modules/iam.md) — never service account key files.

## GitHub Actions

The security scanner composite action requires no installation. Reference it in your workflow:

```yaml
- uses: Nturdsh27/Cloud-IaC/.github/actions/security-scan@v1
  with:
    scan_type: "all"
```

Scanner tools (Trivy, Checkov, TruffleHog) are downloaded automatically on each run.
