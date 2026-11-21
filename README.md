# OSINT Intelligence Investigator

> A universal, privacy-first Open Source Intelligence skill for AI agents. Conduct lawful, authorized defensive research with evidence-ledger provenance, cross-source confidence scoring, and structured intelligence dossiers.

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Platform: Universal](https://img.shields.io/badge/Platform-Hermes%20%7C%20Antigravity%20%7C%20Claude%20%7C%20Codex%20%7C%20OpenCode%20%7C%20Gemini%20%7C%20OpenClaw-blue.svg)](https://github.com/Shival-Gupta/osint-intelligence-investigator)

---

## 🎯 What This Skill Does

| Capability | Description |
|------------|-------------|
| **SOCMINT** | Username/account enumeration across 400+ platforms (Sherlock, Holehe, Epieos) |
| **Email & Breach Analysis** | Zero-touch registration checks, HIBP/DeHashed exposure telemetry |
| **Phone Intelligence** | E.164 normalization, carrier lookup, VoIP detection (PhoneInfoga, WhoCalledMe) |
| **Domain & Infrastructure** | Passive DNS, subdomains, CT logs, Google dorks (theHarvester, Recon-ng, crt.sh) |
| **GEOINT / IMINT** | EXIF forensics, reverse image search, OSM triangulation (ExifTool, TinEye, Overpass Turbo) |
| **Evidence Ledger** | Append-only JSON/SQLite chain-of-custody for every finding |
| **Confidence Scoring** | Mathematically grounded $S_c$ formula with VERIFIED/PROBABLE/HYPOTHETICAL/DISCARDED brackets |
| **OPSEC Compliance** | Passive-first defaults; controlled semi-active; active exploitation strictly prohibited |

---

## 📦 Quick Install (Universal One-Liner)

Copy-paste this into **any** supported AI agent:

```text
I want to install the OSINT Intelligence Investigator skill. Fetch the skill package from https://github.com/Shival-Gupta/osint-intelligence-investigator and install it for my current agent platform (Hermes/Antigravity/Claude/Codex/OpenCode/Gemini/OpenClaw). Follow the platform-specific installation steps in the repo's README.md, then confirm the skill is active and ready for OSINT investigations.
```

> **Why this works:** The prompt tells the agent to (1) fetch the repo, (2) detect its own platform, (3) follow the platform-specific steps below, and (4) verify activation. All major agent platforms can execute git/web fetch + file operations.

---

## 🛠 Platform-Specific Installation

### Hermes Agent (Nous Research)

```bash
# Option 1: CLI (recommended)
hermes skill install https://github.com/Shival-Gupta/osint-intelligence-investigator

# Option 2: Manual
git clone https://github.com/Shival-Gupta/osint-intelligence-investigator ~/.hermes/skills/osint-intelligence-investigator
hermes skill reload

# Option 3: Profile-specific
hermes --profile=osint skill install https://github.com/Shival-Gupta/osint-intelligence-investigator
```

**Activate in chat:**
```
/skill osint-intelligence-investigator
# or
@osint-intelligence-investigator [your investigation request]
```

---

### Google Antigravity (Multi-Agent Swarm)

```bash
# In Antigravity shell / web UI
swarm action:"title" title:"OSINT Intelligence Swarm"

# Add the skill as a specialist agent
swarm action:"add" name:"osint" brief:"Autonomous OSINT investigator with SOCMINT, GEOINT, breach analysis, and infrastructure recon. Uses evidence ledger and confidence scoring."
```

**Or via Antigravity skill registry:**
```yaml
# .antigravity/skills/osint.yaml
name: osint-intelligence-investigator
source: https://github.com/Shival-Gupta/osint-intelligence-investigator
agents:
  - coordinator
  - socmint
  - geoint
  - infra
  - breach
  - opsec
```

---

### Claude Code (Anthropic)

```bash
# Option 1: Global skill directory
git clone https://github.com/Shival-Gupta/osint-intelligence-investigator ~/.claude/skills/osint-intelligence-investigator

# Option 2: Project-local (recommended for team sharing)
git clone https://github.com/Shival-Gupta/osint-intelligence-investigator .claude/skills/osint-intelligence-investigator
```

**Activate:**
```
/osint [your investigation request]
# or reference in CLAUDE.md:
# @skill osint-intelligence-investigator
```

---

### Codex CLI (OpenAI)

```bash
# Codex skills live in ~/.codex/skills/
git clone https://github.com/Shival-Gupta/osint-intelligence-investigator ~/.codex/skills/osint-intelligence-investigator

# Or project-local
git clone https://github.com/Shival-Gupta/osint-intelligence-investigator .codex/skills/osint-intelligence-investigator
```

**Activate in Codex session:**
```
/skill osint-intelligence-investigator
```

---

### OpenCode (Zed / OpenCode CLI)

```bash
# OpenCode skill directory
git clone https://github.com/Shival-Gupta/osint-intelligence-investigator ~/.config/opencode/skills/osint-intelligence-investigator
```

**Activate:**
```
> skill osint-intelligence-investigator
```

---

### Gemini CLI / Google AI Studio

```bash
# Gemini skills directory (adjust per platform)
git clone https://github.com/Shival-Gupta/osint-intelligence-investigator ~/.gemini/skills/osint-intelligence-investigator
```

**In Gemini chat:**
```
@osint-intelligence-investigator [your request]
```

---

### OpenClaw / Generic Markdown Agent

Any agent that loads Markdown instruction files:

```bash
# Clone to your agent's instruction/skill directory
git clone https://github.com/Shival-Gupta/osint-intelligence-investigator /path/to/agent/skills/osint-intelligence-investigator
```

**Load the skill:**
- Reference `SKILL.md` as the primary playbook
- Reference `agents.md` as governing safety policy
- Reference `references/resource_catalog.md` for tool selection

---

## 📁 Repository Structure

```
osint-intelligence-investigator/
├── SKILL.md                      # Primary playbook (all platforms)
├── agents.md                     # Governing safety/OPSEC policy
├── LICENSE                       # MIT
├── README.md                     # This file
└── references/
    └── resource_catalog.md       # 37+ verified OSINT resources
```

---

## 🚀 Quick Start Examples

### Username Investigation (SOCMINT)
```text
@osint Investigate the username "jdoe_sec" across all platforms. 
Find linked accounts, profile bios, avatar hashes, and cross-platform correlations. 
OPSEC level: PASSIVE_ONLY.
```

### Email & Breach Exposure
```text
@osint Target: jane.doe@example-target.com
1. Run Holehe zero-touch registration check
2. Query HIBP for breach timeline
3. Cross-reference DeHashed for linked hashes/phones
4. Epieos Google ecosystem pivot
Report verified findings only.
```

### Domain Infrastructure Recon
```text
@osint Authorized target: example-corp.com
Passive reconnaissance only:
- theHarvester (duckduckgo, bing, crtsh, certspotter)
- crt.sh certificate transparency for subdomains
- Google dorks for exposed files/buckets
- DNS records via passive sources
```

### Image Geolocation (GEOINT)
```text
@osint Analyze image at ./evidence/target_photo.jpg
1. ExifTool full metadata extraction
2. TinEye + Google Lens reverse search
3. If landmarks visible: Overpass Turbo triangulation
Report confidence-scored location hypotheses.
```

### Phone Intelligence
```text
@osint Target: +1-555-019-2834 (user-owned)
- PhoneInfoga scan for carrier, line type, region
- WhoCalledMe spam/reputation check
- Flag if VoIP (disposable)
```

---

## 📊 Confidence Scoring (Built-In)

Every finding receives a computed score $S_c \in [0, 1]$:

$$S_c = \min\left(1.0, \sum_{i=1}^{n} w_i \cdot R_i \cdot C_i\right)$$

| Bracket | Label | Use |
|---------|-------|-----|
| **0.85–1.00** | **VERIFIED** | 2+ independent high-reliability sources → state as fact |
| **0.65–0.84** | **PROBABLE** | Strong correlation, consistent indicators → probable with evidence |
| **0.40–0.64** | **HYPOTHETICAL** | Single unverified source → mark as lead |
| **< 0.40** | **DISCARDED** | Contradictory/debunked → archive, exclude from dossier |

---

## 🔒 Safety & Ethics (Non-Negotiable)

> **This skill enforces strict guardrails. The agent WILL refuse:**

- ❌ Doxxing, stalking, harassment, targeting private individuals
- ❌ Aggregating sensitive personal data (home address, family, private contacts, routines)
- ❌ Real-time tracking or movement prediction
- ❌ Deanonymization of private/pseudonymous people
- ❌ Credential discovery, account takeover, social engineering
- ❌ Bypassing auth, CAPTCHA, rate limits, paywalls
- ❌ Active exploitation (SQLi, brute-force, port scanning, vuln scanning)
- ❌ Sensitive-attribute inference (health, religion, politics, sexuality, etc.)

> ✅ **Allowed:** Self-audits, authorized asset assessment, defensive fraud/scam checks, public-interest research, organization/domain research, public professional info in official capacity.

---

## 📝 Output Formats

### Quick Brief
```markdown
# OSINT Brief
## Question
...
## Key findings
- Claim — Confidence
## Evidence
- [Source](URL) — supports claim; accessed date
## Limitations / unknowns
...
## Recommended next steps
...
```

### Full Report
```markdown
# OSINT Report: [Topic]
## 1. Executive summary
## 2. Scope, authorization, timeframe
## 3. Research questions
## 4. Methodology & sources
## 5. Findings table (claim | source | date | confidence | limitations)
## 6. Timeline
## 7. Evidence-backed relationships
## 8. Contradictions & alternatives
## 9. Gaps & limitations
## 10. Conclusion
## 11. Next steps
## 12. Source list
```

---

## 🔧 Tool Requirements (Optional but Recommended)

| Tool | Install | Purpose |
|------|---------|---------|
| `sherlock` | `pip install sherlock-project` | Username enumeration |
| `holehe` | `pip install holehe` | Email registration check |
| `phoneinfoga` | [releases](https://github.com/sundowndev/PhoneInfoga/releases) | Phone OSINT |
| `theharvester` | `pip install theharvester` | Domain recon |
| `exiftool` | [exiftool.org](https://exiftool.org/) | Metadata extraction |
| `spiderfoot` | [spiderfoot.net](https://www.spiderfoot.net/) | Automation |

> The skill works **without local tools** (uses web-based equivalents), but local CLIs are faster and more reliable.

---

## 🤝 Contributing

1. Fork the repo
2. Add resources to `references/resource_catalog.md` with verification
3. Update playbooks in `SKILL.md` if needed
4. Submit PR with clear description

---

## 📄 License

MIT License — see [LICENSE](LICENSE). Free for personal, commercial, and research use.

---

## 🙏 Acknowledgments

Built on methodologies from:
- **Michael Bazzell / IntelTechniques** — OSINT tradecraft
- **Sherlock Project** — Username enumeration
- **Megadose / Holehe** — Zero-touch email checks
- **Sundowndev / PhoneInfoga** — Telecom intelligence
- **Laramies / theHarvester** — Domain harvesting
- **OpenOSINT** — Agent-native architecture reference
- **Awesome OSINT / Legendary OSINT** — Resource curation

---

## 📞 Support

- **Issues:** [GitHub Issues](https://github.com/Shival-Gupta/osint-intelligence-investigator/issues)
- **Discussions:** [GitHub Discussions](https://github.com/Shival-Gupta/osint-intelligence-investigator/discussions)

---

**Made for analysts, not surveillance.** Use responsibly. 🕵️‍♂️