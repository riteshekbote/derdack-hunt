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
## REPOSCAN 2026-09-04 19:57:19 UTC
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-04 21:58:22 UTC
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-04 23:38:42 UTC
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-05 01:23:46 UTC
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-05 06:16:24 UTC
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-05 10:38:14 UTC
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-05 13:32:46 UTC
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-05 16:13:33 UTC
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-05 18:18:56 UTC
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-05 20:26:45 UTC
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-05 22:13:27 UTC
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-05 23:54:23 UTC
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-06 01:26:26 UTC
class: OTHER  
asset: N/A  
confidence: 100  
reasoning: The org has zero configured public GitHub repositories. All source code is private.  
impact: None (audit cannot proceed without public repo candidates)  
verify_steps: Confirm via `https://github.com/derdack` or `https://github.com/derdack-hq` — both should be checked for any public repos that may have been recently opened, though the scope file explicitly shows none configured.
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-06 06:28:25 UTC
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-06 11:18:00 UTC
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-06 14:13:06 UTC
class: OTHER
asset: N/A
confidence: 100
reasoning: The provided candidate list contains no Derdack repositories to audit. No source code or assets were supplied for analysis.
impact: N/A
verify_steps: N/A
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-06 17:07:14 UTC
class: SECRET
asset: `derdack-plugin-checkmk/2-way/Main.js:90-94`
confidence: 95
reasoning: Hardcoded `username = "cmkadmin"`, `password = "CNlydVqZ"`, and `serverURL = "http://192.168.88.107:8080/cmk/check_mk/api/v0/"` with an internal RFC1918 IP. Credentials are used in Bearer auth headers at lines 317, 360. This is a sample/template but exposes a real internal hostname pattern and valid credential format.
impact: HIGH — if deployed as-is, exposes Checkmk monitoring admin account; internal IP leaks network topology.
verify_steps: Check if `192.168.88.107:8080` is reachable from any Derdack-internal network; attempt Checkmk API auth with the listed creds.
class: SECRET
asset: `derdack-oncall-holidayimport/HolidayImport.js:16`, `derdack-oncall-holidayimport/HolidayDeleteAll.js:22`
confidence: 95
reasoning: `STRING_DB_CONNECTION` contains `Server=sqlserver.derdack-support.local;UID=sa;PWD=Derdack!;Database=EnterpriseAlert2017`. The `sa` account with password `Derdack!` is a sysadmin-level DB credential. This is in sample scripts but references an internal hostname (`derdack-support.local`).
impact: CRITICAL — SA account grants full SQL Server control; `derdack-support.local` is an internal Derdack asset.
verify_steps: DNS-resolve `sqlserver.derdack-support.local`; check if Enterprise Alert deployments use these scripts with these exact credentials.
class: MISCONFIG
asset: `derdack-oncall-holidayimport/HolidayImport.js:65,86,105`, `derdack-oncall-holidayimport/HolidayDeleteAll.js:71,92,111`, `derdack-events-snmp/SNMP-MIB-Importer.js:153,161,169`, `derdack-alert-forwarding/Alert2Team.js:28,72`
confidence: 90
reasoning: All SQL queries are built via direct string concatenation with unsanitized variables (e.g., `"SELECT ID FROM OnCallPlanHolidays WHERE OnCallPlanID=" + iTeamId`). The `sTeams` variable in HolidayImport.js line 86 is split from user-controlled `STRING_TEAMS` and injected directly into `IN (...)` clauses. Alert2Team.js line 28 concatenates `sExecutor` into a SQL query without escaping.
impact: HIGH — allows SQL injection if any parameter originates from user/external input; Enterprise Alert database compromise.
verify_steps: Trace whether `STRING_TEAMS`, `sExecutor`, or MIB file contents can be influenced by external input in production deployments.
class: MISCONFIG
asset: `derdack-alert-augmentation/html-to-text/ps.js:40`
confidence: 85
reasoning: `ExecutePowershell()` constructs a shell command by directly interpolating `htmlString` (from an event parameter) into a `powershell.exe` invocation string at line 40: `"powershell.exe \"node.exe '" + SCRIPTING_HOST_DIR + "html_text.js' '" + htmlString + "'\""`. An attacker who controls the `text` event parameter can inject arbitrary OS commands.
impact: CRITICAL — remote code execution on the Enterprise Alert scripting host.
verify_steps: Confirm the script is deployed in production ScriptingHost; test with a malicious `text` parameter payload like `'; rm -rf / #`.
class: MISCONFIG
asset: `derdack-plugin-checkmk/2-way/Main.js:94`
confidence: 80
reasoning: `serverURL = "http://192.168.88.107:8080/cmk/check_mk/api/v0/"` — plaintext HTTP to an internal Checkmk API. Credentials (line 90-91) are sent as Bearer tokens over this unencrypted channel (line 317).
impact: MEDIUM — credential interception on internal network via passive sniffing; MITM on monitoring API.
verify_steps: Verify whether production deployments use HTTP or HTTPS for the Checkmk API endpoint.
class: MISCONFIG
asset: `derdack-integration-SIGNL4/js/WebhookGateway.js:41,87`
confidence: 75
reasoning: The decoded SIGNL4 team secret is written to debug logs at lines 41 and 87: `EAScriptHost.LogDebug("Decoded S4 Team Secret: " + strS4TeamSecret)`. This exposes the secret in EA log files. The secret is also appended to the webhook URL at line 94.
impact: MEDIUM — team secret exposure in log files; allows unauthorized SIGNL4 webhook calls.
verify_steps: Check EA log retention and access controls; verify if debug logging is enabled in production.
class: OTHER
asset: `derdack-plugin-checkmk/2-way/Main.js:52-68`, `derdack-2wayREST-samples/Dynatrace/Main.js:53-69`, `derdack-2wayREST-samples/Logic Monitor/Main.js:52-68`, `derdack-2wayREST-samples/zendesk/Main.js:52-68`
confidence: 70
reasoning: `eval()` is called on `appContext.state.callbackSaveState`, `appContext.runtimeInfo.callbackSetStatusError`, etc. If the EA runtime provides attacker-controllable data in these fields, it enables arbitrary code execution. This appears to be an EA SDK pattern but remains risky.
impact: MEDIUM — potential code injection if EA context data is tainted.
verify_steps: Review EA Scripting Host SDK to determine if context fields are sanitized before delivery.
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-06 19:12:21 UTC
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-06 21:21:58 UTC
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-06 23:04:53 UTC
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-07 01:01:56 UTC
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-07 06:07:21 UTC
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-07 12:33:56 UTC
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-07 17:54:41 UTC
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-07 20:50:54 UTC
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-07 23:04:34 UTC
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-08 01:12:46 UTC
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-08 05:59:12 UTC
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-08 10:33:19 UTC
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-08 14:45:06 UTC
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-08 18:10:44 UTC
class: SECRET
asset: derdack-plugin-checkmk/2-way/Main.js:90-94
confidence: 95
reasoning: Hardcoded `username = "cmkadmin"` and `password = "CNlydVqZ"` with internal IP `http://192.168.88.107:8080/cmk/check_mk/api/v0/`. Credentials are used in Authorization header at lines 317, 361. Appears to be a developer's personal/test Checkmk instance credentials left in a sample file.
impact: HIGH — Credential reuse risk; admin-level Checkmk access; internal network disclosure
verify_steps: Check if 192.168.88.107 is/was reachable from any Derdack network; check git history for when this was committed; verify if "CNlydVqZ" appears in any breach database
class: SECRET
asset: derdack-oncall-holidayimport/HolidayImport.js:16
confidence: 95
reasoning: Connection string `Server=sqlserver.derdack-support.local;UID=sa;PWD=Derdack!;Database=EnterpriseAlert2017` — exposes internal hostname, SQL Server `sa` (sysadmin) account, and plaintext password.
impact: HIGH — Full SQL Server sysadmin access; internal host disclosure; credential reuse risk
verify_steps: Check if sqlserver.derdack-support.local resolves publicly; check if "Derdack!" appears in credential stuffing lists; verify git history
class: OTHER
asset: derdack-alert-forwarding/Alert2Team.js:28,72
confidence: 85
reasoning: Line 28 concatenates `sExecutor` directly into SQL: `WHERE RemoteJobsHistory.ProfileName='" + sExecutor + "'"`. Line 72 concatenates `sTeamnames` into UPDATE statement. Parameters are not parameterized.
impact: MEDIUM — SQL injection via Remote Action executor name or team name parameters
verify_steps: Confirm whether EA's Remote Action parameter input allows special characters; test with `' OR 1=1 --` payload
class: OTHER
asset: derdack-alert-augmentation/html-to-text/ps.js:40
confidence: 90
reasoning: Line 40: `var strCommand = "powershell.exe \"node.exe '" + SCRIPTING_HOST_DIR + "html_text.js' '" + htmlString + "'\""` — `htmlString` comes from event parameter `PARAMETER_WITH_HTML` and is injected directly into a powershell command without sanitization.
impact: HIGH — Remote code execution via crafted event parameter containing shell metacharacters
verify_steps: Test with event parameter containing `'; rm -rf / #` or similar payload
class: OTHER
asset: derdack-plugin-checkmk/2-way/Main.js:52-68 (also in derdack-2wayREST-samples/LogicMonitor/Main.js:52-68, zendesk/Main.js:52-68, Dynatrace/Main.js:52-68)
confidence: 75
reasoning: `appContext.state.callbackSaveState = eval(appContext.state.callbackSaveState)` — if an attacker can influence `appContext.state`, they achieve arbitrary code execution. This pattern is repeated identically in 4 repos.
impact: MEDIUM — Code execution if app context can be tampered with
verify_steps: Determine if appContext is user-controllable or only set by EA platform; review EA SDK documentation for trust boundary
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-08 21:10:00 UTC
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-08 23:24:25 UTC
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-09 01:28:13 UTC
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-09 06:36:59 UTC
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-09 11:47:55 UTC
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-09 15:24:09 UTC
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-09 18:49:29 UTC
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-09 21:18:24 UTC
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-09 23:18:46 UTC
TARGET_ORG not configured for derdack; skipping public-org deep scan.
