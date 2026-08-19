<!-- markdownlint-disable -->

# Hardening Report: trstringer--manual-approval/v1.13.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **trstringer--manual-approval/v1.13.0** was hardened automatically. 4 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

action.yaml uses a Docker image with a mutable tag instead of a SHA digest: `docker://ghcr.io/trstringer/manual-approval:1.13.0`. This is vulnerable to supply-chain attacks because the tag can be silently redirected to a different image. It should be pinned to a SHA digest, e.g. `docker://ghcr.io/trstringer/manual-approval@sha256:<64-hex-char-digest>`.

Locations:

- `action.yaml:68`

### unpinned-uses (severity: high)

Workflow file uses mutable tag refs instead of full 40-character commit SHAs. Failing reference: `actions/checkout@v2`. These should be pinned to full SHA hashes to prevent supply-chain attacks.

Locations:

- `.github/workflows/ci.yaml:21`

### unpinned-uses (severity: high)

Workflow file uses mutable tag refs instead of full 40-character commit SHAs. Failing references: `actions/checkout@v4`, `actions/setup-go@v5`, `github/codeql-action/init@v3`, `github/codeql-action/autobuild@v3`, `github/codeql-action/analyze@v3`. These should be pinned to full SHA hashes to prevent supply-chain attacks.

Locations:

- `.github/workflows/codeql.yml:20`
- `.github/workflows/codeql.yml:23`
- `.github/workflows/codeql.yml:28`
- `.github/workflows/codeql.yml:33`
- `.github/workflows/codeql.yml:36`

### permissions (severity: medium)

Workflow file has no top-level `permissions:` key and the single job (`ci`) also has no `permissions:` key. Without explicit permissions, the job inherits the default repository token permissions, which may be overly broad. A minimal permissions block (e.g. `permissions: contents: read`) should be added.

Locations:

- `.github/workflows/ci.yaml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, permissions

**Notes:**

Fixed all four findings: (1) Pinned Docker image in action.yaml from `docker://ghcr.io/trstringer/manual-approval:1.13.0` to `docker://ghcr.io/trstringer/manual-approval:1.13.0@sha256:7cac2dde511346ae728d44e6a4c6385e5cd4b1a612e2158712448cfc4414b15b`. (2) Pinned `actions/checkout@v2` in ci.yaml to full SHA `0717577d45739eb3c851188b29f50ed6c0b2194e`. (3) Added top-level `permissions: contents: read` to ci.yaml. (4) Pinned all five unpinned actions in codeql.yml: `actions/checkout@v4` → SHA `11d5960a...`, `actions/setup-go@v5` → SHA `40f1582b...`, and all three `github/codeql-action/*@v3` → SHA `08d09a53...`, each with a tag comment for readability.

