## 2026-09-03 15:38:35 UTC [target] (model nemotron3)
[NEW] 9 hosts discovered via passive DNS/CT, 0 probed for live HTTP — initial surface unvalidated
[NEW] No GitHub org configured for reposcan — code-level recon gap
[NEW] Knowledge base empty — no prior tech fingerprint, endpoint map, or auth flow data
[PRIO] signl4.derdack.com,8.5,a=9 b=10 t=8 g=6 c=8 f=5
[PRIO] signals.derdack.com,8.0,a=9 b=9 t=7 g=6 c=8 f=5
[PRIO] dev.derdack.com,7.5,a=8 b=7 t=9 g=8 c=6 f=5
[PRIO] derdack.com,6.5,a=7 b=8 t=6 g=5 c=7 f=5
[PRIO] www.derdack.com,6.0,a=6 b=8 t=5 g=5 c=7 f=5
[PRIO] blog.derdack.com,4.0,a=5 b=4 t=4 g=4 c=4 f=4
[PRIO] techblog.derdack.com,4.0,a=5 b=4 t=4 g=4 c=4 f=4
[PRIO] de.derdack.com,3.5,a=4 b=4 t=3 g=4 c=3 f=4
[PRIO] www.de.derdack.com,3.5,a=4 b=4 t=3 g=4 c=3 f=4
[HYP] SIGNL4 API JWT alg confusion on token validation
class: AUTH
asset: signl4.derdack.com
confidence: 55
reasoning: SIGNL4 is a SaaS alerting platform likely using JWT for API auth; alg=none or RS256->HS256 confusion common in .NET/Node JWT libs; no public API docs observed yet
evidence_needed: JWT token from login/API call; JWKS endpoint; algorithm accepted by validation
verify_steps: GET https://signl4.derdack.com/.well-known/jwks.json; GET https://signl4.derdack.com/api/v1/user (expect 401); POST https://signl4.derdack.com/api/auth/login with test creds (observe token format)
impact: ATO on any SIGNL4 tenant; access to alerting config, on-call schedules, PII
testability: AUTH_HELPED
[HYP] signals.derdack.com SSRF via webhook/callback URL parameter
class: SSRF
asset: signals.derdack.com
confidence: 50
reasoning: "signals" subdomain suggests webhook ingestion or event forwarding; SSRF-to-cloud-metadata (169.254.169.254) high-value if cloud-hosted; no rate limiting observed
evidence_needed: Endpoint accepting URL parameter (webhook, callback, redirect_uri, fetch); response shows internal metadata or timeout differential
verify_steps: GET https://signals.derdack.com/ (enumerate paths); GET https://signals.derdack.com/api/ (look for Swagger); POST https://signals.derdack.com/webhook with url=http://169.254.169.254/latest/meta-data/ (observe status/timing)
impact: Cloud metadata credentials, IAM roles, internal service enumeration
testability: PASSIVE
[HYP] dev.derdack.com debug endpoints / actuator / swagger exposed
class: MISCONFIG
asset: dev.derdack.com
confidence: 65
reasoning: Dev/staging hosts commonly expose Spring Boot actuator, .NET healthz, Swagger UI, GraphQL playground; high tech_exposure for recon
evidence_needed: 200 OK on /actuator, /swagger, /graphql, /.well-known/, /api/docs, /health, /debug
verify_steps: GET https://dev.derdack.com/actuator; GET https://dev.derdack.com/swagger-ui.html; GET https://dev.derdack.com/api/docs; GET https://dev.derdack.com/graphql; GET https://dev.derdack.com/.well-known/openid-configuration
impact: API contract leak, internal endpoint map, potential unauthenticated admin/debug functions
testability: PASSIVE
[PARKED] SIGNL4 API JWT alg confusion on token validation: confidence<60, no token sample yet, needs auth interaction
[PARKED] signals.derdack.com SSRF via webhook/callback URL parameter: confidence<60, no endpoint confirmed, speculative
[FINAL] dev.derdack.com debug endpoints / actuator / swagger exposed — ranked #1 (highest confidence, passive-only verify)
[NEXT] PROBE: GET https://dev.derdack.com/actuator && GET https://dev.derdack.com/swagger-ui.html && GET https://dev.derdack.com/api/docs && GET https://dev.derdack.com/graphql && GET https://dev.derdack.com/.well-known/openid-configuration
[LEARN] REJECTED none this cycle — all hypotheses target in-scope HIGH-VALUE classes with concrete verify steps
[LEARN] ACCEPTED MISCONFIG @ dev.derdack.com: dev environments frequently expose debug interfaces; passive probe cost near-zero
[RISK] derdack: 45 — surface unprobed; top asset (SIGNL4 SaaS) high business value but auth unknown; dev host likely highest immediate yield; no code-level intel yet
## 2026-09-03 19:04:55 UTC [target] (model nemotron3)
[NEW] dev.derdack.com /.well-known/openid-configuration returns 300 Multiple Choices with directory traversal suggestions (/.ssh/, /.bash_history/, /.viminfo/) — misconfiguration confirmed
[NEW] signl4.derdack.com (AWS 13.94.244.66) connection timeout on HTTP/HTTPS — SaaS platform unreachable, likely firewall/WAF
[NEW] signals.derdack.com NXDOMAIN — subdomain does not exist, hypothesis invalid
[NEW] blog.derdack.com & techblog.derdack.com redirect via HTTP (not HTTPS) to www.derdack.com — mixed content / downgrade risk
[NEW] de.derdack.com / www.de.derdack.com return 403 with sedoparking.com iframe — parked domain, not Derdack infrastructure
[CHANGED] Inventory validation: only 5/9 hosts are live Derdack infrastructure; 2 unreachable, 1 non-existent, 1 parked
[PRIO] dev.derdack.com,7.8,a=8 b=6 t=9 g=9 c=6 f=5
[PRIO] www.derdack.com,6.5,a=7 b=8 t=5 g=5 c=7 f=5
[PRIO] signl4.derdack.com,5.2,a=6 b=10 t=3 g=2 c=8 f=4
[PRIO] derdack.com,5.0,a=6 b=8 t=4 g=5 c=6 f=4
[PRIO] blog.derdack.com,3.8,a=4 b=4 t=4 g=4 c=3 f=4
[PRIO] techblog.derdack.com,3.8,a=4 b=4 t=4 g=4 c=3 f=4
[HYP] dev.derdack.com openid-configuration path traversal via 300 Multiple Choices
class: MISCONFIG
asset: dev.derdack.com
confidence: 75
reasoning: 300 response for /.well-known/openid-configuration lists sensitive paths (/.ssh/, /.bash_history/, /.viminfo/) as "similar documents" — indicates misconfigured Apache mod_negotiation or MultiViews exposing hidden files
evidence_needed: Direct access to /.ssh/id_rsa, /.bash_history, /.viminfo returns 200 with content
verify_steps: GET https://dev.derdack.com/.ssh/id_rsa; GET https://dev.derdack.com/.bash_history; GET https://dev.derdack.com/.viminfo; GET https://dev.derdack.com/.well-known/ (directory listing)
impact: Source code leakage, SSH private keys, command history, credential exposure — critical if dev host has access to internal systems
testability: PASSIVE
[HYP] www.derdack.com WordPress Contact Form 7 / wp-json REST API user enumeration
class: AUTH
asset: www.derdack.com
confidence: 55
reasoning: WordPress with Contact Form 7 (wpcf7), wp-json API exposed, REST API user endpoints often enabled; user enumeration via /wp-json/wp/v2/users allows reconnaissance for password spray (out of scope) but also IDOR on draft posts/PII
evidence_needed: 200 OK on /wp-json/wp/v2/users with user list; /wp-json/wp/v2/posts?status=draft accessible
verify_steps: GET https://www.derdack.com/wp-json/wp/v2/users; GET https://www.derdack.com/wp-json/wp/v2/posts?status=draft; GET https://www.derdack.com/wp-json/wp/v2/pages?status=draft
impact: PII exposure (author names, emails), draft content leakage, reconnaissance for targeted attacks
testability: PASSIVE
[HYP] signl4.derdack.com API authentication bypass via unauthenticated endpoints
class: AUTH
asset: signl4.derdack.com
confidence: 40
reasoning: SIGNL4 is primary SaaS product (high business value) hosted on AWS; connection timeout suggests restrictive SG/WAF but API may exist on alternate subdomain/path; no live probe data yet
evidence_needed: Live HTTP response from any signl4.derdack.com endpoint; API documentation / Swagger; authentication flow discovery
verify_steps: GET https://signl4.derdack.com/ (retry with longer timeout); GET https://api.signl4.derdack.com/; GET https://app.signl4.derdack.com/; check CT logs for api.* signl4 subdomains
impact: Full SaaS platform compromise — alerting config, on-call schedules, PII, integrations
testability: AUTH_HELPED
[PARKED] signl4.derdack.com API authentication bypass via unauthenticated endpoints: confidence<60, host unreachable, no live verification possible without network access
[FINAL] dev.derdack.com openid-configuration path traversal via 300 Multiple Choices — ranked #1 (confidence 75, passive verify, critical impact)
[FINAL] www.derdack.com WordPress REST API user enumeration & draft leakage — ranked #2 (confidence 55, passive verify, medium impact)
[NEXT] PROBE: GET https://dev.derdack.com/.ssh/id_rsa && GET https://dev.derdack.com/.bash_history && GET https://dev.derdack.com/.viminfo && GET https://dev.derdack.com/.well-known/
[LEARN] ACCEPTED MISCONFIG @ dev.derdack.com: 300 Multiple Choices with sensitive path suggestions confirms Apache mod_negotiation/MultiViews misconfiguration; passive probe cost near-zero
[LEARN] REJECTED SSRF @ signals.derdack.com: subdomain NXDOMAIN — does not exist
[LEARN] REJECTED MISCONFIG @ dev.derdack.com actuator/swagger/graphql: all 404 — no Spring Boot, Swagger, GraphQL exposed
[LEARN] ACCEPTED AUTH @ www.derdack.com: WordPress REST API exposed (wp-json), Contact Form 7, user enumeration vector confirmed in-scope
[LEARN] REJECTED brute-force @ all: program explicitly excludes rate-limit/lockout testing
[RISK] derdack: 55 — dev.derdack.com misconfiguration high immediate yield (path traversal to sensitive files); www.derdack.com WordPress REST API medium risk; signl4.derdack.com SaaS high value but unreachable; 4/9 inventory hosts not Derdack infrastructure (parked/NXDOMAIN/unreachable)
