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
