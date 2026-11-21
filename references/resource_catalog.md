# OSINT Resource Catalog (Analysed)

Every resource below was extracted from the source material in `D:\OSINT` (`OSINT Resources.txt`, `idea.md`, `agents.md`, `skill.md` across the root, `hermes_osint_files/`, and `OSINT_Agent_Kit/` packages) and verified reachable. Availability, coverage, terms, pricing, and features change — check official documentation before relying on any entry.

**Legend — Type:** `web` = browser service · `tool` = installable CLI/GUI · `repo` = code repository/framework · `dataset` = queryable spatial/geographic database. **Behaviour:** `passive` = third-party index/lookup · `semi-active` = target-touching but low-impact · `active` = direct target interaction (requires authorization).

---

## 1. Methodology, Directories & Dorks

| Resource | URL | Type | Behaviour | Notes |
|---|---|---|---|---|
| IntelTechniques | https://inteltechniques.com | web | passive | Michael Bazzell's methods, search resources, training, practical OSINT workflows. Industry-standard methodology. |
| Michael Bazzell / Books | https://inteltechniques.com/book1.html | web | passive | Deeper methodology and structured learning. Check editions/currentness. |
| Google Hacking Database (GHDB) | https://www.exploit-db.com/google-hacking-database | web | passive | Categorized search operators/dorks (exposed credentials, misconfigured dirs, cloud buckets, sensitive docs). Use only for bounded public research; avoid sensitive-data hunting. |
| Awesome OSINT | https://github.com/jivoi/awesome-osint | repo | passive | Broad categorized directory of OSINT resources. |
| Legendary OSINT | https://github.com/K2SOsint/Legendary_OSINT | repo | passive | Directory of search engines, source categories, research resources. |
| OSINT Stuff Tool Collection | https://github.com/cipher387/osint_stuff_tool_collection | repo | passive | Large collection of online tools; useful for discovering a tool for a specific question. |
| OpenOSINT | https://github.com/OpenOSINT/OpenOSINT · https://openosint.tech/ | repo/web | mixed | Agent-oriented toolkit with Skill/MCP/CLI; architecture reference for real tool execution, provenance, and passive/noisy distinctions. Review before adapting. |

> [!NOTE]
> Several URLs in the original `OSINT Resources.txt` were truncated (`google-hac...`, `phonein...`, `sherlock-project/s...`). They have been reconstructed to the canonical links above and verified.

---

## 2. People Finders & Public Directory Aggregators

| Resource | URL | Type | Behaviour | Notes |
|---|---|---|---|---|
| Spokeo | https://www.spokeo.com | web | passive | People-search aggregation; privacy-sensitive, coverage/accuracy vary. |
| ThatsThem | https://thatsthem.com | web | passive | People/identifier aggregator; jurisdiction-dependent. |
| BeenVerified | https://www.beenverified.com | web | passive | Commercial people-search and records aggregation. |
| FastPeopleSearch | https://www.fastpeoplesearch.com | web | passive | People-search directory. |
| TruePeopleSearch | https://www.truepeoplesearch.com | web | passive | People-search directory. |
| FamilyTreeNow | https://www.familytreenow.com | web | passive | Public-record/family information aggregation. |
| Yandex People | https://people.yandex.ru | web | passive | People/profile search; availability/coverage varies. Critical for non-Western name transliteration, Cyrillic/eastern-European platforms. |

> [!WARNING]
> **People-search rule:** aggregators are high-recall, low-precision; never treat results as ground truth without secondary corroboration (property tax registry, corporate filing, verified social footprint). Do NOT use aggregators to assemble or expose a private person's sensitive details, home address, family, private contact, routines, location, or vulnerabilities.

---

## 3. Breach & Credential Exposure Intelligence

| Resource | URL | Type | Behaviour | Notes |
|---|---|---|---|---|
| Have I Been Pwned | https://haveibeenpwned.com | web/API | passive | Ethical breach telemetry: breach names, compromise dates, affected data classes — without exposing plaintext credentials. Primary bridging layer from alias to real footprint (authorized use). |
| DeHashed | https://dehashed.com | web/API | passive | High-fidelity correlation of emails, password hashes, usernames, IPs, phones across historical dumps. Requires careful authorization, account/data handling, and terms review. |

> [!CAUTION]
> Self-audits or authorized defensive checks only. Do not download, search through, reproduce, validate, or operationalize stolen credentials, session tokens, private messages, or sensitive leaked records. Report exposure at a high level and recommend remediation (unique passwords, password manager, MFA/passkeys, revoke sessions, rotate secrets).

---

## 4. Phone & Telecom Intelligence

| Resource | URL | Type | Behaviour | Notes |
|---|---|---|---|---|
| PhoneInfoga | https://github.com/sundowndev/phoneinfoga | tool | semi-active | Telecom recon: E.164 parsing, carrier lookup, line type (Mobile/Landline/VoIP), automated search footprinting. Inspect current modules. |
| WhoCalledMe | https://www.whocalledme.com | web | passive | Crowdsourced caller/spam registry: fraud, robocall patterns, call-center associations. Reports can be wrong. |

> [!CAUTION]
> Use only a user-owned number or a bounded fraud/scam verification. Public spam reports are not identity proof. Do not seek subscriber identity, home address, or location tracking. VoIP numbers are disposable/virtual — deprioritize as physical-location anchors.

---

## 5. Images, Metadata & Reverse Search (IMINT)

| Resource | URL | Type | Behaviour | Notes |
|---|---|---|---|---|
| Google Images / Lens | https://www.google.com/imghp?hl=en | web | passive | Broad image discovery and reverse-search entry point. |
| TinEye | https://www.tineye.com | web | passive | Reverse image matching; provenance, modification history, original resolution discovery. |
| ExifTool | https://exiftool.org | tool | local | Comprehensive metadata extraction: EXIF, IPTC, XMP, MakerNotes, GPS, camera serial, lens, software, timestamps. |
| ExifData | https://exifdata.com | web | passive | Browser-based metadata inspection. |

> [!NOTE]
> Image similarity is not identity proof; metadata can be absent, manipulated, or stale. Do not publish private GPS or use image clues to track private individuals.

---

## 6. SOCMINT (Social Media Intelligence)

| Resource | URL | Type | Behaviour | Notes |
|---|---|---|---|---|
| Sherlock | https://github.com/sherlock-project/sherlock | tool | semi-active | High-speed parallel account presence detection across 400+ platforms. Presence is not identity confirmation. |
| Holehe | https://github.com/megadose/holehe | tool | semi-active | Password-reset endpoint prober detecting registration on 120+ platforms via email, without alerting the target (no reset email sent). Narrow/self-audit use only. |
| Epieos | https://epieos.com | web | semi-active | Reverse lookup: Google accounts, Maps reviews, Calendar links, linked corporate profiles from an email. Treat as leads. |
| Facebook Sleep Stats | https://github.com/sqren/fb-sleep-stats | repo | semi-active | Behavioral/temporal analysis reference for activity patterns. Verify current maintenance and data access before use. |

> [!CAUTION]
> Public, permitted content only. Do not infer sensitive traits, private relationships, routines, vulnerabilities, or precise whereabouts. Do not enumerate accounts at scale or attempt logins.

---

## 7. Automation & Orchestration Frameworks

| Resource | URL | Type | Behaviour | Notes |
|---|---|---|---|---|
| SpiderFoot | https://www.spiderfoot.net · https://github.com/smicallef/spiderfoot | tool | mixed | Multi-source asset enumeration, ASN mapping, leak detection. Broad/potentially noisy — configure passive sources, inspect module behaviour. |
| theHarvester | https://github.com/laramies/theHarvester | tool | mixed | Passive search-engine harvesting for emails, subdomains, names, hosts; CT parsing. Source activity classes differ. Authorized targets only. |
| Recon-ng | https://github.com/lanmaster53/recon-ng | tool | mixed | Modular framework: DNS bruteforcing, whois, Netcraft mining. Select modules deliberately; inspect network behaviour. |
| Maltego | https://www.maltego.com | tool | mixed | Visual link analysis and transforms; relationships need independent validation. |
| Hunchly | https://www.hunch.ly | tool | passive | Evidentiary web capture / tamper-evident audit trails. Consider when source retention matters. |
| Mr.Holmes | https://github.com/Lucksi/Mr.Holmes | repo | mixed | Multi-module OSINT tool; review individual modules, dependencies, scope, privacy before use. |

> [!NOTE]
> Passive discovery is the default. Domain/infrastructure research only on assets the user owns or is authorized to assess — no exploitation, no intrusive probing. Distinguish passive provider lookup from direct DNS/HTTP/network interaction.

---

## 8. Geospatial (GEOINT)

| Resource | URL | Type | Behaviour | Notes |
|---|---|---|---|---|
| OpenStreetMap | https://www.openstreetmap.org | dataset | passive | Community-maintained geographic data. |
| Overpass Turbo | https://overpass-turbo.eu | tool | passive | Overpass QL queries + visualization for feature triangulation (landmarks, tram tracks, churches, infrastructure). |

> [!NOTE]
> Use for public geographic context and bounded research. Preserve query, map/data version/date, and limitations. Do NOT geolocate or track a private person.

---

## 9. Agent-Native / AI OSINT Resources

| Resource | URL | Type | Behaviour | Notes |
|---|---|---|---|---|
| OpenOSINT | https://github.com/OpenOSINT/OpenOSINT · https://openosint.tech/ | repo/web | mixed | Agent toolkit (Skill/MCP/CLI) — real tool execution, provenance, passive/noisy distinctions. |
| osint-ai | https://github.com/dkyazzentwatwa/osint-ai | repo | mixed | Phased research, entities, evidence, contradictions, QA, reports. Review modules/policy before adapting. |
| smixs/osint-skill | https://github.com/smixs/osint-skill | repo | mixed | Cross-agent skill architecture, staged workflow, optional integrations. Early-beta — inspect scripts/integrations rather than copying blindly. |

---

## 10. Original Resource List Additions (from `OSINT Resources.txt`)

The following appear in the raw list and are covered by the categories above; listed here for completeness: inteltechniques.com; GHDB; Spokeo; ThatsThem; BeenVerified; FastPeopleSearch; TruePeopleSearch; FamilyTreeNow; Yandex People; HIBP; DeHashed; WhoCalledMe; PhoneInfoga; Google Images; TinEye; ExifTool; ExifData; Facebook Sleep Stats; SpiderFoot; theHarvester; Recon-ng; Maltego; Epieos; Sherlock; Holehe; Hunchly; Overpass Turbo; OpenStreetMap; Michael Bazzell; OpenOSINT; Mr.Holmes; Legendary_OSINT; osint_stuff_tool_collection; awesome-osint; osint-ai; osint-skill.

---

## Category → Agent Vector Mapping

| Agent Vector | Primary Resources |
|---|---|
| SOCMINT (username) | Sherlock, Epieos, platform-native search, GitHub/GitLab/Bitbucket, HackerOne |
| Email & Breach | Holehe, Epieos, HIBP, DeHashed |
| Phone / Telecom | PhoneInfoga, WhoCalledMe, carrier APIs |
| Domain & Infrastructure | theHarvester, Recon-ng, SpiderFoot, crt.sh, GHDB dorks, RDAP/WHOIS |
| Visual / GEOINT | ExifTool, ExifData, TinEye, Google Lens, Overpass Turbo, OSM |
| Behavioral / Temporal | fb-sleep-stats, Git/X timestamp chronolocation |
| People Directories | Spokeo, ThatsThem, BeenVerified, FastPeopleSearch, TruePeopleSearch, FamilyTreeNow, Yandex People |
| Orchestration | SpiderFoot, Maltego, Hunchly, OpenOSINT, Recon-ng |

---

## 11. Tool CLI Command & Parameter Reference

| Tool | Primary Command Syntax | Key Flags & Options | Network Behavior | API / Auth Required? |
|---|---|---|---|---|
| **Sherlock** | `sherlock <username>` | `--timeout 10`, `--print-found`, `--output <file>`, `--proxy <url>` | High-volume HTTP GET across 400+ endpoints; passive to target | No |
| **Holehe** | `holehe <email>` | `--only-used`, `--no-clear`, `--timeout 10` | Password-reset discovery requests; zero-touch (no email sent) | No |
| **PhoneInfoga** | `phoneinfoga scan -n <+1234567890>` | `--recon`, `-s <numverify>` | E.164 parsing (offline libphonenumber) + search dorks | Optional (Numverify) |
| **theHarvester** | `theHarvester -d <domain> -b <sources>` | `-b bing,duckduckgo,crtsh,certspotter`, `-l 200`, `-f <output.json>` | Passive query to public search engines & CT logs | Optional (Shodan, Censys) |
| **ExifTool** | `exiftool -a -u -g1 <file>` | `-G`, `-s`, `-json`, `-csv` | 100% offline local metadata parsing | No |
| **SpiderFoot** | `sf.py -s <target> -m <modules>` | `-m sfp_whois,sfp_dnsresolve`, `-u cli`, `-o json` | Modular; can range from passive DNS to noisy probing | Optional (API keys per module) |
| **Recon-ng** | `recon-ng -w <workspace>` | `modules load recon/...`, `run`, `db insert ...` | Modular; adheres to configured workspaces | Module-dependent |
| **Overpass QL** | `curl -X POST -d @query.osm https://overpass-api.de/api/interpreter` | `[out:json][timeout:25];` | Passive query against OpenStreetMap public API | No (public rate-limited) |

---

## 12. Google Hacking Database (GHDB) Dork Recipes

For authorized defensive security research and discovery of forgotten exposures:

| Objective | Dork Syntax | Notes |
|---|---|---|
| **Exposed Documents** | `site:target.com filetype:pdf OR filetype:docx OR filetype:xlsx "confidential" OR "internal use only"` | Uncovers unintentionally indexed corporate documents. |
| **Administrative Portals** | `site:target.com inurl:admin OR inurl:login OR inurl:portal OR inurl:dashboard` | Locates authentication surfaces and staging login screens. |
| **Database & Config Dumps** | `site:target.com ext:sql OR ext:env OR ext:log OR ext:bak OR ext:conf` | Identifies misconfigured directory indexing or backup files. |
| **Directory Indexing** | `site:target.com intitle:"index of /" OR intitle:"index of /uploads"` | Detects missing web server directory browse restrictions. |
| **Cloud Storage Buckets (AWS S3)** | `site:s3.amazonaws.com "target-brand" OR "target-keyword"` | Identifies exposed public Amazon S3 buckets. |
| **Cloud Storage (GCP & Azure)** | `site:storage.googleapis.com "target-brand"` / `site:blob.core.windows.net "target-brand"` | Identifies exposed GCP storage or Azure Blob storage. |

---

## 13. Overpass QL Geospatial Triangulation Recipes

For pinpointing geographic landmarks and features identified during visual forensics:

### Recipe 1: Triangulating Landmarks Near Public Transit
```text
[out:json][timeout:25];
(
  node["railway"="tram_stop"](around:250, 50.0755, 14.4378);
  node["amenity"="place_of_worship"](around:250, 50.0755, 14.4378);
  way["highway"="pedestrian"](around:250, 50.0755, 14.4378);
);
out body;
>;
out skel qt;
```

### Recipe 2: Identifying Distinctive Architectural Vernacular (Bridges, Towers, Parks)
```text
[out:json][timeout:30];
(
  node["man_made"="tower"](around:500, {{lat}}, {{lon}});
  way["bridge"="yes"](around:500, {{lat}}, {{lon}});
  node["leisure"="park"](around:500, {{lat}}, {{lon}});
);
out body;
>;
out skel qt;
```

---

## 14. Evidence Ledger Attribute Ingestion Mapping

| Evidence Source | Target Entity Type | Ingested Node Attributes | Base Reliability ($w_i$) |
|---|---|---|---|
| `Holehe` | `IDENTITY_PERSON` / `ONLINE_ACCOUNT` | `registered_platforms[]`, `account_verified` | 0.85 |
| `Epieos` | `IDENTITY_PERSON` | `google_gaia_id`, `calendar_url`, `maps_reviews[]`, `picasa_album` | 0.85 |
| `PhoneInfoga` | `PHONE_RECORD` | `country_code`, `carrier_name`, `line_type` (`MOBILE`/`VOIP`/`LANDLINE`) | 0.90 |
| `theHarvester` | `INFRA_DOMAIN` / `NETWORK_HOST` | `subdomains[]`, `harvested_emails[]`, `associated_ips[]` | 0.80 |
| `ExifTool` | `MEDIA_IMAGE` / `GEO_COORDINATE` | `gps_latitude`, `gps_longitude`, `camera_make_model`, `serial_number`, `software` | 0.95 |
| `HaveIBeenPwned` | `BREACH_RECORD` | `breach_names[]`, `compromised_dates[]`, `data_classes[]` | 0.90 |
| `DeHashed` | `CREDENTIAL_LINK` | `hash_type`, `associated_usernames[]`, `associated_ips[]` | 0.85 |
| `People Search (Spokeo/ThatsThem)` | `IDENTITY_PERSON` | `candidate_addresses[]`, `candidate_relatives[]` (Requires corroboration) | 0.40 |

