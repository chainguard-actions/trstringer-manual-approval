# Hardening Report: trstringer--manual-approval/v1.9.1

> This file was generated automatically by the hardening agent.

**Policy SHA:** `ff50f15e4b79bfbf764dafdfd2579175a6ea9771`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `1`

Action **trstringer--manual-approval/v1.9.1** was hardened automatically. 1 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The action.yaml uses a Docker image reference with a mutable version tag (`docker://ghcr.io/trstringer/manual-approval:1.9.1`) instead of an immutable SHA digest. This means the image could be replaced with a different (potentially malicious) version without changing the action reference. It should be pinned to a specific SHA digest, e.g. `docker://ghcr.io/trstringer/manual-approval@sha256:<64-hex-char-digest>`.

Locations:

- `action.yaml:33`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses

**Notes:**

Replaced the mutable Docker image tag `docker://ghcr.io/trstringer/manual-approval:1.9.1` with the immutable SHA256 digest `docker://ghcr.io/trstringer/manual-approval@sha256:5c9f7dc4df19132760033592353b94c72142b1e0bc5fd445dd170c0066c566da # 1.9.1` in action.yaml line 33.

