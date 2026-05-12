# Hardening Report: trstringer--manual-approval/v1.10.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `ff50f15e4b79bfbf764dafdfd2579175a6ea9771`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `1`

Action **trstringer--manual-approval/v1.10.0** was hardened automatically. 1 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The action uses a Docker image referenced by a mutable tag rather than an immutable SHA digest. `image: docker://ghcr.io/trstringer/manual-approval:1.10.0` uses the tag `1.10.0`, which can be silently replaced by a different (potentially malicious) image. It should be pinned to a full SHA256 digest, e.g. `image: docker://ghcr.io/trstringer/manual-approval@sha256:<64-hex-char-digest>`.

Locations:

- `action.yaml:50`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses

**Notes:**

Replaced the mutable Docker image tag `ghcr.io/trstringer/manual-approval:1.10.0` with the immutable SHA256 digest `ghcr.io/trstringer/manual-approval@sha256:3843f35b050dc97c4234f083836d899b12f98ce51a017be3c66690ffe5209d0d # 1.10.0` in action.yaml line 50.

