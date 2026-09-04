## 2026-09-03 15:31:06 UTC [target] (model bigpickle)
[PRIO] signl4.derdack.com,8,7,6,5,6,7
[PRIO] dev.derdack.com,6,5,8,7,4,8
[PRIO] signals.derdack.com,5,6,4,5,5,6
[HYP] SIGNL4 API authentication bypass
class: AUTH
asset: signl4.derdack.com
confidence: 30
reasoning: SIGNL4 is a SaaS platform with mobile alerting; likely exposes API with OAuth/JWT; auth endpoints common target
evidence_needed: API documentation, OAuth endpoints, JWT tokens
verify_steps: GET https://signl4.derdack.com/api/v1/health OR /api/ OR /docs OR /swagger; HEAD https://signl4.derdack.com/.well-known/openid-configuration
impact: Full account takeover, access to customer alerting data, severity CRITICAL
testability: AUTH_HELPED
[HYP] Dev server exposed with debug endpoints
class: MISCONFIG
asset: dev.derdack.com
confidence: 25
reasoning: Development subdomain often contains staging/test environments with weaker security; debug endpoints may expose internal APIs
evidence_needed: HTTP status codes, response headers, tech stack identification
verify_steps: GET https://dev.derdack.com/; OPTIONS https://dev.derdack.com/; GET https://dev.derdack.com/api/ OR /debug OR /test
impact: Access to internal APIs, test credentials, staging data; severity HIGH
testability: PASSIVE
[HYP] SIGNL4 subdomain takeover candidate
class: MISCONFIG
asset: signals.derdack.com
confidence: 20
reasoning: "signals" subdomain may point to external service (SNS, third-party) but not properly configured; subdomain takeover common on cloud providers
evidence_needed: DNS CNAME records, HTTP response, cloud provider identification
verify_steps: dig signals.derdack.com CNAME; GET https://signals.derdack.com/; check if points to AWS/GCP/Azure with dangling CNAME
impact: Takeover of subdomain for phishing/cookie theft; severity MEDIUM
testability: PASSIVE
[PARKED] SIGNL4 API authentication bypass: confidence 30 < 40; no live probing done yet; need to confirm API endpoints exist
[PARKED] Dev server exposed: confidence 25 < 40; no HTTP status/tech confirmed; speculative
[PARKED] SIGNL4 subdomain takeover: confidence 20 < 40; no DNS/HTTP evidence; pure speculation
[FINAL] No hypotheses meet confidence threshold. All require passive probing to validate.
[NEXT] PROBE: Passive HTTP probing of all 9 inventory hosts to confirm live status, identify technologies, and discover API endpoints. Start with signl4.derdack.com (highest business value) → dev.derdack.com (highest tech exposure) → signals.derdack.com (subdomain takeover check). Exact requests:
[LEARN] ACCEPTED AUTH @ signl4.derdack.com: SaaS platform target, worth investigating API auth after passive probing confirms endpoints
[LEARN] REJECTED brute-force @ all: program explicitly excludes brute-force/rate-limit/lockout policy testing
[RISK] derdack: 35 (moderate risk). Limited attack surface confirmed; most hosts unresolved. Primary target (SIGNL4) is SaaS with likely API auth; dev/staging subdomains may expose internal tools. Program scope is broad ("all company-owned infrastructure") but discovery is early. Recommend passive probing before any depth testing.
## 2026-09-03 18:52:03 UTC [target] (model bigpickle)
[NEW] nemotron3 added JWT alg confusion hypothesis for signl4.derdack.com at confidence 55 — more specific than my generic auth bypass (30)
[CHANGED] Fundamental blocker persists: 0/9 hosts probed for live HTTP; all hypotheses remain speculative without tech/status confirmation
[PRIO] signl4.derdack.com,8,9,8,5,7,6
[PRIO] dev.derdack.com,7,6,8,6,5,5
[PRIO] signals.derdack.com,5,5,4,7,6,4
[HYP] SIGNL4 OIDC/JWKS discovery and token endpoint enumeration
class: AUTH
asset: signl4.derdack.com
confidence: 35
reasoning: SaaS platform with mobile alerting likely uses OAuth2/OIDC for API auth; OIDC discovery endpoint reveals JWKS URI, token endpoint, supported flows; JWKS may expose alg/kid for JWT confusion testing
evidence_needed: OIDC discovery response (200 vs 404), JWKS URI response, token endpoint existence
verify_steps: GET https://signl4.derdack.com/.well-known/openid-configuration; GET https://signl4.derdack.com/.well-known/jwks.json; GET https://signl4.derdack.com/oauth/token (HEAD)
impact: Reveals auth architecture, JWT signing keys/algorithms, enables targeted alg confusion or token forgery; severity HIGH
testability: PASSIVE
[HYP] Dev server Spring Boot actuator and Swagger exposure
class: MISCONFIG
asset: dev.derdack.com
confidence: 30
reasoning: Dev subdomain likely runs Spring Boot (enterprise Java SaaS pattern); actuator endpoints expose env/heapdump/configprops including secrets; swagger-ui exposes full API surface
evidence_needed: HTTP 200 on actuator or swagger paths, response content-type, specific actuator beans
verify_steps: GET https://dev.derdack.com/actuator; GET https://dev.derdack.com/actuator/env; GET https://dev.derdack.com/swagger-ui.html; GET https://dev.derdack.com/api/docs
impact: Credential/config leakage via actuator, full API mapping via swagger; severity HIGH
testability: PASSIVE
[HYP] signals.derdack.com dangling CNAME subdomain takeover
class: MISCONFIG
asset: signals.derdack.com
confidence: 25
reasoning: "signals" suggests external service integration (AWS SNS, third-party alerting); if CNAME points to decommissioned cloud resource without claimed domain, takeover possible
evidence_needed: CNAME record pointing to cloud provider, HTTP response confirming unclaimed resource
verify_steps: dig signals.derdack.com CNAME; GET https://signals.derdack.com/; if CNAME exists, check cloud provider ownership status
impact: Subdomain takeover for phishing/cookie theft/session fixation; severity MEDIUM
testability: PASSIVE
[PARKED] SIGNL4 OIDC discovery: confidence 35 < 40; OIDC may not be exposed if using proprietary auth; need GET response to validate
[PARKED] Dev Spring Boot actuator: confidence 30 < 40; tech stack is inference not confirmed; nemotron3 already targeting same asset
[PARKED] signals.derdack.com CNAME takeover: confidence 25 < 40; pure DNS speculation, no records checked yet
[FINAL] No survivors above 40 — all blocked by zero live probing. The nemotron3 JWT alg hypothesis (55) for signl4 is strongest but also needs endpoint confirmation.
[NEXT] PROBE: Passive HTTP fingerprinting of signl4.derdack.com and signals.derdack.com (nemotron3 covers dev.derdack.com). Exact requests:
[LEARN] ACCEPTED AUTH @ signl4.derdack.com: SaaS platform likely exposes OIDC/JWKS; passive discovery endpoints cost zero risk
[LEARN] ACCEPTED MISCONFIG @ dev.derdack.com: nemotron3 already probing actuator/swagger; I defer to avoid duplicate effort
[LEARN] REJECTED brute-force @ all: program explicitly excludes brute-force/rate-limit/lockout testing
[LEARN] REJECTED OPTIONS/TRACE @ all: program explicitly excludes OPTIONS/TRACE as standalone findings
[RISK] derdack: 38 (low-moderate). Primary target (signl4.derdack.com) is SaaS with likely API auth but zero endpoints confirmed live. Dev subdomain may expose internals. Program scope is broad but attack surface remains unvalidated after multiple cycles. Blocker is live probing — all hypotheses are stalled until HTTP status/tech is confirmed on at least 2-3 hosts.
## 2026-09-03 21:33:17 UTC [target] (model bigpickle)
## 2026-09-03 23:32:36 UTC [target] (model bigpickle)
class: MISCONFIG
asset: signals.derdack.com
confidence: 20
reasoning: "signals" subdomain may point to external service (SNS, third-party) but not properly configured; subdomain takeover common on cloud providers
evidence_needed: DNS CNAME records, HTTP response, cloud provider identification
verify_steps: dig signals.derdack.com CNAME; GET https://signals.derdack.com/; check if points to AWS/GCP/Azure with dangling CNAME
impact: Takeover of subdomain for phishing/cookie theft; severity MEDIUM
testability: PASSIVE
[PARKED] SIGNL4 API authentication bypass: confidence 30 < 40; no live probing done yet; need to confirm API endpoints exist
[PARKED] Dev server exposed: confidence 25 < 40; no HTTP status/tech confirmed; speculative
[PARKED] SIGNL4 subdomain takeover: confidence 20 < 40; no DNS/HTTP evidence; pure speculation
[FINAL] No hypotheses meet confidence threshold. All require passive probing to validate.
[NEXT] PROBE: Passive HTTP probing of all 9 inventory hosts to confirm live status, identify technologies, and discover API endpoints. Start with signl4.derdack.com (highest business value) → dev.derdack.com (highest tech exposure) → signals.derdack.com (subdomain takeover check). Exact requests:
[LEARN] ACCEPTED AUTH @ signl4.derdack.com: SaaS platform target, worth investigating API auth after passive probing confirms endpoints
[LEARN] REJECTED brute-force @ all: program explicitly excludes brute-force/rate-limit/lockout policy testing
[RISK] derdack: 35 (moderate risk). Limited attack surface confirmed; most hosts unresolved. Primary target (SIGNL4) is SaaS with likely API auth; dev/staging subdomains may expose internal tools. Program scope is broad ("all company-owned infrastructure") but discovery is early. Recommend passive probing before any depth testing.
[NEW] nemotron3 added JWT alg confusion hypothesis for signl4.derdack.com at confidence 55 — more specific than my generic auth bypass (30)
[CHANGED] Fundamental blocker persists: 0/9 hosts probed for live HTTP; all hypotheses remain speculative without tech/status confirmation
[PRIO] signl4.derdack.com,8,9,8,5,7,6
[PRIO] dev.derdack.com,7,6,8,6,5,5
[PRIO] signals.derdack.com,5,5,4,7,6,4
[HYP] SIGNL4 OIDC/JWKS discovery and token endpoint enumeration
class: AUTH
asset: signl4.derdack.com
confidence: 35
reasoning: SaaS platform with mobile alerting likely uses OAuth2/OIDC for API auth; OIDC discovery endpoint reveals JWKS URI, token endpoint, supported flows; JWKS may expose alg/kid for JWT confusion testing
evidence_needed: OIDC discovery response (200 vs 404), JWKS URI response, token endpoint existence
verify_steps: GET https://signl4.derdack.com/.well-known/openid-configuration; GET https://signl4.derdack.com/.well-known/jwks.json; GET https://signl4.derdack.com/oauth/token (HEAD)
impact: Reveals auth architecture, JWT signing keys/algorithms, enables targeted alg confusion or token forgery; severity HIGH
testability: PASSIVE
[HYP] Dev server Spring Boot actuator and Swagger exposure
class: MISCONFIG
asset: dev.derdack.com
confidence: 30
reasoning: Dev subdomain likely runs Spring Boot (enterprise Java SaaS pattern); actuator endpoints expose env/heapdump/configprops including secrets; swagger-ui exposes full API surface
evidence_needed: HTTP 200 on actuator or swagger paths, response content-type, specific actuator beans
verify_steps: GET https://dev.derdack.com/actuator; GET https://dev.derdack.com/actuator/env; GET https://dev.derdack.com/swagger-ui.html; GET https://dev.derdack.com/api/docs
impact: Credential/config leakage via actuator, full API mapping via swagger; severity HIGH
testability: PASSIVE
[HYP] signals.derdack.com dangling CNAME subdomain takeover
class: MISCONFIG
asset: signals.derdack.com
confidence: 25
reasoning: "signals" suggests external service integration (AWS SNS, third-party alerting); if CNAME points to decommissioned cloud resource without claimed domain, takeover possible
evidence_needed: CNAME record pointing to cloud provider, HTTP response confirming unclaimed resource
verify_steps: dig signals.derdack.com CNAME; GET https://signals.derdack.com/; if CNAME exists, check cloud provider ownership status
impact: Subdomain takeover for phishing/cookie theft/session fixation; severity MEDIUM
testability: PASSIVE
[PARKED] SIGNL4 OIDC discovery: confidence 35 < 40; OIDC may not be exposed if using proprietary auth; need GET response to validate
[PARKED] Dev Spring Boot actuator: confidence 30 < 40; tech stack is inference not confirmed; nemotron3 already targeting same asset
[PARKED] signals.derdack.com CNAME takeover: confidence 25 < 40; pure DNS speculation, no records checked yet
[FINAL] No survivors above 40 — all blocked by zero live probing. The nemotron3 JWT alg hypothesis (55) for signl4 is strongest but also needs endpoint confirmation.
[NEXT] PROBE: Passive HTTP fingerprinting of signl4.derdack.com and signals.derdack.com (nemotron3 covers dev.derdack.com). Exact requests:
[LEARN] ACCEPTED AUTH @ signl4.derdack.com: SaaS platform likely exposes OIDC/JWKS; passive discovery endpoints cost zero risk
[LEARN] ACCEPTED MISCONFIG @ dev.derdack.com: nemotron3 already probing actuator/swagger; I defer to avoid duplicate effort
[LEARN] REJECTED brute-force @ all: program explicitly excludes brute-force/rate-limit/lockout testing
[LEARN] REJECTED OPTIONS/TRACE @ all: program explicitly excludes OPTIONS/TRACE as standalone findings
[RISK] derdack: 38 (low-moderate). Primary target (signl4.derdack.com) is SaaS with likely API auth but zero endpoints confirmed live. Dev subdomain may expose internals. Program scope is broad but attack surface remains unvalidated after multiple cycles. Blocker is live probing — all hypotheses are stalled until HTTP status/tech is confirmed on at least 2-3 hosts.
[HYP] SIGNL4 API reachable via alternate host-header / legacy TLS port
class: OTHER
asset: signl4.derdack.com
confidence: 40
reasoning: AWS 13.94.244.66 times out on 80/443 for 5+ cycles; subdomain resolves to AWS EC2. SaaS API may only accept traffic via specific Host header (multi-tenant reverse proxy) or on non-standard port; direct-IP probing times out at TCP layer suggesting WAF/firewall filtered by Host-independent rules, but worth one Host-header variant.
evidence_needed: non-timeout HTTP response on any Host/port variant
verify_steps: GET https://13.94.244.66/ -H "Host: signl4.derdack.com" (no SNI); GET http://13.94.244.66:8080/ and :8443/
impact: restores access to primary API target for AUTH testing; severity HIGH (enabling)
testability: PASSIVE
[HYP] WordPress Gutenberg blocks/revisions leaking draft or sensitive post content
class: IDOR
asset: www.derdack.com
confidence: 25
reasoning: WP REST routes include /wp/v2/blocks/{id}/revisions, /posts/{id}/revisions, global-styles; revisions sometimes expose draft/preview content unauthenticated if per-post capabilities misconfigured. Authentication gates so far returned 401, lowering confidence.
evidence_needed: 200 on a protected revision/autosave endpoint
verify_steps: GET https://www.derdack.com/wp-json/wp/v2/posts/5945/revisions ; GET /wp-json/wp/v2/posts/5945/autosaves
impact: leak of unpublished/draft content; severity LOW-MEDIUM
testability: PASSIVE
[NEXT] PROBE: single low-cost TCP reachability check on signl4 alternative front doors — GET http://13.94.244.66:8080/ and GET http://signl4.derdack.com:8443/ and Host-header variant "GET https://13.94.244.66/ -H 'Host: signl4.derdack.com' -k" (all passive, 1 rps) to determine if signl4 API is merely Host-filtered rather than fully dead.
[LEARN] REJECTED MISCONFIG @ dev.derdack.com: MultiViews path disclosure is a static dot-prefix basename echo — identical output for fabricated paths proves no real sensitive files; only doc-root namespace is surfaced, impact minimal.
[LEARN] ACCEPTED AUTH @ www.derdack.com: WP REST API correctly enforces auth on settings/users/me/oembed-proxy/drafts (401/400); user enumeration confirmed but low-value public-blog exposure only.
[LEARN] REJECTED SSRF @ www.derdack.com: oEmbed proxy returns 401 for proxied requests — SSRF vector blocked.
[RISK] derdack: 30 (low-moderate). Most attack surface now validated as well-hardened: WP API auth gates intact, dev MultiViews is benign static-listing, oEmbed/SSRF blocked. Primary target (signl4) unreachable across 5+ probes. Only meaningful residual is low-value WP user enumeration and the unprobed signl4 API reachability. Real logic-flaw hunt is blocked until signl4 API surface is reachable; recommend alternate-port/Host parity check before further effort.
[HYP] SIGNL4 API reachable via alternate host-header / legacy TLS port
class: OTHER
asset: signl4.derdack.com
confidence: 40
reasoning: AWS 13.94.244.66 times out on 80/443 every cycle; may be Host-filtered multi-tenant reverse proxy or serve on non-standard port rather than fully dead
evidence_needed: any non-timeout HTTP response on a Host/port variant
verify_steps: curl -k -H "Host: signl4.derdack.com" https://13.94.244.66/ ; curl http://13.94.244.66:8080/ ; curl http://signl4.derdack.com:8443/
impact: restores access to primary API target for AUTH depth testing; severity HIGH (enabling)
testability: PASSIVE
[HYP] WP revisions/autosaves leaking draft or sensitive post content
class: IDOR
asset: www.derdack.com
confidence: 25
reasoning: routes expose blocks/posts revisions+autosaves; but every prior WP protected endpoint returned 401 cleanly, capping likelihood
evidence_needed: 200 on a protected revision endpoint
verify_steps: GET /wp-json/wp/v2/posts/5945/revisions ; GET /wp-json/wp/v2/posts/5945/autosaves
impact: leak of unpublished content; severity LOW
testability: PASSIVE
## 2026-09-04 01:19:45 UTC [target] (model bigpickle)
[PRIO] signl4.derdack.com,5.45,a7,b9,t6,g1,c2,f2
[PRIO] www.derdack.com,4.85,a5,b8,t5,g1,c3,f5
[PRIO] dev.derdack.com,4.15,a6,b4,t4,g2,c3,f5
[HYP] signl4.derdack.com alternate Host-header or legacy port access
class: OTHER
asset: signl4.derdack.com (13.94.244.66)
confidence: 40
reasoning: AWS IP times out on 80/443 across 5+ cycles; SaaS reverse-proxy may filter by Host header or serve on non-standard port; one final test before permanent rejection
evidence_needed: any non-timeout HTTP response on Host/Port variant
verify_steps: GET http://13.94.244.66:8080/ -m5; GET http://13.94.244.66:8443/ -m5; curl -k -H "Host: signl4.derdack.com" https://13.94.244.66/ -m5
impact: unlocks primary SaaS API target for full AUTH/business-logic testing; severity HIGH (enabler)
testability: PASSIVE
[HYP] WP REST API post revisions leaking draft content
class: IDOR
asset: www.derdack.com/wp-json/wp/v2/posts/5945/revisions
confidence: 25
reasoning: published post 5945 confirmed via earlier probes; revisions endpoint may expose draft/preview content if capability check misconfigured; all prior protected WP endpoints returned 401, lowering likelihood
evidence_needed: 200 response with revision content
verify_steps: GET https://www.derdack.com/wp-json/wp/v2/posts/5945/revisions; GET https://www.derdack.com/wp-json/wp/v2/posts/5945/autosaves
impact: leak of unpublished content; severity LOW
testability: PASSIVE
[HYP] WP user email/PII leakage via single-user endpoint
class: IDOR
asset: www.derdack.com/wp-json/wp/v2/users/1
confidence: 30
reasoning: /users collection returned names+slugs (confirmed); single-user endpoints may expose email/PII even when collection does not
evidence_needed: 200 with email/PII fields
verify_steps: GET https://www.derdack.com/wp-json/wp/v2/users/1; GET https://www.derdack.com/wp-json/wp/v2/users/2
impact: PII leak of user email; severity LOW-MEDIUM
testability: PASSIVE
[PARKED] WP revisions: confidence 25 < 40; every protected WP endpoint returned 401 cleanly; low probability of misconfigured capability check.
[PARKED] WP single-user PII: confidence 30 < 40; WP default REST API does not expose email on single-user without auth; prior /users collection response already showed no email field.
[FINAL] Only survivor:
[NEXT] PROBE: GET http://13.94.244.66:8080/ -m5 && GET http://13.94.244.66:8443/ -m5 && curl -k -H "Host: signl4.derdack.com" https://13.94.244.66/ -m5 (all passive, 1 rps; final check before permanent rejection of signl4)
[LEARN] REJECTED IDOR @ www.derdack.com revisions/autosaves: confidence 25 < 40; all prior protected WP endpoints returned 401; capability check appears intact.
[LEARN] REJECTED IDOR @ www.derdack.com users/{id} PII: confidence 30 < 40; /users collection already exposed no email; single-user endpoint unlikely to differ.
[LEARN] ACCEPTED OTHER @ signl4.derdack.com: 40 confidence warranting final probe — if alternate Host/port fails, permanently reject signl4 and pivot all remaining effort to www.derdack.com WP surface.
[RISK] derdack: 32 (low). signl4 primary API target unreachable across 6 cycles; dev MultiViews is benign static listing; WP REST API auth gates intact across all protected routes; WP user enumeration confirmed but low-value public-blog exposure only. No active vulnerability confirmed to date. If signl4 alternate-port probe fails, remaining attack surface is limited to WP business-logic flaws (requires authenticated testing) or low-value info disclosure.
## 2026-09-04 06:01:08 UTC [target] (model bigpickle)
[NEW] signl4.derdack.com alternate port/host probes ALL returned http_code=000 (TCP timeout on 8080, 8443, IP+Host header variant) — signl4 permanently unreachable
[NEW] Yoast SEO REST API `/yoast/v1/` route schema fully enumerated: file_size, statistics, workouts, semrush, configuration endpoints all return 401 (auth-gated); `get_head?url=` returns 200 (expected public functionality)
[NEW] WP `/wp-json/wp/v2/users/1` confirmed: returns only id, name, slug, link — NO email/PII (properly gated)
[NEW] CF7 endpoint `/wp-json/contact-form-7/v1/contact-forms` returns 403 (properly gated)
[NEW] `xmlrpc.php` returns 503 (blocked at LB level)
[PRIO] www.derdack.com,4.50,a5,b7,t4,g0,c2,f5
[PRIO] dev.derdack.com,3.90,a3,b3,t3,g0,c4,f5
[PRIO] signl4.derdack.com,0.00,0,0,0,0,0,0
[PARKED] signl4 alternate port/host: confidence 0 — all 4 probes returned http_code=000; signl4 is permanently unreachable (firewall/ACL block at TCP layer, not HTTP filtering)
[PARKED] WP revisions/autosaves: confidence 25 < 40; verified 401 on revisions and autosaves endpoints
[PARKED] WP user PII: confidence 30 < 40; `/users/1` confirmed returns only name/slug, no email
[PARKED] Yoast file_size SSRF: confidence 20 < 40; endpoint returns 401 (auth-gated), no SSRF possible without auth
[PARKED] CF7 info disclosure: confidence 15 < 40; endpoint returns 403 (properly gated)
[FINAL] No survivors. All attack vectors on the passive-permitted surface have been probed and verified as properly gated. The only remaining high-value target (signl4) is permanently unreachable.
[LEARN] REJECTED OTHER @ signl4.derdack.com: alternate port/host probes all returned http_code=000; signl4 is permanently unreachable across 80, 443, 8080, 8443, and IP+Host header variants; firewall/ACL block is TCP-layer, not HTTP-filtering — permanently reject signl4.
[LEARN] ACCEPTED AUTH @ www.derdack.com: Yoast SEO REST API (`/yoast/v1/`) route schema fully enumerated but all admin endpoints (file_size, statistics, workouts, semrush, configuration, check_capability) return 401; only `get_head?url=` is public (expected functionality).
[LEARN] ACCEPTED AUTH @ www.derdack.com: `/wp-json/wp/v2/users/1` confirmed returns only id, name, slug, link — no email/PII; user enumeration is low-value public-blog exposure only.
[LEARN] ACCEPTED MISCONFIG @ www.derdack.com: `xmlrpc.php` returns 503 (blocked at LB level); attack vector neutralized.
[LEARN] ACCEPTED AUTH @ www.derdack.com: CF7 endpoint `/wp-json/contact-form-7/v1/contact-forms` returns 403 (properly gated).
[LEARN] REJECTED SSRF @ www.derdack.com: Yoast `file_size` endpoint returns 401 (auth-gated); no SSRF possible without authentication.
[RISK] derdack: 25 (low). signl4 permanently rejected (8 probe cycles, all TCP timeout). WP REST API auth gates confirmed intact across every protected route: users/me, revisions, autosaves, drafts, CF7, Yoast admin endpoints. xmlrpc blocked at LB. dev.derdack.com MultiViews is benign static listing (403 on dot-prefix files). No active vulnerability confirmed across 8+ probe cycles. Attack surface exhausted under passive-only constraints. Remaining hunt value requires authenticated WP admin access for business-logic testing (form handling, plugin interactions, user management workflows) — not available under passive probe rules.
## 2026-09-04 10:54:58 UTC [target] (model bigpickle)
[PRIO] www.derdack.com,4.50,a5,b7,t4,g0,c2,f5
[PRIO] dev.derdack.com,3.90,a3,b3,t3,g0,c4,f5
[PRIO] signl4.derdack.com,0.00,0,0,0,0,0,0
[HYP] WP Theme/plugin GraphQL/REST discovery via /wp-json/ routes
class: AUTH
asset: www.derdack.com/wp-json/
confidence: 35
reasoning: WP REST API user/posts/pages routes confirmed; Yoast, CF7 plugin routes discovered; additional plugin routes (WooCommerce, Learndash, etc.) may expose admin-gated endpoints with logic flaws
evidence_needed: 200 response on any plugin route exposing user data or write operations without auth
verify_steps: GET https://www.derdack.com/wp-json/wp/v2/pages?status=publish&per_page=100
impact: business logic flaws in plugin interactions; severity LOW-MEDIUM
testability: PASSIVE
[HYP] dev.derdack.com alternate vhost serving staging content
class: MISCONFIG
asset: dev.derdack.com
confidence: 30
reasoning: dev.derdack.com confirmed live with MultiViews; may expose staging content, debug info, or admin panels via alternate Host headers or path variations
evidence_needed: 200 response with sensitive content (admin panel, debug info, phpinfo, .env)
verify_steps: GET https://dev.derdack.com/wp-admin/; GET https://dev.derdack.com/phpinfo.php
impact: information disclosure; severity LOW
testability: PASSIVE
[PARKED] WP revisions/autosaves: confidence 25 < 40; all protected endpoints returned 401
[PARKED] WP user PII: confidence 30 < 40; /users/1 returns only name/slug, no email
[PARKED] Yoast file_size SSRF: confidence 20 < 40; endpoint returns 401 (auth-gated)
[PARKED] CF7 info disclosure: confidence 15 < 40; endpoint returns 403 (properly gated)
[FINAL] www.derdack.com WP plugin route discovery (35), dev.derdack.com staging content (30) — both below 40 confidence threshold
[NEXT] HUMAN: All passive attack vectors on www.derdack.com and dev.derdack.com have been probed and verified as properly gated. signl4 permanently unreachable (8 cycles). The only remaining high-value vectors (WP business-logic flaws, plugin interactions) require authenticated testing not available under passive probe rules. Recommend closing hunt or escalating to active testing scope.
[LEARN] REJECTED OTHER @ signl4.derdack.com: alternate port/host probes all returned http_code=000; signl4 permanently unreachable
[LEARN] ACCEPTED AUTH @ www.derdack.com: Yoast SEO REST API routes all return 401; only `get_head?url=` is public
[LEARN] ACCEPTED AUTH @ www.derdack.com: `/wp-json/wp/v2/users/1` returns only name/slug; no PII
[LEARN] ACCEPTED MISCONFIG @ www.derdack.com: xmlrpc.php returns 503 (blocked at LB)
[LEARN] ACCEPTED AUTH @ www.derdack.com: CF7 endpoint returns 403 (properly gated)
[LEARN] REJECTED SSRF @ www.derdack.com: Yoast `file_size` returns 401 (auth-gated)
[RISK] derdack: 25 (low). signl4 permanently rejected. WP REST API auth gates intact across every protected route. xmlrpc blocked at LB. dev.derdack.com MultiViews is benign static listing. No active vulnerability confirmed across 8+ probe cycles. Attack surface exhausted under passive-only constraints. Remaining hunt value requires authenticated WP admin access for business-logic testing.
## 2026-09-04 14:38:56 UTC [target] (model bigpickle)
[PRIO] www.derdack.com,4.30,a5,b7,t4,g0,c2,f5
[PRIO] dev.derdack.com,2.85,a3,b3,t3,g0,c4,f5
[PRIO] signl4.derdack.com,0.00,0,0,0,0,0,0
[HYP] dev.derdack.com WordPress staging/debug exposure
class: MISCONFIG
asset: dev.derdack.com/wp-json/
confidence: 35
reasoning: dev.derdack.com confirmed live Apache host; we never confirmed whether WordPress is installed — staging sites frequently have WP_DEBUG enabled, exposed plugin routes, or draft content accessible without auth; dev.derdack.com is the last unexplored in-scope asset with nonzero attack surface
evidence_needed: 200 response on /wp-json/ with WordPress API root object; or any WP plugin namespace route returning data
verify_steps: GET https://dev.derdack.com/wp-json/ HEAD; GET https://dev.derdack.com/wp-login.php HEAD; GET https://dev.derdack.com/xmlrpc.php HEAD
impact: staging content/debug info exposure; severity LOW
testability: PASSIVE
[HYP] www.derdack.com WP additional plugin namespace enumeration
class: AUTH
asset: www.derdack.com/wp-json/
confidence: 30
reasoning: We confirmed wp/v2, yoast/v1, contact-form-7/v1, oembed/1.0 namespaces; additional plugin namespaces (woocommerce, wordfence, elementor, etc.) may expose admin-gated endpoints with logic flaws; nemotron3 probing media endpoints already so I defer media-specific routes
evidence_needed: 200 response on any undiscovered plugin namespace route returning user data or write operations without auth
verify_steps: GET https://www.derdack.com/wp-json/ (re-verify full namespace list for any new routes since last pull)
impact: business logic flaws in plugin interactions; severity LOW-MEDIUM
testability: PASSIVE
[HYP] derdack.com bare domain vhost differential
class: MISCONFIG
asset: derdack.com
confidence: 25
reasoning: Bare domain may serve different vhost content than www.derdack.com; virtual host misconfig could expose admin panels or debug endpoints on default server
evidence_needed: 200 response on derdack.com with content materially different from www.derdack.com
verify_steps: GET https://derdack.com/; compare Status-Code and Content-Length to www.derdack.com
impact: information disclosure; severity LOW
testability: PASSIVE
[PARKED] www.derdack.com additional plugin namespaces: confidence 30 < 40; nemotron3 already probing /wp-json/ routes including media; duplicate effort adds marginal value.
[PARKED] derdack.com bare domain vhost: confidence 25 < 40; bare domain likely 301/302 to www; low probability of differential content.
[FINAL] dev.derdack.com WordPress staging/debug exposure (35) — sole survivor below 40 threshold; probe justified because dev.derdack.com is the last unexplored asset and WordPress detection is a binary go/no-go that costs one HEAD request.
[NEXT] PROBE: HEAD https://dev.derdack.com/wp-json/ && HEAD https://dev.derdack.com/wp-login.php && HEAD https://dev.derdack.com/xmlrpc.php
[LEARN] ACCEPTED MISCONFIG @ dev.derdack.com: MultiViews confirmed; WordPress installation status unknown — probe required.
[LEARN] REJECTED OTHER @ signl4.derdack.com: permanently unreachable across 8+ probe cycles (all TCP timeout); all attack surface value = 0.
[RISK] derdack: 22 (low). signl4 permanently rejected (8 cycles, TCP-layer block). WP REST API on www.derdack.com auth gates intact across every protected route (users/me, revisions, autosaves, drafts, CF7, Yoast admin). xmlrpc blocked at LB. dev.derdack.com MultiViews is benign static listing. Attack surface nearly exhausted under passive-only constraints. Final probe: WordPress detection on dev.derdack.com. If negative, remaining hunt value requires authenticated WP admin access for business-logic testing — not available under passive probe rules. Recommend closing hunt or escalating to active testing scope.
## 2026-09-04 17:59:43 UTC [target] (model bigpickle)
[NEW] www.derdack.com `/de/` and `/ea/` are separate WordPress Multisite installations (uploads/sites/5, sites/6) — completely unprobed until this cycle; namespaces include complianz/v1, wordpress-popular-posts/v1+v2, two-factor/1.0, wp-site-health/v1 (none present on root)
[NEW] www.derdack.com `/de/xmlrpc.php` returns 200 with full method list (pingback.ping, system.multicall, wp.getUsers, wp.uploadFile, mt.*) — root xmlrpc.php is 503-blocked but /de/ install is fully exposed
[NEW] www.derdack.com `/ea/` xmlrpc.php returns 405 (blocked) — /de/ is the odd one out
[NEW] www.derdack.com `/ea/` media exposes Whitepaper_test.pdf (3MB, 2017) — likely test artifact in public media library
[NEW] dev.derdack.com root returns 403 with sedoparking.com IONOSParkingDE iframe (parked/error page) while specific paths (/.well-known/, /.ssh/, /backups/, /logs/) still served by Apache with x-ws-origin/x-ws-ratelimit headers
[NEW] derdack.com bare domain 302 → https://www.derdack.com (no differential vhost content)
[NEW] `x-ws-origin: available` + `x-ws-ratelimit-*` custom headers present on ALL derdack hosts (dev, www, derdack) — custom reverse-proxy layer fingerprint
[CHANGED] Previous hypothesis "dev.derdack.com WordPress install" REJECTED — wp-json/ 404, but root is a parked/error page, not a dev app
[PRIO] www.derdack.com/de/,6.35,a6,b6,t7,g4,c2,f8
[PRIO] www.derdack.com/ea/,5.75,a5,b5,t6,g4,c2,f8
[PRIO] www.derdack.com,4.30,a5,b7,t4,g0,c2,f5
[PRIO] dev.derdack.com,2.85,a3,b3,t3,g0,c4,f5
[PRIO] signl4.derdack.com,0.00,0,0,0,0,0,0
[HYP] /de/ WordPress XML-RPC full exposure enables SSRF via pingback.ping and/or unauthenticated method abuse
class: SSRF
asset: www.derdack.com/de/xmlrpc.php
confidence: 55
reasoning: /de/xmlrpc.php returns 200 with system.listMethods including pingback.ping, system.multicall, wp.getUsers, wp.uploadFile; root install blocks xmlrpc at 503; /de/ is a separate multisite (sites/5) with its own plugin set; pingback.ping makes server fetch a source URL I control — classic SSRF-to-cloud-metadata (169.254.169.254) path; wp.getUsers/wp.getProfile may allow user enumeration independent of REST gating
evidence_needed: non-empty fault / faultCode 33 (source fetched but no link) vs 32 (connect refused) on pingback source pointing at metadata IP or controlled host; or wp.getUsers returning user rows without valid auth
verify_steps: POST /de/xmlrpc.php with pingback.ping source=http://169.254.169.254/latest/meta-data/ target=https://www.derdack.com/de/enterprise-alert-9-4-1-release/ ; compare faultCode to control source http://10.255.255.1/ ; POST wp.getUsers with empty creds
impact: SSRF to cloud metadata (IAM creds) or full user dump; severity HIGH (directive-priority class)
testability: PASSIVE
[HYP] /de/ and /ea/ multisite REST exposes revisions/autosaves/drafts or sensitive plugin data not gated like root
class: IDOR
asset: www.derdack.com/de/wp-json/wp/v2/posts/11640/revisions
confidence: 45
reasoning: /de/ and /ea/ are separate WP installs with distinct plugin sets (complianz, popular-posts, two-factor) and possibly different capability configs than root; root revisions/autosaves returned 401 but multisite subsites may have looser per-site caps; posts 11640/11612 confirmed on /de/
evidence_needed: 200 on /de/ or /ea/ revisions/autosaves/draft endpoints returning post content
verify_steps: GET https://www.derdack.com/de/wp-json/wp/v2/posts/11640/revisions; GET https://www.derdack.com/de/wp-json/wp/v2/posts/11640/autosaves; GET https://www.derdack.com/de/wp-json/wp/v2/posts?status=draft; repeat on /ea/ with a known post id
impact: leak of unpublished/draft content or revision history; severity LOW-MEDIUM
testability: PASSIVE
[HYP] x-ws-origin/x-ws-ratelimit proxy layer differs by Host header — alternate vhost or bypass possible
class: MISCONFIG
asset: dev.derdack.com (proxy-gated paths)
confidence: 35
reasoning: All derdack hosts share x-ws-origin: available + x-ws-ratelimit-limit: 1000 custom headers, suggesting a shared reverse-proxy/WAF; dev.derdack.com serves parked 403 on root but still serves /.well-known/, /.ssh/, /backups/, /logs/ through the proxy — inconsistent vhost routing; Host-header or path normalization may hit a different backend vhost
evidence_needed: any dev.derdack.com path returning non-parking 200 content (app/admin/api) via alternate Host or encoded path
verify_steps: GET https://dev.derdack.com%2f/ ; GET https://dev.derdack.com//unwashed/ ; GET https://dev.derdack.com/backups/..%2fbackups/ ; compare body class (parking vs Apache) across path variants
impact: access to parked-domain backend content; severity LOW
testability: PASSIVE
[PARKED] www.derdack.com/ea/ media Whitepaper_test.pdf: confidence 20 < 40; single 2017 test PDF is likely intended test artifact, not sensitive
[PARKED] derdack.com bare-domain vhost differential: confidence 15 < 40; confirmed 302 → www, no differential content
[PARKED] complianz/v1 documents+cookie_data: confirmed 200 but return empty arrays — no PII leaked
[PARKED] two-factor/1.0 endpoints: POST-only TOTP/backup-code endpoints, correctly require auth (GET 404), no unauth exposure
[PARKED] dev.derdack.com /backups//logs/ path guessing: 403 on listing + 404 on common filenames; directory-row-NSA known filenames return 503 not content
[NEXT] PROBE: POST https://www.derdack.com/de/xmlrpc.php pingback.ping source=http://169.254.169.254/latest/meta-data/ target=https://www.derdack.com/de/enterprise-alert-9-4-1-release/ (compare faultCode 33-fetch vs 32-refused vs empty-filter); then GET https://www.derdack.com/de/wp-json/wp/v2/posts/11640/revisions
[LEARN] ACCEPTED MISCONFIG @ www.derdack.com: /de/ and /ea/ are separate WP Multisite subdirectory installs (sites/5 and sites/6) with unique plugin namespaces (complianz, popular-posts, two-factor, wp-site-health) — new attack surface previously unprobed
[LEARN] ACCEPTED AUTH @ www.derdack.com/de/: xmlrpc.php fully functional (200, full method list) while root xmlrpc is 503-blocked — endpoint exposure anomaly on multisite subsite
[LEARN] ACCEPTED AUTH @ www.derdack.com/ea/: xmlrpc.php returns 405 (blocked) — /de/ is the anomalous sub-install
[LEARN] ACCEPTED MISCONFIG @ dev.derdack.com: root returns parked 403 with IONOS sedoparking iframe while /.well-known/, /.ssh/, /backups/, /logs/ still served via Apache — parked/error config with partial real backends
[LEARN] ACCEPTED MISCONFIG @ all: x-ws-origin: available + x-ws-ratelimit custom headers present on every derdack host — consistent shared reverse-proxy/WAF fingerprint
[LEARN] REJECTED MISCONFIG @ dev.derdack.com: WordPress install — wp-json/ 404, wp-admin 404, xmlrpc not present; previous hypothesis invalidated
[RISK] derdack: 28 (low). signl4 permanently rejected. Root WP REST auth gates intact. NEW this cycle: /de/ multisite subsite exposes fully-functional xmlrpc.php (SSRF/user-enum vector) + untested revisions surface; /ea/ exposes public test PDF only; dev.derdack.com is a parked/error page with only blocked dot-prefix dirs via the shared x-ws proxy. Attack surface was broader than exhausted-inventory suggested — the /de/ xmlrpc + multisite revision checks are the live priorities before declaring the passive surface fully explored.
## 2026-09-04 20:03:59 UTC [target] (model bigpickle)
[NEW] www.derdack.com `/de/xmlrpc.php` returns 200 with full method list including pingback.ping — root xmlrpc is 503-blocked but /de/ is fully exposed
[NEW] www.derdack.com `/ea/` media exposes Whitepaper_test.pdf (3MB, 2017) — public test artifact
[NEW] dev.derdack.com root returns 403 with sedoparking.com IONOSParkingDE iframe while specific paths (/.well-known/, /.ssh/, /backups/, /logs/) still served
[NEW] `x-ws-origin: available` + `x-ws-ratelimit-*` custom headers present on ALL derdack hosts
[CHANGED] Previous hypothesis "dev.derdack.com WordPress install" REJECTED — wp-json/ 404, root is parked page
[PRIO] www.derdack.com/de/,6.35,a6,b6,t7,g4,c2,f8
[PRIO] www.derdack.com/ea/,5.75,a5,b5,t6,g4,c2,f8
[PRIO] www.derdack.com,4.30,a5,b7,t4,g0,c2,f5
[PRIO] dev.derdack.com,2.85,a3,b3,t3,g0,c4,f5
[PRIO] signl4.derdack.com,0.00,0,0,0,0,0,0
[HYP] /de/ WordPress XML-RPC full exposure enables SSRF via pingback.ping and/or unauthenticated method abuse
class: SSRF
asset: www.derdack.com/de/xmlrpc.php
confidence: 55
reasoning: /de/xmlrpc.php returns 200 with system.listMethods including pingback.ping, system.multicall, wp.getUsers, wp.uploadFile; root install blocks xmlrpc at 503; /de/ is a separate multisite (sites/5) with its own plugin set; pingback.ping makes server fetch a source URL I control — classic SSRF-to-cloud-metadata (169.254.169.254) path; wp.getUsers/wp.getProfile may allow user enumeration independent of REST gating
evidence_needed: non-empty fault / faultCode 33 (source fetched but no link) vs 32 (connect refused) on pingback source pointing at metadata IP or controlled host; or wp.getUsers returning user rows without valid auth
verify_steps: POST /de/xmlrpc.php with pingback.ping source=http://169.254.169.254/latest/meta-data/ target=https://www.derdack.com/de/enterprise-alert-9-4-1-release/ ; compare faultCode to control source http://10.255.255.1/ ; POST wp.getUsers with empty creds
impact: SSRF to cloud metadata (IAM creds) or full user dump; severity HIGH (directive-priority class)
testability: PASSIVE
[HYP] /de/ and /ea/ multisite REST exposes revisions/autosaves/drafts or sensitive plugin data not gated like root
class: IDOR
asset: www.derdack.com/de/wp-json/wp/v2/posts/11640/revisions
confidence: 45
reasoning: /de/ and /ea/ are separate WP installs with distinct plugin sets (complianz, popular-posts, two-factor) and possibly different capability configs than root; root revisions/autosaves returned 401 but multisite subsites may have looser per-site caps; posts 11640/11612 confirmed on /de/
evidence_needed: 200 on /de/ or /ea/ revisions/autosaves/draft endpoints returning post content
verify_steps: GET https://www.derdack.com/de/wp-json/wp/v2/posts/11640/revisions; GET https://www.derdack.com/de/wp-json/wp/v2/posts/11640/autosaves; GET https://www.derdack.com/de/wp-json/wp/v2/posts?status=draft; repeat on /ea/ with a known post id
impact: leak of unpublished/draft content or revision history; severity LOW-MEDIUM
testability: PASSIVE
[HYP] x-ws-origin/x-ws-ratelimit proxy layer differs by Host header — alternate vhost or bypass possible
class: MISCONFIG
asset: dev.derdack.com (proxy-gated paths)
confidence: 35
reasoning: All derdack hosts share x-ws-origin: available + x-ws-ratelimit-limit: 1000 custom headers, suggesting a shared reverse-proxy/WAF; dev.derdack.com serves parked 403 on root but still serves /.well-known/, /.ssh/, /backups/, /logs/ through the proxy — inconsistent vhost routing; Host-header or path normalization may hit a different backend vhost
evidence_needed: any dev.derdack.com path returning non-parking 200 content (app/admin/api) via alternate Host or encoded path
verify_steps: GET https://dev.derdack.com%2f/ ; GET https://dev.derdack.com//unwashed/ ; GET https://dev.derdack.com/backups/..%2fbackups/ ; compare body class (parking vs Apache) across path variants
impact: access to parked-domain backend content; severity LOW
testability: PASSIVE
[PARKED] www.derdack.com/ea/ media Whitepaper_test.pdf: confidence 20 < 40; single 2017 test PDF is likely intended test artifact, not sensitive
[PARKED] derdack.com bare-domain vhost differential: confidence 15 < 40; confirmed 302 → www, no differential content
[PARKED] complianz/v1 documents+cookie_data: confirmed 200 but return empty arrays — no PII leaked
[PARKED] two-factor/1.0 endpoints: POST-only TOTP/backup-code endpoints, correctly require auth (GET 404), no unauth exposure
[PARKED] dev.derdack.com /backups//logs/ path guessing: 403 on listing + 404 on common filenames; directory-row-NSA known filenames return 503 not content
[FINAL] Survivors:
[NEXT] PROBE: POST https://www.derdack.com/de/xmlrpc.php with body containing pingback.ping source=http://169.254.169.254/latest/meta-data/ target=https://www.derdack.com/de/enterprise-alert-9-4-1-release/ — compare faultCode 33 (fetch) vs 32 (refused) vs empty-filter
[LEARN] ACCEPTED MISCONFIG @ www.derdack.com: /de/ and /ea/ are separate WP Multisite subdirectory installs (sites/5 and sites/6) with unique plugin namespaces (complianz, popular-posts, two-factor, wp-site-health) — new attack surface previously unprobed
[LEARN] ACCEPTED AUTH @ www.derdack.com/de/: xmlrpc.php fully functional (200, full method list) while root xmlrpc is 503-blocked — endpoint exposure anomaly on multisite subsite
[LEARN] ACCEPTED AUTH @ www.derdack.com/ea/: xmlrpc.php returns 405 (blocked) — /de/ is the anomalous sub-install
[LEARN] ACCEPTED MISCONFIG @ dev.derdack.com: root returns parked 403 with IONOS sedoparking iframe while /.well-known/, /.ssh/, /backups/, /logs/ still served via Apache — parked/error config with partial real backends
[LEARN] ACCEPTED MISCONFIG @ all: x-ws-origin: available + x-ws-ratelimit custom headers present on every derdack host — consistent shared reverse-proxy/WAF fingerprint
[LEARN] REJECTED MISCONFIG @ dev.derdack.com: WordPress install — wp-json/ 404, wp-admin 404, xmlrpc not present; previous hypothesis invalidated
[RISK] derdack: 28 (low). signl4 permanently rejected. Root WP REST auth gates intact. NEW this cycle: /de/ multisite subsite exposes fully-functional xmlrpc.php (SSRF/user-enum vector) + untested revisions surface; /ea/ exposes public test PDF only; dev.derdack.com is a parked/error page with only blocked dot-prefix dirs via the shared x-ws proxy. Attack surface was broader than exhausted-inventory suggested — the /de/ xmlrpc + multisite revision checks are the live priorities before declaring the passive surface fully explored.
## 2026-09-04 22:23:54 UTC [target] (model bigpickle)
[HYP] /de/ multisite XML-RPC legacy methods bypass REST content gating
class: AUTH
asset: www.derdack.com/de/xmlrpc.php
confidence: 50
reasoning: /de/ xmlrpc.php returns 200 with full method list unauthenticated (wp.getUsers, wp.getProfile, wp.getMediaLibrary, mt.*, blogger.*); REST equivalents are auth-gated; XML-RPC is a parallel core API with historically weaker per-method caps; metaWeblog.getUsersBlogs(empty creds)→empty-string (not 401/403 fault) signals non-standard auth handling
evidence_needed: wp.getUsers/wp.getProfile/wp.getMediaLibrary/mt.getPost returning actual rows/content without valid credentials
verify_steps: POST /de/xmlrpc.php wp.getUsers(1,x,x); wp.getProfile(1,x,x); wp.getMediaLibrary(1,x,x); mt.getPost(1,11640,x,x) — compare against expected faultCode 401/403 fault
impact: read of user rows, profile PII, and private media/draft content bypassing REST caps; severity MED
testability: PASSIVE
[HYP] /ea/ multisite revisions/autosaves IDOR
class: IDOR
asset: www.derdack.com/ea/wp-json/wp/v2/posts/{id}/revisions
confidence: 45
reasoning: root revisions/autosaves return 401 (caps intact); /de/ and /ea/ are separate multisite installs (sites/5, sites/6) with distinct plugin/capability configs and their own XML-RPC exposure — per-site caps may differ from network root; /de/ posts 11640/11612 confirmed, /ea/ post id unharvested
evidence_needed: 200 returning revision/autosave content or status=draft rows on /de/ or /ea/
verify_steps: GET /de/wp-json/wp/v2/posts/11640/revisions ; GET /de/wp-json/wp/v2/posts/11640/autosaves ; GET /de/wp-json/wp/v2/posts?status=draft ; GET /ea/wp-json/wp/v2/posts?per_page=1 for id then GET /ea/wp-json/wp/v2/posts/{id}/revisions
impact: unpublished/draft/revision content leak; severity LOW-MED
testability: PASSIVE
[HYP] dev.derdack.com parked-root hides routable backend behind x-ws proxy
class: MISCONFIG
asset: dev.derdack.com
confidence: 45
reasoning: dev root serves parked 403 (sedoparking/IONOS iframe) through the shared x-ws proxy yet /.well-known/, /.ssh/, /backups/, /logs/ still reach Apache backends — inconsistent vhost routing implies a real config coexisting with the parking catch-all; only dot-dir namespaces were enumerated, common app paths unprobed
evidence_needed: any dev.derdack.com path returning non-parking (Apache/app 200/404) content
verify_steps: GET /app/ /api/ /api/v1/ /v1/ /swagger.json /openapi.json /admin/ /index.php /wp-login.php /favicon.ico ; compare body signature (sedoparking iframe vs Apache error vs app)
impact: exposure of dev app surface; severity LOW-MED
testability: PASSIVE
[PARKED] SSRF @ www.derdack.com/de/ pingback (55/70 → 0): faultCode 0 empty on metadata IP — no fetch artifact; aggregated REJECTED; not re-probing
[PARKED] SSRF @ multisite oembed/1.0/proxy (25): root oembed-proxy 401; shared core ⇒ same gating on subsites
[PARKED] MISCONFIG @ dev.derdack.com Host-header differential (35): parking catch-all + blocked dot-dirs already characterized; low yield
[PARKED] OTHER @ www.derdack.com/ea/ Whitepaper_test.pdf (20): absent from /de/+/ea/ media — invalidated
[PARKED] AUTH @ signl4.derdack.com (40): permanently unreachable at TCP layer across 8+ cycles; value 0
[FINAL] survivors ranked: 1. [50] AUTH /de/ XML-RPC legacy-method bypass 2. [45] IDOR /ea+/de/ revisions 3. [45] MISCONFIG dev backend discovery
[NEXT] PROBE: GET https://www.derdack.com/de/wp-json/wp/v2/posts/11640/revisions (200 = IDOR leak, 401 = gated); if 200, also GET /de/wp-json/wp/v2/posts/11640/autosaves and /de/wp-json/wp/v2/posts?status=draft ; then GET https://www.derdack.com/ea/wp-json/wp/v2/posts?per_page=1 to harvest an /ea/ post id and repeat the revisions probe on it.
[LEARN] REJECTED SSRF @ www.derdack.com/de/: pingback.ping→169.254.169.254 returns faultCode 0 empty faultString — no fetch artifact, cloud-metadata SSRF unconfirmed; closed
[LEARN] ACCEPTED AUTH @ www.derdack.com/ea/: xmlrpc.php POST returns full method list (earlier 405 was GET-only) — BOTH /de/ and /ea/ multisite installs run open XML-RPC
[LEARN] ACCEPTED AUTH @ www.derdack.com/de/: metaWeblog.getUsersBlogs(empty creds)→empty string, not 401/403 fault — non-standard XML-RPC auth handling; method-level cap check warranted
[LEARN] REJECTED MISCONFIG @ www.derdack.com/ea/: Whitepaper_test.pdf absent from /de/+/ea/ media (images only) — test-PDF vector invalidated
[RISK] derdack: 30 (low). Open XML-RPC on /de/ and /ea/ is live exposure but pingback→metadata SSRF unconfirmed and rejected; remaining untested high-value primitives are the multisite revisions/autosaves IDOR and XML-RPC legacy-method cap bypass; root REST gates proven intact; dev is parked-with-blocked-dirs; signl4 zero-value. Confidence-weighted exposure moderate-low.
