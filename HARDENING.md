# Hardening Report: trstringer--manual-approval/v1.12.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `ff50f15e4b79bfbf764dafdfd2579175a6ea9771`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `1`

Action **trstringer--manual-approval/v1.12.0** was hardened automatically. 1 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The action's Docker image reference uses a mutable tag instead of a SHA digest. `image: docker://ghcr.io/trstringer/manual-approval:1.12.0` should be pinned to a specific SHA256 digest (e.g., `image: ghcr.io/trstringer/manual-approval@sha256:<64-hex-char-digest>`) to prevent supply-chain attacks where the tag could be silently updated to point to a different image.

Locations:

- `action.yaml:55`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses

**Notes:**

Replaced the mutable Docker image tag `ghcr.io/trstringer/manual-approval:1.12.0` with the pinned SHA256 digest `ghcr.io/trstringer/manual-approval@sha256:59bd4cd8be925c77642bb6a2f32c359ab5568e74d5b47edb3eec26b750d4873c` in action.yaml line 55. The original tag is preserved as a comment for readability.

