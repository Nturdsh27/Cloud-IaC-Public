# Container Signing (Cosign)

Sign container images with Sigstore — no key management required.

## What It Does

After building and pushing a container image, Cosign signs the image digest using GitHub Actions' OIDC identity. No private keys to manage, rotate, or leak.

## Usage

```yaml
# After docker build + push in your CI workflow:
- name: Sign image with Cosign
  uses: sigstore/cosign-installer@v3
- run: cosign sign --yes "${IMAGE}@${DIGEST}"
  env:
    COSIGN_EXPERIMENTAL: "1"
```

## Verification

Anyone can verify the signature:

```bash
cosign verify \
  --certificate-identity-regexp="https://github.com/OWNER/REPO" \
  --certificate-oidc-issuer="https://token.actions.githubusercontent.com" \
  "${IMAGE}@${DIGEST}"
```

## Why Keyless?

| Approach | Key Management | Rotation | Leak Risk |
|----------|---------------|----------|-----------|
| Traditional signing | You manage keys | You rotate keys | High |
| **Cosign keyless** | GitHub OIDC token | Automatic (ephemeral) | None |

The signature identity is tied to the GitHub Actions workflow run — verifiable via Sigstore's transparency log.

## What the Paid Tier Adds

- **SLSA Level 3 provenance** — verified build provenance attestation
- **SBOM generation & attachment** — CycloneDX SBOM as Cosign attestation
- **Binary Authorization** — GKE rejects unsigned images at deploy time
- **Sigstore transparency log** — public verifiability of all signatures
