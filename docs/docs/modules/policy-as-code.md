# Policy-as-Code (OPA)

20+ OPA/Rego policies that catch GCP Terraform misconfigurations before they deploy.

## What It Does

A library of Rego policies evaluated against Terraform plans using [conftest](https://www.conftest.dev/). Run in CI to block insecure infrastructure before it reaches GCP.

## Included Policies

| Policy | What It Prevents |
|--------|-----------------|
| `deny-public-ip` | Compute instances with external IPs |
| `require-encryption` | Storage/DB without encryption-at-rest |
| `deny-default-vpc` | Using the default GCP network |
| `require-private-sql` | Cloud SQL with public IP |
| `deny-overprivileged-sa` | Service accounts with `roles/editor` or `roles/owner` |
| `require-labels` | Resources missing required labels |
| `deny-legacy-auth-gke` | GKE clusters with legacy ABAC |
| `require-vpc-flow-logs` | Subnets without flow logs |
| `deny-public-gcs` | GCS buckets with `allUsers` access |
| `require-ssl-sql` | Cloud SQL without SSL enforcement |

Plus 10+ more covering naming conventions, cost labels, and resource descriptions.

## Usage

### In CI/CD

```yaml
- name: Terraform Plan
  run: |
    terraform plan -out=tfplan.binary
    terraform show -json tfplan.binary > tfplan.json

- name: Policy Check
  run: conftest test tfplan.json --policy policies/terraform/ --output sarif
```

### Locally

```bash
dsk validate  # runs conftest against current Terraform plan
```

## Example Policy

```rego
# policies/terraform/deny_public_ip.rego
package terraform.gcp

deny[msg] {
  resource := input.resource_changes[_]
  resource.type == "google_compute_instance"
  access_config := resource.change.after.network_interface[_].access_config
  count(access_config) > 0
  msg := sprintf("Instance '%s' has a public IP. Use Cloud NAT or IAP.", [resource.address])
}
```

## What the Paid Tier Adds

- **OPA Gatekeeper on GKE** — runtime enforcement, not just CI checks
- **40+ constraint templates** covering CIS GCP Benchmark
- **Policy testing framework** — unit tests for every Rego policy
- **Custom policies** mapped to your compliance framework (SOC2, HIPAA, PCI)
