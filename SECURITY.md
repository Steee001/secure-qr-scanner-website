# Security Policy & Coordinated Vulnerability Disclosure (CVD)

Secure QR Scanner (`com.steee001.secureqrscanner`) acts as a local security firewall between physical QR/barcodes and external Android intents. We treat security vulnerabilities in our link-verification pipeline, Local Mode network isolation, payload parsers, cryptographic storage, and software supply chain with top priority in accordance with the **EU Cyber Resilience Act (CRA — Regulation (EU) 2024/2847)**.

## Supported Versions

Security updates are provided free of charge for the current production release line distributed via Google Play:

| Version | Supported | Distribution Channel |
|---|---|---|
| `3.0.x` (latest Play Store release) | Yes | Google Play (`com.steee001.secureqrscanner`) |
| `< 3.0.0` | No | Upgrade to latest Google Play release |

## Reporting a Vulnerability

**Do NOT report unpatched security vulnerabilities or active exploit proofs-of-concept in public GitHub issues.**

Please submit vulnerability reports confidentially through our Coordinated Vulnerability Disclosure channel:

- **Primary Private Advisory Channel:** https://github.com/Steee001/secure-qr-scanner-website/security/advisories/new
- **RFC 9116 `security.txt`:** https://steee001.github.io/secure-qr-scanner-website/.well-known/security.txt
- **Preferred Languages:** German (`de`), English (`en`)

### What to Include

To accelerate triage and reproduction, please include:

1. Affected app version (`versionName` / `versionCode`) and Android OS version.
2. Operating mode (`Normal Mode` vs. `Local Checks Mode`).
3. Minimal, deterministic reproduction payload (e.g., synthetic QR payload, redirect chain setup, or malformed TLV/URI sample) — **never include real personal secrets, 2FA seeds, Wi-Fi passwords, or banking data**.
4. Concrete security impact (e.g., `PendingOpenReview` bypass, Local Mode outbound network leak, SSRF/redirect evasion, cryptographic/storage flaw, or UI spoofing/tapjacking).

## Triage & Patch SLAs (EU CRA Compliance)

Every good-faith vulnerability report follows binding response and remediation targets:

| Severity | Criteria | Initial Triage | Target Patch Release |
|---|---|---|---|
| **Critical / Actively Exploited** | `CVSS >= 9.0`, remote code execution, review-gate bypass, or active in-the-wild exploitation | `< 24 h` | `< 72 h` emergency release (incl. EU CRA / ENISA / BSI notification readiness) |
| **High** | `CVSS 7.0–8.9` (e.g., Local Mode network leak, phishing/redirect check bypass, SSRF) | `< 24 h` | `< 14 days` |
| **Medium** | `CVSS 4.0–6.9` (e.g., heuristic evasion, UI spoofing edge case, parser DoS) | `< 24 h` | `< 30 days` (next regular release cycle) |
| **Low / Hardening** | `CVSS < 4.0` (defense-in-depth improvements) | `< 72 h` | `< 30 days` or scheduled milestone |

## In-Scope Security Invariants

- **Single Review Gate:** Every external action (`ACTION_VIEW`, `ACTION_DIAL`, `ACTION_SENDTO`, `ACTION_INSERT`, Wi-Fi provisioning, SAF share) must pass through `PendingOpenReview`.
- **Whole-Chain Link Verification:** Every redirect hop (up to 6 hops, 8 s deadline, 8 MiB response cap) is checked against Google Safe Browsing and offline phishing heuristics.
- **Hard Local Mode Isolation:** Zero automatic outbound network requests by the app or bundled SDKs when Local Mode is active (`ScannerInitProvider` `initOrder="101"`, `PolicyCallFactory`, `LocalModeCctBackendFactory`, `LocalModeEmojiInitializer`, uninitialized Firebase).
- **On-Device Encryption & Secret Hygiene:** AES-256-GCM encryption via Android Keystore (`android:allowBackup="false"`), 2,048 UTF-16 code-unit input cap prior to sanitization, and deterministic redaction of `otpauth://` secrets across UI and exports.
- **Supply-Chain & Binary Integrity:** Locked Gradle dependency configurations (`*gradle.lockfile`), SHA-256 artifact verification (`gradle/verification-metadata.xml`), blocking OSV vulnerability scans, and verified `16 KB` ELF page alignment on 64-bit native libraries.

## Safe Harbor

Good-faith security research conducted exclusively against your own devices, local test environments, and synthetic payloads—without accessing, disrupting, or exfiltrating third-party data or services—is authorized and welcomed. We ask researchers to allow remediation within the SLA window above before public disclosure.

