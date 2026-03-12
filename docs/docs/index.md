---
hide:
  - navigation
---

# DevSecOps Starter Kit

**Production-ready, secure-by-default GCP infrastructure for startups that can't afford to get security wrong.**

---

## The Problem

Every startup builds the same infrastructure: VPC, IAM, CI/CD, Kubernetes, database. And every startup makes the same security mistakes: public buckets, overprivileged service accounts, no scanning, SA keys in environment variables.

You shouldn't have to choose between shipping fast and being secure.

## The Solution

The DevSecOps Starter Kit is a collection of **opinionated, pre-hardened Terraform modules, GitHub Actions, and developer tools** for GCP. Each module follows security best practices by default — not as an afterthought.

<div class="grid cards" markdown>

-   :material-shield-check:{ .lg .middle } **Secure by Default**

    ---

    Every module enforces least-privilege IAM, encrypted-at-rest, private networking, and audit logging out of the box.

-   :material-rocket-launch:{ .lg .middle } **Ship in Days, Not Months**

    ---

    Copy a Terraform module, run `terraform apply`, and have a production-grade GCP environment in hours.

-   :material-magnify-scan:{ .lg .middle } **Scan Everything**

    ---

    One GitHub Action scans for vulnerabilities, misconfigurations, secrets, and policy violations on every commit.

-   :material-code-braces:{ .lg .middle } **Developer-First**

    ---

    A Go CLI (`dsk`) wraps security scanning and scaffolding so developers don't need to leave their terminal.

</div>

## Quick Start

```bash
# Install the CLI
brew install Nturdsh27/tap/dsk

# Scaffold a new Terraform module
dsk init terraform-module my-service

# Run a security scan locally
dsk scan --type all

# Validate against OPA policies
dsk validate
```

Or start with the [Multi-Scanner GitHub Action](modules/multi-scanner.md) — add one line to your workflow and scan every PR automatically.

## What's Included

| Domain | Modules | Status |
|--------|---------|--------|
| **Cloud Foundation** | Landing Zone, IAM, GKE, Database Security | :material-progress-wrench: Building |
| **Security Pipeline** | Multi-Scanner, Cosign Signing, Policy-as-Code | :material-progress-wrench: Building |
| **Developer Experience** | Go CLI, Webhook Router, Ephemeral Environments | :material-calendar: Planned |
| **Policy & Compliance** | OPA/Rego, SOC2 Mapping, CIS Benchmarks | :material-calendar: Planned |
| **Network & API** | Cloud Armor WAF, Zero Trust, Service Mesh | :material-calendar: Planned |

[Get Started :material-arrow-right:](getting-started/quickstart.md){ .md-button .md-button--primary }
[View Modules :material-arrow-right:](modules/index.md){ .md-button }
