<!-- markdownlint-disable -->

# Hardening Report: trstringer--manual-approval/v1.13.1

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **trstringer--manual-approval/v1.13.1** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The action.yaml uses a Docker image reference with a mutable tag (`docker://ghcr.io/trstringer/manual-approval:1.13.0`) instead of an immutable SHA digest. A tag can be silently overwritten to point to a different (potentially malicious) image, enabling supply-chain attacks. The image reference should use a SHA digest, e.g. `docker://ghcr.io/trstringer/manual-approval@sha256:<64-hex-char-digest>`.

Locations:

- `action.yaml:68`

### broad-permissions (severity: medium)

The workflow file `.github/workflows/scorecards.yml` sets top-level `permissions: read-all`, which grants overly broad read access across all permission scopes. This should be replaced with specific minimal permissions (the job-level block already lists the specific permissions needed and can serve as the model).

Locations:

- `.github/workflows/scorecards.yml:20`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, broad-permissions

**Notes:**

1. action.yaml line 68: Pinned Docker image from mutable tag `docker://ghcr.io/trstringer/manual-approval:1.13.0` to immutable digest `docker://ghcr.io/trstringer/manual-approval:1.13.0@sha256:7cac2dde511346ae728d44e6a4c6385e5cd4b1a612e2158712448cfc4414b15b`, preserving the docker:// scheme and tag inline. 2. .github/workflows/scorecards.yml line 20: Replaced broad `permissions: read-all` with specific minimal permissions (security-events: write, id-token: write, contents: read, actions: read, issues: read, pull-requests: read, checks: read) matching the job-level permissions already defined.

