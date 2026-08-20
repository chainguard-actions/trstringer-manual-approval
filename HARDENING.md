<!-- markdownlint-disable -->

# Hardening Report: trstringer--manual-approval/v1.9.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **trstringer--manual-approval/v1.9.0** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The action.yaml Docker image reference uses a mutable tag (`docker://ghcr.io/trstringer/manual-approval:1.9.0`) instead of a SHA digest. This is vulnerable to supply-chain attacks if the tag is moved. Additionally, the workflow file `.github/workflows/ci.yaml` uses `actions/checkout@v2` (a tag reference) instead of a pinned 40-character commit SHA. Both references should be pinned to immutable SHA digests.

Locations:

- `action.yaml:30`
- `.github/workflows/ci.yaml:19`

### missing-permissions (severity: medium)

The workflow file `.github/workflows/ci.yaml` has no top-level `permissions:` key, and the single job `ci` also has no job-level `permissions:` key. Without explicit permissions, the workflow inherits the default (potentially broad) repository permissions. A minimal `permissions:` block (e.g., `contents: read`) should be added.

Locations:

- `.github/workflows/ci.yaml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

1. action.yaml: Pinned Docker image `docker://ghcr.io/trstringer/manual-approval:1.9.0` to its immutable SHA digest `sha256:8e56c8e3f7d052adb81fea7dd64b3acc0760e70291da84e475201a58f7454cc7`, preserving the `docker://` scheme and tag inline. 2. .github/workflows/ci.yaml: Pinned `actions/checkout@v2` to its full commit SHA `0717577d45739eb3c851188b29f50ed6c0b2194e` with a `# v2` comment for readability. 3. .github/workflows/ci.yaml: Added a top-level `permissions: contents: read` block to restrict the workflow to the minimum required permissions.

