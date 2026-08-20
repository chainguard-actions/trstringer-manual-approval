<!-- markdownlint-disable -->

# Hardening Report: trstringer--manual-approval/v1.11.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **trstringer--manual-approval/v1.11.0** was hardened automatically. 3 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

action.yaml uses a Docker image pinned to a mutable tag (`docker://ghcr.io/trstringer/manual-approval:1.11.0`) instead of an immutable SHA digest. This is vulnerable to supply-chain attacks if the tag is moved. It should be replaced with a reference like `ghcr.io/trstringer/manual-approval@sha256:<64-hex-char-digest>`.

Locations:

- `action.yaml:55`

### unpinned-uses (severity: high)

Workflow files reference actions pinned to mutable version tags instead of full 40-character commit SHAs. Affected references: ci.yaml — `actions/checkout@v2`; codeql.yml — `actions/checkout@v4`, `actions/setup-go@v5`, `github/codeql-action/init@v3`, `github/codeql-action/autobuild@v3`, `github/codeql-action/analyze@v3`. Each should be pinned to a full SHA, e.g. `actions/checkout@11bd71901bbe5b1630ceea73d27597364c9af683 # v4`.

Locations:

- `.github/workflows/ci.yaml:19`
- `.github/workflows/codeql.yml:18`
- `.github/workflows/codeql.yml:21`
- `.github/workflows/codeql.yml:25`
- `.github/workflows/codeql.yml:30`
- `.github/workflows/codeql.yml:33`

### missing-permissions (severity: medium)

The workflow file `.github/workflows/ci.yaml` has no top-level `permissions:` key and its only job (`ci`) also has no job-level `permissions:` key. Without explicit permissions, the job inherits the default repository token permissions, which may be overly broad (write access to contents, etc.). A minimal `permissions:` block should be added.

Locations:

- `.github/workflows/ci.yaml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

1. action.yaml: Pinned `docker://ghcr.io/trstringer/manual-approval:1.11.0` to `docker://ghcr.io/trstringer/manual-approval:1.11.0@sha256:f7efbe95b374f2c25de2515723596a4bc93a02e1613695727d9b313a9afd98dc`, preserving the docker:// scheme and tag. 2. ci.yaml: Pinned `actions/checkout@v2` to `actions/checkout@0717577d45739eb3c851188b29f50ed6c0b2194e # v2` and added top-level `permissions: contents: read` block. 3. codeql.yml: Pinned all five action references — `actions/checkout@v4`, `actions/setup-go@v5`, `github/codeql-action/init@v3`, `github/codeql-action/autobuild@v3`, and `github/codeql-action/analyze@v3` — to their respective full commit SHAs with original tags preserved as comments.

