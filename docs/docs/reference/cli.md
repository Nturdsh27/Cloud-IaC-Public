# CLI Reference

Complete reference for `dsk` CLI commands.

## Global Flags

| Flag | Description |
|------|-------------|
| `--config` | Path to `.dsk.yml` config file (default: `.dsk.yml` in repo root) |
| `--verbose` | Enable verbose output |
| `--version` | Print version and exit |

## `dsk scan`

Run security scanners against the current directory or a container image.

```
dsk scan [flags]
```

| Flag | Default | Description |
|------|---------|-------------|
| `--type` | `all` | Scan type: `all`, `iac`, `container`, `secrets` |
| `--image` | — | Container image to scan (required for `container` type) |
| `--severity` | `HIGH` | Minimum severity to report |
| `--output` | `text` | Output format: `text`, `json`, `sarif` |
| `--fail-on` | `HIGH` | Fail (exit 1) on this severity or above |

**Examples:**

```bash
dsk scan                                    # scan everything
dsk scan --type iac --severity MEDIUM       # IaC with medium+ findings
dsk scan --type container --image myapp:v1  # scan a container image
dsk scan --output sarif > results.sarif     # SARIF output for CI
```

## `dsk init`

Scaffold a new repository from a secure template.

```
dsk init <template> <name>
```

| Template | Description |
|----------|-------------|
| `go-service` | Go service with Dockerfile, CI workflow, Makefile |
| `python-service` | Python FastAPI service with Dockerfile, CI workflow |
| `terraform-module` | Terraform module with tests, examples, terraform-docs |

**Examples:**

```bash
dsk init go-service my-api
dsk init terraform-module my-landing-zone
```

## `dsk validate`

Validate Terraform against OPA policies.

```
dsk validate [path] [flags]
```

| Flag | Default | Description |
|------|---------|-------------|
| `--policy-dir` | `policies/terraform/` | Directory containing Rego policies |

**Examples:**

```bash
dsk validate                        # validate current directory
dsk validate ./modules/gke/         # validate specific module
dsk validate --policy-dir my-rules/ # custom policy directory
```
