## REPOSCAN 2026-09-03 15:10:29 UTC
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-03 18:40:05 UTC
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-03 21:20:17 UTC
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-03 23:19:28 UTC
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-04 01:02:53 UTC
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-04 05:58:17 UTC
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-04 10:02:04 UTC
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-04 14:23:16 UTC
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-04 17:50:03 UTC
[HYP] Hardcoded SIGNL4 Team Secret in Google IoT Integration Sample
class: SECRET
asset: signl4/signl4-integration-google-iot/index.js:19
confidence: 85
reasoning: SIGNL4 team secret `96sbq38s` is hardcoded directly in the webhook URL `https://connect.signl4.com/webhook/96sbq38s` — not a placeholder (no `<team-secret>` or `YOUR_SECRET` marker). This is a public repo under the signl4 GitHub org (Derdack-owned). The secret is a real alphanumeric string committed to source. No other files in this repo reference this value, suggesting it may be a Derdack-internal demo/test team.
impact: Medium — If valid, any party can send arbitrary alerts to this SIGNL4 team via the webhook. Could be used for alert flooding, social engineering via fake incident notifications, or to probe the team's response workflows. Impact取决于 whether the team still exists and is active.
verify_steps: Passive only: (1) Confirm repo ownership at github.com/signl4/signl4-integration-google-iot (2) Check if `connect.signl4.com/webhook/96sbq38s` returns HTTP 201 vs 404 via `curl -s -o /dev/null -w '%{http_code}' -X POST https://connect.signl4.com/webhook/96sbq38s -H 'Content-Type: application/json' -d '{"Title":"test"}'` (3) If 201, secret is live — rotate immediately. If 404, team was deleted and finding is historical only.
[HYP] Hardcoded SIGNL4 Team Secret in Postman Collection & DevTools YAML (same secret, two files)
class: SECRET
asset: signl4/code-snippets/SIGNL4.postman_collection.json:42 + signl4/docs/integrations/devtools/SIGNL4_Alerting.yaml:7
confidence: 80
reasoning: Team secret `vbguzfsi` appears in two public repos: (1) Postman collection path array `[webhook, vbguzfsi]` while the `raw` field shows `--team-secret--` placeholder — the path array was not sanitized before commit; (2) DevTools YAML `url: https://connect.signl4.com/webhook/vbguzfsi` hardcoded directly. Both are under signl4 GitHub org. Same secret reused across two sample repos suggests a Derdack employee's real team secret used during development.
impact: Medium — Same as above: unauthorized alert injection, alert flooding, potential social engineering via fake incidents. Two repos expose the same secret, increasing the blast radius.
verify_steps: Passive only: (1) Confirm repo ownership (2) `curl -s -o /dev/null -w '%{http_code}' -X POST https://connect.signl4.com/webhook/vbguzfsi -H 'Content-Type: application/json' -d '{"Title":"test"}'` (3) If 201, rotate immediately.
[HYP] Commented-Out Pipedream Debug Webhook in Zabbix Integration
class: OTHER
asset: signl4/signl4-integration-zabbix/signl4-mediatype.yaml:103
confidence: 70
reasoning: Line contains commented-out debug endpoint: `//endpoint = 'https://b58aee12b873eae71b5db8b4fdc77d78.m.pipedream.net';` — a Pipedream request inspection URL. This is a developer debug/test artifact left in production Zabbix media type export. While commented out, it reveals an internal testing endpoint and confirms Pipedream was used for webhook debugging. The UUID `b58aee12b873eae71b5db8b4fdc77d78` is a real Pipedream endpoint ID.
impact: Low — Commented-out code is not executed. However, it leaks a historical debug endpoint that could be investigated for further information. If someone uncomments it, all Zabbix alerts would be sent to a third-party service (Pipedream) instead of SIGNL4.
verify_steps: Passive only: (1) Check if the Pipedream endpoint is still active: `curl -s -o /dev/null -w '%{http_code}' https://b58aee12b873eae71b5db8b4fdc77d78.m.pipedream.net` (2) If active, confirms debug artifact was real (not just a test UUID).
TARGET_ORG not configured for derdack; skipping public-org deep scan.
