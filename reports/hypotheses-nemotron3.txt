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
