<!-- markdownlint-disable -->

# Hardening Report: trstringer--manual-approval/v1.9.1

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **trstringer--manual-approval/v1.9.1** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

Two unpinned references were found:
1. action.yaml uses a Docker image with a mutable tag (`docker://ghcr.io/trstringer/manual-approval:1.9.1`) instead of a SHA digest. A tag can be silently repointed to a different image, enabling supply-chain attacks.
2. .github/workflows/ci.yaml uses `actions/checkout@v2` (a tag) instead of a full 40-character commit SHA. Tags are mutable and can be moved to point to malicious commits.

Locations:

- `action.yaml:33`
- `.github/workflows/ci.yaml:18`

### missing-permissions (severity: medium)

The workflow file .github/workflows/ci.yaml has no top-level `permissions:` key and the single job `ci` also has no job-level `permissions:` block. Without explicit permissions, the workflow inherits the repository's default token permissions, which may be overly broad (e.g., write access to contents). A minimal explicit permissions block should be added.

Locations:

- `.github/workflows/ci.yaml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed two findings: (1) Pinned the Docker image in action.yaml from mutable tag `docker://ghcr.io/trstringer/manual-approval:1.9.1` to immutable digest `docker://ghcr.io/trstringer/manual-approval:1.9.1@sha256:5c9f7dc4df19132760033592353b94c72142b1e0bc5fd445dd170c0066c566da`, preserving the `docker://` scheme and tag. (2) Pinned `actions/checkout@v2` to its full commit SHA `0717577d45739eb3c851188b29f50ed6c0b2194e` with a `# v2` comment for readability. (3) Added a top-level `permissions: contents: read` block to ci.yaml to restrict the GITHUB_TOKEN to the minimum needed for checkout and build/test/lint operations.

