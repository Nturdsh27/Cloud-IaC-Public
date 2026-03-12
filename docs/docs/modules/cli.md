# Developer CLI (`dsk`)

A Go CLI that wraps security scanning, scaffolding, and validation into developer-friendly commands.

## Commands

### `dsk scan`

Run security scans locally — same scanners as CI/CD.

```bash
dsk scan --type all          # run all scanners
dsk scan --type iac          # Terraform/Dockerfile only
dsk scan --type secrets      # TruffleHog only
dsk scan --type container --image myapp:latest
```

### `dsk init`

Scaffold a new repository from secure templates.

```bash
dsk init go-service my-api          # Go service with Dockerfile + CI
dsk init python-service my-worker   # Python with FastAPI + CI
dsk init terraform-module my-infra  # Terraform module with tests
```

Each template includes:

- Pre-configured CI/CD workflow with security scanning
- Dockerfile following container security best practices
- `.securityignore.yml` template
- README with usage instructions

### `dsk validate`

Pre-commit validation: OPA policies against Terraform plan.

```bash
dsk validate                 # validate current directory
dsk validate ./modules/gke/  # validate specific module
```

## Installation

=== "macOS"

    ```bash
    brew install Nturdsh27/tap/dsk
    ```

=== "Linux"

    ```bash
    curl -sSL https://github.com/Nturdsh27/Cloud-IaC/releases/latest/download/dsk_linux_amd64.tar.gz | tar xz
    sudo mv dsk /usr/local/bin/
    ```

## Configuration

The CLI reads `.dsk.yml` from the repo root:

```yaml
# .dsk.yml
scan:
  severity_threshold: HIGH
  scanners:
    trivy: true
    checkov: true
    trufflehog: true
    tfsec: false
validate:
  policy_dir: policies/terraform/
```

## What the Paid Tier Adds

- `dsk deploy [env]` — trigger ephemeral environments
- `dsk secrets [get|set]` — read/write from Vault or Secret Manager
- `dsk audit [resource]` — show IAM bindings for a GCP resource
- `dsk drift [module]` — check for infrastructure drift
- `dsk status` — security posture summary across all modules
