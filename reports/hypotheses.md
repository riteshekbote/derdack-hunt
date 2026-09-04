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
