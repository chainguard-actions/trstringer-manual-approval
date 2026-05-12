# Hardening Report: trstringer--manual-approval/v1.11.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `ff50f15e4b79bfbf764dafdfd2579175a6ea9771`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `1`

Action **trstringer--manual-approval/v1.11.0** was hardened automatically. 1 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The action.yaml uses a Docker image referenced by a mutable version tag (`1.11.0`) rather than an immutable SHA digest. This means the image could be replaced with a different (potentially malicious) version without changing the action reference. The failing reference is: `image: docker://ghcr.io/trstringer/manual-approval:1.11.0`. It should instead use a SHA digest, e.g. `image: docker://ghcr.io/trstringer/manual-approval@sha256:<64-hex-char-digest>`.

Locations:

- `action.yaml:52`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses

**Notes:**

Replaced the mutable Docker image tag reference `docker://ghcr.io/trstringer/manual-approval:1.11.0` with the immutable SHA256 digest `docker://ghcr.io/trstringer/manual-approval@sha256:f7efbe95b374f2c25de2515723596a4bc93a02e1613695727d9b313a9afd98dc # 1.11.0` in action.yaml line 52. The original tag is preserved as a comment for readability.

