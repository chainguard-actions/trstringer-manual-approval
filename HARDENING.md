<!-- markdownlint-disable -->

# Hardening Report: trstringer--manual-approval/v1.10.0

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **trstringer--manual-approval/v1.10.0** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

Multiple workflow files and action.yaml reference actions and Docker images by mutable tags instead of full 40-character commit SHAs or SHA digests, making the action vulnerable to supply-chain attacks.

.github/workflows/ci.yaml:
  - uses: actions/checkout@v2  (tag, not SHA)

.github/workflows/codeql.yml:
  - uses: actions/checkout@v4  (tag, not SHA)
  - uses: actions/setup-go@v5  (tag, not SHA)
  - uses: github/codeql-action/init@v3  (tag, not SHA)
  - uses: github/codeql-action/autobuild@v3  (tag, not SHA)
  - uses: github/codeql-action/analyze@v3  (tag, not SHA)

action.yaml:
  - image: docker://ghcr.io/trstringer/manual-approval:1.10.0  (mutable tag, not a SHA digest like @sha256:<64-hex-chars>)

Locations:

- `.github/workflows/ci.yaml:19`
- `.github/workflows/codeql.yml:18`
- `.github/workflows/codeql.yml:22`
- `.github/workflows/codeql.yml:27`
- `.github/workflows/codeql.yml:31`
- `.github/workflows/codeql.yml:34`
- `action.yaml:50`

### missing-permissions (severity: medium)

The workflow file .github/workflows/ci.yaml has no top-level `permissions:` key and its only job (`ci`) also has no job-level `permissions:` key. Without explicit permissions, the GITHUB_TOKEN is granted default (potentially write) permissions, violating the principle of least privilege.

Locations:

- `.github/workflows/ci.yaml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed all unpinned action references:
- .github/workflows/ci.yaml: pinned actions/checkout@v2 → @0717577d45739eb3c851188b29f50ed6c0b2194e # v2; added top-level `permissions: {}` block
- .github/workflows/codeql.yml: pinned actions/checkout@v4 → @11d5960a326750d5838078e36cf38b85af677262 # v4; actions/setup-go@v5 → @40f1582b2485089dde7abd97c1529aa768e1baff # v5; github/codeql-action/init@v3, autobuild@v3, analyze@v3 → @f3712979fa5f215279b101dd0a2e3bdfb4353324 # v3 each
- action.yaml: pinned docker://ghcr.io/trstringer/manual-approval:1.10.0 → :1.10.0@sha256:3843f35b050dc97c4234f083836d899b12f98ce51a017be3c66690ffe5209d0d (preserving docker:// scheme and tag inline)

