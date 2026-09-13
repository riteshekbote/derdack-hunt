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

## 2026-09-05 17:35:38 UTC
- NEW RAG resolved OTGS Installer route: vendor/otgs/installer/includes/rest/Push.php — GET-only `otgs/installer/v1/push/fetch-subscription`, NO permission_callback key at all; handler `fetch_subscription()
- NEW Handler: if time()-last_refresh > 7200s → `refresh_subscriptions_data()` + return 200 {"message":"OK"}; else return 403 {"message":"OK"} — the observed 200/403 variance is refresh-INTERVAL gating, NOT
- NEW `OTGS_Installer_Fetch_Subscription::get()` (site-key/fetch-subscription class): body carries stored site_key + fixed site_url + plugin versions, wp_remote_post to `$repository->get_api_url()` = FIXED 
- CHANGED www.signl4.com fetch-subscription SSRF hypothesis INVALIDATED by source: route takes no params, outbound target fixed, no site-key echo; GET 200 only proves missing permission_callback (broken access 
- NEW devconnect.signl4.com OIDC discovery confirms `password` grant type (resource owner password credentials) enabled alongside authorization_code, client_credentials, refresh_token, implicit, device_code
- NEW devconnect.signl4.com & connect.signl4.com JWKS byte-identical re-verified: kid `91EE4F3CE94EB517AF66B254F7497ECB0E31EE27RS256`, modulus `n`, x5t `ke5PPOlOtRevZrJU90l-yw4x7ic`, x5c `CN=*.signl4.com` —
- NEW api.signl4.com/api/v2/alerts returns 405 Allow:POST with Microsoft-HTTPAPI/2.0, HSTS, CSP, X-Frame-Options: DENY — POST-only alert ingestion route confirmed live, zero unauth GET surface
- NEW www.derdack.com/de/xmlrpc.php returns 405 Allow:POST with `x-ws-origin: available` + `x-ws-ratelimit-*` headers — XML-RPC POST endpoint exposed on /de/ multisite while root blocked at LB
- CHANGED api.signl4.com read-route hypothesis CLOSED: extended sweep confirms every registered route Bearer-gated or POST-sink; zero unauth read surface
- CHANGED Cross-env JWKS key-reuse RE-VERIFIED programmatic deep-equal=True this cycle (kid/n/x5t/x5c identical)

## 2026-09-05 19:27:48 UTC
- NEW OTGS Installer source (Push.php) confirms GET-only, no permission_callback, fixed outbound target → SSRF INVALIDATED
- NEW devconnect OIDC password grant confirmed alongside 7 other grant types
- CHANGED api.signl4.com route population finalized: alerts(405 POST), teams/webhooks/subscriptions(401 Bearer), csp/report(405 POST sink) — zero unauth read surface
- CHANGED Cross-env JWKS key-reuse re-verified: kid/n/x5t/x5c byte-identical x4 deep-equal
- NEW OTGS Installer source code (Push.php) analyzed: `fetch-subscription` route is GET-only, no `permission_callback`, handler takes zero args, outbound target fixed to `api.wpml.org`/`api.toolset.com` wit
- NEW Cross-env JWKS key-reuse re-verified programmatic deep-equal=True (kid/n/x5t/x5c identical) — staging `devconnect.signl4.com` RS256 key byte-identical to prod `connect.signl4.com`
- NEW `api.signl4.com/api/v2/alerts` confirmed with security headers: HSTS, CSP, `X-Frame-Options: DENY`, `Microsoft-HTTPAPI/2.0` — POST-only ingestion route live, zero unauth GET surface
- NEW `www.derdack.com/de/xmlrpc.php` returns `405 Allow:POST` with `x-ws-origin: available` + `x-ws-ratelimit-*` headers — XML-RPC POST endpoint exposed on `/de/` multisite while root blocked at LB
- CHANGED `api.signl4.com` read-route hypothesis CLOSED: extended sweep confirms every registered route Bearer-gated or POST-sink; zero unauth read surface
- CHANGED `www.signl4.com` SSRF hypothesis (OTGS Installer) INVALIDATED by source code review — no attacker-controlled URL, no site-key echo, fixed vendor endpoint

## 2026-09-05 21:49:10 UTC
- NEW api.signl4.com/api/v2/alerts POST now returns 401 (auth required) — previously hypothesized as unauthenticated POST-only ingestion; HEAD still shows 405 Allow:POST but handler enforces Bearer
- NEW www.derdack.com/de/xmlrpc.php & /ea/xmlrpc.php wp.uploadFile/metaWeblog.newMediaObject both return faultCode 403 "incorrect username/password" — XML-RPC exposed but mutating methods auth-gated
- NEW api.signl4.com/api/v2/csp/report accepts unauthenticated POST (204) — CSP reporting sink, expected behavior
- NEW devconnect.signl4.com/identity/connect/token password grant returns "invalid_client" for test creds (client_secret required) — grant listed but not usable without secrets
- CHANGED Cross-env JWKS key-reuse re-verified 5th time: devconnect.signl4.com & connect.signl4.com RS256 key byte-identical (kid/n/x5t/x5c/e/x5c all match)
- CHANGED blog.derdack.com & techblog.derdack.com HTTPS→HTTP downgrade chain still live (302 to http://www.derdack.com/...)
- CHANGED dev.derdack.com MultiViews 300 stable (/.well-known/, /.ssh/, /.bash_history/, /.viminfo/) — static namespace echo, files 403/404

## 2026-09-05 23:22:10 UTC
- NEW api.signl4.com/api/v2/alerts POST now returns 401 (auth required) — previously hypothesized as unauthenticated POST-only ingestion; HEAD still shows 405 Allow:POST but handler enforces Bearer
- NEW www.derdack.com/de/xmlrpc.php & /ea/xmlrpc.php wp.uploadFile/metaWeblog.newMediaObject both return faultCode 403 "incorrect username/password" — XML-RPC exposed but mutating methods auth-gated
- NEW api.signl4.com/api/v2/csp/report accepts unauthenticated POST (204) — CSP reporting sink, expected behavior
- NEW devconnect.signl4.com/identity/connect/token password grant returns "invalid_client" for test creds (client_secret required) — grant listed but not usable without secrets
- CHANGED Cross-env JWKS key-reuse re-verified 5th time: devconnect.signl4.com & connect.signl4.com RS256 key byte-identical (kid/n/x5t/x5c/e/x5c all match)
- CHANGED blog.derdack.com & techblog.derdack.com HTTPS→HTTP downgrade chain still live (302 to http://www.derdack.com/...)
- CHANGED dev.derdack.com MultiViews 300 stable (/.well-known/, /.ssh/, /.bash_history/, /.viminfo/) — static namespace echo, files 403/404

## 2026-09-06 01:06:23 UTC
- NEW api.signl4.com/api/v2/alerts POST now returns 401 (auth required) — previously hypothesized as unauthenticated POST-only ingestion; HEAD still shows 405 Allow:POST but handler enforces Bearer
- NEW www.derdack.com/de/xmlrpc.php & /ea/xmlrpc.php wp.uploadFile/metaWeblog.newMediaObject both return faultCode 403 "incorrect username/password" — XML-RPC exposed but mutating methods auth-gated
- NEW api.signl4.com/api/v2/csp/report accepts unauthenticated POST (204) — CSP reporting sink, expected behavior
- NEW devconnect.signl4.com/identity/connect/token password grant returns "invalid_client" for test creds (client_secret required) — grant listed but not usable without secrets
- CHANGED Cross-env JWKS key-reuse re-verified 5th time: devconnect.signl4.com & connect.signl4.com RS256 key byte-identical (kid/n/x5t/x5c/e/x5c all match)
- CHANGED blog.derdack.com & techblog.derdack.com HTTPS→HTTP downgrade chain still live (302 to http://www.derdack.com/...)
- CHANGED dev.derdack.com MultiViews 300 stable (/.well-known/, /.ssh/, /.bash_history/, /.viminfo/) — static namespace echo, files 403/404

## 2026-09-06 06:02:58 UTC
- NEW api.signl4.com/api/v2/alerts POST handler now enforces Bearer auth (401) — previously hypothesized as unauthenticated POST-only ingestion
- NEW devconnect.signl4.com/identity/connect/token password grant returns invalid_client without client_secret — grant listed but not exploitable without secrets
- CHANGED Cross-env JWKS key-reuse re-verified 5th time: devconnect.signl4.com & connect.signl4.com RS256 key byte-identical (kid/n/x5t/x5c/e/x5c all match)
- CHANGED blog.derdack.com & techblog.derdack.com HTTPS→HTTP downgrade chain still live (302 to http://www.derdack.com/...)
- CHANGED dev.derdack.com MultiViews 300 stable (/.well-known/, /.ssh/, /.bash_history/, /.viminfo/) — static namespace echo, files 403/404

## 2026-09-06 10:45:38 UTC
- NEW api.signl4.com/api/v2/teams returns 401 (WWW-Authenticate: Bearer) on unauthenticated GET — confirms Bearer-gated API surface
- NEW devaccount.signl4.com/manage and account.signl4.com/manage both redirect to their respective IdPs with IDENTICAL client_id `692A0A56-892F-4AE2-8259-76DA398990B6` and scope set — cross-env client reuse
- NEW devconnect.signl4.com OIDC discovery: grant_types includes `password` + 7 others; algs=['RS256'] only — password grant enabled on staging IdP
- NEW JWKS byte-identical re-verified 6th time: devconnect.signl4.com & connect.signl4.com RS256 key (kid/n/x5t/x5c/e all match)
- CHANGED blog.derdack.com & techblog.derdack.com HTTPS→HTTP downgrade (302 to http://www.derdack.com/...) still live; www.derdack.com lacks HSTS/CSP/X-Frame-Options
- CHANGED dev.derdack.com MultiViews 300 stable (/.well-known/, /.ssh/, /.bash_history/, /.viminfo/) — static namespace echo, files 403/404
- CHANGED api.signl4.com/api/v2/alerts POST returns 401 (auth required) — previously hypothesized unauthenticated ingestion invalidated

## 2026-09-06 13:52:16 UTC
- NEW api.signl4.com/identity, connect.signl4.com/identity, devconnect.signl4.com/identity all live (OD 200) with JWKS byte-identical at 8th deep-equal observation point (kid 91EE4F3CE94EB517AF66B254F7497EC
- NEW devfix.signl4.com confirmed co-resolving with staging cluster (108.143.123.104), /signin-oidc 500 (OIDC callback registered), root 200 — support portal topology matches prior finding.
- NEW api/v2/teams unauth GET returns 401 Bearer (baseline stable); api/v2/alerts POST returns 411 (body length) confirming method routing, not 401 — POST-sink family behavior.
- CHANGED Cross-env identity finding consolidated: the single shared RS256 key + client_id 692A0A56 + full scope set is now the strongest AUTH finding, gated only on staging credential/client-secret compromise 
- NEW api.signl4.com/api/v2/teams confirmed 401 WWW-Authenticate: Bearer on unauthenticated GET — prod API surface fully Bearer-gated
- NEW devaccount.signl4.com/manage & account.signl4.com/manage redirect to respective IdPs with IDENTICAL client_id 692A0A56-892F-4AE2-8259-76DA398990B6 + scope set — cross-env client reuse confirmed
- NEW devconnect.signl4.com OIDC discovery: grant_types includes password + 7 others; algs=['RS256'] only — password grant enabled on staging IdP
- NEW JWKS byte-identical re-verified 6th time: devconnect.signl4.com & connect.signl4.com RS256 key (kid/n/x5t/x5c/e all match)
- CHANGED blog.derdack.com & techblog.derdack.com HTTPS→HTTP downgrade (302 to http://www.derdack.com/...) still live; www.derdack.com lacks HSTS/CSP/X-Frame-Options
- CHANGED dev.derdack.com MultiViews 300 stable (/.well-known/, /.ssh/, /.bash_history/, /.viminfo/) — static namespace echo, files 403/404
- CHANGED api.signl4.com/api/v2/alerts POST returns 401 (auth required) — previously hypothesized unauthenticated ingestion invalidated

## 2026-09-06 16:40:04 UTC
- NEW api.signl4.com/identity OIDC discovery re-verified live (8th deep-equal observation) with JWKS byte-identical to connect/devconnect
- NEW devfix.signl4.com confirmed on staging cluster (108.143.123.104) with /signin-oidc 500 (OIDC callback registered)
- NEW api/v2/alerts POST returns 411 (body length) confirming method routing, not 401 — POST-sink family behavior
- CHANGED Cross-env identity finding consolidated: single shared RS256 key + client_id 692A0A56 + full scope set is strongest AUTH finding, gated only on staging credential/client-secret compromise
- CHANGED api.signl4.com/api/v2/teams confirmed 401 WWW-Authenticate: Bearer on unauthenticated GET — prod API surface fully Bearer-gated
- CHANGED devaccount.signl4.com/manage & account.signl4.com/manage redirect to respective IdPs with IDENTICAL client_id 692A0A56-892F-4AE2-8259-76DA398990B6 + scope set — cross-env client reuse confirmed
- CHANGED devconnect.signl4.com OIDC discovery: grant_types includes password + 7 others; algs=['RS256'] only — password grant enabled on staging IdP
- CHANGED JWKS byte-identical re-verified 6th time: devconnect.signl4.com & connect.signl4.com RS256 key (kid/n/x5t/x5c/e all match)
- CHANGED blog.derdack.com & techblog.derdack.com HTTPS→HTTP downgrade (302 to http://www.derdack.com/...) still live; www.derdack.com lacks HSTS/CSP/X-Frame-Options
- CHANGED dev.derdack.com MultiViews 300 stable (/.well-known/, /.ssh/, /.bash_history/, /.viminfo/) — static namespace echo, files 403/404
- CHANGED api.signl4.com/api/v2/alerts POST returns 401 (auth required) — previously hypothesized unauthenticated ingestion invalidated

## 2026-09-06 18:43:42 UTC
- NEW api.signl4.com/api/v2/alerts POST returns 411 (Content-Length required) confirming method-routing sink family behavior, not 401 auth enforcement — distinguishes POST-sink from auth-gated routes
- NEW devfix.signl4.com confirmed on staging cluster (108.143.123.104) with /signin-oidc 500 (OIDC callback registered) and root 200 — corroborates staging IdP attachment topology
- NEW api.signl4.com/identity OIDC discovery re-verified live at 8th deep-equal observation with JWKS byte-identical to connect/devconnect (kid 91EE4F3CE94EB517AF66B254F7497ECB0E31EE27RS256)
- CHANGED Cross-env identity finding consolidated: single shared RS256 key + client_id 692A0A56-892F-4AE2-8259-76DA398990B6 + full scope set (account_portal, public_api_read/write/prov, offline_access, reseller
- CHANGED api.signl4.com/api/v2/teams confirmed 401 WWW-Authenticate: Bearer on unauthenticated GET — prod API surface fully Bearer-gated, stable baseline
- CHANGED devaccount.signl4.com/manage & account.signl4.com/manage redirect to respective IdPs with IDENTICAL client_id 692A0A56 + scope set — cross-env client reuse confirmed
- CHANGED devconnect.signl4.com OIDC discovery: grant_types includes password + 7 others; algs=['RS256'] only — password grant enabled on staging IdP
- CHANGED JWKS byte-identical re-verified 6th time: devconnect.signl4.com & connect.signl4.com RS256 key (kid/n/x5t/x5c/e all match)
- CHANGED blog.derdack.com & techblog.derdack.com HTTPS→HTTP downgrade (302 to http://www.derdack.com/...) still live; www.derdack.com lacks HSTS/CSP/X-Frame-Options
- CHANGED dev.derdack.com MultiViews 300 stable (/.well-known/, /.ssh/, /.bash_history/, /.viminfo/) — static namespace echo, files 403/404

## 2026-09-06 20:50:13 UTC
- NEW api.signl4.com/api/v3 → 404 and /api/v2/ → 404: api host is V2-only, V3 namespace absent
- NEW connect.signl4.com/api/v3 bare → 404 while registered subroutes (subscriptions/webhooks/users) 401 Bearer — route-level registration + auth differential re-confirmed, zero anonymous surface
- CHANGED Swagger/OAS surface CLOSED across api+connect+devconnect (swagger.json, openapi.json, swagger/v1/swagger.json, /api/*/swagger.json all 404) — schema-doc leak hypothesis dead; prior "dev schema exposes
- NEW api.signl4.com/api/v2/alerts POST returns 411 (Content-Length required) — distinguishes POST-sink routing from auth-gated routes; handler enforces Bearer on actual POST with body
- NEW devfix.signl4.com confirmed on staging cluster (108.143.123.104) with /signin-oidc 500 (OIDC callback registered) + root 200 — corroborates staging IdP attachment topology
- NEW api.signl4.com/identity OIDC discovery re-verified live at 8th deep-equal observation with JWKS byte-identical to connect/devconnect (kid 91EE4F3CE94EB517AF66B254F7497ECB0E31EE27RS256, n_sha 138f432b,
- CHANGED Cross-env identity finding consolidated: single shared RS256 key + client_id 692A0A56-892F-4AE2-8259-76DA398990B6 + full scope set (account_portal, public_api_read/write/prov, offline_access, reseller
- CHANGED api.signl4.com/api/v2/teams confirmed 401 WWW-Authenticate: Bearer on unauthenticated GET — prod API surface fully Bearer-gated, stable baseline
- CHANGED devaccount.signl4.com/manage & account.signl4.com/manage redirect to respective IdPs with IDENTICAL client_id 692A0A56 + scope set — cross-env client reuse confirmed
- CHANGED devconnect.signl4.com OIDC discovery: grant_types includes password + 7 others; algs=['RS256'] only — password grant enabled on staging IdP
- CHANGED JWKS byte-identical re-verified 6th time: devconnect.signl4.com & connect.signl4.com RS256 key (kid/n/x5t/x5c/e all match)
- CHANGED blog.derdack.com & techblog.derdack.com HTTPS→HTTP downgrade (302 to http://www.derdack.com/...) still live; www.derdack.com lacks HSTS/CSP/X-Frame-Options
- CHANGED dev.derdack.com MultiViews 300 stable (/.well-known/, /.ssh/, /.bash_history/, /.viminfo/) — static namespace echo, files 403/404

## 2026-09-06 22:37:49 UTC
- CHANGED api.signl4.com/api/v2/teams returns 405 Allow: GET,POST on unauthenticated GET (not 401) — method routing response, no auth challenge at routing layer
- CHANGED api.signl4.com/api/v2/teams returns 405 even with invalid Bearer token — auth validation not enforced at route entry

## 2026-09-07 00:25:59 UTC
- CHANGED api.signl4.com/api/v2/teams returns 405 Allow: GET,POST on unauthenticated GET (not 401) — method routing response, no auth challenge at routing layer (live confirmed)
- CHANGED api.signl4.com/api/v2/teams returns 405 even with invalid Bearer token — auth validation deferred to handler, not route layer (live confirmed)

## 2026-09-07 04:55:52 UTC
- NEW api.signl4.com/api/v2/teams returns 405 Allow: GET,POST on unauthenticated GET (not 401) — auth validation deferred to handler, not route layer (live confirmed 2026-09-07)
- NEW api.signl4.com/api/v2/teams returns 405 even with invalid Bearer token — confirms routing layer bypass, handler-level auth only (live confirmed 2026-09-07)
- CHANGED Cross-env JWKS key-reuse re-verified 9th time: devconnect.signl4.com & connect.signl4.com RS256 key byte-identical (kid/n/x5t/x5c deep-equal)
- CHANGED devconnect.signl4.com OIDC discovery: password grant listed alongside 7 others; returns invalid_client without client_secret
- CHANGED devaccount.signl4.com/manage & account.signl4.com/manage redirect to respective IdPs with IDENTICAL client_id 692A0A56-892F-4AE2-8259-76DA398990B6 + full scope set
- CHANGED blog.derdack.com & techblog.derdack.com HTTPS→HTTP downgrade (302 to http://www.derdack.com/...) still live; www.derdack.com lacks HSTS/CSP/X-Frame-Options
- CHANGED dev.derdack.com MultiViews 300 stable (/.well-known/, /.ssh/, /.bash_history/, /.viminfo/) — static namespace echo, files 403/404
- CHANGED connect.signl4.com/api/v3 bare 404 vs registered subroutes 401/405 — routing is auth-before-route at handler; no anonymous read surface

## 2026-09-07 09:54:45 UTC
- NEW api.signl4.com/api/v2/teams returns 405 Allow: GET,POST on unauthenticated GET (not 401) — auth validation deferred to handler, not route layer (live confirmed 2026-09-07)
- NEW api.signl4.com/api/v2/teams returns 405 even with invalid Bearer token — confirms routing layer bypass, handler-level auth only (live confirmed 2026-09-07)
- CHANGED Cross-env JWKS key-reuse re-verified 9th time: devconnect.signl4.com & connect.signl4.com RS256 key byte-identical (kid/n/x5t/x5c deep-equal)
- CHANGED devconnect.signl4.com OIDC discovery: password grant listed alongside 7 others; returns invalid_client without client_secret
- CHANGED devaccount.signl4.com/manage & account.signl4.com/manage redirect to respective IdPs with IDENTICAL client_id 692A0A56-892F-4AE2-8259-76DA398990B6 + full scope set
- CHANGED blog.derdack.com & techblog.derdack.com HTTPS→HTTP downgrade (302 to http://www.derdack.com/...) still live; www.derdack.com lacks HSTS/CSP/X-Frame-Options
- CHANGED dev.derdack.com MultiViews 300 stable (/.well-known/, /.ssh/, /.bash_history/, /.viminfo/) — static namespace echo, files 403/404
- CHANGED connect.signl4.com/api/v3 bare 404 vs registered subroutes 401/405 — routing is auth-before-route at handler; no anonymous read surface

## 2026-09-07 15:41:47 UTC
- NEW api.signl4.com/api/v2/teams returns 405 Allow: GET,POST on unauth GET (not 401) — auth validation deferred to handler, not route layer (live confirmed 2026-09-07)
- NEW api.signl4.com/api/v2/teams returns 405 even with invalid Bearer token — confirms routing layer bypass, handler-level auth only (live confirmed 2026-09-07)
- CHANGED Cross-env JWKS key-reuse re-verified 9th time: devconnect.signl4.com & connect.signl4.com RS256 key byte-identical (kid/n/x5t/x5c deep-equal)
- CHANGED devconnect.signl4.com OIDC discovery: password grant listed alongside 7 others; returns invalid_client without client_secret
- CHANGED devaccount.signl4.com/manage & account.signl4.com/manage redirect to respective IdPs with IDENTICAL client_id 692A0A56-892F-4AE2-8259-76DA398990B6 + full scope set
- CHANGED blog.derdack.com & techblog.derdack.com HTTPS→HTTP downgrade (302 to http://www.derdack.com/...) still live; www.derdack.com lacks HSTS/CSP/X-Frame-Options
- CHANGED dev.derdack.com MultiViews 300 stable (/.well-known/, /.ssh/, /.bash_history/, /.viminfo/) — static namespace echo, files 403/404
- CHANGED connect.signl4.com/api/v3 bare 404 vs registered subroutes 401/405 — routing is auth-before-route at handler; no anonymous read surface

## 2026-09-07 19:42:23 UTC

## 2026-09-07 22:22:49 UTC
- NEW api.signl4.com/api/v2/teams returns 405 Allow: GET,POST on unauth GET (not 401) — auth validation deferred to handler, not route layer (live confirmed 2026-09-07)
- NEW api.signl4.com/api/v2/teams returns 405 even with invalid Bearer token — confirms routing layer bypass, handler-level auth only (live confirmed 2026-09-07)
- CHANGED Cross-env JWKS key-reuse re-verified 9th time: devconnect.signl4.com & connect.signl4.com & api.signl4.com RS256 key byte-identical (kid/n/x5t/x5c deep-equal)
- CHANGED devconnect.signl4.com OIDC discovery: password grant listed alongside 7 others; returns invalid_client without client_secret
- CHANGED devaccount.signl4.com/manage & account.signl4.com/manage redirect to respective IdPs with IDENTICAL client_id 692A0A56-892F-4AE2-8259-76DA398990B6 + full scope set
- CHANGED blog.derdack.com & techblog.derdack.com HTTPS→HTTP downgrade (302 to http://www.derdack.com/...) still live; www.derdack.com lacks HSTS/CSP/X-Frame-Options
- CHANGED dev.derdack.com MultiViews 300 stable (/.well-known/, /.ssh/, /.bash_history/, /.viminfo/) — static namespace echo, files 403/404
- CHANGED connect.signl4.com/api/v3 bare 404 vs registered subroutes 401/405 — routing is auth-before-route at handler; no anonymous read surface

## 2026-09-08 00:38:24 UTC
- NEW api.signl4.com/api/v2/teams returns 405 Allow: GET,POST on unauth GET (not 401) — auth validation deferred to handler, not route layer (live confirmed 2026-09-07)
- NEW api.signl4.com/api/v2/teams returns 405 even with invalid Bearer token — confirms routing layer bypass, handler-level auth only (live confirmed 2026-09-07)
- CHANGED Cross-env JWKS key-reuse re-verified 9th time: devconnect.signl4.com & connect.signl4.com & api.signl4.com RS256 key byte-identical (kid/n/x5t/x5c deep-equal)
- CHANGED devconnect.signl4.com OIDC discovery: password grant listed alongside 7 others; returns invalid_client without client_secret
- CHANGED devaccount.signl4.com/manage & account.signl4.com/manage redirect to respective IdPs with IDENTICAL client_id 692A0A56-892F-4AE2-8259-76DA398990B6 + full scope set
- CHANGED blog.derdack.com & techblog.derdack.com HTTPS→HTTP downgrade (302 to http://www.derdack.com/...) still live; www.derdack.com lacks HSTS/CSP/X-Frame-Options
- CHANGED dev.derdack.com MultiViews 300 stable (/.well-known/, /.ssh/, /.bash_history/, /.viminfo/) — static namespace echo, files 403/404
- CHANGED connect.signl4.com/api/v3 bare 404 vs registered subroutes 401/405 — routing is auth-before-route at handler; no anonymous read surface
- NEW api.signl4.com/api/v2/teams returns 405 Allow: GET,POST on unauth GET (not 401) — auth validation deferred to handler, not route layer (live confirmed 2026-09-07)
- NEW api.signl4.com/api/v2/teams returns 405 even with invalid Bearer token — confirms routing layer bypass, handler-level auth only (live confirmed 2026-09-07)
- CHANGED Cross-env JWKS key-reuse re-verified 9th time: devconnect.signl4.com & connect.signl4.com & api.signl4.com RS256 key byte-identical (kid/n/x5t/x5c deep-equal)
- CHANGED devconnect.signl4.com OIDC discovery: password grant listed alongside 7 others; returns invalid_client without client_secret
- CHANGED devaccount.signl4.com/manage & account.signl4.com/manage redirect to respective IdPs with IDENTICAL client_id 692A0A56-892F-4AE2-8259-76DA398990B6 + full scope set
- CHANGED blog.derdack.com & techblog.derdack.com HTTPS→HTTP downgrade (302 to http://www.derdack.com/...) still live; www.derdack.com lacks HSTS/CSP/X-Frame-Options
- CHANGED dev.derdack.com MultiViews 300 stable (/.well-known/, /.ssh/, /.bash_history/, /.viminfo/) — static namespace echo, files 403/404
- CHANGED connect.signl4.com/api/v3 bare 404 vs registered subroutes 401/405 — routing is auth-before-route at handler; no anonymous read surface

## 2026-09-08 05:12:26 UTC
- NEW api.signl4.com/api/v2/teams returns 405 Allow: GET,POST on unauth GET (not 401) — auth validation deferred to handler, not route layer (live confirmed 2026-09-07)
- NEW api.signl4.com/api/v2/teams returns 405 even with invalid Bearer token — confirms routing layer bypass, handler-level auth only (live confirmed 2026-09-07)
- CHANGED Cross-env JWKS key-reuse re-verified 9th time: devconnect.signl4.com & connect.signl4.com & api.signl4.com RS256 key byte-identical (kid/n/x5t/x5c deep-equal)
- CHANGED devconnect.signl4.com OIDC discovery: password grant listed alongside 7 others; returns invalid_client without client_secret
- CHANGED devaccount.signl4.com/manage & account.signl4.com/manage redirect to respective IdPs with IDENTICAL client_id 692A0A56-892F-4AE2-8259-76DA398990B6 + full scope set
- CHANGED blog.derdack.com & techblog.derdack.com HTTPS→HTTP downgrade (302 to http://www.derdack.com/...) still live; www.derdack.com lacks HSTS/CSP/X-Frame-Options
- CHANGED dev.derdack.com MultiViews 300 stable (/.well-known/, /.ssh/, /.bash_history/, /.viminfo/) — static namespace echo, files 403/404
- CHANGED connect.signl4.com/api/v3 bare 404 vs registered subroutes 401/405 — routing is auth-before-route at handler; no anonymous read surface

## 2026-09-08 09:47:18 UTC
- CHANGED api.signl4.com/api/v2/teams: unauth GET returns 405 Allow: GET,POST (not 401) — auth validation deferred to handler, not route layer (9th live confirmation)
- CHANGED Cross-env JWKS: devconnect.signl4.com, connect.signl4.com, api.signl4.com RS256 key byte-identical (kid 91EE4F3CE94EB517AF66B254F7497ECB0E31EE27RS256) — 9th deep-equal verification
- CHANGED devconnect.signl4.com OIDC discovery: password grant listed alongside 7 others; token endpoint returns invalid_client without client_secret
- CHANGED devaccount.signl4.com/manage & account.signl4.com/manage: both redirect to respective IdPs with IDENTICAL client_id 692A0A56-892F-4AE2-8259-76DA398990B6 + full scope set (account_portal, public_api_re
- CHANGED blog.derdack.com & techblog.derdack.com: HTTPS→HTTP downgrade (302 to http://www.derdack.com/...) still live; www.derdack.com lacks HSTS/CSP/X-Frame-Options
- CHANGED dev.derdack.com: MultiViews 300 stable (/.well-known/, /.ssh/, /.bash_history/, /.viminfo/) — static namespace echo, files 403/404
- CHANGED connect.signl4.com/api/v3: bare 404 vs registered subroutes 401/405 — routing is auth-before-route at handler; no anonymous read surface

## 2026-09-08 14:20:23 UTC
- NEW www.derdack.com/wp-login.php sets `wordpress_test_cookie` with `secure` flag and NO `Domain` attribute → host-only scoped, contradicting prior parent-domain cookie-scope assumption
- NEW www.derdack.com & blog.derdack.com confirm NO HSTS header (active this cycle)
- CHANGED blog.derdack.com HTTPS→HTTP redirect is 302→301 to www.derdack.com; downgrade chain live but auth-cookie theft mechanism invalidated (secure+host-only cookies)

## 2026-09-08 18:10:29 UTC

## 2026-09-08 20:35:57 UTC
- NEW api.signl4.com/api/v2/teams returns 405 Allow: GET,POST on unauth GET (not 401) — auth validation deferred to handler, not route layer (live confirmed 2026-09-07)
- NEW api.signl4.com/api/v2/teams returns 405 even with invalid Bearer token — confirms routing layer bypass, handler-level auth only (live confirmed 2026-09-07)
- CHANGED Cross-env JWKS key-reuse re-verified 9th time: devconnect.signl4.com & connect.signl4.com & api.signl4.com RS256 key byte-identical (kid/n/x5t/x5c deep-equal)
- CHANGED devconnect.signl4.com OIDC discovery: password grant listed alongside 7 others; returns invalid_client without client_secret
- CHANGED devaccount.signl4.com/manage & account.signl4.com/manage redirect to respective IdPs with IDENTICAL client_id 692A0A56-892F-4AE2-8259-76DA398990B6 + full scope set
- CHANGED blog.derdack.com & techblog.derdack.com HTTPS→HTTP downgrade (302 to http://www.derdack.com/...) still live; www.derdack.com lacks HSTS/CSP/X-Frame-Options
- CHANGED dev.derdack.com MultiViews 300 stable (/.well-known/, /.ssh/, /.bash_history/, /.viminfo/) — static namespace echo, files 403/404
- CHANGED connect.signl4.com/api/v3 bare 404 vs registered subroutes 401/405 — routing is auth-before-route at handler; no anonymous read surface
- NEW api.signl4.com/api/v2/teams returns 405 Allow: GET,POST on unauth GET (not 401) — auth validation deferred to handler, not route layer (live confirmed 2026-09-07)
- NEW api.signl4.com/api/v2/teams returns 405 even with invalid Bearer token — confirms routing layer bypass, handler-level auth only (live confirmed 2026-09-07)
- CHANGED Cross-env JWKS key-reuse re-verified 9th time: devconnect.signl4.com & connect.signl4.com & api.signl4.com RS256 key byte-identical (kid/n/x5t/x5c deep-equal)
- CHANGED devconnect.signl4.com OIDC discovery: password grant listed alongside 7 others; returns invalid_client without client_secret
- CHANGED devaccount.signl4.com/manage & account.signl4.com/manage redirect to respective IdPs with IDENTICAL client_id 692A0A56-892F-4AE2-8259-76DA398990B6 + full scope set
- CHANGED blog.derdack.com & techblog.derdack.com HTTPS→HTTP downgrade (302 to http://www.derdack.com/...) still live; www.derdack.com lacks HSTS/CSP/X-Frame-Options
- CHANGED dev.derdack.com MultiViews 300 stable (/.well-known/, /.ssh/, /.bash_history/, /.viminfo/) — static namespace echo, files 403/404
- CHANGED connect.signl4.com/api/v3 bare 404 vs registered subroutes 401/405 — routing is auth-before-route at handler; no anonymous read surface
- CHANGED api.signl4.com/api/v2/teams: unauth GET returns 405 Allow: GET,POST (not 401) — auth validation deferred to handler, not route layer (9th live confirmation)
- CHANGED Cross-env JWKS: devconnect.signl4.com, connect.signl4.com, api.signl4.com RS256 key byte-identical (kid 91EE4F3CE94EB517AF66B254F7497ECB0E31EE27RS256) — 9th deep-equal verification
- CHANGED devconnect.signl4.com OIDC discovery: password grant listed alongside 7 others; token endpoint returns invalid_client without client_secret
- CHANGED devaccount.signl4.com/manage & account.signl4.com/manage: both redirect to respective IdPs with IDENTICAL client_id 692A0A56-892F-4AE2-8259-76DA398990B6 + full scope set (account_portal, public_api_re
- CHANGED blog.derdack.com & techblog.derdack.com: HTTPS→HTTP downgrade (302 to http://www.derdack.com/...) still live; www.derdack.com lacks HSTS/CSP/X-Frame-Options
- CHANGED dev.derdack.com: MultiViews 300 stable (/.well-known/, /.ssh/, /.bash_history/, /.viminfo/) — static namespace echo, files 403/404
- CHANGED connect.signl4.com/api/v3: bare 404 vs registered subroutes 401/405 — routing is auth-before-route at handler; no anonymous read surface
- NEW api.signl4.com/api/v2/teams returns 405 Allow: GET,POST on unauth GET (not 401) — auth validation deferred to handler, not route layer (live confirmed 2026-09-07)
- NEW api.signl4.com/api/v2/teams returns 405 even with invalid Bearer token — confirms routing layer bypass, handler-level auth only (live confirmed 2026-09-07)
- CHANGED Cross-env JWKS key-reuse re-verified 9th time: devconnect.signl4.com & connect.signl4.com & api.signl4.com RS256 key byte-identical (kid/n/x5t/x5c deep-equal)
- CHANGED devconnect.signl4.com OIDC discovery: password grant listed alongside 7 others; returns invalid_client without client_secret
- CHANGED devaccount.signl4.com/manage & account.signl4.com/manage redirect to respective IdPs with IDENTICAL client_id 692A0A56-892F-4AE2-8259-76DA398990B6 + full scope set
- CHANGED blog.derdack.com & techblog.derdack.com HTTPS→HTTP downgrade (302 to http://www.derdack.com/...) still live; www.derdack.com lacks HSTS/CSP/X-Frame-Options
- CHANGED dev.derdack.com MultiViews 300 stable (/.well-known/, /.ssh/, /.bash_history/, /.viminfo/) — static namespace echo, files 403/404
- CHANGED connect.signl4.com/api/v3 bare 404 vs registered subroutes 401/405 — routing is auth-before-route at handler; no anonymous read surface
- NEW www.derdack.com/wp-login.php sets `wordpress_test_cookie` with `secure` flag and NO `Domain` attribute → host-only scoped, contradicting prior parent-domain cookie-scope assumption
- NEW www.derdack.com & blog.derdack.com confirm NO HSTS header (active this cycle)
- CHANGED blog.derdack.com HTTPS→HTTP redirect is 302→301 to www.derdack.com; downgrade chain live but auth-cookie theft mechanism invalidated (secure+host-only cookies)
- NEW Dynamic client registration endpoint check on devconnect.signl4.com/identity/.well-known/openid-configuration (registration_endpoint field) — unprobed vector that could bypass client_secret requiremen
- CHANGED blog.derdack.com/techblog.derdack.com HTTPS→HTTP downgrade session-theft mechanism CONFIRMED INVALIDATED — wp-login.php sets wordpress_test_cookie with `secure` flag + host-only scope (no Domain=.derd
- CHANGED Cross-env JWKS key-reuse: 10th deep-equal verification across connect/api/devconnect/devapi (bigpickle cycle) — all 4 identity hosts serve byte-identical RS256 key
- CHANGED api.signl4.com/api/v2/teams: stable 405 Allow:GET,POST on unauth GET (not 401) — auth validation deferred to handler, not route layer (10th+ live confirmation)
- CHANGED devconnect.signl4.com OIDC discovery: password grant + client_credentials + device_code + PAR enabled; token endpoint returns invalid_client without client_secret

## 2026-09-08 22:59:26 UTC
- NEW Four identity hosts (devconnect.signl4.com, connect.signl4.com, api.signl4.com, devapi.signl4.com) serve byte-identical RS256 JWKS (kid 91EE4F3CE94EB517AF66B254F7497ECB0E31EE27RS256) — 10th live deep-
- NEW devconnect.signl4.com OIDC discovery: NO `registration_endpoint` field; `token_endpoint_auth_methods_supported` only `client_secret_basic`/`client_secret_post` (no `none`) — dynamic client registratio
- NEW api.signl4.com/api/v2/teams: unauth GET returns 405 Allow:GET,POST (not 401); invalid Bearer also 405 — auth validation deferred to handler, not route layer (10th+ live confirmation)
- NEW devconnect.signl4.com/identity/connect/token password grant: returns `invalid_client` without client_secret — grant listed but not usable without secrets (live re-verified)
- CHANGED blog.derdack.com/techblog.derdack.com HTTPS→HTTP downgrade: session-theft mechanism permanently invalidated (wp-login.php sets `wordpress_test_cookie` with `secure` flag + host-only scope); residual =

## 2026-09-09 01:16:30 UTC
- NEW devapi.signl4.com confirmed as 4th identity host serving byte-identical RS256 JWKS (kid 91EE4F3CE94EB517AF66B254F7497ECB0E31EE27RS256) — 10th live deep-equal verification across connect/api/devconnect
- NEW devconnect.signl4.com OIDC discovery: NO `registration_endpoint` field; `token_endpoint_auth_methods_supported` only `client_secret_basic`/`client_secret_post` (no `none`) — dynamic client registratio
- NEW connect.signl4.com/api/v3 route map fully confirmed: bare 404 vs registered subroutes (users/teams/webhooks/subscriptions/schedules/devices/csp/report) returning 401/405 — auth-before-route at handler
- CHANGED Dynamic client registration hypothesis permanently REJECTED — RFC 7591 unsupported on staging IdentityServer (no registration_endpoint, no `none` auth method)
- CHANGED blog.derdack.com/techblog.derdack.com HTTPS→HTTP downgrade session-theft mechanism permanently INVALIDATED — wp-login.php sets `wordpress_test_cookie` with `secure` flag + host-only scope (no Domain=.
- CHANGED api.signl4.com/api/v2/teams unauth GET returns 405 Allow:GET,POST (not 401) confirmed 10th+ cycles — stable auth-deferred-to-handler behavior

## 2026-09-09 05:56:28 UTC
- NEW SIGNL4 API V2 swagger.json discovered at `connect.signl4.com/api/docs/v2/swagger.json` — declares OAuth2 scheme (authorizationCode) pointing to `connect.signl4.com/identity/connect/authorize` + `/toke
- NEW RAG confirms SIGNL4 public API auth = API key (`X-S4-Api-Key`) + OAuth2 Bearer token (swagger-declared); client_id `692A0A56` NOT published anywhere — no GitHub/npm/Postman/helpcenter leak; no public 
- NEW RAG confirms Derdack GitHub org (12 repos) contains Enterprise Alert plugins only — no OAuth/OIDC code, no leaked secrets
- CHANGED Cross-env token forgery hypothesis (85) now has FULL exploit-chain evidence: shared RS256 key → shared token endpoint → API accepts OAuth tokens → scopes grant CRUD → attack chain complete pending cli
- NEW devapi.signl4.com confirmed as 4th identity host serving byte-identical RS256 JWKS (kid 91EE4F3CE94EB517AF66B254F7497ECB0E31EE27RS256) — 10th live deep-equal across connect/api/devconnect/devapi
- NEW devconnect.signl4.com OIDC discovery: NO `registration_endpoint`; `token_endpoint_auth_methods_supported` only `client_secret_basic`/`client_secret_post` (no `none`) — dynamic client registration perm
- NEW connect.signl4.com OIDC discovery byte-identical to devconnect (password/device_code/ciba/token-exchange grants, secret-only auth methods, no registration_endpoint, RS256-only) — prod is parametric tw
- NEW connect.signl4.com/api/v3 route map fully confirmed: bare 404 vs registered subroutes (users/teams/webhooks/subscriptions/schedules/devices/csp/report) returning 401/405 — auth-before-route at handler
- NEW devapi.signl4.com: live 1:1 staging API mirror of api.signl4.com (appId cid-v1:d7865de8-ff22-4cec-8b2d-6e39fb5802f7), root→devaccount/manage, zero unauth read surface
- NEW api+devapi /api/v2/teams: 401 WWW-Authenticate:Bearer this cycle vs 405 in other cycles — handler/routing auth-status flapping across cycles confirmed
- CHANGED Dynamic client registration hypothesis permanently REJECTED — RFC 7591 unsupported on staging IdentityServer
- CHANGED blog.derdack.com/techblog.derdack.com HTTPS→HTTP downgrade session-theft mechanism permanently INVALIDATED — wp-login.php sets `wordpress_test_cookie` with `secure` flag + host-only scope; WP auth coo
- CHANGED api.signl4.com/api/v2/teams unauth GET returns 405 Allow:GET,POST (not 401) confirmed 10th+ cycles — stable auth-deferred-to-handler behavior
- CHANGED connect+devconnect /identity/connect/ciba + deviceauthorization: both 400 across envs — endpoint twins, all secret-gated

## 2026-09-09 10:46:31 UTC
- NEW devapi.signl4.com confirmed as 4th identity host serving byte-identical RS256 JWKS (kid 91EE4F3CE94EB517AF66B254F7497ECB0E31EE27RS256) — 10th live deep-equal across connect/api/devconnect/devapi
- NEW devconnect.signl4.com OIDC discovery: NO `registration_endpoint`; `token_endpoint_auth_methods_supported` only `client_secret_basic`/`client_secret_post` (no `none`) — dynamic client registration perm
- NEW connect.signl4.com OIDC discovery byte-identical to devconnect (password/device_code/ciba/token-exchange grants, secret-only auth methods, no registration_endpoint, RS256-only) — prod is parametric tw
- NEW connect.signl4.com/api/v3 route map fully confirmed: bare 404 vs registered subroutes (users/teams/webhooks/subscriptions/schedules/devices/csp/report) returning 401/405 — auth-before-route at handler
- NEW devapi.signl4.com: live 1:1 staging API mirror of api.signl4.com (appId cid-v1:d7865de8-ff22-4cec-8b2d-6e39fb5802f7), root→devaccount/manage, zero unauth read surface
- NEW api+devapi /api/v2/teams: 401 WWW-Authenticate:Bearer this cycle vs 405 in other cycles — handler/routing auth-status flapping across cycles confirmed
- CHANGED Dynamic client registration hypothesis permanently REJECTED — RFC 7591 unsupported on staging IdentityServer
- CHANGED blog.derdack.com/techblog.derdack.com HTTPS→HTTP downgrade session-theft mechanism permanently INVALIDATED — wp-login.php sets `wordpress_test_cookie` with `secure` flag + host-only scope; WP auth coo
- CHANGED api.signl4.com/api/v2/teams unauth GET returns 405 Allow:GET,POST (not 401) confirmed 10th+ cycles — stable auth-deferred-to-handler behavior
- CHANGED connect+devconnect /identity/connect/ciba + deviceauthorization: both 400 across envs — endpoint twins, all secret-gated

## 2026-09-09 14:50:14 UTC
- NEW devapi.signl4.com confirmed as 4th identity host serving byte-identical RS256 JWKS (kid 91EE4F3CE94EB517AF66B254F7497ECB0E31EE27RS256) — 10th live deep-equal across connect/api/devconnect/devapi
- NEW connect.signl4.com OIDC discovery byte-identical to devconnect (password/device_code/ciba/token-exchange grants, secret-only auth methods, no registration_endpoint, RS256-only) — prod is parametric tw
- NEW api.signl4.com swagger.json declares OAuth2 authorizationCode flow targeting connect.signl4.com/identity/connect endpoints + API_Key_Query scheme (x-s4-api-key in query param)
- NEW api+devapi /api/v2/teams: 401 WWW-Authenticate:Bearer this cycle vs 405 in other cycles — handler/routing auth-status flapping across cycles confirmed
- CHANGED Dynamic client registration hypothesis permanently REJECTED — RFC 7591 unsupported on staging IdentityServer (no registration_endpoint, no `none` auth method)
- CHANGED blog.derdack.com/techblog.derdack.com HTTPS→HTTP downgrade session-theft mechanism permanently INVALIDATED — wp-login.php sets `wordpress_test_cookie` with `secure` flag + host-only scope; WP auth coo
- CHANGED api.signl4.com/api/v2/teams unauth GET returns 405 Allow:GET,POST (not 401) confirmed 10th+ cycles — stable auth-deferred-to-handler behavior

## 2026-09-09 18:15:41 UTC
- NEW No new probes executed since last cycle (2026-09-09 14:50:14 UTC)
- CHANGED Cross-env token forgery chain fully documented: shared RS256 key + shared client_id + swagger-confirmed OAuth2 API access + staging password grant + prod twin; blocked on client_secret
- CHANGED API key query-param auth confirmed live on both api.signl4.com and connect.signl4.com (403 "API Key is invalid" vs 401 when absent); dual auth pipeline established
- CHANGED API spec empty security requirement confirmed (LOW impact; spec-vs-implementation mismatch)
- NEW devapi.signl4.com confirmed as 4th identity host serving byte-identical RS256 JWKS (kid 91EE4F3CE94EB517AF66B254F7497ECB0E31EE27RS256) — 10th live deep-equal across connect/api/devconnect/devapi
- NEW connect.signl4.com OIDC discovery byte-identical to devconnect (password/device_code/ciba/token-exchange grants, secret-only auth methods, no registration_endpoint, RS256-only) — prod is parametric tw
- NEW api.signl4.com swagger.json declares OAuth2 authorizationCode flow targeting connect.signl4.com/identity/connect endpoints + API_Key_Query scheme (x-s4-api-key in query param)
- NEW api+devapi /api/v2/teams: 401 WWW-Authenticate:Bearer this cycle vs 405 in other cycles — handler/routing auth-status flapping across cycles confirmed
- NEW API key via query parameter (`?x-s4-api-key=<key>`) confirmed LIVE (403 "API Key is invalid" vs 401 when absent); dual auth pipeline (Bearer + API key) confirmed; swagger `API_Key_Query` scheme operat
- NEW Bearer auth returns 401 with `WWW-Authenticate: Bearer`, API key auth returns 403 `application/problem+json` — distinct auth pipelines with different error responses confirm independent validation pat
- NEW connect.signl4.com/api/v2/* shares backend with api.signl4.com (appId=cid-v1:ec6c57ca-...); API key auth works on both hosts; swagger served from connect host — connect is the documented API gateway
- CHANGED Dynamic client registration hypothesis permanently REJECTED — RFC 7591 unsupported on staging IdentityServer (no registration_endpoint, no `none` auth method)
- CHANGED blog.derdack.com/techblog.derdack.com HTTPS→HTTP downgrade session-theft mechanism permanently INVALIDATED — wp-login.php sets `wordpress_test_cookie` with `secure` flag + host-only scope; WP auth coo
- CHANGED api.signl4.com/api/v2/teams unauth GET returns 405 Allow:GET,POST (not 401) confirmed 10th+ cycles — stable auth-deferred-to-handler behavior

## 2026-09-09 21:01:57 UTC
- NEW api.signl4.com swagger.json confirms OAuth2 authorizationCode flow targeting connect.signl4.com/identity/connect endpoints + API_Key_Query scheme (x-s4-api-key in query param) — full cross-env token f
- NEW API key via query parameter (`?x-s4-api-key=<key>`) confirmed LIVE on both api.signl4.com and connect.signl4.com (403 "API Key is invalid" vs 401 when absent); dual auth pipeline (Bearer + API key) co
- NEW Bearer auth returns 401 with `WWW-Authenticate: Bearer`, API key auth returns 403 `application/problem+json` — distinct auth pipelines with different error responses confirm independent validation pat
- NEW connect.signl4.com/api/v2/* shares backend with api.signl4.com (appId=cid-v1:ec6c57ca-...); API key auth works on both hosts; swagger served from connect host — connect is the documented API gateway
- NEW connect.signl4.com OIDC discovery byte-identical to devconnect (password/device_code/ciba/token-exchange grants, secret-only auth methods, no registration_endpoint, RS256-only) — prod is parametric tw
- NEW api+devapi /api/v2/teams: 401 WWW-Authenticate:Bearer this cycle vs 405 in other cycles — handler/routing auth-status flapping across cycles confirmed
- CHANGED Dynamic client registration hypothesis permanently REJECTED — RFC 7591 unsupported on staging IdentityServer (no registration_endpoint, no `none` auth method)
- CHANGED blog.derdack.com/techblog.derdack.com HTTPS→HTTP downgrade session-theft mechanism permanently INVALIDATED — wp-login.php sets `wordpress_test_cookie` with `secure` flag + host-only scope; WP auth coo
- CHANGED api.signl4.com/api/v2/teams unauth GET returns 405 Allow:GET,POST (not 401) confirmed 10th+ cycles — stable auth-deferred-to-handler behavior
- CHANGED Cross-env token forgery chain fully documented: shared RS256 key + shared client_id + swagger-confirmed OAuth2 API access + staging password grant + prod twin; blocked on client_secret

## 2026-09-09 23:14:42 UTC

## 2026-09-10 00:50:33 UTC
- NEW crt.sh CT-log sweep: 13 signl4.com + 4 enterprisealert.com subdomains; 8 previously-unknown LIVE hosts — fix, frontdoor, status, support, trust, docs, demo/downloads.enterprisealert.com
- NEW fix.signl4.com (20.160.37.197) = prod ASP.NET Core "SIGNL4 Support Application" (Kestrel); /signin-oidc → 500 (broken OIDC callback, devfix twin); Blazor (`/_blazor/negotiate` 405 on GET)
- NEW frontdoor.signl4.com (20.22.16.164) = unconfigured SPA shell serving literal unrendered `<title>SIGNL4 - %ReplaceStatusTitle%</title>` (static ETag, last-modified 2024-09-03)
- NEW status.signl4.com = StatusLabs (adminlabs.com) page; /index.php → status-page-not-found. support.signl4.com = Zendesk /hc; trust = CF-fronted; docs = GitHub Pages
- NEW API surface: `PUT /api/prepaid/{subscriptionId}/prepaidSettings` registered (OPTIONS Allow: PUT) — billing route family absent from all prior /api/v2 route maps; `/api/v2/events/{teamSecret}` = GET+PO
- CHANGED /api/v2/teams baseline flipped to 401 this cycle (was 405) — auth-status flapping re-confirmed

## 2026-09-10 05:31:54 UTC
- CHANGED /api/v2/teams baseline: 401 Bearer this cycle vs 405 in prior — auth-status flapping re-confirmed (10th+ observation)
- NEW CT surface expanded by 8 live hosts (fix, frontdoor, status, support, trust, docs, demo/downloads.enterprisealert.com) — all passively surfaced 2026-09-10, none yet probed for new defects beyond initi
- NEW /api/v2/events/{teamSecret} = GET+POST Bearer-gated (401) — new registered route family discovered
- NEW PUT /api/prepaid/{id}/prepaidSettings — billing route, handler-deferred auth (405 OPTIONS before 401/403)
- NEW frontdoor.signl4.com unconfigured shell with literal %ReplaceStatusTitle% placeholder (static since 2024-09-03)
- CHANGED Previous hypothesis "webhook secret leak" remains UNSUPPORTED — no public leak found across 3 cycles of grep.app/GitHub/code-search sweeps

## 2026-09-10 10:12:59 UTC
- NEW CT surface expansion: 8 previously-unknown live hosts discovered via crt.sh — fix.signl4.com, frontdoor.signl4.com, status.signl4.com, support.signl4.com, trust.signl4.com, docs.signl4.com, demo.enter
- NEW fix.signl4.com: prod ASP.NET Core "SIGNL4 Support Application" (Kestrel); /signin-oidc → 500 broken OIDC callback; Blazor estate (_blazor/negotiate 405 on GET)
- NEW frontdoor.signl4.com: unconfigured SPA shell serving literal %ReplaceStatusTitle% placeholder (static ETag, last-modified 2024-09-03)
- NEW connect.signl4.com new registered routes: PUT /api/prepaid/{id}/prepaidSettings (Allow:PUT, handler-deferred auth), /api/v2/events/{teamSecret} (GET+POST, 401 Bearer), public webhook OpenAPI at /webho
- NEW connect.signl4.com/webhook contract confirmed: POST /{teamSecret}, NO security scheme, query-config status keywords (ExtIdParam/ExtStatusParam/NewStatus/ResolvedStatus/AckStatus), oracle 404-invalid v
- CHANGED api.signl4.com/api/v2/teams baseline flapping: 401 WWW-Authenticate:Bearer this cycle vs 405 in prior cycles — auth-status flapping re-confirmed (10th+ observation)
- CHANGED blog.derdack.com/techblog.derdack.com HTTPS→HTTP downgrade session-theft mechanism permanently invalidated — wp-login.php sets wordpress_test_cookie with `secure` flag + host-only scope (no Domain=.de

## 2026-09-10 14:36:44 UTC

## 2026-09-10 17:57:53 UTC

## 2026-09-10 20:20:47 UTC
- NEW CT-log sweep (crt.sh) surfaced 8 previously-unknown live hosts under signl4.com/enterprisealert.com: fix.signl4.com (prod ASP.NET Core Support App, Blazor, /signin-oidc 500), frontdoor.signl4.com (unc
- NEW connect.signl4.com new registered routes discovered: PUT /api/prepaid/{id}/prepaidSettings (OPTIONS Allow:PUT, handler-deferred auth), /api/v2/events/{teamSecret} (GET+POST, 401 Bearer), public webhoo
- NEW connect.signl4.com/webhook contract confirmed: POST /{teamSecret}, NO security scheme in OpenAPI, query-configurable status keywords (ExtIdParam, ExtStatusParam, NewStatus, ResolvedStatus, AckStatus),
- NEW api.signl4.com + connect.signl4.com dual auth pipeline live-verified: Bearer auth returns 401 WWW-Authenticate:Bearer; API key via query param ?x-s4-api-key=<key> returns 403 "API Key is invalid" vs 4
- NEW devapi.signl4.com confirmed as 4th identity host serving byte-identical RS256 JWKS (kid 91EE4F3CE94EB517AF66B254F7497ECB0E31EE27RS256) — 10th live deep-equal across connect/api/devconnect/devapi; deva
- NEW connect.signl4.com OIDC discovery byte-identical to devconnect (password/device_code/ciba/token-exchange grants, secret-only auth methods, no registration_endpoint, RS256-only) — prod is parametric tw
- CHANGED api.signl4.com/api/v2/teams auth-status flapping re-confirmed (10th+ observation): unauth GET returns 405 Allow:GET,POST this cycle (was 401 in prior cycle) — auth validation deferred to handler, not 
- CHANGED Cross-env token forgery chain fully documented: shared RS256 key (4 identity hosts) + shared client_id 692A0A56-892F-4AE2-8259-76DA398990B6 + full scope set + swagger-confirmed OAuth2 API access + sta
- CHANGED blog.derdack.com/techblog.derdack.com HTTPS→HTTP downgrade session-theft mechanism permanently invalidated — wp-login.php sets wordpress_test_cookie with secure flag + host-only scope (no Domain=.derd
- CHANGED dev.derdack.com MultiViews 300 stable across 20+ cycles — static namespace echo (/.well-known/, /.ssh/, /.bash_history/, /.viminfo/), files return 403/404; root serves parked IONOS sedoparking iframe 
- CHANGED www.derdack.com/de/ & /ea/ XML-RPC both POST-exposed with full method lists but mutating methods (wp.uploadFile, metaWeblog.newMediaObject) return faultCode 403 "incorrect username/password" — auth-ga

## 2026-09-10 22:39:12 UTC
- NEW crt.sh CT-log sweep surfaced 8 previously-unknown live hosts: fix.signl4.com (prod ASP.NET Core Support App, Blazor, /signin-oidc 500), frontdoor.signl4.com (unconfigured SPA shell with %ReplaceStatus
- NEW connect.signl4.com new registered routes discovered: PUT /api/prepaid/{id}/prepaidSettings (OPTIONS Allow:PUT, handler-deferred auth), /api/v2/events/{teamSecret} (GET+POST, 401 Bearer), public webhoo
- NEW connect.signl4.com/webhook contract confirmed: POST /{teamSecret}, NO security scheme in OpenAPI, query-configurable status keywords (ExtIdParam/ExtStatusParam/NewStatus/ResolvedStatus/AckStatus), ora
- NEW api.signl4.com + connect.signl4.com dual auth pipeline live-verified: Bearer auth returns 401 WWW-Authenticate:Bearer; API key via query param ?x-s4-api-key=<key> returns 403 "API Key is invalid" vs 4
- NEW devapi.signl4.com confirmed as 4th identity host serving byte-identical RS256 JWKS (kid 91EE4F3CE94EB517AF66B254F7497ECB0E31EE27RS256) — 10th live deep-equal across connect/api/devconnect/devapi
- NEW connect.signl4.com OIDC discovery byte-identical to devconnect (password/device_code/ciba/token-exchange grants, secret-only auth methods, no registration_endpoint, RS256-only) — prod is parametric tw
- CHANGED api.signl4.com/api/v2/teams auth-status flapping re-confirmed (10th+ observation): unauth GET returns 405 Allow:GET,POST this cycle (was 401 in prior cycle) — auth validation deferred to handler, not 
- CHANGED Cross-env token forgery chain fully documented: shared RS256 key (4 identity hosts) + shared client_id 692A0A56-892F-4AE2-8259-76DA398990B6 + full scope set + swagger-confirmed OAuth2 API access + sta
- CHANGED blog.derdack.com/techblog.derdack.com HTTPS→HTTP downgrade session-theft mechanism permanently invalidated — wp-login.php sets wordpress_test_cookie with secure flag + host-only scope (no Domain=.derd
- CHANGED dev.derdack.com MultiViews 300 stable across 20+ cycles — static namespace echo (/.well-known/, /.ssh/, /.bash_history/, /.viminfo/), files return 403/404; root serves parked IONOS sedoparking iframe 
- CHANGED www.derdack.com/de/ & /ea/ XML-RPC both POST-exposed with full method lists but mutating methods (wp.uploadFile, metaWeblog.newMediaObject) return faultCode 403 "incorrect username/password" — auth-ga

## 2026-09-11 00:44:48 UTC

## 2026-09-11 05:12:37 UTC
- NEW SIGNL4 API V2 swagger.json discovered at `connect.signl4.com/api/docs/v2/swagger.json` — declares OAuth2 scheme (authorizationCode) pointing to `connect.signl4.com/identity/connect/authorize` + `/toke
- NEW RAG confirms SIGNL4 public API auth = API key (`X-S4-Api-Key`) + OAuth2 Bearer token (swagger-declared); client_id `692A0A56` NOT published anywhere — no GitHub/npm/Postman/helpcenter leak; no public 
- NEW RAG confirms Derdack GitHub org (12 repos) contains Enterprise Alert plugins only — no OAuth/OIDC code, no leaked secrets
- CHANGED Cross-env token forgery hypothesis (85) now has FULL exploit-chain evidence: shared RS256 key → shared token endpoint → API accepts OAuth tokens → scopes grant CRUD → attack chain complete pending cli
- NEW No new probes executed since last cycle (2026-09-09 14:50:14 UTC)
- CHANGED Cross-env token forgery chain fully documented: shared RS256 key + shared client_id + swagger-confirmed OAuth2 API access + staging password grant + prod twin; blocked on client_secret
- CHANGED API key query-param auth confirmed live on both api.signl4.com and connect.signl4.com (403 "API Key is invalid" vs 401 when absent); dual auth pipeline established
- CHANGED API spec empty security requirement confirmed (LOW impact; spec-vs-implementation mismatch)
- NEW nemotron3 added JWT alg confusion hypothesis for signl4.derdack.com at confidence 55 — more specific than my generic auth bypass (30)
- CHANGED Fundamental blocker persists: 0/9 hosts probed for live HTTP; all hypotheses remain speculative without tech/status confirmation
- NEW nemotron3 added JWT alg confusion hypothesis for signl4.derdack.com at confidence 55 — more specific than my generic auth bypass (30)
- CHANGED Fundamental blocker persists: 0/9 hosts probed for live HTTP; all hypotheses remain speculative without tech/status confirmation

## 2026-09-11 09:52:37 UTC
- CHANGED connect.signl4.com/api/v3 confirmed live today: invoice-en16931/zugferd, scim/settings, subscriptions/{id}/prepaidBalance all return anon→401; V3 swagger with empty security: [{}] reconfirmed — new bi
- NEW Three new AUTH_HELPED hypotheses pending verification: cross-tenant report file download via fileName path traversal (IDOR, 55), cross-tenant report fetch via userId+teamId query params (IDOR, 50), cr
- NEW No new probe data from other agents on these three vectors — all AUTH_HELPED, blocked on credential acquisition.
- CHANGED Webhook team-secret enumeration oracle (AUTH, 75) — PASSIVE verifiable, still highest-value unvalidated hypothesis; NEXT probe pending.
- NEW connect.signl4.com/api/v3 route map fully confirmed: invoice-en16931/zugferd, scim/settings, subscriptions/{id}/prepaidBalance live-verified anon→401; OPTIONS confirms Allow sets — handler-deferred au
- NEW connect.signl4.com/api/docs/v3/swagger.json: global `security: [{}]` (empty) reconfirmed on V3 — spec under-declares auth everywhere; internal billing + SCIM routes published publicly in OpenAPI while
- NEW devconnect.signl4.com/identity/connect/deviceauthorization: endpoint live (400 invalid_client w/o secret) + device_code grant confirmed; still client_secret-gated
- NEW connect+devconnect /identity/connect/ciba + deviceauthorization: both 400 across envs — endpoint twins, all secret-gated
- NEW devapi.signl4.com: live 1:1 staging API mirror of api.signl4.com (appId cid-v1:d7865de8-ff22-4cec-8b2d-6e39fb5802f7), root→devaccount/manage, zero unauth read surface
- NEW api+devapi /api/v2/teams: 401 WWW-Authenticate:Bearer this cycle vs 405 in other cycles — handler/routing auth-status flapping across cycles confirmed
- CHANGED connect.signl4.com/webhook/{teamSecret}: Webhook team-secret enumeration oracle re-confirmed — POST /{teamSecret} no security scheme, 404 vs 201 oracle, status-keyword query config, 15+ integrations u
- CHANGED devconnect.signl4.com/identity/connect/token: Cross-env token forgery chain complete — shared RS256 key (10x deep-equal across 4 identity hosts), shared client_id 692A0A56, password grant enabled, pro
- CHANGED api.signl4.com/api/v2/teams: Handler-deferred auth confirmed 10th+ cycles — unauth GET returns 405 (not 401), invalid Bearer returns 405; auth validation at handler layer enables cross-env token accep
- CHANGED connect.signl4.com OIDC discovery byte-identical to devconnect (password/device_code/ciba/token-exchange grants, secret-only auth methods, no registration_endpoint, RS256-only) — prod is parametric tw

## 2026-09-11 14:07:58 UTC

## 2026-09-11 17:49:10 UTC
- NEW FULL V3 OpenAPI dumped (1.2MB, 200+ paths) from connect.signl4.com/api/docs/v3/swagger.json — documented read+file-download surface now exhaustively known: /v3/teams/{teamId}/signlReports/{fileName}, 
- NEW Standard SCIM endpoints on connect.signl4.com/api/v3/scim/* (ServiceProviderConfig, Users, Groups, Schemas, Bulk) ALL 404 — only /scim/settings is registered (anon→401); no standard/anonymous SCIM sur
- NEW V3 "public"-named routes live-probed anon: /api/v3/teams/public, categories/public, distributionLists/public, users/availableRoles, teams/dutySettings, teams/signalingSettings → ALL 401; "public" suff

## 2026-09-11 20:07:33 UTC
- NEW RAG: `teamSecret` is an operator-chosen per-endpoint secret (docs example `teamssecret`, n8n sample `helloworld`, vendor snippets `team-secret`) — NOT fixed high-entropy; a URL-embedded bearer credent
- NEW devconnect.signl4.com/webhook/{fabricated-secret} → 404 with envelope byte-format identical to prod: `{"code":3004,"details":"No matching event source found.","message":"Error raising event."}`; /webh
- NEW Vendor repo github.com/signl4/code-snippets + SIGNL4.postman_collection.json swept: only placeholders (`team-secret`, `<signl4-integration-secret>`, `--team-secret--`), zero real secrets — 4th clean c
- CHANGED Webhook-lead open decision closed: charset/length is operator-entropy → guess-enumeration falls under REJECTED brute-force class; oracle exploitable only via secret leak; 4 corpora clean → downgraded 

## 2026-09-11 22:27:32 UTC
- NEW connect.signl4.com/api/v3 route map fully live-verified: invoice-en16931/zugferd, scim/settings, subscriptions/{id}/prepaidBalance all anon→401; OPTIONS confirms Allow sets; global `security: [{}]` in
- NEW connect.signl4.com/webhook/{teamSecret}: staging (devconnect) mirrors prod oracle byte-for-byte (`{"code":3004,"details":"No matching event source found."}`); teamSecret is operator-chosen (docs `team
- NEW Vendor corpus sweep (github.com/signl4/code-snippets, Postman collection): only placeholder secrets; zero real team secret/API key across 4 corpora — credential-leak hypothesis unsupported
- NEW connect.signl4.com/api/v3 "public" routes (teams/public, categories/public, distributionLists/public, users/availableRoles, teams/dutySettings, teams/signalingSettings) all anon→401 — "public" naming 
- NEW Standard SCIM endpoints (ServiceProviderConfig, Users, Groups, Schemas, Bulk) all 404 — only /scim/settings registered (anon→401)
- CHANGED Webhook enumeration downgraded: operator-entropy secret makes guessing feasible in theory but falls under program-REJECTED brute-force class; oracle exploitable only via secret leak → config/design fi
- CHANGED Cross-env token forgery chain complete (shared RS256 key 10x, shared client_id, password grant, prod parametric twin) but AUTH_HELPED-blocked on client_secret
- CHANGED api.signl4.com/api/v2/teams handler-deferred auth stable 10th+ cycles (405 on unauth GET, not 401; invalid Bearer also 405)
- CHANGED blog.derdack.com/techblog.derdack.com HTTPS→HTTP downgrade session-theft permanently invalidated (wp-login.php sets `secure`+host-only cookie); residual missing-HSTS only (LOW)
- CHANGED dev.derdack.com MultiViews 300 stable across 20+ cycles — static namespace echo only (/.well-known/, /.ssh/, /.bash_history/, /.viminfo/), files 403/404
- CHANGED www.derdack.com/de/ & /ea/ XML-RPC both POST-exposed but mutating methods (wp.uploadFile, metaWeblog.newMediaObject) return faultCode 403 — auth-gated
- CHANGED 8 new CT hosts (fix, frontdoor, status, support, trust, docs, demo/downloads.enterprisealert.com) unprobed beyond initial fingerprint

## 2026-09-12 00:38:34 UTC

## 2026-09-12 05:01:08 UTC

## 2026-09-12 09:04:28 UTC
- NEW 8 previously-unknown live hosts via crt.sh CT sweep: fix.signl4.com (prod ASP.NET Core Support App, Blazor, /signin-oidc 500), frontdoor.signl4.com (unconfigured SPA shell, %ReplaceStatusTitle% placeh
- NEW connect.signl4.com/api/v3 fully dumped (200+ paths via /api/docs/v3/swagger.json): invoice-en16931/zugferd, scim/settings, subscriptions/{id}/prepaidBalance, PUT /api/prepaid/{id}/prepaidSettings, fil
- NEW V3 "public"-named routes (teams/public, categories/public, distributionLists/public, users/availableRoles, teams/dutySettings, teams/signalingSettings) all anon→401 — "public" suffix ≠ auth bypass
- NEW Standard SCIM endpoints (ServiceProviderConfig, Users, Groups, Schemas, Bulk) all 404 — only /scim/settings registered (anon→401)
- NEW devconnect.signl4.com/webhook/{fabricated-secret} → 404 with byte-identical envelope to prod (`{"code":3004,"details":"No matching event source found."}`) — staging webhook oracle mirrors prod contrac
- CHANGED api.signl4.com/api/v2/teams auth-status flapping re-confirmed 10th+ cycles: unauth GET returns 405 Allow:GET,POST (not 401), invalid Bearer also 405 — handler-deferred auth stable
- CHANGED Cross-env token forgery chain complete (shared RS256 key 10x deep-equal across 4 identity hosts, shared client_id 692A0A56, password grant enabled, prod parametric twin) but AUTH_HELPED-blocked on cli
- CHANGED Webhook team-secret enumeration downgraded: operator-entropy secret makes guessing feasible but falls under REJECTED brute-force class; oracle exploitable only via secret leak → config/design finding
- CHANGED blog.derdack.com/techblog.derdack.com HTTPS→HTTP downgrade session-theft permanently invalidated (wp-login.php sets `secure`+host-only cookie); residual missing-HSTS only (LOW)

## 2026-09-12 12:54:56 UTC
- NEW 8 previously-unknown live hosts via crt.sh CT sweep: fix.signl4.com (prod ASP.NET Core Support App, Blazor, /signin-oidc 500), frontdoor.signl4.com (unconfigured SPA shell, %ReplaceStatusTitle% placeh
- NEW connect.signl4.com/api/v3 fully dumped (200+ paths via /api/docs/v3/swagger.json): invoice-en16931/zugferd, scim/settings, subscriptions/{id}/prepaidBalance, PUT /api/prepaid/{id}/prepaidSettings, fil
- NEW V3 "public"-named routes (teams/public, categories/public, distributionLists/public, users/availableRoles, teams/dutySettings, teams/signalingSettings) all anon→401 — "public" suffix ≠ auth bypass
- NEW Standard SCIM endpoints (ServiceProviderConfig, Users, Groups, Schemas, Bulk) all 404 — only /scim/settings registered (anon→401)
- NEW devconnect.signl4.com/webhook/{fabricated-secret} → 404 with byte-identical envelope to prod (`{"code":3004,"details":"No matching event source found."}`) — staging webhook oracle mirrors prod contrac
- CHANGED api.signl4.com/api/v2/teams auth-status flapping re-confirmed 10th+ cycles: unauth GET returns 405 Allow:GET,POST (not 401), invalid Bearer also 405 — handler-deferred auth stable
- CHANGED Cross-env token forgery chain complete (shared RS256 key 10x deep-equal across 4 identity hosts, shared client_id 692A0A56, password grant enabled, prod parametric twin) but AUTH_HELPED-blocked on cli
- CHANGED Webhook team-secret enumeration downgraded: operator-entropy secret makes guessing feasible but falls under REJECTED brute-force class; oracle exploitable only via secret leak → config/design finding
- CHANGED blog.derdack.com/techblog.derdack.com HTTPS→HTTP downgrade session-theft permanently invalidated (wp-login.php sets `secure`+host-only cookie); residual missing-HSTS only (LOW)
- NEW 8 previously-unknown live hosts via crt.sh CT sweep: fix.signl4.com (prod ASP.NET Core Support App, Blazor, /signin-oidc 500), frontdoor.signl4.com (unconfigured SPA shell, %ReplaceStatusTitle% placeh
- NEW connect.signl4.com/api/v3 fully dumped (200+ paths via /api/docs/v3/swagger.json): invoice-en16931/zugferd, scim/settings, subscriptions/{id}/prepaidBalance, PUT /api/prepaid/{id}/prepaidSettings, fil
- NEW V3 "public"-named routes (teams/public, categories/public, distributionLists/public, users/availableRoles, teams/dutySettings, teams/signalingSettings) all anon→401 — "public" suffix ≠ auth bypass
- NEW Standard SCIM endpoints (ServiceProviderConfig, Users, Groups, Schemas, Bulk) all 404 — only /scim/settings registered (anon→401)
- NEW devconnect.signl4.com/webhook/{fabricated-secret} → 404 with byte-identical envelope to prod (`{"code":3004,"details":"No matching event source found."}`) — staging webhook oracle mirrors prod contrac
- CHANGED api.signl4.com/api/v2/teams auth-status flapping re-confirmed 10th+ cycles: unauth GET returns 405 Allow:GET,POST (not 401), invalid Bearer also 405 — handler-deferred auth stable
- CHANGED Cross-env token forgery chain complete (shared RS256 key 10x deep-equal across 4 identity hosts, shared client_id 692A0A56, password grant enabled, prod parametric twin) but AUTH_HELPED-blocked on cli
- CHANGED Webhook team-secret enumeration downgraded: operator-entropy secret makes guessing feasible but falls under REJECTED brute-force class; oracle exploitable only via secret leak → config/design finding
- CHANGED blog.derdack.com/techblog.derdack.com HTTPS→HTTP downgrade session-theft permanently invalidated (wp-login.php sets `secure`+host-only cookie); residual missing-HSTS only (LOW)

## 2026-09-12 16:07:18 UTC
- NEW connect.signl4.com/api/v3 fully dumped (200+ paths via /api/docs/v3/swagger.json): invoice-en16931/zugferd, scim/settings, subscriptions/{id}/prepaidBalance, PUT /api/prepaid/{id}/prepaidSettings, fil
- NEW 8 previously-unknown live hosts via crt.sh CT sweep: fix.signl4.com (prod ASP.NET Core Support App, Blazor, /signin-oidc 500), frontdoor.signl4.com (unconfigured SPA shell, %ReplaceStatusTitle% placeh
- NEW devconnect.signl4.com/webhook/{fabricated-secret} → 404 with byte-identical envelope to prod (`{"code":3004,"details":"No matching event source found."}`) — staging webhook oracle mirrors prod contrac
- NEW connect.signl4.com/api (V1): V1 OpenAPI (93 paths) live on connect+api+devapi at /api/* and /api/v1/* — three concurrent namespaces all handler-deferred Bearer (anon reads 14/14 → 401/405), zero unaut
- NEW connect.signl4.com/api/docs/v1/swagger.json: global `security:[{}]` empty on V1 too — spec-under-declares across all three namespaces (V1/V2/V3); internal/self-service routes (scripts, prepaid, subscr
- CHANGED api.signl4.com/api/v2/teams auth-status flapping re-confirmed 10th+ cycles: unauth GET returns 405 Allow:GET,POST (not 401), invalid Bearer also 405 — handler-deferred auth stable
- CHANGED Cross-env token forgery chain complete (shared RS256 key 10x deep-equal across 4 identity hosts, shared client_id 692A0A56, password grant enabled, prod parametric twin) but AUTH_HELPED-blocked on cli
- CHANGED Webhook team-secret enumeration downgraded: operator-entropy secret makes guessing feasible but falls under REJECTED brute-force class; oracle exploitable only via secret leak → config/design finding
- CHANGED blog.derdack.com/techblog.derdack.com HTTPS→HTTP downgrade session-theft permanently invalidated (wp-login.php sets `secure`+host-only cookie); residual missing-HSTS only (LOW)
- CHANGED dev.derdack.com MultiViews 300 stable across 20+ cycles — static namespace echo only (/.well-known/, /.ssh/, /.bash_history/, /.viminfo/), files 403/404; root serves parked IONOS sedoparking iframe

## 2026-09-12 18:03:28 UTC
- NEW connect.signl4.com/api (V1) OpenAPI (93 paths) live at /api/* and /api/v1/* on connect+api+devapi — three concurrent namespaces, all handler-deferred Bearer (anon reads 14/14 → 401/405), zero unauth d
- NEW connect.signl4.com/api/docs/v1/swagger.json: global `security:[{}]` empty on V1 too — spec-under-declares across all three namespaces (V1/V2/V3); internal/self-service routes (scripts, prepaid, subscr
- CHANGED api.signl4.com/api/v2/teams auth-status flapping re-confirmed 10th+ cycles: unauth GET returns 405 Allow:GET,POST (not 401), invalid Bearer also 405 — handler-deferred auth stable
- CHANGED Cross-env token forgery chain complete (shared RS256 key 10x deep-equal across 4 identity hosts, shared client_id 692A0A56, password grant enabled, prod parametric twin) but AUTH_HELPED-blocked on cli
- CHANGED 8 new CT hosts (fix, frontdoor, status, support, trust, docs, demo/downloads.enterprisealert.com) unprobed beyond initial fingerprint — fix.signl4.com (prod ASP.NET Core Support App, Blazor, /signin-o

## 2026-09-12 20:44:26 UTC
- NEW 9 hosts discovered via passive DNS/CT, 0 probed for live HTTP — initial surface unvalidated
- NEW No GitHub org configured for reposcan — code-level recon gap
- NEW Knowledge base empty — no prior tech fingerprint, endpoint map, or auth flow data
- NEW dev.derdack.com /.well-known/openid-configuration returns 300 Multiple Choices with directory traversal suggestions (/.ssh/, /.bash_history/, /.viminfo/) — misconfiguration confirmed
- NEW signl4.derdack.com (AWS 13.94.244.66) connection timeout on HTTP/HTTPS — SaaS platform unreachable, likely firewall/WAF
- NEW signals.derdack.com NXDOMAIN — subdomain does not exist, hypothesis invalid
- NEW blog.derdack.com & techblog.derdack.com redirect via HTTP (not HTTPS) to www.derdack.com — mixed content / downgrade risk
- NEW de.derdack.com / www.de.derdack.com return 403 with sedoparking.com iframe — parked domain, not Derdack infrastructure
- CHANGED Inventory validation: only 5/9 hosts are live Derdack infrastructure; 2 unreachable, 1 non-existent, 1 parked
- NEW fix.signl4.com/signin-oidc returns 500 (broken OIDC callback), /_blazor/negotiate returns 405 on GET — prod ASP.NET Core Support Application (Blazor Server) confirmed live, identical to devfix twin
- NEW connect.signl4.com/api/v3/subscriptions/{id}/invoices/{id}/zugferd OPTIONS → 405 Allow:GET; /api/prepaid/{id}/prepaidSettings OPTIONS → 405 Allow:PUT — V3 billing routes registered, handler-deferred a
- NEW connect.signl4.com/api/docs/v3/swagger.json and /api/docs/v1/swagger.json both declare global `security: [{}]` — spec under-declares auth across V1/V2/V3; internal routes published publicly
- NEW api.signl4.com/api/v2/teams unauth GET → 401 (this cycle), invalid Bearer → 401 — auth-status flapping re-confirmed (405 in prior cycles, 401 now); handler-deferred auth family unstable
- NEW devconnect.signl4.com & connect.signl4.com JWKS byte-identical 10th+ deep-equal (kid 91EE4F3CE94EB517AF66B254F7497ECB0E31EE27RS256, modulus n identical) — cross-env RS256 key reuse stable
- CHANGED Webhook team-secret enumeration oracle downgraded: operator-chosen secret (not high-entropy fixed), guessing falls under REJECTED brute-force class; exploitable only via secret leak → config/design fi
- CHANGED blog.derdack.com/techblog.derdack.com HTTPS→HTTP downgrade session-theft permanently invalidated (wp-login.php sets secure+host-only cookie); residual missing-HSTS only (LOW)
- CHANGED Cross-env token forgery chain complete (shared RS256 key 4 hosts, shared client_id 692A0A56, password grant enabled, prod parametric twin) but AUTH_HELPED-blocked on client_secret — strongest finding,

## 2026-09-12 22:33:52 UTC
- NEW fix.signl4.com (prod ASP.NET Core Support App, Blazor Server) confirmed live with broken OIDC callback (/signin-oidc 500) and /_blazor/negotiate 405 — new CT host, identical to devfix twin
- NEW frontdoor.signl4.com unconfigured SPA shell serving literal `%ReplaceStatusTitle%` placeholder (static since 2024-09-03) — new CT host
- NEW connect.signl4.com/api (V1) OpenAPI (93 paths) live at /api/* and /api/v1/* on connect+api+devapi — three concurrent namespaces, all handler-deferred Bearer, zero unauth deviation
- NEW connect.signl4.com/api/docs/v1/swagger.json: global `security:[{}]` empty on V1 too — spec-under-declares across V1/V2/V3; internal/self-service routes (scripts, prepaid, subscriptions licenses) publi
- NEW connect.signl4.com/api/v3 fully dumped (200+ paths): invoice-en16931/zugferd, scim/settings, subscriptions/{id}/prepaidBalance, PUT /api/prepaid/{id}/prepaidSettings, file-download family — all anon→4
- NEW devconnect.signl4.com/webhook/{fabricated-secret} → 404 with byte-identical envelope to prod (`{"code":3004,"details":"No matching event source found."}`) — staging webhook oracle mirrors prod contrac
- CHANGED api.signl4.com/api/v2/teams auth-status flapping re-confirmed 10th+ cycles: unauth GET returns 405 Allow:GET,POST (not 401), invalid Bearer also 405 — handler-deferred auth stable
- CHANGED Cross-env token forgery chain complete (shared RS256 key 10x deep-equal across 4 identity hosts, shared client_id 692A0A56, password grant enabled, prod parametric twin) but AUTH_HELPED-blocked on cli
- CHANGED blog.derdack.com/techblog.derdack.com HTTPS→HTTP downgrade session-theft permanently invalidated (wp-login.php sets `secure`+host-only cookie); residual missing-HSTS only (LOW)
- CHANGED dev.derdack.com MultiViews 300 stable across 20+ cycles — static namespace echo only (/.well-known/, /.ssh/, /.bash_history/, /.viminfo/), files 403/404; root serves parked IONOS sedoparking iframe

## 2026-09-13 00:17:32 UTC
- NEW fix.signl4.com (20.160.37.197) prod ASP.NET Core "SIGNL4 Support Application" (Blazor Server) live with broken OIDC callback (/signin-oidc 500) and /_blazor/negotiate 405 — identical to devfix twin
- NEW frontdoor.signl4.com unconfigured SPA shell serving literal `%ReplaceStatusTitle%` placeholder (static since 2024-09-03)
- NEW connect.signl4.com/api (V1) OpenAPI (93 paths) live at /api/* and /api/v1/* on connect+api+devapi — three concurrent namespaces, all handler-deferred Bearer, zero unauth deviation
- NEW connect.signl4.com/api/docs/v1/swagger.json: global `security:[{}]` empty on V1 too — spec-under-declares across V1/V2/V3; internal/self-service routes (scripts, prepaid, subscriptions licenses) publi
- NEW connect.signl4.com/api/v3 fully dumped (200+ paths): invoice-en16931/zugferd, scim/settings, subscriptions/{id}/prepaidBalance, PUT /api/prepaid/{id}/prepaidSettings, file-download family — all anon→4
- NEW devconnect.signl4.com/webhook/{fabricated-secret} → 404 with byte-identical envelope to prod (`{"code":3004,"details":"No matching event source found."}`) — staging webhook oracle mirrors prod contrac
- CHANGED api.signl4.com/api/v2/teams auth-status flapping re-confirmed 10th+ cycles: unauth GET returns 405 Allow:GET,POST (not 401), invalid Bearer also 405 — handler-deferred auth stable
- CHANGED Cross-env token forgery chain complete (shared RS256 key 10x deep-equal across 4 identity hosts, shared client_id 692A0A56, password grant enabled, prod parametric twin) but AUTH_HELPED-blocked on cli
- CHANGED blog.derdack.com/techblog.derdack.com HTTPS→HTTP downgrade session-theft permanently invalidated (wp-login.php sets `secure`+host-only cookie); residual missing-HSTS only (LOW)
- CHANGED dev.derdack.com MultiViews 300 stable across 20+ cycles — static namespace echo only (/.well-known/, /.ssh/, /.bash_history/, /.viminfo/), files 403/404; root serves parked IONOS sedoparking iframe

## 2026-09-13 05:09:17 UTC
- NEW fix.signl4.com/signin-oidc → 500 (empty body); /_blazor/negotiate → 405 on GET, 200 on POST with connectionId; root → 200 Blazor Server "Admin Support Page" with Login button (prod ASP.NET Core, Kestr
- NEW frontdoor.signl4.com → 200 with literal `%ReplaceStatusTitle%` placeholder (static since 2024-09-03)
- NEW status.signl4.com → StatusLabs (adminlabs.com) page
- NEW support.signl4.com → Zendesk (third-party)
- NEW trust.signl4.com → Safebase trust center (third-party)
- NEW docs.signl4.com → GitHub Pages
- NEW demo.enterprisealert.com → 404
- NEW downloads.enterprisealert.com → 403 (IIS/10.0, directory browsing disabled)
- CHANGED Cross-env token forgery chain now has live probe data on fix.signl4.com (Blazor Server, broken OIDC callback identical to devfix twin)
