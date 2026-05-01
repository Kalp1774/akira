# How to Use Akira

## Step 1 - Install

```bash
git clone https://github.com/Kalp1774/akira
cd akira
bash install.sh
bash bootstrap.sh
```

`install.sh` drops the skills into `~/.claude/skills/`.
`bootstrap.sh` installs the tools (subfinder, nuclei, dalfox, sqlmap, etc.).

Open Claude Code. You're ready.

---

## Step 2 - Run an Engagement

All 7 commands follow the same pattern: `/skill-name target.com`

```
/plan-engagement target.com
```
Sets up the session, defines scope, builds the attack plan.

```
/recon target.com
```
Finds subdomains, live hosts, ports, URLs, tech stack.

```
/secrets target.com
```
Hunts for API keys, tokens, credentials in JS bundles, git history, Postman collections.

```
/exploit target.com
```
Tests XSS, SQLi, SSRF, deserialization, SSTI, GraphQL, CORS, and more.

```
/zerodayhunt target.com
```
Goes deeper - logic chains, supply chain vectors, cryptographic weaknesses, chained attacks.

```
/triage target.com
```
Clusters findings by severity, scores confidence (0-100), filters false positives.

```
/report target.com
```
Generates a pentest report + bug bounty submission (HackerOne/Bugcrowd format).

---

## Step 3 - Read the Output

Each skill writes its findings to `~/pentest-toolkit/results/target.com/`.

| File | What's in it |
|---|---|
| `plan.md` | Scope, attack surface, PTT |
| `interesting_recon.md` | Live hosts, ports, tech stack |
| `interesting_secrets.md` | Confirmed credentials and tokens |
| `interesting_exploit.md` | Confirmed vulnerabilities with evidence |
| `interesting_zerodayhunt.md` | Chained/logic findings |
| `triage.md` | Severity clusters, confidence scores |
| `report-YYYY-MM-DD.md` | Final pentest report |
| `bugbounty-YYYY-MM-DD.md` | Bug bounty submission format |
| `session.json` | Live state shared across all skills |

---

## Rules

- Every finding needs a reproducible HTTP response with actual sensitive data. No evidence = no finding.
- OOB callbacks alone are never Critical - Akira won't report it until the full chain is proven.
- Confidence below 70 is auto-downgraded.

---

## Specialized Skills

For specific attack surfaces, use these directly at any point:

| Skill | Use When |
|---|---|
| `/cloud-audit` | AWS/GCP/Azure credentials found |
| `/ad-attacks` | Active Directory in scope |
| `/oauth-attacks` | OAuth or SSO login flows |
| `/race-conditions` | Rate limits, coupons, wallets, OTPs |
| `/403-bypass` | Getting blocked by WAF or access controls |
| `/redteam` | Full red team / MITRE ATT&CK emulation |
| `/ctf` | HackTheBox, TryHackMe, CTF challenges |

---

## Update

```bash
cd akira && git pull && bash install.sh
```
