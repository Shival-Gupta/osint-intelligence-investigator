---
name: osint-intelligence-investigator
description: "Autonomous, multi-phase Open Source Intelligence (OSINT) investigation skill for lawful, authorized defensive research, target footprinting, identity correlation, SOCMINT, GEOINT/IMINT, breach exposure analysis, and infrastructure reconnaissance. Use when analyzing an email, username, domain, phone number, image, or person of interest using verified open sources. Enforces strict passive-first collection, OPSEC compliance, evidence-ledger provenance, source-linked confidence scoring, and privacy-preserving reporting."
version: 1.0.0
author: Hermes Agent + Nous Research
license: MIT
platforms: [linux, macos, windows]
metadata:
  hermes:
    tags: [osint, intelligence, investigation, security-research, open-source-intelligence, privacy, threat-intelligence, socmint, geoint, breach-analysis]
---

# OSINT Intelligence Investigator

A systematic, multi-modal Open Source Intelligence (OSINT) skill for AI agents operating in autonomous and semi-autonomous environments (Hermes, Google Antigravity, Claude Code, Codex, OpenCode, Gemini, and standalone scripts).

The agent ingests one or more initial seeds (email address, corporate domain, username, phone number, image, or geographical coordinate), builds a dynamic graph of known and inferred entities, executes passive and semi-active queries against verified OSINT resources, correlates multi-modal evidence, computes cross-source confidence scores, and produces verified intelligence dossiers adhering strictly to legal, privacy, and OPSEC guardrails.

---

## 1. Operating Rules & Ethical Constraints

Before executing any investigative action, the agent **MUST** enforce the following rules:

> [!IMPORTANT]
> **Strict Passive & Non-Intrusive Reconnaissance:**
> - **ALLOWED:** Querying public web indexes, search engines, public APIs, DNS records, certificate transparency logs (`crt.sh`), historical archives (Wayback Machine), and public databases.
> - **CONTROLLED:** Querying password-reset discovery APIs (e.g., Holehe) or platform profile endpoints. Must use randomized User-Agents and rate limiting.
> - **STRICTLY PROHIBITED:** Active vulnerability exploitation, automated injection testing (SQLi/XSS), brute-forcing, attempting unauthorized credential logins, or network penetration.

> [!CAUTION]
> **Defensive & Authorized Scope Only:**
> - Do NOT perform non-consensual tracking, harassment, or doxxing.
> - Strip or redact unrelated third-party private sensitive data (minors, non-public medical/financial details) encountered during correlation.
> - Always record evidentiary provenance (URL, timestamp, tool, content hash).

### 1.1 Scope Gate (Before Research)

Establish before collection:
- **Objective:** What question must be answered?
- **Target type:** Organization, domain, public event, public figure in official capacity, user's own footprint, or other?
- **Authorization:** Is the target an asset the user owns, controls, or has permission to assess?
- **Boundaries:** What is explicitly excluded?
- **Timeframe:** Is current information needed, or a historical window?
- **Deliverable:** Brief, timeline, source list, report, or risk assessment?

If the request is clearly benign and adequately scoped, do not burden the user with unnecessary questions. If target ownership/authorization is unclear and the task involves technical probing, ask for clarification or limit to passive public-source research.

### 1.2 Disallowed Work

Do not assist with: doxxing, stalking, harassment, intimidation, blackmail, targeting; aggregating private-person sensitive details (home address, family, private phone/email, precise location, daily routines, vulnerabilities, or sensitive attributes) into a dossier; real-time tracking or movement prediction; deanonymization of private/pseudonymous people from clues or media; credential discovery, validation, theft, account takeover, social engineering, or use of leaked secrets; accessing private accounts or bypassing authentication/CAPTCHA/rate limits; intrusive probing, exploitation, or scanning without explicit authorization; sensitive-attribute inference or profiling.

When a request crosses these boundaries, briefly explain the privacy/safety issue and offer a safe alternative (self-audit, scam verification, organization-level research, or high-level methodology).

---

## 2. Investigation Lifecycle

1. **Define:** clarify the question, scope, timeframe, assets, authorization, and exclusions.
2. **Plan:** map intelligence questions to source types; choose low-impact methods first.
3. **Discover:** identify candidate sources and search paths.
4. **Collect:** capture only relevant public data; record URLs, access time, context.
5. **Normalize:** standardize dates, domains, usernames, locations, entity labels.
6. **Correlate:** connect observations only when evidence supports the relationship.
7. **Verify:** corroborate material claims; check contradictions; assess source reliability.
8. **Analyze:** distinguish direct observations, inferences, hypotheses, and unknowns.
9. **Report:** produce a structured report with source links and confidence.
10. **Review / close:** summarize gaps, stop when marginal value is low, apply retention/cleanup policy.

---

## 3. Step-by-Step Execution Playbooks

### Playbook A: Username Reconnaissance (SOCMINT)
**Target:** An online alias or username (e.g., `target_handle`).

1. **High-Speed Account Enumeration with Sherlock:**
   ```bash
   sherlock <target_handle> --timeout 5 --print-found --output ./cases/<case_id>/sherlock_results.txt
   ```
2. **Detect Sub-Community Platform Profiles:** scan developer repositories (GitHub, GitLab, Bitbucket); security forums and bug bounty platforms (HackerOne, Bugcrowd); discussion boards (Reddit, Hacker News, Telegram channels).
3. **Handle Disambiguation:** compare account creation dates, bios, profile avatar perceptual hashes, and stylistic writing patterns to determine if same-username accounts belong to the same person.

### Playbook B: Email & Breach Exposure Analysis
**Target:** Email address (e.g., `target@example.com`).

1. **Zero-Touch Account Registration Check with Holehe:**
   ```bash
   holehe <target@example.com> --only-used --no-clear
   ```
   *Identifies if the email is registered on Twitter, GitHub, Amazon, Deliveroo, LinkedIn, Spotify, etc., without sending reset emails to the target.*
2. **Google Account & Ecosystem Pivot with Epieos:**
   - Query Epieos (`https://epieos.com/?q=<target@example.com>`).
   - Extract Google User ID (Gaia ID).
   - Review publicly submitted Google Maps reviews (reveals travel patterns, hometown, favorite locations).
3. **Breach Exposure Telemetry (HaveIBeenPwned & DeHashed):**
   - Query HIBP for historical incident names, dates, and compromised data classes.
   - Cross-reference on DeHashed for linked historical hashes, associated IP addresses, and historical phone numbers.

### Playbook C: Phone & Telecom Intelligence
**Target:** Telephone number (e.g., `+1-555-019-2834`).

1. **E.164 Standardization & Telecom Footprinting with PhoneInfoga:**
   ```bash
   phoneinfoga scan -n <+155****2834>
   ```
   *Extracts carrier name, line type (VoIP / Landline / Mobile), country code, and ITU prefixes.*
2. **Spam & Reputation Database Verification:** query WhoCalledMe (`https://whocalledme.com`) and similar spam registries for reports, company associations, or robocall notes.
3. **VoIP Identification:** if line type is `VoIP` (e.g., Twilio, Bandwidth, Google Voice), flag as disposable/virtual and deprioritize as a physical location anchor.

### Playbook D: Domain & Infrastructure Reconnaissance
**Target:** Domain name (e.g., `target-organization.com`).

1. **Harvesting Public Intelligence with theHarvester:**
   ```bash
   theHarvester -d target-organization.com -b duckduckgo,bing,crtsh,certspotter -l 200
   ```
2. **Certificate Transparency Mining (`crt.sh`):**
   - Query `https://crt.sh/?q=%25.target-organization.com&output=json` to uncover unlinked subdomains, dev portals, VPN endpoints.
3. **Google Dorking for Sensitive Exposures:**
   ```text
   site:target-organization.com filetype:pdf OR filetype:docx OR filetype:xlsx "confidential"
   site:target-organization.com inurl:admin OR inurl:login OR inurl:portal
   site:target-organization.com ext:sql OR ext:env OR ext:log OR ext:bak
   site:s3.amazonaws.com "target-organization"
   site:storage.googleapis.com "target-organization"
   ```

### Playbook E: Visual & Geospatial Forensics (GEOINT / IMINT)
**Target:** Photograph, screenshot, or coordinate.

1. **Forensic Metadata Inspection with ExifTool:**
   ```bash
   exiftool -a -u -g1 -G -s ./cases/<case_id>/evidence/target_image.jpg
   ```
   *Inspect for:* GPSLatitude / GPSLongitude; Make / Model (camera/device); SerialNumber (unique hardware identifier); Software (Photoshop, Lightroom, or mobile OS build); CreateDate vs. ModifyDate.
2. **Reverse Visual Search & Provenance:** submit hash or image to TinEye (`https://tineye.com`) and Google Lens; identify original uncropped photograph, earliest upload date, alternate higher-resolution versions.
3. **Geospatial Triangulation with Overpass Turbo (OpenStreetMap):** when landmarks or features are visible:
   ```text
   [out:json][timeout:25];
   (
     node["railway"="tram_stop"](around:200, 50.0755, 14.4378);
     node["amenity"="place_of_worship"](around:200, 50.0755, 14.4378);
   );
   out body;
   >;
   out skel qt;
   ```
4. **Chronolocation & Solar Azimuth Analysis:**
   - Measure shadow length and direction relative to known vertical objects.
   - Use sun angle / azimuth calculators (e.g., SunCalc) against estimated capture dates to bound latitude/longitude candidates.

### Playbook F: Public Records & People Directory Corroboration
**Target:** Subject legal name, candidate aliases, or geographic association.

1. **Multi-Source Aggregator Querying:**
   - Cross-query primary public directories: Spokeo (`https://www.spokeo.com`), ThatsThem (`https://thatsthem.com`), BeenVerified (`https://www.beenverified.com`), FastPeopleSearch (`https://www.fastpeoplesearch.com`), TruePeopleSearch (`https://www.truepeoplesearch.com`), and FamilyTreeNow (`https://www.familytreenow.com`).
   - For Eastern European, Russian, or Cyrillic-language subjects: query Yandex People (`https://people.yandex.ru`) for VKontakte, Odnoklassniki, and Moimir social profile indexing.
2. **High-Recall / Low-Precision Filter Gate:**
   - Never accept an aggregator match as fact ($w_i = 0.40$).
   - Require corroboration across at least two independent primary records (e.g., state business filings, public SEC/corporate records, domain registrant history).
3. **Privacy & Protective Boundaries:**
   - Redact unrelated household members, minors, and non-relevant private contacts.
   - Exclude home addresses and sensitive financial details from general output dossiers.

### Playbook G: Behavioral, Temporal & Chronolocation Analysis
**Target:** Time-series activity data (Git commits, messaging timestamps, social media posts).

1. **Circadian Activity Histogram (`fb-sleep-stats` Methodology):**
   - Ingest all observable activity timestamps and normalize to UTC (`YYYY-MM-DDTHH:MM:SSZ`).
   - Bucket actions into a 24-hour UTC activity distribution histogram.
   - Identify the continuous 6–8 hour trough of lowest activity (the natural biological sleep window).
2. **Timezone Derivation:**
   - Assume typical sleep occurs between 23:00 and 07:00 local time.
   - Calculate candidate UTC offset: $\text{Offset} \approx \text{Local Sleep Midpoint} - \text{Observed UTC Inactivity Midpoint}$.
   - Correlate with candidate geographic regions and language/locale markers (date format, keyboard layouts).

### Playbook H: Multi-Source Automation & Chain of Custody Preservation
**Target:** Enterprise asset discovery and evidentiary capture.

1. **Passive Automated Reconnaissance with SpiderFoot:**
   ```bash
   python3 sf.py -s target-organization.com -m sfp_whois,sfp_dnsresolve,sfp_crt -u cli -o json
   ```
   *Enforce passive-only modules; prohibit active port scanning or intrusive vulnerability crawls.*
2. **Modular Workspace Intelligence with Recon-ng:**
   ```text
   recon-ng
   workspaces create case_investigation
   db insert domains target-organization.com
   modules load recon/domains-hosts/brute_hosts
   run
   ```
3. **Tamper-Evident Evidence Preservation (Hunchly / Hash Ledger):**
   - Capture full web page DOM and HTTP response headers.
   - Compute SHA-256 hash immediately upon ingest:
     ```bash
     sha256sum ./evidence/page_snapshot.mhtml > ./evidence/page_snapshot.sha256
     ```
   - Record in the append-only Evidence Ledger to ensure non-repudiation.

---

## 4. Evidence Ledger & Chain of Custody

All agents communicate asynchronously via an append-only JSON/SQLite **Evidence Ledger**.

### 4.1 Evidence Record Schema
```json
{
  "evidence_id": "ev_48a17c",
  "target_entity_id": "ent_9f82d1",
  "source_type": "TELECOM_LOOKUP",
  "source_url_or_tool": "phoneinfoga://lookup?number=15550192834",
  "source_reliability": 0.90,
  "raw_data_hash": "sha256:...",
  "findings": {
    "carrier": "Verizon Wireless",
    "line_type": "MOBILE",
    "valid": true,
    "registered_location": "Arlington, VA"
  },
  "opsec_cleared": true,
  "timestamp": "2026-11-21T18:05:12Z"
}
```

### 4.2 Entity Node & Graph Edge Schemas
```json
{
  "entity_id": "ent_9f82d1",
  "type": "IDENTITY_PERSON",
  "canonical_value": "Jane Doe",
  "confidence_score": 0.88,
  "status": "VERIFIED",
  "attributes": { "aliases": ["jdoe_sec", "janedoe99"], "primary_email": "jane.doe@example-target.com" },
  "first_observed": "2026-11-21T18:00:00Z",
  "last_updated": "2026-11-21T18:15:30Z",
  "discovered_by": "identity-breach-auditor"
}
```

```json
{
  "edge_id": "rel_c7120a",
  "source_node": "ent_9f82d1",
  "target_node": "ent_33b821",
  "relationship": "OWNS_DOMAIN",
  "weight": 0.85,
  "evidence_refs": ["ev_48a17c", "ev_11d29e"],
  "notes": "Domain WHOIS historical contact email matches canonical email from breach correlation."
}
```

**Chain of Custody & Verifiability:** Every assertion in an agent report must carry a cryptographic hash of raw inputs, an exact timestamp, and an archived source link (or Wayback Machine snapshot).

---

## 5. Verification & Confidence Scoring Framework

Every assertion and graph node must receive a computed **Confidence Score ($S_c$)** between 0.0 and 1.0:

$$S_c = \min\left(1.0, \sum_{i=1}^{n} w_i \cdot R_i \cdot C_i\right)$$

Where:
- $w_i$: Weight of source type (Official Government Registry = 0.95, Breach Record = 0.85, Verified Social Media OAuth = 0.80, Generic People Search Directory = 0.40, Automated Scraping = 0.30).
- $R_i$: Source reliability score (historical accuracy, recency of observation).
- $C_i$: Corroboration factor (number of independent sources confirming the identical attribute).

**Score Brackets:**
| Score | Classification | Definition | Reporting Rule |
| :---: | :--- | :--- | :--- |
| **0.85 – 1.00** | **VERIFIED** | Confirmed by 2+ independent, high-reliability primary sources. | State as definitive fact. |
| **0.65 – 0.84** | **PROBABLE** | Strong correlation with consistent indicators. | State as probable finding with listed evidence. |
| **0.40 – 0.64** | **HYPOTHETICAL** | Single unverified source (e.g., people-search aggregator or common username). | Mark explicitly as unverified lead. |
| **< 0.40** | **DISCARDED** | Discrepant data, debunked collision, or contradictory timeline. | Archive in scratch log; exclude from dossier. |

**Qualitative labels:** High (direct primary evidence or independent corroboration, little ambiguity), Medium (credible evidence but incomplete corroboration or some ambiguity), Low (indirect, ambiguous, stale, or single-source), Unverified (plausible lead only). Never present these as general investigation quality; they apply per-claim.

---

## 6. Reporting & Output Formats

### 6.1 Quick Brief
```markdown
# OSINT Brief
## Question
...
## Key findings
- [Claim] — [Confidence]
## Evidence
- [Source](URL) — supports [specific claim]; accessed [date]
## Confidence
...
## Limitations / unknowns
...
## Recommended next steps
...
```

### 6.2 Full Report
```markdown
# OSINT Report: [Topic]
## 1. Executive summary
## 2. Scope, timeframe, and authorization
## 3. Research questions
## 4. Methodology and sources
## 5. Findings
| Finding | Source / evidence | Date | Confidence | Limitations |
## 6. Timeline
## 7. Evidence-backed relationships
## 8. Contradictions and alternative explanations
## 9. Gaps and limitations
## 10. Conclusion
## 11. Recommended next steps
## 12. Source list
```

**Style rules:** Direct, precise, neutral; avoid dramatic language and speculation; use tables where they improve scanability; explain technical terms briefly when needed; cite sources next to claims; clearly label assumptions and inference; don't inflate reports with irrelevant discoveries.

---

## 7. Tool Discipline & Execution Gates

Before using any automation, the agent must confirm:
1. Does the tool add value?
2. Is it installed/available? What does it actually do on the network?
3. Does it require API keys, cookies, accounts, or paid credits?
4. Is the operation passive, target-touching, noisy, or side-effecting?
5. Is the target authorized and exact?
6. Can results be verified?

- Passive discovery is the default. Active/noisy/costly execution requires clear scope and explicit approval.
- Do not install packages, run unknown code, create accounts, contact people, publish, or schedule monitoring without required approval. Respect service terms, rate limits, access controls.
- Treat automated results as leads, not proof; confirm important results independently where feasible.

---

## 8. Completion Checklist & Stop Conditions

**Stop collection when:** the research question is sufficiently answered; new results are duplicative; permitted scope is exhausted; collection would become invasive/unauthorized/costly; sensitive personal information is encountered outside scope; a safety or authorization concern appears.

**Before finalizing, verify:**
- [ ] The original question is answered.
- [ ] Scope and authorization were respected.
- [ ] Claims are source-linked.
- [ ] Original sources were opened where practical.
- [ ] Material claims were corroborated.
- [ ] Dates and context were checked.
- [ ] Facts and inferences are separated.
- [ ] Contradictions and uncertainty are included.
- [ ] Private/sensitive data was minimized.
- [ ] Tool execution is described honestly.
- [ ] No unsafe scope expansion occurred.
- [ ] Recommendations are concrete and proportionate.

---

## 9. Resource Catalog (Analysed)

See `references/resource_catalog.md` for the full analysed resource directory, including methodology, search engines/dorks, people-finders, breach databases, phone intelligence, image/metadata tools, SOCMINT tooling, automation frameworks, geospatial sources, and agent-native AI OSINT resources.

> [!NOTE]
> Availability, coverage, terms, features, pricing, and APIs change. The agent should check official documentation before claiming a tool is current or invoking it. A resource list is a catalog — not a mandate to use every tool.

---

## 10. Cross-Agent Portability

This playbook is intentionally tool-neutral and portable across agent hosts:

```text
osint/
├── SKILL.md
├── agents.md
└── references/
    └── resource_catalog.md
```

- **Hermes:** follow the installed Hermes skill/workspace discovery conventions; keep the skill concise and link references.
- **Claude Code:** package in its skill directory using the current Agent Skills format and Claude-specific frontmatter only if required.
- **Antigravity:** expose core rules in project/global agent instructions; reference the playbook as a skill/task resource where supported.
- **Codex / OpenCode / other agents:** use the host's documented skill directory or instruction-file mechanism.

Avoid host-specific syntax in the core skill. Optional adapters can live in separate files.
