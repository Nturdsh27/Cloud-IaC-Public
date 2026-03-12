# Quickstart

Get a secure GCP environment running in under 30 minutes.

## Prerequisites

- [Terraform](https://developer.hashicorp.com/terraform/install) >= 1.5
- [Google Cloud SDK](https://cloud.google.com/sdk/docs/install) (`gcloud`)
- A GCP project with billing enabled
- GitHub repository for CI/CD

## Step 1: Authenticate with GCP

```bash
gcloud auth application-default login
gcloud config set project YOUR_PROJECT_ID
```

## Step 2: Deploy the Landing Zone

```hcl
# main.tf
module "landing_zone" {
  source = "github.com/Nturdsh27/Cloud-IaC//modules/foundation/landing-zone"

  project_id = "your-project-id"
  region     = "us-central1"

  vpc_name = "main"
  subnets = {
    app = { cidr = "10.0.1.0/24", region = "us-central1" }
    gke = {
      cidr            = "10.0.2.0/24"
      region          = "us-central1"
      secondary_ranges = {
        pods     = "10.4.0.0/14"
        services = "10.8.0.0/20"
      }
    }
  }

  enable_cloud_nat = true
}
```

```bash
terraform init
terraform plan
terraform apply
```

## Step 3: Add Security Scanning to CI/CD

Add the Multi-Scanner Action to any workflow:

```yaml
# .github/workflows/ci.yml
name: CI
on: [pull_request]

jobs:
  security-scan:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: Nturdsh27/Cloud-IaC/.github/actions/security-scan@main
        with:
          scan_type: "all"
```

Every PR now gets scanned for vulnerabilities, misconfigurations, and leaked secrets.

## Step 4: Validate Locally

```bash
# Install the DSK CLI
brew install Nturdsh27/tap/dsk

# Run the same scans locally before pushing
dsk scan --type all

# Validate Terraform against OPA policies
dsk validate
```

## What's Next

- [Installation guide](installation.md) — detailed setup for each component
- [Your First Scan](first-scan.md) — walkthrough of scanner output
- [Module catalog](../modules/index.md) — explore all available modules
