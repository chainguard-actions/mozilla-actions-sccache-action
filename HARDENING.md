<!-- markdownlint-disable -->

# Hardening Report: Mozilla-Actions--sccache-action/v0.0.11

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **Mozilla-Actions--sccache-action/v0.0.11** was hardened automatically. 2 finding(s) were identified and resolved across 1 iteration(s).

## Findings Fixed

### unpinned-uses (severity: high)

Multiple `uses:` references in CI.yml use mutable tag-based refs instead of full 40-character commit SHAs, making the workflow vulnerable to supply-chain attacks if those tags are moved. Failing references: `actions/checkout@v7` (build job, test job, test_disable_annotations job), `actions/setup-node@v7` (build job, test job, test_disable_annotations job), `actions/checkout@v6` (verify-dist job), `actions/setup-node@v6` (verify-dist job).

Locations:

- `.github/workflows/CI.yml:22`
- `.github/workflows/CI.yml:24`
- `.github/workflows/CI.yml:40`
- `.github/workflows/CI.yml:42`
- `.github/workflows/CI.yml:72`
- `.github/workflows/CI.yml:75`
- `.github/workflows/CI.yml:88`
- `.github/workflows/CI.yml:91`

### missing-permissions (severity: medium)

The workflow file CI.yml has no top-level `permissions:` key and none of its jobs (build, verify-dist, test, test_disable_annotations) define a `permissions:` block. Without explicit permissions, the workflow inherits the repository's default token permissions, which may be overly broad (write access to contents, pull-requests, etc.).

Locations:

- `.github/workflows/CI.yml:1`

## Iteration Notes

### Iteration 1

**Fixes applied:** unpinned-uses, missing-permissions

**Notes:**

Fixed all 8 unpinned `uses:` references in .github/workflows/CI.yml by replacing mutable tags with full 40-character commit SHAs (actions/checkout@v7→3d3c42e5..., actions/setup-node@v7→820762786..., actions/checkout@v6→d23441a4..., actions/setup-node@v6→249970729...). Added a top-level `permissions: contents: read` block to restrict the workflow token to the minimum required permissions.

