# Your First Scan

Walk through a security scan from start to finish.

## What Gets Scanned

The Multi-Scanner runs four tools in sequence:

| Scanner | What It Finds | Output |
|---------|--------------|--------|
| **TruffleHog** | Leaked secrets, API keys, passwords | SARIF |
| **Trivy** | Container image CVEs, IaC misconfigs | SARIF |
| **Checkov** | Terraform/Dockerfile misconfigurations | SARIF |
| **tfsec** | Terraform-specific security issues | SARIF |

All results are uploaded to GitHub's **Security tab** as SARIF, giving you a unified view.

## Running Locally

```bash
# Scan everything in the current directory
dsk scan --type all

# Scan only Terraform files
dsk scan --type iac

# Scan a container image
dsk scan --type container --image myapp:latest

# Scan for secrets only
dsk scan --type secrets
```

## Understanding the Output

```
🔍 DSK Security Scan Results
────────────────────────────
Scanner: Trivy (IaC)
  🔴 CRITICAL: 0
  🟠 HIGH:     2
  🟡 MEDIUM:   4
  🔵 LOW:      1

Findings:
  HIGH | modules/database/main.tf:15
       | Cloud SQL instance has public IP enabled
       | Fix: Set ipv4_enabled = false

  HIGH | modules/gke/main.tf:42
       | GKE cluster has legacy ABAC enabled
       | Fix: Set enable_legacy_abac = false
```

## In CI/CD

When the scanner runs on a PR, findings appear in two places:

1. **GitHub Security tab** — full SARIF results with file and line references
2. **PR check status** — fails on HIGH+ severity by default

!!! warning "Severity Threshold"
    The default threshold is `HIGH` — the pipeline fails if any HIGH or CRITICAL findings exist. Configure this in your workflow:

    ```yaml
    - uses: Nturdsh27/Cloud-IaC/.github/actions/security-scan@v1
      with:
        scan_type: "all"
        severity_threshold: "CRITICAL"  # only fail on CRITICAL
    ```

## Handling False Positives

If a finding is a known false positive, document it in `.securityignore.yml`:

```yaml
overrides:
  - rule_id: "AVD-GCP-0001"
    file: "modules/dev-only/main.tf"
    justification: "Dev environment intentionally uses default VPC"
    approved_by: "you@example.com"
    expires: "2026-06-01"
```

The scanner reads this file and filters matched findings before the pass/fail decision.

## Next Steps

- [Multi-Scanner module docs](../modules/multi-scanner.md) — full configuration reference
- [Policy-as-Code](../modules/policy-as-code.md) — add OPA/Rego policies to your pipeline
- [CLI reference](../reference/cli.md) — all `dsk` commands
