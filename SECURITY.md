# Security Policy

This repository (`hsld/encbackup`) provides a lightweight Bash utility to create **encrypted backup archives** (tar → lz4 → gpg) and to decrypt/restore them.

Because this tool is used to protect sensitive data, security reports are welcome.

## Supported Versions

Only the **latest commit on the default branch** is considered supported for security fixes.
Older commits/tags/forks are not maintained.

## Reporting a Vulnerability

### Please avoid public disclosure of sensitive details

Do **not** open a public issue if your report includes any of the following:

- passphrases, key material, or command lines containing secrets
- a practical method to recover plaintext without the passphrase
- arbitrary file write outside the intended extraction directory (path traversal)
- command injection or unsafe handling of user-controlled input
- anything that could reasonably be used to compromise users

### Preferred: GitHub private vulnerability reporting

Use GitHub’s private reporting if available:

1. Repository → **Security** → **Advisories**
2. **Report a vulnerability**

If private reporting is not available, open a public issue with **minimal information** (no PoC, no secrets) and state you can share full details privately.

### What to include

- Affected file(s) (e.g., `encbackup`) and a concise description
- Steps to reproduce (as safely as possible)
- Expected vs. actual behavior
- Impact assessment (confidentiality/integrity/availability)
- Any proposed fix or mitigation

## Scope

### In scope

- The `encbackup` script (argument parsing, quoting, temporary files, error handling)
- Encryption/decryption flow (tar/lz4/gpg invocation and flags)
- Passphrase handling (`--passphrase-file`, `--passphrase VAR`, environment variable usage)
- Extraction behavior and filesystem safety (path traversal, symlinks, permissions)
- Documentation that recommends usage patterns

### Out of scope

- Vulnerabilities in external tools (`tar`, `lz4`, `gpg`, `bash`) unless this repository enables unsafe usage patterns
- Misconfiguration or insecure usage by downstream users (e.g., weak passphrases, storing secrets in world-readable files)

## Disclosure and Fixes

- Best effort will be made to acknowledge reports, but **no response time or fix timeline is guaranteed**.
- Fixes will be delivered via commits to the default branch.
- If you need coordinated disclosure, propose a date in your report.

## Operational Security Notes (for users)

- Treat passphrases as secrets: do not put them in shell history, logs, or process listings.
- If using `--passphrase VAR`, prefer sourcing the variable from a protected location (not interactive history).
- Protect passphrase files with strict permissions (e.g., `chmod 600`).
- Verify restore operations in a safe location before overwriting important data.
