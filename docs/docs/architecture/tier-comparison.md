# Tier Comparison

What you get at each tier of the DevSecOps Starter Kit.

## Overview

| | Community | Starter | Growth | Enterprise |
|---|:---------:|:-------:|:------:|:----------:|
| **Price** | Free | $299/mo | $999/mo | $2,499/mo |
| **Distribution** | Public GitHub | Private repo | Private repo | Private + advisory |
| **Support** | GitHub Issues | Email | Priority email | Dedicated Slack |

## Feature Matrix

### Cloud Foundation

| Feature | Community | Starter | Growth | Enterprise |
|---------|:---------:|:-------:|:------:|:----------:|
| Custom VPC + Cloud NAT | :material-check: | :material-check: | :material-check: | :material-check: |
| Basic firewall rules | :material-check: | :material-check: | :material-check: | :material-check: |
| Service account module | :material-check: | :material-check: | :material-check: | :material-check: |
| Shared VPC | | :material-check: | :material-check: | :material-check: |
| Hierarchical firewalls | | :material-check: | :material-check: | :material-check: |
| Workload Identity Federation | | :material-check: | :material-check: | :material-check: |
| GKE Autopilot hardened | | :material-check: | :material-check: | :material-check: |
| GKE Standard + Binary Auth | | | :material-check: | :material-check: |
| HashiCorp Vault on GKE | | | :material-check: | :material-check: |
| Custom org hierarchy | | | | :material-check: |

### Security Pipeline

| Feature | Community | Starter | Growth | Enterprise |
|---------|:---------:|:-------:|:------:|:----------:|
| Multi-scanner Action | :material-check: | :material-check: | :material-check: | :material-check: |
| Cosign keyless signing | :material-check: | :material-check: | :material-check: | :material-check: |
| Configurable scanner matrix | | :material-check: | :material-check: | :material-check: |
| PR comment summaries | | :material-check: | :material-check: | :material-check: |
| SLSA Level 3 provenance | | | :material-check: | :material-check: |
| DAST (ZAP) scanning | | | :material-check: | :material-check: |
| Drift detection | | | :material-check: | :material-check: |
| Supply chain (SBOM) monitoring | | | :material-check: | :material-check: |

### Policy & Compliance

| Feature | Community | Starter | Growth | Enterprise |
|---------|:---------:|:-------:|:------:|:----------:|
| 20+ OPA/Rego policies | :material-check: | :material-check: | :material-check: | :material-check: |
| SOC2 control mapping doc | | :material-check: | :material-check: | :material-check: |
| OPA Gatekeeper on GKE | | | :material-check: | :material-check: |
| CIS Benchmark automation | | | :material-check: | :material-check: |
| Automated evidence collection | | | :material-check: | :material-check: |
| Custom compliance framework | | | | :material-check: |

### Developer Experience

| Feature | Community | Starter | Growth | Enterprise |
|---------|:---------:|:-------:|:------:|:----------:|
| `dsk` CLI (scan, init, validate) | :material-check: | :material-check: | :material-check: | :material-check: |
| Webhook router (Slack) | | :material-check: | :material-check: | :material-check: |
| Ephemeral environments | | | :material-check: | :material-check: |
| Self-service IAM portal | | | :material-check: | :material-check: |
| PR security reviewer (LLM) | | | :material-check: | :material-check: |
| Backstage developer portal | | | | :material-check: |

## Who Should Use Each Tier

=== "Community (Free)"

    **You're a solo developer or small team** getting started with GCP security.

    - You want secure defaults without reading 100 pages of GCP docs
    - You're happy with a single-project setup
    - GitHub Issues for support is fine

=== "Starter ($299/mo)"

    **You're a Series A startup (5-20 engineers)** that needs to look professional.

    - You need Shared VPC for team isolation
    - Workload Identity Federation is a must (no more SA keys)
    - Your first SOC2 audit is on the horizon

=== "Growth ($999/mo)"

    **You're a Series B company (20-100 engineers)** scaling your platform.

    - Multiple teams need self-service infrastructure
    - Compliance is a hard requirement (SOC2, CIS)
    - You want security dashboards for leadership

=== "Enterprise ($2,499/mo)"

    **You're a Series C+ or mid-market company** that needs a tailored solution.

    - Custom org hierarchy matching your team structure
    - Advisory hours with a senior security architect
    - Backstage portal for full developer self-service
