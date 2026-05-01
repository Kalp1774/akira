# Changelog

All notable changes to Akira will be documented here.
Each version is named after a creature, animal, or mythical legend based on its behavior.

---

## [Hydra - v1.0.1] - 2026-04-21

*13 heads now. The hydra grew one more.*

Patch release adding a new specialized skill and upgrading recon to full conference-grade coverage.

### Added
- `403-bypass` - new specialized skill with 29+ techniques across 5 priority layers
  - Layer 1: IP spoofing headers, hop-by-hop stripping, URL rewrite headers (X-Original-URL)
  - Layer 2: path manipulation, double URL encoding (DEF CON 2024), Unicode normalization, Nginx off-by-slash
  - Layer 3: H2C smuggling, CL.TE/TE.CL request smuggling, JWT algorithm confusion
  - Layer 4: IIS tilde/ADS, prototype pollution, mass assignment, host header tricks, port ACL gaps
  - Layer 5: automated sweep (nomore403, 403-Bypasser, nuclei templates)
  - **2024-2026 research:** Apache `?` ACL bypass - Orange Tsai Confusion Attacks (Black Hat USA 2024)
  - **2024-2026 research:** CVE-2025-32094 - OPTIONS + obsolete line folding smuggling (Akamai, James Kettle BH2025)
  - **2024-2026 research:** BreakingWAF - CDN/WAF misconfiguration origin IP bypass (Zafran Dec 2024, affects 40% of Fortune 100)
  - **2024-2026 research:** CVE-2026-34950 - fast-jwt whitespace-prefix RSA key confusion (CVSS 9.1)
  - **2024-2026 research:** JSON body path traversal WAF bypass

### Upgraded
- `recon` - rewritten from 71-line script wrapper to full 23-step conference-grade pipeline
  - **Step 16:** AXFR zone transfer against ALL nameservers (forgotten NS often still allow it)
  - **Step 17:** Passive DNS historical intel - SecurityTrails + Farsight DNSDB (100B+ records) + VirusTotal graph pivot
  - **Step 18:** Advanced scanner queries - FOFA full-text HTML, Netlas, LeakIX, Criminal IP, ZoomEye
  - **Step 19:** JARM/JA4+ TLS fingerprinting for infrastructure correlation and CDN origin bypass
  - **Step 20:** Supply chain recon - dependency confusion (Alex Birsan technique), source map mining, npm/PyPI unclaimed check
  - **Step 21:** Wayback CDX API advanced mining - collapse=urlkey, statuscode filters, shadow endpoints
  - **Step 22:** reconFTW orchestration - 50+ tool automated pipeline

---

## [Hydra - v1.0.0] - 2026-04-16

*12 heads. 12 skills. The full attack chain.*

Like the mythological hydra, each skill operates independently but feeds the same body. Cut one path, three more open.

### Added - Core 7-Phase Engagement Lifecycle
- `plan-engagement` - scope, PTT generation, session.json initialization
- `recon` - subdomains, live hosts, ports, URLs, tech stack fingerprint
- `secrets` - API keys, tokens, credentials in JS/source/git/Postman collections
- `exploit` - XSS (dalfox), SQLi (sqlmap), nuclei, deserialization, SSTI, XXE, NoSQLi, WebSocket
- `zerodayhunt` - chain attacks, JWT confusion, SSRF->IAM, WAF bypass, type juggling, prototype pollution
- `triage` - severity clustering, confidence scoring (0-100), FP verification gate, deduplication
- `report` - pentest report + HackerOne/Bugcrowd submission format

### Added - Specialized Attack Modules
- `ad-attacks` - BloodHound path analysis, Kerberoasting, AS-REP roasting, DCSync, Pass-the-Hash,
  Pass-the-Ticket, ADCS ESC1-8, unconstrained/constrained delegation, Golden/Silver Ticket
- `oauth-attacks` - redirect URI bypass, CSRF, PKCE downgrade, JWT confusion, implicit flow token theft,
  postMessage leakage, authorization code interception chains
- `race-conditions` - HTTP/2 single-packet attack, coupon reuse, wallet double-spend, OTP bypass, TOCTOU
- `cloud-audit` - AWS SSRF->IAM, S3 enum, IAM privesc (Pacu), GCP service account, Azure RBAC,
  K8s API unauthenticated access, etcd exposure, kubelet API
- `ctf` - HackTheBox/TryHackMe methodology, web/crypto/pwn/RE/forensics/OSINT/stego

### Added - Architecture
- Phase handoff system: each skill reads `interesting_<phase>.md` from previous phases
- `session.json` cross-phase intelligence tracking (live hosts, credentials, PTT, tech stack)
- Anti-hallucination evidence gate enforced in every skill
- Confidence scoring system (0-100) with auto-downgrade below 70
- False positive verification gate in triage
- Pentest Task Tree (PTT) living attack graph in session.json

### Added - Platform Support
- Claude Code native (primary) via `~/.claude/skills/`
- Gemini CLI adapter (`GEMINI.md`)
- Cursor rules (`.cursor/rules/akira.mdc`)
- Codex/AGENTS.md pattern
- Generic agent support via `AGENTS.md`

### Added - Toolchain
- `install.sh` - one-command skill installer
- `bootstrap.sh` - installs nuclei, dalfox, subfinder, httpx, dnsx, ffuf, sqlmap, nmap, trufflehog
- `FINDINGS.md` - live bug bounty findings (updated weekly)

---

---

## [Basilisk - v1.1.0] - 2026-05-01

*Kills through indirect contact. Supply chain, deserialization, prototype pollution.*

Architecture rewrite. Every skill got deeper. Two new skills shipped. Docker image now auto-published to GHCR.

### Added
- `redteam` - full red team methodology: C2 frameworks, initial access, lateral movement, persistence, ADCS, delegation abuse, credential attacks, evasion, exfil, OPSEC, LOTL
- `compact` - context compression skill for long engagements
- `_shared` framework - cross-skill shared utilities (phase0 initialization, signal bus)
- Dockerfile + GHCR auto-publish workflow (`docker pull ghcr.io/kalp1774/akira`)
- `validate-skills` GitHub Actions CI workflow

### Expanded
- `exploit` - 9 new technique modules: deserialization, GraphQL, IDOR/mass assignment, CORS misconfiguration, cache smuggling, credential spray, 2FA bypass to ATO, business logic, JNDI/Log4Shell CVE chains
- `recon` - 15 new technique modules: ASN/subdomain, cloud buckets, advanced DNS, GitHub recon, OSINT, reconFTW, scanners, supply chain, takeover, TLS fingerprinting, URL mining, Wayback deep-dive
- `zerodayhunt` - 18 new technique modules: XS-leaks, JWT/SAML/SSO, SSRF/OOB, GraphQL, supply chain, CI/CD, file/crypto, WAF header mining, WebSocket/API, business logic, chain blueprints, mobile APK, race timing, SSTI/deser/XXE, CORS/host header, admin infra, client-side protocols, takeover/cloud
- `plan-engagement` - session schema, memory schema, intelligence protocol, fork protocol references
- All existing skills updated: `secrets`, `triage`, `report`, `oauth-attacks`, `race-conditions`, `cloud-audit`, `ad-attacks`

---

## Upcoming

### [Raven - v1.2.0] - June 2026

*Legendary memory. Dark perception. Intelligence that accumulates.*

Ravens are known for long memory and pattern recognition. This release gives Akira a memory of its own - context that builds across sessions and targets.

- Akira Context Engine - auto CVE lookup for detected stack + HackerOne public report correlation
- `cache-attacks` - poisoning + deception unified playbook
- `csp-bypass` - JSONP, nonce reuse, base-URI injection

### [Phantom - v1.3.0] - July 2026

*Slips through defenses. No trace. No certificate. No barrier.*

Mobile targets and Burp integration - expanding Akira's reach into surfaces that traditional tools struggle to touch.

- `mobile` - Android APK, Firebase, iOS, Frida certificate pinning bypass
- `burp-integration` - native Burp MCP tools (Repeater, Intruder, proxy history)

### [Leviathan - v2.0.0] - September 2026

*Ancient. Massive. Unchained. Remembers everything.*

The leviathan is not a single strike - it is a persistent force that cannot be stopped once awakened. Akira Brain gives the tool memory across sessions. Nothing is forgotten.

- Akira Brain - persistent attack tree across sessions
- `postmap-recon` - PostmapDB integration (leaked Postman collections -> live secrets)
- `red-team` - MITRE ATT&CK full emulation
