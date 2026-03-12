# IAM & Workload Identity

Least-privilege service accounts and zero-trust CI/CD authentication.

## What It Does

- **Service account module** with pre-built role templates for common patterns
- **Zero SA key files** — Workload Identity Federation for GitHub Actions (Better tier)
- **Least-privilege by default** — no `roles/editor` or `roles/owner`, ever

## Usage

### Service Account (Good Tier)

```hcl
module "app_sa" {
  source = "github.com/Nturdsh27/Cloud-IaC//modules/foundation/iam/service-account"

  project_id   = "your-project-id"
  account_id   = "app-runner"
  display_name = "Application Runtime SA"

  project_roles = [
    "roles/cloudsql.client",
    "roles/secretmanager.secretAccessor",
    "roles/logging.logWriter",
    "roles/monitoring.metricWriter",
  ]
}
```

### Pre-built Templates

| Template | Roles | Use Case |
|----------|-------|----------|
| `ci-cd` | `artifactregistry.writer`, `container.developer` | CI/CD pipeline |
| `app-runtime` | `cloudsql.client`, `secretmanager.secretAccessor`, `logging.logWriter` | Application workload |
| `monitoring` | `monitoring.metricWriter`, `logging.logWriter` | Observability agents |

## Inputs

| Variable | Type | Default | Description |
|----------|------|---------|-------------|
| `project_id` | `string` | — | GCP project ID |
| `account_id` | `string` | — | SA account ID (unique within project) |
| `display_name` | `string` | — | Human-readable name |
| `project_roles` | `list(string)` | — | IAM roles to bind at project level |

## Outputs

| Output | Description |
|--------|-------------|
| `email` | Service account email |
| `id` | Service account unique ID |

## Security Controls

- [x] No SA key generation — keys are an anti-pattern
- [x] Roles scoped to minimum required permissions
- [x] No `roles/editor` or `roles/owner` allowed
- [x] SA naming convention enforced

## What the Paid Tier Adds

- **Workload Identity Federation** — GitHub Actions authenticates via OIDC, zero key files
- **Custom IAM roles** — narrower than GCP predefined roles
- **SA key creation alerting** — instant Slack alert if anyone creates a key
- **Organization-level IAM audit policy**

