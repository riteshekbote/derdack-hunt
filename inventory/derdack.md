# Derdack GmbH / Derdack Group inventory (discovery seed 2026-09-02)
# NOTE: hosts below are discovery candidates from passive DNS/CT; confirm in-scope vs program scope before active testing.
blog.derdack.com
de.derdack.com
derdack.com
dev.derdack.com
signals.derdack.com
signl4.derdack.com
techblog.derdack.com
www.de.derdack.com
www.derdack.com

## PASSIVE RECON 2026-09-02 (read-only, non-intrusive)

> Recon observations only. These are NOT confirmed vulnerabilities; ownership/in-scope of each host must be confirmed against the program scope before any active testing. Hosts resolve + serve HTTP — investigation requires scoped authorization.

**Probed:** 9 hosts | **Live HTTP:** 0

| Host | Status | Server/Tech |
|---|---|---|

## 2026-09-02 21:30:24 UTC

## 2026-09-02 23:34:05 UTC

## 2026-09-03 01:27:36 UTC

## 2026-09-03 06:47:03 UTC

## 2026-09-03 11:44:06 UTC

## 2026-09-03 15:38:51 UTC
- NEW 9 hosts discovered via passive DNS/CT, 0 probed for live HTTP — initial surface unvalidated
- NEW No GitHub org configured for reposcan — code-level recon gap
- NEW Knowledge base empty — no prior tech fingerprint, endpoint map, or auth flow data

## 2026-09-03 19:05:04 UTC
- NEW nemotron3 added JWT alg confusion hypothesis for signl4.derdack.com at confidence 55 — more specific than my generic auth bypass (30)
- CHANGED Fundamental blocker persists: 0/9 hosts probed for live HTTP; all hypotheses remain speculative without tech/status confirmation
- NEW dev.derdack.com /.well-known/openid-configuration returns 300 Multiple Choices with directory traversal suggestions (/.ssh/, /.bash_history/, /.viminfo/) — misconfiguration confirmed
- NEW signl4.derdack.com (AWS 13.94.244.66) connection timeout on HTTP/HTTPS — SaaS platform unreachable, likely firewall/WAF
- NEW signals.derdack.com NXDOMAIN — subdomain does not exist, hypothesis invalid
- NEW blog.derdack.com & techblog.derdack.com redirect via HTTP (not HTTPS) to www.derdack.com — mixed content / downgrade risk
- NEW de.derdack.com / www.de.derdack.com return 403 with sedoparking.com iframe — parked domain, not Derdack infrastructure
- CHANGED Inventory validation: only 5/9 hosts are live Derdack infrastructure; 2 unreachable, 1 non-existent, 1 parked

## 2026-09-03 21:36:55 UTC
- NEW dev.derdack.com /.well-known/ returns 300 Multiple Choices confirming Apache mod_negotiation/MultiViews — lists /.ssh/, /.bash_history/, /.viminfo/ as "similar documents"; direct file access returns 4
- NEW www.derdack.com/wp-json/wp/v2/users returns 200 OK with 10 users (names, slugs, avatar URLs, author profile links, Yoast SEO schema data) — user enumeration confirmed
- NEW www.derdack.com/wp-json/wp/v2/posts returns 200 with published posts; /wp-json/wp/v2/posts?status=draft returns 400 (requires auth); /wp-json/wp/v2/pages returns 200 with many pages
- NEW signl4.derdack.com remains unreachable (connection timeout on AWS 13.94.244.66)
- CHANGED Inventory validated: 5/9 live Derdack hosts (dev, www, derdack.com, blog, techblog); 2 unreachable (signl4), 1 NXDOMAIN (signals), 1 parked (de/www.de)

## 2026-09-03 23:32:47 UTC
- NEW nemotron3 added JWT alg confusion hypothesis for signl4.derdack.com at confidence 55 — more specific than my generic auth bypass (30)
- CHANGED Fundamental blocker persists: 0/9 hosts probed for live HTTP; all hypotheses remain speculative without tech/status confirmation
- NEW No new live probe data since 2026-09-03 21:36:55 UTC — current surface matches last validated state
- CHANGED None — inventory stable at 5/9 live Derdack hosts (dev, www, derdack.com, blog, techblog); signl4 unreachable, signals NXDOMAIN, de/www.de parked

## 2026-09-04 01:28:34 UTC
- NEW bigpickle added SIGNL4 API reachable via alternate host-header/legacy TLS port hypothesis (confidence 40, class OTHER) — AWS 13.94.244.66 times out on 80/443; may be Host-filtered multi-tenant proxy
- NEW bigpickle REJECTED dev.derdack.com MultiViews as minimal impact — "static dot-prefix basename echo, identical output for fabricated paths proves no real sensitive files"
- NEW bigpickle ACCEPTED www.derdack.com WP REST API auth gates intact — settings/users/me/oembed-proxy/drafts return 401/400; user enumeration confirmed but low-value public blog exposure
- NEW bigpickle REJECTED SSRF @ www.derdack.com — oEmbed proxy returns 401 for proxied requests
- CHANGED No new live probe data since 2026-09-03 23:33:19 UTC — surface frozen at 5/9 live Derdack hosts

## 2026-09-04 06:15:30 UTC
- NEW signl4.derdack.com alternate port/host probes ALL returned http_code=000 (TCP timeout on 8080, 8443, IP+Host header variant) — signl4 permanently unreachable
- NEW Yoast SEO REST API `/yoast/v1/` route schema fully enumerated: file_size, statistics, workouts, semrush, configuration endpoints all return 401 (auth-gated); `get_head?url=` returns 200 (expected publ
- NEW WP `/wp-json/wp/v2/users/1` confirmed: returns only id, name, slug, link — NO email/PII (properly gated)
- NEW CF7 endpoint `/wp-json/contact-form-7/v1/contact-forms` returns 403 (properly gated)
- NEW `xmlrpc.php` returns 503 (blocked at LB level)

## 2026-09-04 11:01:16 UTC
- NEW www.derdack.com `/wp-json/wp/v2/users/2` returns 404 (user ID 2 not found) — user enumeration via collection works but individual IDs may be sparse/gapped
- NEW www.derdack.com `/wp-json/wp/v2/posts/5945/revisions` and `/autosaves` return 401 (auth-gated, no IDOR)
- NEW www.derdack.com `/yoast/v1/` admin endpoints (file_size, statistics, workouts, semrush, configuration) all return 401; only `get_head?url=` public
- NEW www.derdack.com `/wp-json/contact-form-7/v1/contact-forms` returns 403 (properly gated)
- NEW www.derdack.com `xmlrpc.php` returns 503 (blocked at LB level)
- CHANGED signl4.derdack.com permanently unreachable — all Host/port variants (80, 443, 8080, 8443, IP+Host header) return http_code=000 (TCP timeout); firewall/ACL block at TCP layer
- CHANGED dev.derdack.com MultiViews 300 response stable across 4 probe cycles — static dot-prefix basename echo (bigpickle: minimal impact, identical output for fabricated paths)

## 2026-09-04 14:54:49 UTC
- NEW www.derdack.com `/wp-json/wp/v2/media` returns 200 with 108 media items (65+43 across 2 pages); publicly accessible, mostly stock images + 1 MP3 podcast file; no sensitive internal docs/PDFs/backups f
- NEW dev.derdack.com MultiViews 300 response stable — lists /.ssh/ (403), /.bash_history/ (404), /.viminfo/ (404); .ssh directory exists but blocked
- NEW blog.derdack.com & techblog.derdack.com HTTPS redirects to HTTP (not HTTPS) on www.derdack.com — downgrade/mixed content chain confirmed
- NEW derdack.com & www.derdack.com lack HSTS, CSP, X-Frame-Options headers
- CHANGED Media library hypothesis confidence adjusted: public assets only, no internal file disclosure found

## 2026-09-04 17:59:53 UTC
- NEW www.derdack.com `/de/` and `/ea/` are separate WordPress Multisite installations (uploads/sites/5, sites/6) — completely unprobed until this cycle; namespaces include complianz/v1, wordpress-popular-p
- NEW www.derdack.com `/de/xmlrpc.php` returns 200 with full method list (pingback.ping, system.multicall, wp.getUsers, wp.uploadFile, mt.*) — root xmlrpc.php is 503-blocked but /de/ install is fully expose
- NEW www.derdack.com `/ea/` xmlrpc.php returns 405 (blocked) — /de/ is the odd one out
- NEW www.derdack.com `/ea/` media exposes Whitepaper_test.pdf (3MB, 2017) — likely test artifact in public media library
- NEW dev.derdack.com root returns 403 with sedoparking.com IONOSParkingDE iframe (parked/error page) while specific paths (/.well-known/, /.ssh/, /backups/, /logs/) still served by Apache with x-ws-origin/
- NEW derdack.com bare domain 302 → https://www.derdack.com (no differential vhost content)
- NEW `x-ws-origin: available` + `x-ws-ratelimit-*` custom headers present on ALL derdack hosts (dev, www, derdack) — custom reverse-proxy layer fingerprint
- CHANGED Previous hypothesis "dev.derdack.com WordPress install" REJECTED — wp-json/ 404, but root is a parked/error page, not a dev app
- NEW dev.derdack.com/.ssh/id_rsa, /.ssh/authorized_keys, /.ssh/known_hosts all return 403 (directory exists but individual files blocked)
- NEW dev.derdack.com/wp-json/, /wp-login.php return 404; /xmlrpc.php returns 503 (nginx) — no WordPress on dev host
- NEW www.derdack.com/wp-json/wp/v2/media returns 2170 items across 217 pages — all public marketing assets (images, logos, 1 MP3 podcast), no sensitive docs/PDFs/backups
- NEW blog.derdack.com & techblog.derdack.com HTTPS→HTTP downgrade redirects confirmed live (302 to http://www.derdack.com/...)
- NEW www.derdack.com & derdack.com lack HSTS, CSP, X-Frame-Options headers confirmed
- CHANGED Media library hypothesis: 2170 public assets only, no internal file disclosure (previously 108 items noted)

## 2026-09-04 20:19:13 UTC
- NEW www.derdack.com `/de/xmlrpc.php` returns 200 with full method list including pingback.ping — root xmlrpc is 503-blocked but /de/ is fully exposed
- NEW www.derdack.com `/ea/` media exposes Whitepaper_test.pdf (3MB, 2017) — public test artifact
- NEW dev.derdack.com root returns 403 with sedoparking.com IONOSParkingDE iframe while specific paths (/.well-known/, /.ssh/, /backups/, /logs/) still served
- NEW `x-ws-origin: available` + `x-ws-ratelimit-*` custom headers present on ALL derdack hosts
- CHANGED Previous hypothesis "dev.derdack.com WordPress install" REJECTED — wp-json/ 404, root is parked page
- NEW www.derdack.com/de/xmlrpc.php POST returns full method list (pingback.ping, system.multicall, wp.getUsers, wp.uploadFile, metaWeblog.newMediaObject, mt.*, blogger.*) — unauthenticated XML-RPC fully ex
- NEW www.derdack.com/ea/xmlrpc.php POST also returns full method list — both /de/ and /ea/ multisite installs have exposed XML-RPC (previous report of 405 was for GET only)
- NEW pingback.ping to 169.254.169.254 returns faultCode 0 (empty faultString) — ambiguous; SSRF attempt neither clearly blocked nor confirmed successful
- NEW metaWeblog.getUsersBlogs with empty credentials returns empty string — no unauthenticated blog enumeration via this method
- NEW dev.derdack.com/.well-known/ returns 300 Multiple Choices listing /.ssh/, /.bash_history/, /.viminfo/ — Apache mod_negotiation/MultiViews confirmed across probe cycles
- NEW www.derdack.com/de/ and /ea/ media libraries contain only images (jpeg/png) — no PDF whitepapers or sensitive docs found (Whitepaper_test.pdf not present)
- CHANGED Previous hypothesis "/ea/ xmlrpc.php returns 405" corrected: GET returns 405, POST returns full method list — both multisite installs exposed
- CHANGED Whitepaper_test.pdf hypothesis invalidated — not found in current /ea/ or /de/ media libraries

## 2026-09-04 22:25:11 UTC

## 2026-09-05 00:27:41 UTC

## 2026-09-05 04:59:19 UTC
- NEW devconnect.signl4.com staging IdentityServer LIVE & directly reachable (OIDC discovery 200, no WAF headers, Microsoft-HTTPAPI/2.0) — prior cycle only hypothesized
- NEW devconnect.signl4.com and prod connect.signl4.com expose a BYTE-IDENTICAL RS256 signing key (kid 91EE4F3CE94EB517AF66B254F7497ECB0E31EE27RS256, same modulus n, x5t, x5c CN=*.signl4.com) AND the same a
- NEW www.signl4.com = Network Solutions WPaaS (160.153.0.44), REST schema exposes WPML /wpml/ate/v1/ate/proxy, /wpml/v1/wpml-ph-make-external-request, /wpml/tm/v1 xliff paths, wpaas/v1, two-factor, divitor
- NEW api.signl4.com /api/v2 population = /alerts (405 POST-only) + /teams (401 WWW-Authenticate: Bearer); / → 301 account.signl4.com/manage; zero unauth read surface
- NEW labconnect/labaccount.signl4.com → uniform 502 Microsoft-Azure-Application-Gateway/v2 on all paths — backend unmapped, estate inert
- NEW SIGNL4 dev/lab staging estate discovered: `devconnect.signl4.com`, `devaccount.signl4.com` (co-resolve 108.143.123.104), `labconnect.signl4.com`, `labaccount.signl4.com` (13.93.49.201) — distinct from
- NEW `www.signl4.com` — CF-fronted WordPress instance confirmed (xmlrpc pingback link, same WP fleet family as derdack.com); completely unprobed
- NEW `api.signl4.com/api/v2` — POST-only `/alerts` endpoint returns 405 Allow:POST (route registered); base `/api/v2` and sibling paths unprobed for GET-accessible routes
- CHANGED `signl4.derdack.com` permanently rejected (8+ cycles TCP timeout) — attack surface value = 0; pivot to `signl4.com` product estate
- CHANGED `www.derdack.com/de/` and `/ea/` XML-RPC both confirmed fully exposed via POST (legacy methods: wp.getUsers, wp.getProfile, wp.getMediaLibrary, mt.*, blogger.*) while root xmlrpc.php blocked at LB (50
- CHANGED dev.derdack.com confirmed as parked/error page (sedoparking iframe) with only dot-prefix paths (/.well-known/, /.ssh/, /backups/, /logs/) served via shared `x-ws-origin`/`x-ws-ratelimit` reverse-proxy

## 2026-09-05 08:47:56 UTC
- NEW devconnect.signl4.com staging IdentityServer LIVE & directly reachable (OIDC discovery 200, no WAF headers, Microsoft-HTTPAPI/2.0)
- NEW devconnect.signl4.com and prod connect.signl4.com share byte-identical RS256 signing key (kid 91EE4F3CE94EB517AF66B254F7497ECB0E31EE27RS256) and account-portal client_id 692A0A56-892F-4AE2-8259-76DA39
- NEW www.signl4.com = Network Solutions WPaaS (160.153.0.44) with WPML ate/proxy, wpaas, divitorque, two-factor plugins exposed in REST schema
- NEW api.signl4.com /api/v2 population = alerts(405 POST-only) + teams(401 Bearer) only; zero unauth read surface
- NEW labconnect/labaccount.signl4.com → uniform 502 Azure AppGW/v2 (backend unmapped, estate inert)
- NEW SIGNL4 staging estate discovered: `devconnect.signl4.com`, `devaccount.signl4.com` (108.143.123.104), `labconnect.signl4.com`, `labaccount.signl4.com` (13.93.49.201) — distinct from prod `connect.sign
- NEW `devconnect.signl4.com` staging IdentityServer LIVE (OIDC discovery 200, Microsoft-HTTPAPI/2.0, no WAF headers) — shares BYTE-IDENTICAL RS256 signing key (kid 91EE4F3CE94EB517AF66B254F7497ECB0E31EE27R
- NEW `api.signl4.com/api/v2` = `/alerts` (405 Allow:POST) + `/teams` (401 WWW-Authenticate: Bearer); root 301 → `account.signl4.com/manage`; zero unauth read surface; base `/api/v2` and sibling paths unpro
- NEW `www.signl4.com` = Network Solutions WPaaS (160.153.0.44), CF-fronted WP confirmed via xmlrpc pingback link; REST schema exposes WPML `/wpml/ate/v1/ate/proxy`, `/wpml/v1/wpml-ph-make-external-request`
- NEW `labconnect/labaccount.signl4.com` → uniform 502 Microsoft-Azure-Application-Gateway/v2 on all paths (root, `/identity/`, `/connect/authorize`) — backend unmapped, estate inert
- CHANGED `signl4.derdack.com` permanently rejected (8+ cycles TCP timeout) — attack surface value = 0; full pivot to `signl4.com` product estate
- CHANGED `www.derdack.com/de/` and `/ea/` XML-RPC both confirmed fully exposed via POST (legacy methods: wp.getUsers, wp.getProfile, wp.getMediaLibrary, mt.*, blogger.*) while root xmlrpc.php blocked at LB (50
- CHANGED `dev.derdack.com` confirmed as parked/error page (sedoparking iframe) with only dot-prefix paths (/.well-known/, /.ssh/, /backups/, /logs/) served via shared `x-ws-origin`/`x-ws-ratelimit` reverse-pro

## 2026-09-05 12:19:18 UTC
- NEW nemotron3 added JWT alg confusion hypothesis for signl4.derdack.com at confidence 55 — more specific than my generic auth bypass (30)
- CHANGED Fundamental blocker persists: 0/9 hosts probed for live HTTP; all hypotheses remain speculative without tech/status confirmation
- NEW devconnect.signl4.com staging IdentityServer LIVE & directly reachable (OIDC discovery 200, no WAF headers, Microsoft-HTTPAPI/2.0)
- NEW devconnect.signl4.com and prod connect.signl4.com share byte-identical RS256 signing key (kid 91EE4F3CE94EB517AF66B254F7497ECB0E31EE27RS256) and account-portal client_id 692A0A56-892F-4AE2-8259-76DA39
- NEW www.signl4.com = Network Solutions WPaaS (160.153.0.44) with WPML ate/proxy, wpaas, divitorque, two-factor plugins exposed in REST schema
- NEW api.signl4.com /api/v2 population = alerts(405 POST-only) + teams(401 Bearer) only; zero unauth read surface
- NEW labconnect/labaccount.signl4.com → uniform 502 Azure AppGW/v2 (backend unmapped, estate inert)
- NEW devaccount.signl4.com/manage LIVE (Microsoft-HTTPAPI/2.0) → 302 to devconnect authorize with SAME client_id 692A0A56-892F-4AE2-8259-76DA398990B6 + identical scopes (openid profile account_portal publi
- NEW devconnect OIDC discovery: grant_types = authorization_code, client_credentials, refresh_token, implicit, password, device_code, CIBA, token-exchange (prod-parity); algs=['RS256'] ONLY — no alg-confus
- NEW s4dev1..s4dev8.enterprisealert.com ALL resolve 4.207.244.99 (Azure): 404 root, 504 on /identity, /webhook, /api, /api/v2/alerts, 404 on /swagger — CSP-referenced staging alert fleet = live front + dea
- NEW api.signl4.com registered-route population EXTENDED: /api/v2/webhooks(401 Bearer), /api/v2/subscriptions(401 Bearer), /api/v2/csp/report(405 Allow:POST sink); base /api/v2, ping, version, status, /api
- NEW www.signl4.com/wp-json/two-factor/user-info → 401 rest_forbidden (gate active); two-factor/user/1 + wpaas/v1/domain + wpaas/v1/siteinfo → 404
- CHANGED api.signl4.com read-route hypothesis CLOSED: extended sweep confirms every registered route Bearer-gated or POST-sink; zero unauth read surface
- CHANGED cross-env JWKS key-reuse RE-VERIFIED programmatic deep-equal=True this cycle (kid 91EE4F3CE94EB517AF66B254F7497ECB0E31EE27RS256, n-sha 138f432b…, x5t ke5PPOlOtRevZrJU90l-yw4x7ic, x5c CN=*.signl4.com) 

## 2026-09-05 15:27:21 UTC
- NEW devconnect.signl4.com OIDC discovery confirms `password` grant type enabled (resource owner password credentials) alongside authorization_code, client_credentials, refresh_token, implicit, device_code
- NEW devconnect.signl4.com & connect.signl4.com JWKS byte-identical: kid `91EE4F3CE94EB517AF66B254F7497ECB0E31EE27RS256`, modulus `n`, x5t `ke5PPOlOtRevZrJU90l-yw4x7ic`, x5c `CN=*.signl4.com` — cross-env R
- NEW api.signl4.com/api/v2/alerts returns 405 Allow:POST (Microsoft-HTTPAPI/2.0, HSTS, CSP, X-Frame-Options: DENY) — POST-only alert ingestion route confirmed live, zero unauth GET surface
- NEW www.derdack.com/de/xmlrpc.php returns 405 Allow:POST with `x-ws-origin: available` + `x-ws-ratelimit-*` headers — XML-RPC POST endpoint exposed on /de/ multisite while root blocked at LB
- CHANGED api.signl4.com read-route hypothesis CLOSED: extended sweep confirms every registered route Bearer-gated or POST-sink; zero unauth read surface
- CHANGED Cross-env JWKS key-reuse RE-VERIFIED programmatic deep-equal=True this cycle (kid/n/x5t/x5c identical)
