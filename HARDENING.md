<!-- markdownlint-disable -->

# Hardening Report: trstringer--manual-approval/v1.12.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **trstringer--manual-approval/v1.12.0** was hardened automatically. 4 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

The action.yaml uses a Docker image pinned to a mutable tag rather than an immutable SHA digest. `image: docker://ghcr.io/trstringer/manual-approval:1.12.0` — the tag `1.12.0` can be overwritten at any time, enabling a supply-chain attack. It should be replaced with a SHA digest reference, e.g. `docker://ghcr.io/trstringer/manual-approval@sha256:<64-hex-char-digest>`.

Locations:

- `action.yaml:57`

### unpinned-uses (severity: high)

The CI workflow references Actions by mutable version tags instead of full 40-character commit SHAs, making the workflow vulnerable to supply-chain attacks if those tags are moved. Unpinned reference: `actions/checkout@v2` (line 14).

Locations:

- `.github/workflows/ci.yaml:14`

### unpinned-uses (severity: high)

The CodeQL workflow references Actions by mutable version tags instead of full 40-character commit SHAs. Unpinned references: `actions/checkout@v4` (line 22), `actions/setup-go@v5` (line 25), `github/codeql-action/init@v3` (line 30), `github/codeql-action/autobuild@v3` (line 34), `github/codeql-action/analyze@v3` (line 37).

Locations:

- `.github/workflows/codeql.yml:22`
- `.github/workflows/codeql.yml:25`
- `.github/workflows/codeql.yml:30`
- `.github/workflows/codeql.yml:34`
- `.github/workflows/codeql.yml:37`

### missing-permissions (severity: medium)

The CI workflow file has no top-level `permissions:` block and the single job `ci` also has no job-level `permissions:` block. Without explicit permissions, the job inherits the default token permissions (which may include write access to contents, pull-requests, etc.), violating the principle of least privilege.

Locations:

- `.github/workflows/ci.yaml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed all four findings:
1. action.yaml (line 57): Pinned `docker://ghcr.io/trstringer/manual-approval:1.12.0` to `docker://ghcr.io/trstringer/manual-approval:1.12.0@sha256:59bd4cd8be925c77642bb6a2f32c359ab5568e74d5b47edb3eec26b750d4873c`, preserving the docker:// scheme and tag.
2. ci.yaml (line 14): Pinned `actions/checkout@v2` to full SHA `0717577d45739eb3c851188b29f50ed6c0b2194e # v2`.
3. ci.yaml (line 1): Added top-level `permissions: {}` block to enforce least privilege.
4. codeql.yml (lines 22, 25, 30, 34, 37): Pinned all five action references — `actions/checkout@v4` → SHA `11d5960a...`, `actions/setup-go@v5` → SHA `40f1582b...`, and all three `github/codeql-action/*@v3` → SHA `f3712979...`.

