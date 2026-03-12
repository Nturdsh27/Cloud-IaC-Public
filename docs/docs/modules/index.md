# Modules

All modules in the DevSecOps Starter Kit, organized by domain.

## Cloud Foundation

Build a secure GCP base layer.

| Module | Description | Tier |
|--------|-------------|------|
| [Landing Zone](landing-zone.md) | VPC, subnets, Cloud NAT, firewall rules | :material-lock-open: Free |
| [IAM & Workload Identity](iam.md) | Service accounts, least-privilege roles, WIF | :material-lock-open: Free |

## Security Pipeline

Automate security scanning in CI/CD.

| Module | Description | Tier |
|--------|-------------|------|
| [Multi-Scanner CI/CD](multi-scanner.md) | Trivy + Checkov + TruffleHog in one Action | :material-lock-open: Free |
| [Container Signing (Cosign)](cosign.md) | Keyless image signing with Sigstore | :material-lock-open: Free |

## Policy & Compliance

Enforce security standards as code.

| Module | Description | Tier |
|--------|-------------|------|
| [Policy-as-Code (OPA)](policy-as-code.md) | 20+ OPA/Rego policies for GCP Terraform | :material-lock-open: Free |

## Developer Experience

Tools for engineering productivity.

| Module | Description | Tier |
|--------|-------------|------|
| [Developer CLI](cli.md) | `dsk scan`, `dsk init`, `dsk validate` | :material-lock-open: Free |

---

!!! info "More modules coming"
    Release 2 adds GKE Bedrock, Database Security, Drift Detection, Webhook Router, Cloud Armor WAF, and SOC2 Automation. [See the roadmap](../architecture/overview.md).
