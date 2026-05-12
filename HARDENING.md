# Hardening Report: trstringer--manual-approval/v1.9.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `ff50f15e4b79bfbf764dafdfd2579175a6ea9771`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `1`

Action **trstringer--manual-approval/v1.9.0** was hardened automatically. 1 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The action uses a Docker image referenced by a mutable version tag rather than an immutable SHA256 digest. In action.yaml, `image: docker://ghcr.io/trstringer/manual-approval:1.9.0` uses the tag `1.9.0`, which can be overwritten at any time, exposing the action to supply-chain attacks. It should be pinned to a specific SHA256 digest, e.g. `image: ghcr.io/trstringer/manual-approval@sha256:<64-hex-char-digest> # 1.9.0`.

Locations:

- `action.yaml:27`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses

**Notes:**

Pinned the Docker image reference in action.yaml from `docker://ghcr.io/trstringer/manual-approval:1.9.0` to `docker://ghcr.io/trstringer/manual-approval@sha256:8e56c8e3f7d052adb81fea7dd64b3acc0760e70291da84e475201a58f7454cc7 # 1.9.0`. The SHA256 digest was resolved via the Docker Registry HTTP API v2, ensuring the image reference is now immutable and protected against supply-chain attacks via tag mutation.

