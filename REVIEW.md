---
schema_version: "1.0"
repo: fw_bin
project: WMCUSW

analyze_paths:
  - "**/*.c"
  - "**/*.h"
  - "**/*.py"
  - scr.txt

skip_paths:
  - "**/*.bin"
  - "**/*.se"
  - "**/*.inc"
  - SBOM.spdx.json

# blocker_threshold: Medium — active development repo; Medium catches High+Medium severity
# issues. Raise to High if noise becomes excessive.
blocker_threshold: Medium

code_quality:
  cert_c: [EXP33-C, ERR33-C, MEM30-C]
  cwe: [CWE-119, CWE-120, CWE-125, CWE-787]

review_focus:
  # Version metadata — must be updated on every firmware binary update
  - pattern: scr.txt
    reason: >
      Firmware version record — verify version numbers are updated for all changed SoCs
      and that versions are consistent with the binary files included in the PR.

  # C header/source wrappers — must stay in sync with the corresponding .bin/.bin.se files
  - pattern: "**/*.h"
    reason: >
      Firmware C header — must be regenerated from the corresponding binary file;
      verify it is in sync with the binary updated in the same PR.
  - pattern: "**/*.c"
    reason: >
      Firmware C source — version info and cpu1/cpu2 split; verify consistency
      with the corresponding binary and header files in the same PR.

  # Script — generates .inc files from .bin; changes affect all SoCs
  - pattern: script/wlan_gen_fw_incs.py
    reason: Firmware inc generator — changes affect all SoC inc file generation

# ─────────────────────────────────────────────────────────────────────────────
# AI review tracking label
#
# The MOMENT a PR review is triggered — BEFORE reading the diff, analyzing code,
# or posting any comment — extract the associated Jira issue key and silently
# tag that Jira issue with the `ai-review` label. Bind the labelling to the
# trigger of the review, NOT to its completion: label first, then review.
# Labelling after the review does not work — the turn usually ends with the
# review output, so the label is silently lost.
#
# Get the Jira key from the PR TITLE first; if absent, fall back to the
# BRANCH NAME (e.g. bugfix/nxf57321/WSW-XXXXX-desc).
# Match with regex (WSW|MCUX)-\d+
#
# This mirrors the AI tracking-label convention used by the jira skill:
#   from jira_client import jira_add_labels
#   jira_add_labels("WSW-XXXXX", ["ai-review"])
review_actions:
  jira_labels:
    enabled: true
    label: ai-review
    issue_key_source: pr_title        # primary: Jira key in PR title
                                      # fallback 1: (WSW|MCUX)-\d+ in branch name
                                      # fallback 2: warn in review comment if no key found
    apply_when: on_review_trigger
    silent: true

# ─────────────────────────────────────────────────────────────────────────────
# Commit message format checks
#
# These mirror the repo's CI checkers (CHECKER_JIRA_ID_BLOCK, CHECKER_COMMIT_FORMAT).
# Vero should flag violations during review so issues are caught before PreMerge CI.
commit_checks:
  jira_id_block:
    enabled: true
    pattern: (WSW|MCUX)-\d+
    message: >
      Jira IDs are not allowed in commit messages for this repo.
      Move the Jira key to the PR title instead.
  commit_format:
    enabled: true
    required_tags: ["[Description]", "[Root Cause]", "[Fix]", "[Testing]", "Change-Id:"]
    optional_tags: ["[Reviewers]", "[Port proposal]"]
