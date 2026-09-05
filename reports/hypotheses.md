# Hypotheses (ranked)

## RANKED HYPOTHESES 2026-09-02 21:30:24 UTC

## RANKED HYPOTHESES 2026-09-02 23:34:05 UTC

## RANKED HYPOTHESES 2026-09-03 01:27:36 UTC

## RANKED HYPOTHESES 2026-09-03 06:47:03 UTC

## RANKED HYPOTHESES 2026-09-03 11:44:06 UTC

## RANKED HYPOTHESES 2026-09-03 15:38:51 UTC
- [55] signl4.derdack.com: SIGNL4 API JWT alg confusion on token validation (from art/lead_nemotron3.txt)
- [30] signl4.derdack.com: SIGNL4 API authentication bypass (from art/lead_bigpickle.txt)
- NEXT(hypotheses-nemotron3.txt): PROBE: GET https://dev.derdack.com/actuator && GET https://dev.derdack.com/swagger-ui.html && GET https://dev.derdack.com/api/docs && GET https://dev.derdack.co
- NEXT(hypotheses-bigpickle.txt): PROBE: Passive HTTP probing of all 9 inventory hosts to confirm live status, identify technologies, and discover API endpoints. Start with signl4.derdack.com (h
- LEARN: REJECTED none this cycle — all hypotheses target in-scope HIGH-VALUE classes with concrete verify steps
- LEARN: ACCEPTED MISCONFIG @ dev.derdack.com: dev environments frequently expose debug interfaces; passive probe cost near-zero
- LEARN: ACCEPTED AUTH @ signl4.derdack.com: SaaS platform target, worth investigating API auth after passive probing confirms endpoints
- LEARN: REJECTED brute-force @ all: program explicitly excludes brute-force/rate-limit/lockout policy testing

## RANKED HYPOTHESES 2026-09-03 19:05:04 UTC
- [75] dev.derdack.com: dev.derdack.com openid-configuration path traversal via 300 Multiple Choices (from art/lead_nemotron3.txt)
- [35] signl4.derdack.com: SIGNL4 OIDC/JWKS discovery and token endpoint enumeration (from art/lead_bigpickle.txt)
- NEXT(hypotheses-bigpickle.txt): PROBE: Passive HTTP fingerprinting of signl4.derdack.com and signals.derdack.com (nemotron3 covers dev.derdack.com). Exact requests:
- NEXT(hypotheses-nemotron3.txt): PROBE: GET https://dev.derdack.com/.ssh/id_rsa && GET https://dev.derdack.com/.bash_history && GET https://dev.derdack.com/.viminfo && GET https://dev.derdack.c
- LEARN: ACCEPTED AUTH @ signl4.derdack.com: SaaS platform likely exposes OIDC/JWKS; passive discovery endpoints cost zero risk
- LEARN: ACCEPTED MISCONFIG @ dev.derdack.com: nemotron3 already probing actuator/swagger; I defer to avoid duplicate effort
- LEARN: REJECTED brute-force @ all: program explicitly excludes brute-force/rate-limit/lockout testing
- LEARN: REJECTED OPTIONS/TRACE @ all: program explicitly excludes OPTIONS/TRACE as standalone findings
- LEARN: ACCEPTED MISCONFIG @ dev.derdack.com: 300 Multiple Choices with sensitive path suggestions confirms Apache mod_negotiation/MultiViews misconfiguration; passive 
- LEARN: REJECTED SSRF @ signals.derdack.com: subdomain NXDOMAIN — does not exist
- LEARN: REJECTED MISCONFIG @ dev.derdack.com actuator/swagger/graphql: all 404 — no Spring Boot, Swagger, GraphQL exposed
- LEARN: ACCEPTED AUTH @ www.derdack.com: WordPress REST API exposed (wp-json), Contact Form 7, user enumeration vector confirmed in-scope
- LEARN: REJECTED brute-force @ all: program explicitly excludes rate-limit/lockout testing

## RANKED HYPOTHESES 2026-09-03 21:36:55 UTC
- [80] dev.derdack.com: dev.derdack.com Apache mod_negotiation MultiViews path disclosure (from art/lead_nemotron3.txt)
- NEXT(hypotheses-nemotron3.txt): PROBE: GET https://www.derdack.com/wp-json/wp/v2/users/1 (check individual user endpoint for email/PII); GET https://www.derdack.com/wp-json/wp/v2/media (check 
- LEARN: ACCEPTED MISCONFIG @ dev.derdack.com: 300 Multiple Choices with sensitive path suggestions confirms Apache mod_negotiation/MultiViews misconfiguration; passive 
- LEARN: ACCEPTED AUTH @ www.derdack.com: WordPress REST API exposed (wp-json), Contact Form 7, user enumeration vector confirmed in-scope
- LEARN: REJECTED SSRF @ signals.derdack.com: subdomain NXDOMAIN — does not exist
- LEARN: REJECTED MISCONFIG @ dev.derdack.com actuator/swagger/graphql: all 404 — no Spring Boot, Swagger, GraphQL exposed
- LEARN: REJECTED brute-force @ all: program explicitly excludes rate-limit/lockout testing

## RANKED HYPOTHESES 2026-09-03 23:32:47 UTC
- [85] dev.derdack.com: dev.derdack.com Apache mod_negotiation MultiViews sensitive file path disclosure (from art/lead_nemotron3.txt)
- [20] signals.derdack.com: SIGNL4 OIDC/JWKS discovery and token endpoint enumeration (from art/lead_bigpickle.txt)
- NEXT(hypotheses-bigpickle.txt): PROBE: Passive HTTP probing of all 9 inventory hosts to confirm live status, identify technologies, and discover API endpoints. Start with signl4.derdack.com (h
- NEXT(hypotheses-nemotron3.txt): PROBE: GET https://www.derdack.com/wp-json/wp/v2/users/1 && GET https://www.derdack.com/wp-json/wp/v2/media && GET https://dev.derdack.com/.well-known/openid-co
- LEARN: ACCEPTED AUTH @ signl4.derdack.com: SaaS platform target, worth investigating API auth after passive probing confirms endpoints
- LEARN: REJECTED brute-force @ all: program explicitly excludes brute-force/rate-limit/lockout policy testing
- LEARN: ACCEPTED AUTH @ signl4.derdack.com: SaaS platform likely exposes OIDC/JWKS; passive discovery endpoints cost zero risk
- LEARN: ACCEPTED MISCONFIG @ dev.derdack.com: nemotron3 already probing actuator/swagger; I defer to avoid duplicate effort
- LEARN: REJECTED brute-force @ all: program explicitly excludes brute-force/rate-limit/lockout testing
- LEARN: REJECTED OPTIONS/TRACE @ all: program explicitly excludes OPTIONS/TRACE as standalone findings
- LEARN: REJECTED MISCONFIG @ dev.derdack.com: MultiViews path disclosure is a static dot-prefix basename echo — identical output for fabricated paths proves no real sen
- LEARN: ACCEPTED AUTH @ www.derdack.com: WP REST API correctly enforces auth on settings/users/me/oembed-proxy/drafts (401/400); user enumeration confirmed but low-valu
- LEARN: REJECTED SSRF @ www.derdack.com: oEmbed proxy returns 401 for proxied requests — SSRF vector blocked.
- LEARN: ACCEPTED MISCONFIG @ dev.derdack.com: 300 Multiple Choices with sensitive path suggestions confirms Apache mod_negotiation/MultiViews misconfiguration; passive 
- LEARN: ACCEPTED AUTH @ www.derdack.com: WordPress REST API exposed (wp-json), Contact Form 7, user enumeration vector confirmed in-scope
- LEARN: REJECTED SSRF @ signals.derdack.com: subdomain NXDOMAIN — does not exist
- LEARN: REJECTED MISCONFIG @ dev.derdack.com actuator/swagger/graphql: all 404 — no Spring Boot, Swagger, GraphQL exposed
- LEARN: REJECTED brute-force @ all: program explicitly excludes rate-limit/lockout testing

## RANKED HYPOTHESES 2026-09-04 01:28:34 UTC
- [85] dev.derdack.com: dev.derdack.com Apache mod_negotiation MultiViews sensitive file path disclosure (from art/lead_nemotron3.txt)
- [40] signl4.derdack.com: signl4.derdack.com alternate Host-header or legacy port access (from art/lead_bigpickle.txt)
- NEXT(hypotheses-bigpickle.txt): PROBE: GET http://13.94.244.66:8080/ -m5 && GET http://13.94.244.66:8443/ -m5 && curl -k -H "Host: signl4.derdack.com" https://13.94.244.66/ -m5 (all passive, 1
- NEXT(hypotheses-nemotron3.txt): PROBE: GET https://www.derdack.com/wp-json/wp/v2/users/1 && GET https://www.derdack.com/wp-json/wp/v2/media && GET https://dev.derdack.com/.well-known/openid-co
- LEARN: REJECTED IDOR @ www.derdack.com revisions/autosaves: confidence 25 < 40; all prior protected WP endpoints returned 401; capability check appears intact.
- LEARN: REJECTED IDOR @ www.derdack.com users/{id} PII: confidence 30 < 40; /users collection already exposed no email; single-user endpoint unlikely to differ.
- LEARN: ACCEPTED OTHER @ signl4.derdack.com: 40 confidence warranting final probe — if alternate Host/port fails, permanently reject signl4 and pivot all remaining effo
- LEARN: ACCEPTED MISCONFIG @ dev.derdack.com: 300 Multiple Choices with sensitive path suggestions confirms Apache mod_negotiation/MultiViews misconfiguration; passive 
- LEARN: ACCEPTED AUTH @ www.derdack.com: WordPress REST API exposed (wp-json), Contact Form 7, user enumeration vector confirmed in-scope
- LEARN: REJECTED SSRF @ signals.derdack.com: subdomain NXDOMAIN — does not exist
- LEARN: REJECTED MISCONFIG @ dev.derdack.com actuator/swagger/graphql: all 404 — no Spring Boot, Swagger, GraphQL exposed
- LEARN: REJECTED brute-force @ all: program explicitly excludes rate-limit/lockout testing
- LEARN: REJECTED OPTIONS/TRACE @ all: program explicitly excludes OPTIONS/TRACE as standalone findings
- LEARN: REJECTED MISCONFIG @ dev.derdack.com: MultiViews path disclosure is a static dot-prefix basename echo — identical output for fabricated paths proves no real sen
- LEARN: ACCEPTED AUTH @ www.derdack.com: WP REST API correctly enforces auth on settings/users/me/oembed-proxy/drafts (401/400); user enumeration confirmed but low-valu
- LEARN: REJECTED SSRF @ www.derdack.com: oEmbed proxy returns 401 for proxied requests — SSRF vector blocked

## RANKED HYPOTHESES 2026-09-04 06:15:30 UTC
- LEARN: REJECTED OTHER @ signl4.derdack.com: alternate port/host probes all returned http_code=000; signl4 is permanently unreachable across 80, 443, 8080, 8443, and IP
- LEARN: ACCEPTED AUTH @ www.derdack.com: Yoast SEO REST API (`/yoast/v1/`) route schema fully enumerated but all admin endpoints (file_size, statistics, workouts, semru
- LEARN: ACCEPTED AUTH @ www.derdack.com: `/wp-json/wp/v2/users/1` confirmed returns only id, name, slug, link — no email/PII; user enumeration is low-value public-blog 
- LEARN: ACCEPTED MISCONFIG @ www.derdack.com: `xmlrpc.php` returns 503 (blocked at LB level); attack vector neutralized.
- LEARN: ACCEPTED AUTH @ www.derdack.com: CF7 endpoint `/wp-json/contact-form-7/v1/contact-forms` returns 403 (properly gated).
- LEARN: REJECTED SSRF @ www.derdack.com: Yoast `file_size` endpoint returns 401 (auth-gated); no SSRF possible without authentication.

## RANKED HYPOTHESES 2026-09-04 11:01:16 UTC
- [85] dev.derdack.com: dev.derdack.com Apache mod_negotiation MultiViews sensitive file path disclosure (from art/lead_nemotron3.txt)
- [35] www.derdack.com/wp-json/: WP Theme/plugin GraphQL/REST discovery via /wp-json/ routes (from art/lead_bigpickle.txt)
- NEXT(hypotheses-bigpickle.txt): HUMAN: All passive attack vectors on www.derdack.com and dev.derdack.com have been probed and verified as properly gated. signl4 permanently unreachable (8 cycl
- NEXT(hypotheses-nemotron3.txt): PROBE: GET https://www.derdack.com/wp-json/wp/v2/media?per_page=100 && GET https://www.derdack.com/wp-json/wp/v2/media?page=2 && GET https://www.derdack.com/wp-
- LEARN: REJECTED OTHER @ signl4.derdack.com: alternate port/host probes all returned http_code=000; signl4 permanently unreachable
- LEARN: ACCEPTED AUTH @ www.derdack.com: Yoast SEO REST API routes all return 401; only `get_head?url=` is public
- LEARN: ACCEPTED AUTH @ www.derdack.com: `/wp-json/wp/v2/users/1` returns only name/slug; no PII
- LEARN: ACCEPTED MISCONFIG @ www.derdack.com: xmlrpc.php returns 503 (blocked at LB)
- LEARN: ACCEPTED AUTH @ www.derdack.com: CF7 endpoint returns 403 (properly gated)
- LEARN: REJECTED SSRF @ www.derdack.com: Yoast `file_size` returns 401 (auth-gated)
- LEARN: ACCEPTED MISCONFIG @ dev.derdack.com: 300 Multiple Choices with sensitive path suggestions confirms Apache mod_negotiation/MultiViews misconfiguration; passive 
- LEARN: ACCEPTED AUTH @ www.derdack.com: WordPress REST API exposed (wp-json), Contact Form 7, user enumeration vector confirmed in-scope
- LEARN: REJECTED SSRF @ signals.derdack.com: subdomain NXDOMAIN — does not exist
- LEARN: REJECTED MISCONFIG @ dev.derdack.com actuator/swagger/graphql: all 404 — no Spring Boot, Swagger, GraphQL exposed
- LEARN: REJECTED brute-force @ all: program explicitly excludes rate-limit/lockout testing
- LEARN: REJECTED OPTIONS/TRACE @ all: program explicitly excludes OPTIONS/TRACE as standalone findings
- LEARN: REJECTED MISCONFIG @ dev.derdack.com: MultiViews path disclosure is a static dot-prefix basename echo — identical output for fabricated paths proves no real sen
- LEARN: ACCEPTED AUTH @ www.derdack.com: WP REST API correctly enforces auth on settings/users/me/oembed-proxy/drafts (401/400); user enumeration confirmed but low-valu
- LEARN: REJECTED SSRF @ www.derdack.com: oEmbed proxy returns 401 for proxied requests — SSRF vector blocked
- LEARN: REJECTED IDOR @ www.derdack.com revisions/autosaves: confidence 25 < 40; all prior protected WP endpoints returned 401; capability check appears intact
- LEARN: REJECTED IDOR @ www.derdack.com users/{id} PII: confidence 30 < 40; /users collection already exposed no email; single-user endpoint unlikely to differ
- LEARN: REJECTED OTHER @ signl4.derdack.com: alternate port/host probes all returned http_code=000; signl4 is permanently unreachable across 80, 443, 8080, 8443, and IP
- LEARN: ACCEPTED AUTH @ www.derdack.com: Yoast SEO REST API (`/yoast/v1/`) route schema fully enumerated but all admin endpoints (file_size, statistics, workouts, semru
- LEARN: ACCEPTED AUTH @ www.derdack.com: `/wp-json/wp/v2/users/1` confirmed returns only id, name, slug, link — no email/PII; user enumeration is low-value public-blog 
- LEARN: ACCEPTED MISCONFIG @ www.derdack.com: `xmlrpc.php` returns 503 (blocked at LB level); attack vector neutralized
- LEARN: ACCEPTED AUTH @ www.derdack.com: CF7 endpoint `/wp-json/contact-form-7/v1/contact-forms` returns 403 (properly gated)
- LEARN: REJECTED SSRF @ www.derdack.com: Yoast `file_size` endpoint returns 401 (auth-gated); no SSRF possible without authentication

## RANKED HYPOTHESES 2026-09-04 14:54:49 UTC
- [85] dev.derdack.com: dev.derdack.com Apache mod_negotiation MultiViews sensitive file path disclosure (from art/lead_nemotron3.txt)
- [35] dev.derdack.com/wp-json/: dev.derdack.com WordPress staging/debug exposure (from art/lead_bigpickle.txt)
- NEXT(hypotheses-bigpickle.txt): PROBE: HEAD https://dev.derdack.com/wp-json/ && HEAD https://dev.derdack.com/wp-login.php && HEAD https://dev.derdack.com/xmlrpc.php
- NEXT(hypotheses-nemotron3.txt): PROBE: GET https://dev.derdack.com/.ssh/id_rsa && GET https://dev.derdack.com/.ssh/authorized_keys && GET https://dev.derdack.com/.ssh/known_hosts (test if indi
- LEARN: ACCEPTED MISCONFIG @ dev.derdack.com: MultiViews confirmed; WordPress installation status unknown — probe required.
- LEARN: REJECTED OTHER @ signl4.derdack.com: permanently unreachable across 8+ probe cycles (all TCP timeout); all attack surface value = 0.
- LEARN: ACCEPTED MISCONFIG @ dev.derdack.com: 300 Multiple Choices with sensitive path suggestions confirms Apache mod_negotiation/MultiViews misconfiguration; passive 
- LEARN: ACCEPTED AUTH @ www.derdack.com: WordPress REST API exposed (wp-json), Contact Form 7, user enumeration vector confirmed in-scope
- LEARN: REJECTED SSRF @ signals.derdack.com: subdomain NXDOMAIN — does not exist
- LEARN: REJECTED MISCONFIG @ dev.derdack.com actuator/swagger/graphql: all 404 — no Spring Boot, Swagger, GraphQL exposed
- LEARN: REJECTED brute-force @ all: program explicitly excludes rate-limit/lockout testing
- LEARN: REJECTED OPTIONS/TRACE @ all: program explicitly excludes OPTIONS/TRACE as standalone findings
- LEARN: REJECTED MISCONFIG @ dev.derdack.com: MultiViews path disclosure is a static dot-prefix basename echo — identical output for fabricated paths proves no real sen
- LEARN: ACCEPTED AUTH @ www.derdack.com: WP REST API correctly enforces auth on settings/users/me/oembed-proxy/drafts (401/400); user enumeration confirmed but low-valu
- LEARN: REJECTED SSRF @ www.derdack.com: oEmbed proxy returns 401 for proxied requests — SSRF vector blocked
- LEARN: REJECTED IDOR @ www.derdack.com revisions/autosaves: confidence 25 < 40; all prior protected WP endpoints returned 401; capability check appears intact
- LEARN: REJECTED IDOR @ www.derdack.com users/{id} PII: confidence 30 < 40; /users collection already exposed no email; single-user endpoint unlikely to differ
- LEARN: REJECTED OTHER @ signl4.derdack.com: alternate port/host probes all returned http_code=000; signl4 is permanently unreachable across 80, 443, 8080, 8443, and IP
- LEARN: ACCEPTED AUTH @ www.derdack.com: Yoast SEO REST API (`/yoast/v1/`) route schema fully enumerated but all admin endpoints (file_size, statistics, workouts, semru
- LEARN: ACCEPTED AUTH @ www.derdack.com: `/wp-json/wp/v2/users/1` confirmed returns only id, name, slug, link — no email/PII; user enumeration is low-value public-blog 
- LEARN: ACCEPTED MISCONFIG @ www.derdack.com: `xmlrpc.php` returns 503 (blocked at LB level); attack vector neutralized
- LEARN: ACCEPTED AUTH @ www.derdack.com: CF7 endpoint `/wp-json/contact-form-7/v1/contact-forms` returns 403 (properly gated)
- LEARN: REJECTED SSRF @ www.derdack.com: Yoast `file_size` endpoint returns 401 (auth-gated); no SSRF possible without authentication
- LEARN: ACCEPTED MISCONFIG @ www.derdack.com: blog.derdack.com & techblog.derdack.com HTTPS redirects to HTTP (downgrade chain) — mixed content risk confirmed
- LEARN: REJECTED AUTH @ www.derdack.com: Media library `/wp-json/wp/v2/media` returns 200 but only public assets (stock images, 1 MP3 podcast); no internal docs/PDFs/ba

## RANKED HYPOTHESES 2026-09-04 17:59:53 UTC
- [85] dev.derdack.com: dev.derdack.com Apache mod_negotiation MultiViews sensitive path disclosure (from art/lead_nemotron3.txt)
- [55] www.derdack.com/de/xmlrpc.php: /de/ WordPress XML-RPC full exposure enables SSRF via pingback.ping and/or unauthenticated method abuse (from art/lead_bigpickle.txt)
- NEXT(hypotheses-bigpickle.txt): PROBE: POST https://www.derdack.com/de/xmlrpc.php pingback.ping source=http://169.254.169.254/latest/meta-data/ target=https://www.derdack.com/de/enterprise-ale
- NEXT(hypotheses-nemotron3.txt): PROBE: GET https://dev.derdack.com/.well-known/ (confirm 300 body still lists /.ssh/, /.bash_history/, /.viminfo/ as "similar documents" for evidence package)
- LEARN: ACCEPTED MISCONFIG @ www.derdack.com: /de/ and /ea/ are separate WP Multisite subdirectory installs (sites/5 and sites/6) with unique plugin namespaces (complia
- LEARN: ACCEPTED AUTH @ www.derdack.com/de/: xmlrpc.php fully functional (200, full method list) while root xmlrpc is 503-blocked — endpoint exposure anomaly on multisi
- LEARN: ACCEPTED AUTH @ www.derdack.com/ea/: xmlrpc.php returns 405 (blocked) — /de/ is the anomalous sub-install
- LEARN: ACCEPTED MISCONFIG @ dev.derdack.com: root returns parked 403 with IONOS sedoparking iframe while /.well-known/, /.ssh/, /backups/, /logs/ still served via Apac
- LEARN: ACCEPTED MISCONFIG @ all: x-ws-origin: available + x-ws-ratelimit custom headers present on every derdack host — consistent shared reverse-proxy/WAF fingerprint
- LEARN: REJECTED MISCONFIG @ dev.derdack.com: WordPress install — wp-json/ 404, wp-admin 404, xmlrpc not present; previous hypothesis invalidated
- LEARN: ACCEPTED MISCONFIG @ dev.derdack.com: 300 Multiple Choices with sensitive path suggestions confirms Apache mod_negotiation/MultiViews misconfiguration; passive 
- LEARN: ACCEPTED MISCONFIG @ blog.derdack.com & techblog.derdack.com: HTTPS redirects to HTTP (downgrade chain) — mixed content risk confirmed
- LEARN: REJECTED MISCONFIG @ dev.derdack.com: WordPress staging/debug exposure — wp-json/wp-login/xmlrpc all 404/503; no WP on dev host
- LEARN: ACCEPTED AUTH @ www.derdack.com: Media library `/wp-json/wp/v2/media` returns 200 with 2170 items but only public marketing assets (images, logos, 1 MP3 podcast
- LEARN: REJECTED OTHER @ signl4.derdack.com: permanently unreachable across 8+ probe cycles (all TCP timeout); all attack surface value = 0
- LEARN: REJECTED brute-force @ all: program explicitly excludes rate-limit/lockout testing
- LEARN: REJECTED OPTIONS/TRACE @ all: program explicitly excludes OPTIONS/TRACE as standalone findings

## RANKED HYPOTHESES 2026-09-04 20:19:13 UTC
- [70] www.derdack.com/de/xmlrpc.php: www.derdack.com/de/ XML-RPC pingback.ping SSRF to cloud metadata (from art/lead_nemotron3.txt)
- [55] www.derdack.com/de/xmlrpc.php: /de/ WordPress XML-RPC full exposure enables SSRF via pingback.ping and/or unauthenticated method abuse (from art/lead_bigpickle.txt)
- NEXT(hypotheses-bigpickle.txt): PROBE: POST https://www.derdack.com/de/xmlrpc.php with body containing pingback.ping source=http://169.254.169.254/latest/meta-data/ target=https://www.derdack.
- NEXT(hypotheses-nemotron3.txt): PROBE: GET https://dev.derdack.com/.well-known/ (confirm 300 body still lists /.ssh/, /.bash_history/, /.viminfo/ for evidence package)
- LEARN: ACCEPTED MISCONFIG @ www.derdack.com: /de/ and /ea/ are separate WP Multisite subdirectory installs (sites/5 and sites/6) with unique plugin namespaces (complia
- LEARN: ACCEPTED AUTH @ www.derdack.com/de/: xmlrpc.php fully functional (200, full method list) while root xmlrpc is 503-blocked — endpoint exposure anomaly on multisi
- LEARN: ACCEPTED AUTH @ www.derdack.com/ea/: xmlrpc.php returns 405 (blocked) — /de/ is the anomalous sub-install
- LEARN: ACCEPTED MISCONFIG @ dev.derdack.com: root returns parked 403 with IONOS sedoparking iframe while /.well-known/, /.ssh/, /backups/, /logs/ still served via Apac
- LEARN: ACCEPTED MISCONFIG @ all: x-ws-origin: available + x-ws-ratelimit custom headers present on every derdack host — consistent shared reverse-proxy/WAF fingerprint
- LEARN: REJECTED MISCONFIG @ dev.derdack.com: WordPress install — wp-json/ 404, wp-admin 404, xmlrpc not present; previous hypothesis invalidated
- LEARN: ACCEPTED MISCONFIG @ dev.derdack.com: 300 Multiple Choices with sensitive path suggestions confirms Apache mod_negotiation/MultiViews misconfiguration; passive 
- LEARN: ACCEPTED AUTH @ www.derdack.com/de/: xmlrpc.php fully functional (200, full method list) while root xmlrpc is 503-blocked — endpoint exposure anomaly on multisi
- LEARN: ACCEPTED AUTH @ www.derdack.com/ea/: xmlrpc.php POST returns full method list (GET returns 405) — /ea/ also exposed, not just /de/
- LEARN: REJECTED SSRF @ www.derdack.com/de/: pingback.ping to 169.254.169.254 returns faultCode 0 empty — ambiguous, not confirmed SSRF
- LEARN: REJECTED MISCONFIG @ www.derdack.com/ea/: Whitepaper_test.pdf not found in media library — hypothesis invalidated
- LEARN: REJECTED brute-force @ all: program explicitly excludes rate-limit/lockout testing
- LEARN: REJECTED OPTIONS/TRACE @ all: program explicitly excludes OPTIONS/TRACE as standalone findings

## RANKED HYPOTHESES 2026-09-04 22:25:11 UTC
- [50] www.derdack.com/de/xmlrpc.php: /de/ multisite XML-RPC legacy methods bypass REST content gating (from art/lead_bigpickle.txt)
- NEXT(hypotheses-bigpickle.txt): PROBE: GET https://www.derdack.com/de/wp-json/wp/v2/posts/11640/revisions (200 = IDOR leak, 401 = gated); if 200, also GET /de/wp-json/wp/v2/posts/11640/autosav
- LEARN: REJECTED SSRF @ www.derdack.com/de/: pingback.ping→169.254.169.254 returns faultCode 0 empty faultString — no fetch artifact, cloud-metadata SSRF unconfirmed; c
- LEARN: ACCEPTED AUTH @ www.derdack.com/ea/: xmlrpc.php POST returns full method list (earlier 405 was GET-only) — BOTH /de/ and /ea/ multisite installs run open XML-RP
- LEARN: ACCEPTED AUTH @ www.derdack.com/de/: metaWeblog.getUsersBlogs(empty creds)→empty string, not 401/403 fault — non-standard XML-RPC auth handling; method-level ca
- LEARN: REJECTED MISCONFIG @ www.derdack.com/ea/: Whitepaper_test.pdf absent from /de/+/ea/ media (images only) — test-PDF vector invalidated
- LEARN: ACCEPTED MISCONFIG @ dev.derdack.com: 300 Multiple Choices with sensitive path suggestions confirms Apache mod_negotiation/MultiViews misconfiguration; passive 
- LEARN: ACCEPTED AUTH @ www.derdack.com/de/: xmlrpc.php fully functional (200, full method list) while root xmlrpc is 503-blocked — endpoint exposure anomaly on multisi
- LEARN: ACCEPTED AUTH @ www.derdack.com/ea/: xmlrpc.php POST returns full method list (GET returns 405) — /ea/ also exposed, not just /de/
- LEARN: REJECTED SSRF @ www.derdack.com/de/: pingback.ping to 169.254.169.254 returns faultCode 0 empty — ambiguous, not confirmed SSRF
- LEARN: REJECTED MISCONFIG @ www.derdack.com/ea/: Whitepaper_test.pdf not found in media library — hypothesis invalidated
- LEARN: REJECTED brute-force @ all: program explicitly excludes rate-limit/lockout testing
- LEARN: REJECTED OPTIONS/TRACE @ all: program explicitly excludes OPTIONS/TRACE as standalone findings

## RANKED HYPOTHESES 2026-09-05 00:27:41 UTC
- [55] devconnect.signl4.com: SIGNL4 dev/lab OIDC+account staging estate exposes unauthenticated or debug surface (from art/lead_bigpickle.txt)
- [50] www.derdack.com/de/xmlrpc.php: www.derdack.com/de/ XML-RPC legacy method cap bypass via parallel API (from art/lead_nemotron3.txt)
- NEXT(hypotheses-bigpickle.txt): PROBE: GET https://devaccount.signl4.com/ and GET https://devconnect.signl4.com/identity/.well-known/openid-configuration — if staging issuer differs from prod 
- NEXT(hypotheses-nemotron3.txt): PROBE: POST https://www.derdack.com/de/xmlrpc.php with body `<?xml version="1.0"?><methodCall><methodName>wp.getUsers</methodName><params><param><value><int>1</
- LEARN: ACCEPTED MISCONFIG @ dev.derdack.com: 300 Multiple Choices with sensitive path suggestions confirms Apache mod_negotiation/MultiViews misconfiguration; passive 
- LEARN: ACCEPTED AUTH @ www.derdack.com/de/: xmlrpc.php fully functional (200, full method list) while root xmlrpc is 503-blocked — endpoint exposure anomaly on multisi
- LEARN: ACCEPTED AUTH @ www.derdack.com/ea/: xmlrpc.php POST returns full method list (GET returns 405) — /ea/ also exposed, not just /de/
- LEARN: REJECTED SSRF @ www.derdack.com/de/: pingback.ping to 169.254.169.254 returns faultCode 0 empty — ambiguous, not confirmed SSRF
- LEARN: REJECTED MISCONFIG @ www.derdack.com/ea/: Whitepaper_test.pdf not found in media library — hypothesis invalidated
- LEARN: REJECTED brute-force @ all: program explicitly excludes rate-limit/lockout testing
- LEARN: REJECTED OPTIONS/TRACE @ all: program explicitly excludes OPTIONS/TRACE as standalone findings
- LEARN: REJECTED OTHER @ signl4.derdack.com: permanently unreachable across 8+ probe cycles (all TCP timeout); all attack surface value = 0

## RANKED HYPOTHESES 2026-09-05 04:59:19 UTC
- [75] devconnect.signl4.com/identity: devconnect staging IdP shares prod token-signing key + OAuth client → cross-env token forgery (from art/lead_bigpickle.txt)
- [60] devconnect.signl4.com/identity/.well-known/openid-configuration: SIGNL4 staging IdentityServer exposes debug endpoints or relaxed auth (from art/lead_nemotron3.txt)
- NEXT(hypotheses-bigpickle.txt): PROBE: GET https://www.signl4.com/wp-json/two-factor/user-info (only untested registered REST read left on signl4.com estate; 200 = 2FA-status/user-meta disclos
- NEXT(hypotheses-nemotron3.txt): PROBE: GET https://devconnect.signl4.com/identity/.well-known/openid-configuration && GET https://devaccount.signl4.com/ — observe issuer, endpoints, server hea
- LEARN: ACCEPTED AUTH @ devconnect.signl4.com: staging IdentityServer live + shares prod RS256 signing key (kid/n/x5t/x5c identical) and account-portal client_id 692A0A
- LEARN: ACCEPTED MISCONFIG @ labconnect/labaccount.signl4.com: Azure AppGW/v2 502 on all probed paths (root, /identity/, /connect/authorize) — unmapped backend, estate 
- LEARN: ACCEPTED MISCONFIG @ api.signl4.com: /api/v2 = alerts(405)+teams(401 Bearer) only; no unauth read surface; root 301 → account.signl4.com/manage
- LEARN: REJECTED AUTH @ www.signl4.com: WP users/media REST is public-blog-only; users/1 no email/PII — same low value as derdack.com
- LEARN: ACCEPTED MISCONFIG @ www.signl4.com: WPML ate/proxy 401, wpaas activity-logs 401, divitorque settings 401 (gated); wpml-ph-make-external-request + wpaas diagnos
- LEARN: ACCEPTED AUTH @ devconnect.signl4.com: SIGNL4 dev/lab OIDC+account staging estate resolves on dedicated IPs (dev 108.143.123.104, lab 13.93.49.201); CSP explici
- LEARN: ACCEPTED MISCONFIG @ api.signl4.com: /api/v2/alerts returns 405 Allow:POST confirming live API namespace; base routes unprobed for GET
- LEARN: ACCEPTED AUTH @ www.signl4.com: CF-fronted WordPress confirmed via xmlrpc pingback link; same fleet family as derdack.com
- LEARN: ACCEPTED AUTH @ www.derdack.com/de/: xmlrpc.php fully functional (200, full method list) while root xmlrpc is 503-blocked — endpoint exposure anomaly on multisi
- LEARN: ACCEPTED AUTH @ www.derdack.com/ea/: xmlrpc.php POST returns full method list (GET returns 405) — /ea/ also exposed, not just /de/
- LEARN: REJECTED SSRF @ www.derdack.com/de/: pingback.ping to 169.254.169.254 returns faultCode 0 empty — ambiguous, not confirmed SSRF
- LEARN: REJECTED MISCONFIG @ www.derdack.com/ea/: Whitepaper_test.pdf not found in media library — hypothesis invalidated
- LEARN: REJECTED brute-force @ all: program explicitly excludes rate-limit/lockout testing
- LEARN: REJECTED OPTIONS/TRACE @ all: program explicitly excludes OPTIONS/TRACE as standalone findings
- LEARN: REJECTED OTHER @ signl4.derdack.com: permanently unreachable across 8+ probe cycles (all TCP timeout); all attack surface value = 0
- LEARN: REJECTED IDOR @ www.derdack.com revisions/autosaves: all protected endpoints return 401; capability check intact
- LEARN: REJECTED IDOR @ www.derdack.com users/{id} PII: collection exposes no email; single endpoint unlikely to differ
- LEARN: ACCEPTED MISCONFIG @ dev.derdack.com: 300 Multiple Choices with sensitive path suggestions confirms Apache mod_negotiation/MultiViews; passive probe cost near-z
- LEARN: ACCEPTED MISCONFIG @ blog.derdack.com & techblog.derdack.com: HTTPS redirects to HTTP (downgrade chain) — mixed content risk confirmed
- LEARN: ACCEPTED MISCONFIG @ www.derdack.com: Missing HSTS, CSP, X-Frame-Options on primary domain
- LEARN: ACCEPTED AUTH @ www.derdack.com: WP REST API auth gates intact on settings/users/me/oembed-proxy/drafts/CF7/Yoast admin (401/403/400)

## RANKED HYPOTHESES 2026-09-05 08:47:56 UTC
- [85] devconnect.signl4.com/identity/.well-known/openid-configuration: SIGNL4 devconnect staging IdentityServer shares PROD RS256 signing key enabling cross-env token forgery (from art/lead_nemotron3.txt)
- [75] devconnect.signl4.com/identity: devconnect staging IdP shares prod token-signing key + OAuth client → cross-env token forgery (from art/lead_bigpickle.txt)
- NEXT(hypotheses-bigpickle.txt): PROBE: GET https://www.signl4.com/wp-json/two-factor/user-info (only untested registered REST read left on signl4.com estate; 200 = 2FA-status/user-meta disclos
- NEXT(hypotheses-nemotron3.txt): PROBE: GET https://devconnect.signl4.com/identity/.well-known/openid-configuration && GET https://devconnect.signl4.com/identity/.well-known/jwks.json && GET ht
- LEARN: ACCEPTED AUTH @ devconnect.signl4.com: staging IdentityServer live + shares prod RS256 signing key (kid/n/x5t/x5c identical) and account-portal client_id 692A0A
- LEARN: ACCEPTED MISCONFIG @ labconnect/labaccount.signl4.com: Azure AppGW/v2 502 on all probed paths (root, /identity/, /connect/authorize) — unmapped backend, estate 
- LEARN: ACCEPTED MISCONFIG @ api.signl4.com: /api/v2 = alerts(405)+teams(401 Bearer) only; no unauth read surface; root 301 → account.signl4.com/manage
- LEARN: REJECTED AUTH @ www.signl4.com: WP users/media REST is public-blog-only; users/1 no email/PII — same low value as derdack.com
- LEARN: ACCEPTED MISCONFIG @ www.signl4.com: WPML ate/proxy 401, wpaas activity-logs 401, divitorque settings 401 (gated); wpml-ph-make-external-request + wpaas diagnos
- LEARN: ACCEPTED AUTH @ devconnect.signl4.com: SIGNL4 dev/lab OIDC+account staging estate resolves on dedicated IPs (dev 108.143.123.104, lab 13.93.49.201); CSP explici
- LEARN: ACCEPTED MISCONFIG @ api.signl4.com: /api/v2/alerts returns 405 Allow:POST confirming live API namespace; base routes unprobed for GET
- LEARN: ACCEPTED AUTH @ www.signl4.com: CF-fronted WordPress confirmed via xmlrpc pingback link; same fleet family as derdack.com
- LEARN: REJECTED IDOR @ www.derdack.com revisions/autosaves: all protected endpoints return 401; capability check intact
- LEARN: REJECTED IDOR @ www.derdack.com users/{id} PII: collection exposes no email; single endpoint unlikely to differ
- LEARN: ACCEPTED MISCONFIG @ dev.derdack.com: 300 Multiple Choices with sensitive path suggestions confirms Apache mod_negotiation/MultiViews; passive probe cost near-z
- LEARN: ACCEPTED MISCONFIG @ blog.derdack.com & techblog.derdack.com: HTTPS redirects to HTTP (downgrade chain) — mixed content risk confirmed
- LEARN: ACCEPTED MISCONFIG @ www.derdack.com: Missing HSTS, CSP, X-Frame-Options on primary domain
- LEARN: ACCEPTED AUTH @ www.derdack.com: WP REST API auth gates intact on settings/users/me/oembed-proxy/drafts/CF7/Yoast admin (401/403/400)
- LEARN: ACCEPTED AUTH @ devconnect.signl4.com: staging IdentityServer live + shares prod RS256 signing key (kid/n/x5t/x5c identical) and account-portal client_id 692A0A
- LEARN: ACCEPTED MISCONFIG @ labconnect/labaccount.signl4.com: Azure AppGW/v2 502 on all probed paths (root, /identity/, /connect/authorize) — unmapped backend, estate 
- LEARN: ACCEPTED MISCONFIG @ api.signl4.com: /api/v2 = alerts(405)+teams(401 Bearer) only; no unauth read surface; root 301 → account.signl4.com/manage
- LEARN: REJECTED AUTH @ www.signl4.com: WP users/media REST is public-blog-only; users/1 no email/PII — same low value as derdack.com
- LEARN: ACCEPTED MISCONFIG @ www.signl4.com: WPML ate/proxy 401, wpaas activity-logs 401, divitorque settings 401 (gated); wpml-ph-make-external-request + wpaas diagnos
- LEARN: ACCEPTED AUTH @ devconnect.signl4.com: SIGNL4 dev/lab OIDC+account staging estate resolves on dedicated IPs (dev 108.143.123.104, lab 13.93.49.201); CSP explici
- LEARN: ACCEPTED MISCONFIG @ api.signl4.com: /api/v2/alerts returns 405 Allow:POST confirming live API namespace; base routes unprobed for GET
- LEARN: ACCEPTED AUTH @ www.signl4.com: CF-fronted WordPress confirmed via xmlrpc pingback link; same fleet family as derdack.com
- LEARN: ACCEPTED AUTH @ www.derdack.com/de/: xmlrpc.php fully functional (200, full method list) while root xmlrpc is 503-blocked — endpoint exposure anomaly on multisi
- LEARN: ACCEPTED AUTH @ www.derdack.com/ea/: xmlrpc.php POST returns full method list (GET returns 405) — /ea/ also exposed, not just /de/
- LEARN: REJECTED SSRF @ www.derdack.com/de/: pingback.ping to 169.254.169.254 returns faultCode 0 empty — ambiguous, not confirmed SSRF
- LEARN: REJECTED MISCONFIG @ www.derdack.com/ea/: Whitepaper_test.pdf not found in media library — hypothesis invalidated
- LEARN: REJECTED brute-force @ all: program explicitly excludes rate-limit/lockout testing
- LEARN: REJECTED OPTIONS/TRACE @ all: program explicitly excludes OPTIONS/TRACE as standalone findings
- LEARN: REJECTED OTHER @ signl4.derdack.com: permanently unreachable across 8+ probe cycles (all TCP timeout); all attack surface value = 0
- LEARN: REJECTED IDOR @ www.derdack.com revisions/autosaves: all protected endpoints return 401; capability check intact
- LEARN: REJECTED IDOR @ www.derdack.com users/{id} PII: collection exposes no email; single endpoint unlikely to differ
- LEARN: ACCEPTED MISCONFIG @ dev.derdack.com: 300 Multiple Choices with sensitive path suggestions confirms Apache mod_negotiation/MultiViews; passive probe cost near-z
- LEARN: ACCEPTED MISCONFIG @ blog.derdack.com & techblog.derdack.com: HTTPS redirects to HTTP (downgrade chain) — mixed content risk confirmed
- LEARN: ACCEPTED MISCONFIG @ www.derdack.com: Missing HSTS, CSP, X-Frame-Options on primary domain
- LEARN: ACCEPTED AUTH @ www.derdack.com: WP REST API auth gates intact on settings/users/me/oembed-proxy/drafts/CF7/Yoast admin (401/403/400)

## RANKED HYPOTHESES 2026-09-05 12:19:18 UTC
- [85] devconnect.signl4.com/identity/.well-known/openid-configuration: SIGNL4 devconnect staging IdentityServer shares PROD RS256 signing key enabling cross-env token forgery (from art/lead_nemotron3.txt)
- [30] signl4.derdack.com: SIGNL4 API authentication bypass (from art/lead_bigpickle.txt)
- NEXT(hypotheses-bigpickle.txt): PROBE: Passive HTTP probing of all 9 inventory hosts to confirm live status, identify technologies, and discover API endpoints. Start with signl4.derdack.com (h
- NEXT(hypotheses-nemotron3.txt): PROBE: GET https://devconnect.signl4.com/identity/.well-known/openid-configuration && GET https://devconnect.signl4.com/identity/.well-known/jwks.json && GET ht
- LEARN: ACCEPTED AUTH @ signl4.derdack.com: SaaS platform target, worth investigating API auth after passive probing confirms endpoints
- LEARN: REJECTED brute-force @ all: program explicitly excludes brute-force/rate-limit/lockout policy testing
- LEARN: ACCEPTED AUTH @ devconnect.signl4.com: staging IdentityServer live + shares prod RS256 signing key (kid/n/x5t/x5c identical) and account-portal client_id 692A0A
- LEARN: ACCEPTED MISCONFIG @ labconnect/labaccount.signl4.com: Azure AppGW/v2 502 on all probed paths (root, /identity/, /connect/authorize) — unmapped backend, estate 
- LEARN: ACCEPTED MISCONFIG @ api.signl4.com: /api/v2 = alerts(405)+teams(401 Bearer) only; no unauth read surface; root 301 → account.signl4.com/manage
- LEARN: REJECTED AUTH @ www.signl4.com: WP users/media REST is public-blog-only; users/1 no email/PII — same low value as derdack.com
- LEARN: ACCEPTED MISCONFIG @ www.signl4.com: WPML ate/proxy 401, wpaas activity-logs 401, divitorque settings 401 (gated); wpml-ph-make-external-request + wpaas diagnos
- LEARN: ACCEPTED AUTH @ devconnect.signl4.com: staging IdentityServer live + shares prod RS256 signing key (kid/n/x5t/x5c identical) and account-portal client_id 692A0A
- LEARN: ACCEPTED MISCONFIG @ labconnect/labaccount.signl4.com: Azure AppGW/v2 502 on all probed paths (root, /identity/, /connect/authorize) — unmapped backend, estate 
- LEARN: ACCEPTED MISCONFIG @ api.signl4.com: /api/v2 = alerts(405)+teams(401 Bearer) only; no unauth read surface; root 301 → account.signl4.com/manage
- LEARN: REJECTED AUTH @ www.signl4.com: WP users/media REST is public-blog-only; users/1 no email/PII — same low value as derdack.com
- LEARN: ACCEPTED MISCONFIG @ www.signl4.com: WPML ate/proxy 401, wpaas activity-logs 401, divitorque settings 401 (gated); wpml-ph-make-external-request + wpaas diagnos
- LEARN: ACCEPTED AUTH @ devconnect.signl4.com: SIGNL4 dev/lab OIDC+account staging estate resolves on dedicated IPs (dev 108.143.123.104, lab 13.93.49.201); CSP explici
- LEARN: ACCEPTED MISCONFIG @ api.signl4.com: /api/v2/alerts returns 405 Allow:POST confirming live API namespace; base routes unprobed for GET
- LEARN: ACCEPTED AUTH @ www.signl4.com: CF-fronted WordPress confirmed via xmlrpc pingback link; same fleet family as derdack.com
- LEARN: REJECTED IDOR @ www.derdack.com revisions/autosaves: all protected endpoints return 401; capability check intact
- LEARN: REJECTED IDOR @ www.derdack.com users/{id} PII: collection exposes no email; single endpoint unlikely to differ
- LEARN: ACCEPTED MISCONFIG @ dev.derdack.com: 300 Multiple Choices with sensitive path suggestions confirms Apache mod_negotiation/MultiViews; passive probe cost near-z
- LEARN: ACCEPTED MISCONFIG @ blog.derdack.com & techblog.derdack.com: HTTPS redirects to HTTP (downgrade chain) — mixed content risk confirmed
- LEARN: ACCEPTED MISCONFIG @ www.derdack.com: Missing HSTS, CSP, X-Frame-Options on primary domain
- LEARN: ACCEPTED AUTH @ www.derdack.com: WP REST API auth gates intact on settings/users/me/oembed-proxy/drafts/CF7/Yoast admin (401/403/400)
- LEARN: ACCEPTED AUTH @ devaccount.signl4.com: staging account portal live → devconnect authorize w/ SAME client_id 692A0A56- + scopes (account_portal, public_api_read/
- LEARN: ACCEPTED MISCONFIG @ api.signl4.com: registered route population = alerts(405 POST), teams/webhooks/subscriptions(401 Bearer), csp/report(405 POST sink); all ot
- LEARN: ACCEPTED OTHER @ s4dev1-8.enterprisealert.com: CSP-referenced staging alert fleet resolves 4.207.244.99, 404 root / 504 on identity+webhook+api paths (live fron
- LEARN: ACCEPTED AUTH @ www.signl4.com: two-factor/user-info 401 rest_forbidden — gated, no 2FA-status disclosure
- LEARN: REJECTED MISCONFIG @ devconnect.signl4.com: algs=['RS256'] only + no JWT alg-confusion surface on staging IdP
- LEARN: ACCEPTED AUTH @ devconnect.signl4.com: staging IdentityServer live + shares prod RS256 signing key (kid/n/x5t/x5c identical) and account-portal client_id 692A0A
- LEARN: ACCEPTED MISCONFIG @ labconnect/labaccount.signl4.com: Azure AppGW/v2 502 on all probed paths (root, /identity/, /connect/authorize) — unmapped backend, estate 
- LEARN: ACCEPTED MISCONFIG @ api.signl4.com: /api/v2 = alerts(405)+teams(401 Bearer) only; no unauth read surface; root 301 → account.signl4.com/manage
- LEARN: REJECTED AUTH @ www.signl4.com: WP users/media REST is public-blog-only; users/1 no email/PII — same low value as derdack.com
- LEARN: ACCEPTED MISCONFIG @ www.signl4.com: WPML ate/proxy 401, wpaas activity-logs 401, divitorque settings 401 (gated); wpml-ph-make-external-request + wpaas diagnos
- LEARN: ACCEPTED AUTH @ devconnect.signl4.com: SIGNL4 dev/lab OIDC+account staging estate resolves on dedicated IPs (dev 108.143.123.104, lab 13.93.49.201); CSP explici
- LEARN: ACCEPTED MISCONFIG @ api.signl4.com: /api/v2/alerts returns 405 Allow:POST confirming live API namespace; base routes unprobed for GET
- LEARN: ACCEPTED AUTH @ www.signl4.com: CF-fronted WordPress confirmed via xmlrpc pingback link; same fleet family as derdack.com
- LEARN: REJECTED IDOR @ www.derdack.com revisions/autosaves: all protected endpoints return 401; capability check intact
- LEARN: REJECTED IDOR @ www.derdack.com users/{id} PII: collection exposes no email; single endpoint unlikely to differ
- LEARN: ACCEPTED MISCONFIG @ dev.derdack.com: 300 Multiple Choices with sensitive path suggestions confirms Apache mod_negotiation/MultiViews; passive probe cost near-z
- LEARN: ACCEPTED MISCONFIG @ blog.derdack.com & techblog.derdack.com: HTTPS redirects to HTTP (downgrade chain) — mixed content risk confirmed
- LEARN: ACCEPTED MISCONFIG @ www.derdack.com: Missing HSTS, CSP, X-Frame-Options on primary domain
- LEARN: ACCEPTED AUTH @ www.derdack.com: WP REST API auth gates intact on settings/users/me/oembed-proxy/drafts/CF7/Yoast admin (401/403/400)
- LEARN: ACCEPTED AUTH @ www.derdack.com/de/: xmlrpc.php fully functional (200, full method list) while root xmlrpc is 503-blocked — endpoint exposure anomaly on multisi
- LEARN: ACCEPTED AUTH @ www.derdack.com/ea/: xmlrpc.php POST returns full method list (GET returns 405) — /ea/ also exposed, not just /de/
- LEARN: REJECTED SSRF @ www.derdack.com/de/: pingback.ping to 169.254.169.254 returns faultCode 0 empty — ambiguous, not confirmed SSRF
- LEARN: REJECTED MISCONFIG @ www.derdack.com/ea/: Whitepaper_test.pdf not found in media library — hypothesis invalidated
- LEARN: REJECTED brute-force @ all: program explicitly excludes rate-limit/lockout testing
- LEARN: REJECTED OPTIONS/TRACE @ all: program explicitly excludes OPTIONS/TRACE as standalone findings
- LEARN: REJECTED OTHER @ signl4.derdack.com: permanently unreachable across 8+ probe cycles (all TCP timeout); all attack surface value = 0
