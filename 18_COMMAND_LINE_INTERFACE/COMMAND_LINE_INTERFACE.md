# Command Line Interface — L_MOVEIT2

**Project:** `L_MOVEIT2`
**Tier:** TIER_9_ROBOTICS_IOT
**Domain:** robotics, IoT, embedded systems, ROS2, microcontrollers, edge deployment
**Maintainer:** Anticloud FZ LLE · 0-1.gg · lois@0-1.gg · Dubai, UAE
**Model:** Anticloud PAX L5 Narrow L2 General 27B
**AIOSS Chain:** `8b4a8a4f6312dfbe885de8280716985637c163fd2a4b5590341d56db1cc4e560`
**Date:** October 2026

---

## CLI Reference

`L_MOVEIT2` ships with a command-line interface for deployment, verification, and operations.

## Installation

```bash
pip install anticloud-cli
# or via the project package
pip install ./l_moveit2/
```

## Global Options

```
anticloud l-moveit2 [OPTIONS] COMMAND

Options:
  --project TEXT          Project name (default: L_MOVEIT2)
  --chain TEXT            AIOSS genesis hash
  --key PATH              Ed25519 signing key path
  --compliance TEXT       Compliance mode: gdpr|hipaa|fedramp|pci-dss
  --verbose / --quiet     Output verbosity
  --version               Show version and exit
```

## Core Commands

### `deploy` — Deploy a package

```bash
anticloud l-moveit2 deploy \
  --package l_moveit2.tar.gz \
  --verify-k5 \
  --chain 8b4a8a4f6312dfbe885de82807169856... \
  --mode air-gap
```

### `verify` — Verify deployment integrity

```bash
anticloud l-moveit2 verify \
  --k5-hashes HASHES.md \
  --chain-hash 8b4a8a4f6312dfbe885de82807169856...

# Output:
# K5 verification:    PASS
# Chain continuity:   PASS
# Compliance checks:  PASS (GDPR, HIPAA, FedRAMP)
# Brand integrity:    PASS
```

### `infer` — Run a single inference

```bash
anticloud l-moveit2 infer \
  --prompt "Analyze this document" \
  --compliance hipaa \
  --max-tokens 512 \
  --log-chain
```

### `chain-status` — Inspect AIOSS chain

```bash
anticloud l-moveit2 chain-status

# Output:
# Genesis:      8b4a8a4f6312dfbe885de82807169856...
# Current:      <current_hash>
# Entries:      <count>
# Last entry:   <timestamp>
# Integrity:    VERIFIED
```

### `audit-export` — Export compliance audit report

```bash
anticloud l-moveit2 audit-export \
  --frameworks gdpr,hipaa \
  --from 2026-01-01 \
  --to 2026-12-31 \
  --output audit_report.pdf
```

### `update` — Update with brand preservation

```bash
anticloud l-moveit2 update \
  --package l_moveit2-latest.tar.gz \
  --brand-preserve \
  --zero-downtime
```

## Exit Codes

| Code | Meaning |
|---|---|
| 0 | Success |
| 1 | K5 verification failed |
| 2 | Chain continuity error |
| 3 | Compliance check failed |
| 4 | Brand integrity violation |

**Support:** lois@0-1.gg · 0-1.gg
