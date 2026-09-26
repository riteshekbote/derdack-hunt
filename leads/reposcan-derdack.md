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
## REPOSCAN 2026-09-10 01:07:58 UTC
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-10 05:58:55 UTC
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-10 10:31:51 UTC
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-10 14:36:45 UTC
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-10 17:50:06 UTC
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-10 20:08:09 UTC
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-10 22:38:03 UTC
[HYP] Hardcoded MySQL Credentials in SIGNL4 MariaDB Integration Sample
class: SECRET
asset: signl4/signl4-integration-mysql-mariadb/db2signl.php:10-13
confidence: 75
reasoning: `STRING_DB_USER = "signl4"` and `STRING_DB_PASS = "signl4"` are hardcoded real credential values (not placeholders like `<password>`). While intended as sample code, users who deploy this without changing credentials expose a local MySQL instance with known username/password pair. The password `signl4` matches the database name, suggesting a default install pattern.
impact: Low — Sample code only; impact depends on whether any deployment ships with these defaults. No Derdack-internal hostname exposed.
verify_steps: Passive only: (1) Confirm repo ownership at github.com/signl4/signl4-integration-mysql-mariadb (2) Search GitHub code search for `STRING_DB_PASS = "signl4"` to see if any forks/deployments use this verbatim (3) No live infrastructure to probe — credentials are for localhost MySQL only.
[HYP] SIGNL4 Team Secret Logged at INFO Level in ioBroker Adapter
class: SECRET
asset: signl4/ioBroker.signl4/main.js:40
confidence: 85
reasoning: Line 40: `this.log.info('config team_secret: ' + this.config.team_secret);` logs the SIGNL4 team secret to ioBroker's info-level log on adapter ready. This is a different repo from the prior finding in `derdack-integration-SIGNL4/js/WebhookGateway.js:41,87` (which logged at DEBUG level). INFO-level logs are typically retained longer and are more accessible than DEBUG logs in production ioBroker installations.
impact: Medium — Team secret exposure in ioBroker log files. Any user with access to ioBroker admin/logs can read the secret and send arbitrary alerts to the SIGNL4 team. Impact取决于 whether the ioBroker adapter is deployed in production.
verify_steps: Passive only: (1) Confirm repo ownership at github.com/signl4/ioBroker.signl4 (2) Check if ioBroker log files are typically stored in a world-readable location (3) Verify if the `this.log.info` call is present in the published npm package version (4) No live infrastructure to probe — this is a code-level finding.
[HYP] Commented-Out SQL Server SA Credentials with Internal Derdack Hostname
class: SECRET
asset: signl4/signl4-integration-sql-server/db2signl.ps1:14
confidence: 70
reasoning: Line 14 contains a commented-out connection string: `Server=sqlserver.derdack-support.local;Trusted_Connection=No;UID=sa;PWD=none;Database=EnterpriseAlert2017`. This exposes: (1) internal Derdack hostname `sqlserver.derdack-support.local`, (2) SQL Server SA (sysadmin) account, (3) password `none`. While commented out and in a different file from the prior finding in `derdack-oncall-holidayimport/HolidayImport.js:16` (which had password `Derdack!`), this confirms the internal hostname pattern and shows a second credential variant for the same SA account.
impact: Low — Commented-out code is not executed. However, it leaks an internal Derdack hostname and a second password variant for the SA account. If `sqlserver.derdack-support.local` resolves on any Derdack-internal network, the hostname disclosure is valuable for lateral movement.
verify_steps: Passive only: (1) Confirm repo ownership (2) DNS-resolve `sqlserver.derdack-support.local` from external (should fail — internal only) (3) Compare with prior finding: HolidayImport.js has `PWD=Derdack!` while this has `PWD=none` — two password variants for the same SA account suggest credential rotation or multiple test environments.
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-11 00:33:06 UTC
[HYP] Hardcoded SIGNL4 Team Secret `96sbq38s` in Google IoT Integration
class: SECRET
asset: signl4/signl4-integration-google-iot/index.js:19
confidence: 85
reasoning: Team secret `96sbq38s` is hardcoded directly in the webhook URL `https://connect.signl4.com/webhook/96sbq38s` — not a placeholder (no `<team-secret>` or `YOUR_SECRET` marker). This is a real alphanumeric string committed to source. The repo is owned by the signl4 GitHub org (Derdack-owned).
impact: Medium — Any party can send arbitrary alerts to this SIGNL4 team via the webhook. Could be used for alert flooding, social engineering via fake incident notifications, or to probe the team's response workflows.
verify_steps: (1) Confirm repo ownership at github.com/signl4/signl4-integration-google-iot (2) `curl -s -o /dev/null -w '%{http_code}' -X POST https://connect.signl4.com/webhook/96sbq38s -H 'Content-Type: application/json' -d '{"Title":"test"}'` (3) If 201, secret is live — rotate immediately. If 404, team was deleted and finding is historical only.
[HYP] Hardcoded SIGNL4 Team Secret `vbguzfsi` in Postman Collection & DevTools YAML
class: SECRET
asset: signl4/code-snippets/SIGNL4.postman_collection.json:40 + signl4/docs/integrations/devtools/SIGNL4_Alerting.yaml:7
confidence: 80
reasoning: Team secret `vbguzfsi` appears in two files: (1) Postman collection path array `["webhook", "vbguzfsi"]` while the `raw` field shows `--team-secret--` placeholder — the path array was not sanitized before commit; (2) DevTools YAML `url: https://connect.signl4.com/webhook/vbguzfsi` hardcoded directly. Same secret reused across two files suggests a Derdack employee's real team secret used during development.
impact: Medium — Unauthorized alert injection, alert flooding, potential social engineering via fake incidents. Two files expose the same secret, increasing blast radius.
verify_steps: (1) Confirm repo ownership (2) `curl -s -o /dev/null -w '%{http_code}' -X POST https://connect.signl4.com/webhook/vbguzfsi -H 'Content-Type: application/json' -d '{"Title":"test"}'` (3) If 201, rotate immediately.
[HYP] Hardcoded Checkmk Admin Credentials with Internal IP
class: SECRET
asset: derdack-plugin-checkmk/2-way/Main.js:90-94
confidence: 95
reasoning: Hardcoded `username = "cmkadmin"`, `password = "CNlydVqZ"`, and `serverURL = "http://192.168.88.107:8080/cmk/check_mk/api/v0/"` with an internal RFC1918 IP. Credentials are used in Bearer auth headers at lines 317, 360. This exposes a real internal hostname pattern and valid credential format. The IP `192.168.88.107` matches the pattern used in other Derdack samples (e.g., `derdack-2wayREST-samples/README.md:147`).
impact: HIGH — If deployed as-is, exposes Checkmk monitoring admin account; internal IP leaks network topology. Credential reuse risk if same password is used elsewhere.
verify_steps: (1) Check if 192.168.88.107 is/was reachable from any Derdack network (2) Check git history for when this was committed (3) Verify if "CNlydVqZ" appears in any breach database.
[HYP] Hardcoded SQL Server SA Credentials with Internal Derdack Hostname
class: SECRET
asset: derdack-oncall-holidayimport/HolidayImport.js:16 + HolidayDeleteAll.js:22
confidence: 95
reasoning: Connection string `Server=sqlserver.derdack-support.local;Trusted_Connection=No;UID=sa;PWD=Derdack!;Database=EnterpriseAlert2017` — exposes internal hostname, SQL Server `sa` (sysadmin) account, and plaintext password. The `sa` account with password `Derdack!` is a sysadmin-level DB credential. `derdack-support.local` is an internal Derdack asset.
impact: CRITICAL — SA account grants full SQL Server control; internal host disclosure; credential reuse risk. If `sqlserver.derdack-support.local` resolves on any Derdack-internal network, this is a direct compromise vector.
verify_steps: (1) DNS-resolve `sqlserver.derdack-support.local` from external (should fail — internal only) (2) Check if "Derdack!" appears in credential stuffing lists (3) Verify git history.
[HYP] Commented-Out SQL Server SA Credentials (Second Password Variant)
class: SECRET
asset: signl4/signl4-integration-sql-server/db2signl.ps1:14
confidence: 70
reasoning: Line 14 contains a commented-out connection string: `Server=sqlserver.derdack-support.local;Trusted_Connection=No;UID=sa;PWD=none;Database=EnterpriseAlert2017`. This exposes: (1) internal Derdack hostname `sqlserver.derdack-support.local`, (2) SQL Server SA account, (3) password `none`. Two password variants for the same SA account (`Derdack!` in HolidayImport.js vs `none` here) suggest credential rotation or multiple test environments.
impact: Low — Commented-out code is not executed. However, it leaks an internal Derdack hostname and a second password variant for the SA account. Valuable for lateral movement if the hostname resolves internally.
verify_steps: (1) Confirm repo ownership (2) DNS-resolve `sqlserver.derdack-support.local` from external (3) Compare with prior finding: HolidayImport.js has `PWD=Derdack!` while this has `PWD=none`.
[HYP] SQL Injection via String Concatenation in Enterprise Alert Scripts
class: MISCONFIG
asset: derdack-oncall-holidayimport/HolidayImport.js:65,86,105 + derdack-alert-forwarding/Alert2Team.js:28,72
confidence: 90
reasoning: All SQL queries are built via direct string concatenation with unsanitized variables. HolidayImport.js:65 — `"SELECT ID FROM OnCallPlanHolidays WHERE OnCallPlanID=" + iTeamId + " AND Holiday='" + sDate + "'"`. HolidayImport.js:86 — `sTeams` variable split from user-controlled `STRING_TEAMS` and injected directly into `IN (...)` clauses. Alert2Team.js:28 concatenates `sExecutor` into a SQL query without escaping. Alert2Team.js:72 concatenates `sTeamnames` into UPDATE statement.
impact: HIGH — Allows SQL injection if any parameter originates from user/external input; Enterprise Alert database compromise.
verify_steps: Trace whether `STRING_TEAMS`, `sExecutor`, or MIB file contents can be influenced by external input in production deployments.
[HYP] Command Injection via PowerShell in HTML-to-Text Script
class: MISCONFIG
asset: derdack-alert-augmentation/html-to-text/ps.js:40
confidence: 85
reasoning: `ExecutePowershell()` constructs a shell command by directly interpolating `htmlString` (from event parameter `PARAMETER_WITH_HTML`) into a `powershell.exe` invocation: `"powershell.exe \"node.exe '" + SCRIPTING_HOST_DIR + "html_text.js' '" + htmlString + "'\""`. An attacker who controls the `text` event parameter can inject arbitrary OS commands. Line 143 also concatenates `alertID` and `executor` into a powershell command without sanitization.
impact: CRITICAL — Remote code execution on the Enterprise Alert scripting host via crafted event parameter.
verify_steps: Confirm the script is deployed in production ScriptingHost; test with a malicious `text` parameter payload.
[HYP] eval() on Application Context Data in Multiple EA Plugins
class: MISCONFIG
asset: derdack-2wayREST-samples/Logic Monitor/Main.js:52-68, zendesk/Main.js:52-68, Dynatrace/Main.js:53-69, derdack-plugin-checkmk/2-way/Main.js:52-68
confidence: 75
reasoning: `eval()` is called on `appContext.state.callbackSaveState`, `appContext.runtimeInfo.callbackSetStatusError`, `appContext.runtimeInfo.callbackSetStatusOK`, `appContext.runtimeInfo.callbackSendMail`. If the EA runtime provides attacker-controllable data in these fields, it enables arbitrary code execution. This pattern is repeated identically in 4 repos.
impact: MEDIUM — Potential code execution if app context can be tampered with. Risk depends on EA SDK trust boundary.
verify_steps: Review EA Scripting Host SDK to determine if context fields are sanitized before delivery.
[HYP] SIGNL4 Team Secret Logged at DEBUG Level in EA WebhookGateway
class: SECRET
asset: derdack-integration-SIGNL4/js/WebhookGateway.js:41,87
confidence: 80
reasoning: The decoded SIGNL4 team secret is written to debug logs at lines 41 and 87: `EAScriptHost.LogDebug("Decoded S4 Team Secret: " + strS4TeamSecret)`. The secret is also appended to the webhook URL at line 94. This exposes the secret in EA log files.
impact: MEDIUM — Team secret exposure in log files; allows unauthorized SIGNL4 webhook calls if logs are accessible.
verify_steps: Check EA log retention and access controls; verify if debug logging is enabled in production.
[HYP] SIGNL4 Team Secret Logged at INFO Level in ioBroker Adapter
class: SECRET
asset: signl4/ioBroker.signl4/main.js:40
confidence: 85
reasoning: Line 40: `this.log.info('config team_secret: ' + this.config.team_secret);` logs the SIGNL4 team secret to ioBroker's info-level log on adapter ready. INFO-level logs are typically retained longer and are more accessible than DEBUG logs in production ioBroker installations.
impact: MEDIUM — Team secret exposure in ioBroker log files. Any user with access to ioBroker admin/logs can read the secret and send arbitrary alerts.
verify_steps: (1) Confirm repo ownership at github.com/signl4/ioBroker.signl4 (2) Check if ioBroker log files are typically stored in a world-readable location (3) Verify if the `this.log.info` call is present in the published npm package version.
[HYP] Commented-Out Pipedream Debug Webhook in Zabbix Integration
class: OTHER
asset: signl4/signl4-integration-zabbix/signl4-mediatype.yaml:122
confidence: 70
reasoning: Line contains commented-out debug endpoint: `//endpoint = 'https://b58aee12b873eae71b5db8b4fdc77d78.m.pipedream.net';` — a Pipedream request inspection URL. This is a developer debug/test artifact left in production Zabbix media type export. While commented out, it reveals an internal testing endpoint and confirms Pipedream was used for webhook debugging.
impact: Low — Commented-out code is not executed. However, it leaks a historical debug endpoint. If someone uncomments it, all Zabbix alerts would be sent to a third-party service (Pipedream) instead of SIGNL4.
verify_steps: (1) Check if the Pipedream endpoint is still active: `curl -s -o /dev/null -w '%{http_code}' https://b58aee12b873eae71b5db8b4fdc77d78.m.pipedream.net` (2) If active, confirms debug artifact was real.
[HYP] Hardcoded MySQL Credentials in SIGNL4 MariaDB Integration Sample
class: SECRET
asset: signl4/signl4-integration-mysql-mariadb/db2signl.php:10-13
confidence: 75
reasoning: `STRING_DB_USER = "signl4"` and `STRING_DB_PASS = "signl4"` are hardcoded real credential values (not placeholders). While intended as sample code, users who deploy this without changing credentials expose a local MySQL instance with known username/password pair. The password matches the database name, suggesting a default install pattern.
impact: Low — Sample code only; impact depends on whether any deployment ships with these defaults. No Derdack-internal hostname exposed.
verify_steps: (1) Confirm repo ownership at github.com/signl4/signl4-integration-mysql-mariadb (2) Search GitHub code search for `STRING_DB_PASS = "signl4"` to see if any forks/deployments use this verbatim.
[HYP] PII and Internal Infrastructure URLs in Public CSV Export
class: MISCONFIG
asset: signl4/signl4-reporting/AlertAuditReport.csv
confidence: 90
reasoning: CSV file contains real user email addresses (`ron@signl4.com`, `system@signl4.com`) and internal Grafana URLs (`ronlab.grafana.net`). This is operational alert audit data that should not be in a public repo. The file has 821 lines of production alert data from May 2022.
impact: MEDIUM — PII exposure of Derdack employee email; internal infrastructure URL disclosure (Grafana instance).
verify_steps: (1) Confirm the CSV is in the public repo (2) Check if `ronlab.grafana.net` is accessible externally (3) Verify if the email addresses are valid Derdack accounts.
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-11 05:07:35 UTC
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-11 09:44:12 UTC
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-11 13:54:56 UTC
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-11 17:22:38 UTC
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-11 19:59:21 UTC
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-11 22:15:36 UTC
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-12 00:19:01 UTC
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-12 04:42:16 UTC
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-12 08:53:59 UTC
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-12 12:26:43 UTC
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-12 15:47:41 UTC
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-12 17:55:04 UTC
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-12 19:43:09 UTC
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-12 21:43:53 UTC
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-12 23:28:34 UTC
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-13 01:22:52 UTC
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-13 06:43:47 UTC
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-13 12:22:01 UTC
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-13 16:35:43 UTC
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-13 18:55:16 UTC
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-13 21:10:25 UTC
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-13 23:11:13 UTC
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-14 01:05:54 UTC
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-14 06:24:44 UTC
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-14 12:54:49 UTC
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-14 18:14:57 UTC
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-14 21:50:31 UTC
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-15 00:02:28 UTC
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-15 04:56:23 UTC
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-15 09:40:13 UTC
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-15 14:27:17 UTC
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-15 18:27:10 UTC
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-15 21:42:53 UTC
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-15 23:51:25 UTC
[HYP] Hardcoded SQL Server SA Credentials in Public Plugin
class: SECRET
asset: Derdack/derdack-oncall-holidayimport/HolidayImport.js:16, HolidayDeleteAll.js:22
confidence: 95
reasoning: Connection string contains `UID=sa;PWD=Derdack!;Database=EnterpriseAlert2017` with internal hostname `sqlserver.derdack-support.local`. The SA account is SQL Server's super-admin. These are real production/support credentials, not placeholders — the same string appears across two separate scripts in the same repo, and matches a pattern already reported in valid-bugs.md (hardcoded SQL Server SA creds `Derdack!`).
impact: HIGH (8.1 CVSS) — full database takeover if host is reachable; credential reuse risk across environments
verify_steps: Passively confirm repo is public on github.com/Derdack; check git log for commit author (Frank Gutacker, Derdack employee); verify `sqlserver.derdack-support.local` resolves from Derdack VPN/office network
[HYP] Hardcoded Checkmk Admin Credentials + Internal IP in Public Plugin
class: SECRET
asset: Derdack/derdack-plugin-checkmk/2-way/Main.js:90-94
confidence: 95
reasoning: Lines 90-94 contain `username = "cmkadmin"`, `password = "CNlydVqZ"`, `serverURL = "http://192.168.88.107:8080/cmk/check_mk/api/v0/"`. This is a real Checkmk admin account with plaintext password and RFC1918 internal IP, committed to a public GitHub repo. Already noted in valid-bugs.md (Hardcoded Checkmk creds + internal IP).
impact: MEDIUM (7.5 CVSS) — internal network credential exposure; Checkmk admin can modify monitoring config, ack alerts, execute scripts
verify_steps: Passively confirm repo is public; verify `192.168.88.107` is a private IP (RFC1918); check if Checkmk is exposed on any public-facing interface
[HYP] SIGNL4 Team Secret Logged at INFO Level in ioBroker Adapter
class: SECRET
asset: signl4/ioBroker.signl4/main.js:40
confidence: 90
reasoning: `this.log.info('config team_secret: ' + this.config.team_secret)` logs the SIGNL4 team secret in plaintext at INFO level on adapter startup. Team secrets are authentication tokens for SIGNL4 webhooks — anyone with log access can forge alerts. Already reported in valid-bugs.md.
impact: MEDIUM (5.3 CVSS) — secret exposure in logs enables alert forgery; log aggregation systems may persist the secret
verify_steps: Install ioBroker.signl4 adapter, configure with a test team secret, observe logs at info level; confirm secret appears in syslog/journald
[HYP] PII + Internal Infrastructure URLs in Public CSV Export
class: OTHER
asset: signl4/signl4-reporting/AlertAuditReport.csv, ShiftReport.csv
confidence: 80
reasoning: AlertAuditReport.csv contains employee email addresses (`ron@signl4.com`), internal Grafana dashboard URLs (`ronlab.grafana.net`), alert content with internal datasource UIDs, and operational data. ShiftReport.csv contains employee names, emails, and shift schedules. These are real SIGNL4 employee data committed to a public repo. Already reported in valid-bugs.md.
impact: MEDIUM (5.3 CVSS) — PII disclosure of employee emails, work schedules, and internal infrastructure topology
verify_steps: Passively confirm files are public on github.com/signl4; `ronlab.grafana.net` may reveal internal Grafana instance
[HYP] Internal SQL Server Hostname in Commented Code
class: OTHER
asset: signl4/signl4-integration-sql-server/db2signl.ps1:14
confidence: 70
reasoning: Commented-out line contains full connection string: `Server=sqlserver.derdack-support.local;Trusted_Connection=No;UID=sa;PWD=none;Database=EnterpriseAlert2017`. While commented out, it reveals internal hostname, database name, and SA credentials (password `none`). This is distinct from the HolidayImport finding — different repo, different integration.
impact: LOW (5.3 CVSS) — credential in comment still leaks internal infra details; `PWD=none` may be a weak/real password
verify_steps: Passively confirm file is public; check git blame for commit context
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-16 01:53:52 UTC
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-16 07:04:19 UTC
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-16 12:15:27 UTC
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-16 16:55:55 UTC
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-16 19:48:28 UTC
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-16 22:26:56 UTC
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-17 00:51:15 UTC
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-17 05:32:35 UTC
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-17 10:21:38 UTC
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-17 15:18:05 UTC
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-17 19:04:01 UTC
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-17 22:11:03 UTC
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-18 00:20:20 UTC
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-18 04:53:34 UTC
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-18 09:16:41 UTC
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-18 13:38:37 UTC
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-18 17:18:37 UTC
[HYP] Hardcoded SQL Server SA Credentials — Derdack Internal Hostname
class: SECRET
asset: Derdack/derdack-oncall-holidayimport/HolidayImport.js:16, HolidayDeleteAll.js:22
confidence: 95
reasoning: Connection string contains UID=sa;PWD=Derdack!;Database=EnterpriseAlert2017 with internal hostname sqlserver.derdack-support.local. SA is SQL Server's super-admin account. Appears identically in two separate scripts in the same public repo. Not a placeholder — no <password> or YOUR_PASSWORD markers. Authored by Frank Gutacker (Derdack employee per git metadata).
impact: HIGH — SA account grants full SQL Server control (DDL, DCL, backup/restore, OS shell). Internal hostname disclosure aids lateral movement. If credentials reused across environments, direct database compromise.
verify_steps: (1) Confirm repo is public: github.com/Derdack/derdack-oncall-holidayimport (2) Check git log for author (Frank Gutacker) (3) DNS-resolve sqlserver.derdack-support.local externally (should fail — internal only) (4) If reachable from any Derdack network, rotate credential immediately
[HYP] Hardcoded Checkmk Admin Credentials + RFC1918 Internal IP
class: SECRET
asset: Derdack/derdack-plugin-checkmk/2-way/Main.js:90-94
confidence: 95
reasoning: Lines 90-94 contain username="cmkadmin", password="CNlydVqZ", serverURL="http://192.168.88.107:8080/cmk/check_mk/api/v0/". Plaintext HTTP to internal Checkmk API. Credentials used in Bearer auth headers at lines 317, 360. The RFC1918 IP 192.168.88.107 matches the pattern used in derdack-2wayREST-samples/README.md:147 (192.168.88.88), confirming this is a Derdack internal network range.
impact: HIGH — Checkmk admin can modify monitoring config, ack alerts, execute check scripts, read host/service data. Internal IP leaks network topology. Plaintext HTTP means credential interception via passive sniffing on internal network.
verify_steps: (1) Confirm repo is public: github.com/Derdack/derdack-plugin-checkmk (2) Verify 192.168.88.107 is RFC1918 (it is) (3) Check if Checkmk is exposed on any public-facing interface (4) Verify credential reuse risk: check if "CNlydVqZ" appears in breach databases
[HYP] SIGNL4 Team Secret Hardcoded in Google IoT Integration Sample
class: SECRET
asset: signl4/signl4-integration-google-iot/index.js:19
confidence: 85
reasoning: Team secret 96sbq38s is hardcoded directly in the webhook URL https://connect.signl4.com/webhook/96sbq38s — not a placeholder (no <team-secret> or YOUR_SECRET marker). Same secret also appears in signl4-integration-losant/signl4-alert-v100.node:148 as a stringTeamSecret payload. Both repos are under signl4 GitHub org (Derdack-owned). The secret is a real alphanumeric string committed to source.
impact: MEDIUM — Any party can send arbitrary alerts to this SIGNL4 team via the webhook. Could be used for alert flooding, social engineering via fake incident notifications, or to probe the team's response workflows. Impact depends on whether the team still exists.
verify_steps: (1) Confirm repo ownership: github.com/signl4/signl4-integration-google-iot (2) POST test payload: curl -s -o /dev/null -w '%{http_code}' -X POST https://connect.signl4.com/webhook/96sbq38s -H 'Content-Type: application/json' -d '{"Title":"test"}' (3) If 201, secret is live — rotate immediately. If 404, team was deleted.
[HYP] SIGNL4 Team Secret in Postman Collection + DevTools YAML (Same Secret, Two Files)
class: SECRET
asset: signl4/code-snippets/SIGNL4.postman_collection.json:40 + signl4/docs/integrations/devtools/SIGNL4_Alerting.yaml:7
confidence: 80
reasoning: Team secret vbguzfsi appears in two public repos: (1) Postman collection path array ["webhook","vbguzfsi"] while the raw field shows "--team-secret--" placeholder — path array was not sanitized before commit; (2) DevTools YAML url hardcoded as https://connect.signl4.com/webhook/vbguzfsi. Same secret reused across two files suggests a Derdack employee's real team secret used during development.
impact: MEDIUM — Unauthorized alert injection, alert flooding, potential social engineering via fake incidents. Two repos expose the same secret, increasing blast radius.
verify_steps: (1) Confirm repo ownership (2) POST test: curl -s -o /dev/null -w '%{http_code}' -X POST https://connect.signl4.com/webhook/vbguzfsi -H 'Content-Type: application/json' -d '{"Title":"test"}' (3) If 201, rotate immediately.
[HYP] Command Injection via PowerShell in Enterprise Alert Scripting Host
class: MISCONFIG
asset: Derdack/derdack-alert-augmentation/html-to-text/ps.js:40,143
confidence: 90
reasoning: Line 40: ExecutePowershell() constructs a shell command by directly interpolating htmlString (from event parameter PARAMETER_WITH_HTML) into a powershell.exe invocation: "powershell.exe \"node.exe '" + SCRIPTING_HOST_DIR + "html_text.js' '" + htmlString + "'\"". Line 143: strCommand = "powershell.exe" + " c:\\exportsimple.ps1 " + alertID + " " + executor — alertID and executor are also unsanitized. An attacker who controls event parameters can inject arbitrary OS commands.
impact: CRITICAL — Remote code execution on the Enterprise Alert scripting host via crafted event parameter containing shell metacharacters (e.g., '; rm -rf / # or & net user admin P@ss /add &).
verify_steps: (1) Confirm script is deployed in production ScriptingHost (2) Trace whether PARAMETER_WITH_HTML can be influenced by external input in production EA deployments (3) Test with event parameter payload containing shell metacharacters
[HYP] SQL Injection via String Concatenation in Enterprise Alert Scripts
class: MISCONFIG
asset: Derdack/derdack-oncall-holidayimport/HolidayImport.js:65,86,105,191 + HolidayDeleteAll.js:71,92,111,197 + Derdack/derdack-alert-forwarding/Alert2Team.js:28,72 + Derdack/derdack-events-snmp/SNMP-MIB-Importer.js:153,161,169
confidence: 90
reasoning: All SQL queries are built via direct string concatenation with unsanitized variables. HolidayImport.js:65 — "SELECT ID FROM OnCallPlanHolidays WHERE OnCallPlanID=" + iTeamId + " AND Holiday='" + sDate + "'". HolidayImport.js:86 — sTeams variable split from user-controlled STRING_TEAMS and injected directly into IN (...) clauses. Alert2Team.js:28 concatenates sExecutor into a SQL query. SNMP-MIB-Importer.js:161 concatenates MIB XML data directly into INSERT statements.
impact: HIGH — Allows SQL injection if any parameter originates from user/external input; Enterprise Alert database compromise (read, modify, delete data, potentially OS execution via xp_cmdshell).
verify_steps: (1) Trace whether STRING_TEAMS, sExecutor, or MIB file contents can be influenced by external input in production deployments (2) Check if Enterprise Alert uses parameterized queries elsewhere for comparison
[HYP] eval() on Application Context Data in 4 EA Plugins (Code Injection Risk)
class: MISCONFIG
asset: Derdack/derdack-2wayREST-samples/Logic Monitor/Main.js:52-68, zendesk/Main.js:52-68, Dynatrace/Main.js:53-69, Derdack/derdack-plugin-checkmk/2-way/Main.js:52-68
confidence: 75
reasoning: eval() is called on appContext.state.callbackSaveState, appContext.runtimeInfo.callbackSetStatusError, appContext.runtimeInfo.callbackSetStatusOK, appContext.runtimeInfo.callbackSendMail. Identical pattern across 4 repos. If the EA runtime provides attacker-controllable data in these fields, it enables arbitrary code execution. The eval() wrapping appears to be an EA SDK convention, but the trust boundary is unclear.
impact: MEDIUM — Potential code execution if app context can be tampered with. Risk depends on EA SDK trust boundary — whether appContext fields are sanitized before delivery.
verify_steps: (1) Review EA Scripting Host SDK documentation for trust boundary (2) Determine if appContext fields are user-controllable or only set by EA platform (3) Check if EA runtime sanitizes callback fields before delivery
[HYP] SIGNL4 Team Secret Logged at INFO Level in ioBroker Adapter
class: SECRET
asset: signl4/ioBroker.signl4/main.js:40
confidence: 85
reasoning: Line 40: this.log.info('config team_secret: ' + this.config.team_secret) logs the SIGNL4 team secret in plaintext at INFO level on adapter startup. INFO-level logs are typically retained longer and are more accessible than DEBUG logs. The secret is also used in the webhook URL construction at line 157.
impact: MEDIUM — Team secret exposure in ioBroker log files. Any user with access to ioBroker admin/logs can read the secret and send arbitrary alerts to the SIGNL4 team.
verify_steps: (1) Confirm repo: github.com/signl4/ioBroker.signl4 (2) Check if ioBroker log files are typically stored in world-readable locations (3) Verify the this.log.info call is in the published npm package version
[HYP] PII + Internal Infrastructure URLs in Public CSV Export
class: MISCONFIG
asset: signl4/signl4-reporting/AlertAuditReport.csv, ShiftReport.csv
confidence: 90
reasoning: AlertAuditReport.csv (821 lines) contains: employee email (system@signl4.com), internal Grafana URLs (ronlab.grafana.net), alert datasource UIDs, operational alert data from May 2022. ShiftReport.csv contains employee names (Ron), emails (ron@signl4.com), and shift schedules. These are real SIGNL4 production alert data and employee PII committed to a public repo. The README.md also embeds the same data with ronlab.grafana.net URLs.
impact: MEDIUM — PII disclosure of Derdack employee email, work schedules. Internal Grafana instance URL (ronlab.grafana.net) disclosed — may reveal internal monitoring stack.
verify_steps: (1) Confirm files are public: github.com/signl4/signl4-reporting (2) Check if ronlab.grafana.net is accessible externally (3) Verify email addresses are valid Derdack accounts
[HYP] SQL Server SA Credentials (Commented) — Second Password Variant
class: SECRET
asset: signl4/signl4-integration-sql-server/db2signl.ps1:14
confidence: 70
reasoning: Line 14 contains commented-out connection string: Server=sqlserver.derdack-support.local;Trusted_Connection=No;UID=sa;PWD=none;Database=EnterpriseAlert2017. This exposes: (1) internal Derdack hostname sqlserver.derdack-support.local, (2) SQL Server SA account, (3) password "none". Two password variants for the same SA account (Derdack! in HolidayImport.js vs none here) suggest credential rotation or multiple test environments.
impact: LOW — Commented-out code is not executed. However, leaks internal hostname and a second SA password variant. Valuable for lateral movement if hostname resolves internally.
verify_steps: (1) Confirm file is public (2) DNS-resolve sqlserver.derdack-support.local externally (3) Compare with HolidayImport.js: PWD=Derdack! vs PWD=none
[HYP] Commented-Out Pipedream Debug Webhook in Zabbix Integration
class: OTHER
asset: signl4/signl4-integration-zabbix/signl4-mediatype.yaml:122
confidence: 70
reasoning: Line contains commented-out debug endpoint: //endpoint = 'https://b58aee12b873eae71b5db8b4fdc77d78.m.pipedream.net'; — a Pipedream request inspection URL. Developer debug/test artifact left in production Zabbix media type export. Confirms Pipedream was used for webhook debugging. The UUID is a real Pipedream endpoint ID.
impact: LOW — Commented-out code is not executed. However, if uncommented, all Zabbix alerts would be routed to a third-party service (Pipedream) instead of SIGNL4.
verify_steps: (1) Check if the Pipedream endpoint is still active: curl -s -o /dev/null -w '%{http_code}' https://b58aee12b873eae71b5db8b4fdc77d78.m.pipedream.net (2) If active, confirms debug artifact was real
[HYP] Hardcoded MySQL Credentials in SIGNL4 MariaDB Integration Sample
class: SECRET
asset: signl4/signl4-integration-mysql-mariadb/db2signl.php:10-13
confidence: 60
reasoning: STRING_DB_USER="signl4" and STRING_DB_PASS="signl4" are hardcoded real credential values (not placeholders). While intended as sample code, users who deploy without changing credentials expose a local MySQL instance with known username/password pair. Password matches database name, suggesting a default install pattern.
[HYP] Hardcoded MySQL Credentials in SIGNL4 MariaDB Integration Sample
class: SECRET
asset: signl4/signl4-integration-mysql-mariadb/db2signl.php:10-13
confidence: 60
reasoning: STRING_DB_USER="signl4" and STRING_DB_PASS="signl4" are hardcoded real credential values (not placeholders). While intended as sample code, users who deploy without changing credentials expose a local MySQL instance with known username/password pair. Password matches database name, suggesting a default install pattern.
impact: LOW — Sample code only; no Derdack-internal hostname exposed. Impact depends on whether any deployment ships with these defaults.
verify_steps: (1) Confirm repo: github.com/signl4/signl4-integration-mysql-mariadb (2) GitHub code search for STRING_DB_PASS = "signl4" to find forks/deployments using this verbatim
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-18 19:37:24 UTC
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-18 21:49:14 UTC
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-18 23:40:53 UTC
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-19 01:52:58 UTC
[HYP] Hardcoded Checkmk admin credentials with internal IP leak
class: SECRET
asset: Derdack/derdack-plugin-checkmk/2-way/Main.js:90-94
confidence: 95
reasoning: var username = "cmkadmin"; var password = "CNlydVqZ"; var serverURL = "http://192.168.88.107:8080/cmk/check_mk/api/v0/"; Credentials are real-looking (not placeholder), used in Authorization header on lines 317, 360. Internal RFC1918 IP 192.168.88.107 leaked.
impact: HIGH — Exposed admin creds to Checkmk monitoring system; internal network topology disclosed. If Checkmk instance is internet-accessible or creds reused, full monitoring compromise.
verify_steps: 1) Check if 192.168.88.107:8080 is accessible externally. 2) Confirm password "CNlydVqZ" still valid for cmkadmin. 3) Check git history for when this was committed (may be stale demo but pattern indicates real deployment).
[HYP] Hardcoded SIGNL4 team secret in Google IoT integration
class: SECRET
asset: signl4/signl4-integration-google-iot/index.js:19
confidence: 85
reasoning: request.post('https://connect.signl4.com/webhook/96sbq38s', ...). Team secret "96sbq38s" appears in 2 files (index.js and signl4-alert-v100.node:148). Not a placeholder — real webhook secret committed to public repo.
impact: HIGH — Anyone with this secret can send spoofed alerts to the SIGNL4 team or potentially read team data depending on API scope.
verify_steps: 1) POST a test payload to https://connect.signl4.com/webhook/96sbq38s and check if alert is received. 2) Verify team still exists in SIGNL4.
[HYP] eval() on untrusted callback strings — code injection vector
class: OTHER
asset: Derdack/derdack-plugin-checkmk/2-way/Main.js:52-68 (and 3 other Main.js files)
confidence: 75
reasoning: Four eval() calls on appContext.state.callbackSaveState, callbackSetStatusError, callbackSetStatusOK, callbackSendMail — all from EA framework context objects. Pattern is identical across derdack-2wayREST-samples (Logic Monitor, zendesk, Dynatrace) and derdack-plugin-checkmk. If appContext is attacker-influenced (e.g. via malicious EA plugin config), arbitrary code execution is possible.
impact: MEDIUM — Requires control over Enterprise Alert plugin configuration. Could lead to full server-side code execution in EA scripting host context.
verify_steps: 1) Confirm EA scripting host uses Node.js eval semantics. 2) Check if appContext callbacks can be externally influenced. 3) Test if a malicious EA REST source config can inject JS.
[HYP] SSRF via weak redirect validation in Jira integration
class: SSRF
asset: signl4/signl4-integration-jira/jira.php:12-16
confidence: 70
reasoning: strpos("connect.signl4.com", $sValue) == 0 checks if $sValue is a substring of "connect.signl4.com" starting at position 0. This passes for $sValue = "c", "co", "connect", etc. curl_init($sSignlUrl) is then called with this user-controlled URL. An attacker can set redirect=connect.evil.com and the check passes (strpos returns false which is not == 0, but redirect=connect passes).
impact: MEDIUM — Requires PHP deployment. Could allow outbound HTTP requests from the Jira-integrated server to attacker-controlled endpoints.
verify_steps: 1) Deploy jira.php on a PHP server. 2) Send request with redirect=http://attacker.com/test. 3) Verify if strpos logic allows bypass.
[HYP] API key passed in URL query parameter
class: MISCONFIG
asset: Derdack/derdack-plugin-checkmk/notifications/derdack:104,114
confidence: 90
reasoning: requests.post(url + '?apiKey=' + password, ...) sends Enterprise Alert REST API key as URL query parameter. Query parameters are logged in server access logs, proxy logs, browser history, and potentially in analytics tools.
impact: LOW — API key exposure in logs. Standard recommendation is Authorization header.
verify_steps: 1) Verify this script is used in production EA deployments. 2) Check EA REST API documentation for key transmission method.
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-19 06:44:35 UTC
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-19 11:39:16 UTC
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-19 14:50:24 UTC
[HYP] Hardcoded Checkmk Admin Credentials in Sample Code
class: SECRET
asset: derdack-plugin-checkmk/2-way/Main.js:85-87
confidence: 95
reasoning: >
impact: HIGH — Exposes Checkmk admin account; allows host acknowledgment/
verify_steps: >
[HYP] Hardcoded SQL Server Connection String with Database Name
class: SECRET
asset: derdack-alert-forwarding/Alert2Team.js:15
confidence: 70
reasoning: >
impact: MEDIUM — Information disclosure; no direct credential exposure but
verify_steps: >
[HYP] Shell Command Injection via unsanitized event parameter
class: SSRF
asset: derdack-alert-augmentation/html-to-text/ps.js:40
confidence: 80
reasoning: >
impact: HIGH — Remote code execution on the Enterprise Alert scripting host
verify_steps: >
[HYP] eval() on framework-provided callback strings
class: OTHER
asset: derdack-2wayREST-samples/zendesk/Main.js:48-55,
confidence: 60
reasoning: >
impact: MEDIUM — Exploitation requires compromising the EA plugin loading
verify_steps: >
[HYP] Hardcoded internal IP address in sample code
class: MISCONFIG
asset: derdack-plugin-checkmk/2-way/Main.js:89
confidence: 50
reasoning: >
impact: LOW — Information disclosure only; no direct exploitation path
verify_steps: >
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-19 17:31:29 UTC
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-19 19:33:19 UTC
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-19 21:42:05 UTC
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-19 23:41:30 UTC
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-20 01:54:14 UTC
class: SECRET
asset: derdack-oncall-holidayimport/HolidayDeleteAll.js:22
confidence: 100
reasoning: Line 22 contains `Server=sqlserver.derdack-support.local;UID=sa;PWD=Derdack!;Database=EnterpriseAlert2017` — plaintext `sa` (SQL sysadmin) password and internal DNS hostname. Identical in HolidayImport.js:16. This is not a placeholder; the scripts have `BOOL_DRY_RUN = false`, indicating live use.
impact: Critical — `sa` grants full SQL Server admin. Internal hostname reveals infrastructure. Credential reuse likely.
verify_steps: Confirm `sqlserver.derdack-support.local` resolves; attempt login with `sa`/`Derdack!` against Derdack's support DB.
class: SECRET
asset: derdack-plugin-checkmk/2-way/Main.js:90-94
confidence: 100
reasoning: Lines 90-91: `username = "cmkadmin"`, `password = "CNlydVqZ"`. Line 94: `serverURL = "http://192.168.88.107:8080/cmk/check_mk/api/v0/"` — credentials transmitted in cleartext over HTTP. Internal IP `192.168.88.107` exposed.
impact: Critical — Checkmk admin access; credentials sent unencrypted. Internal network topology leaked.
verify_steps: Confirm `192.168.88.107` is reachable or was reachable at commit time; test `cmkadmin`/`CNlydVqZ` against any live Checkmk instance.
class: OTHER
asset: derdack-alert-augmentation/html-to-text/ps.js:40,143
confidence: 95
reasoning: Line 40: `strCommand = "powershell.exe \"node.exe '" + SCRIPTING_HOST_DIR + "html_text.js' '" + htmlString + "'\""` — `htmlString` from event parameters is interpolated into a shell command with no escaping. Attacker-controlled HTML containing `'\"` can break out and execute arbitrary commands. Line 143: `alertID` and `executor` also unsanitized in shell command.
impact: Critical — Remote code execution on the Enterprise Alert scripting host server.
verify_steps: Craft an event parameter containing `'; rm -rf / #` and trigger the script in a test environment.
class: OTHER
asset: derdack-alert-forwarding/Alert2Team.js:28,72
confidence: 90
reasoning: Line 28: `sExecutor` is concatenated directly into a SQL WHERE clause: `WHERE RemoteJobsHistory.ProfileName='" + sExecutor + "'"`. Line 72: `sTeamnames` built from DB results and concatenated into an UPDATE. No parameterized queries used.
impact: High — SQL injection enabling data exfiltration or modification in the Enterprise Alert database.
verify_steps: Pass `' OR '1'='1` as the `sExecutor` parameter and observe if query returns unauthorized rows.
class: OTHER
asset: derdack-events-snmp/SNMP-MIB-Importer.js:153,161,169
confidence: 85
reasoning: Lines 153, 161, 169: MIB data (`aMibs[i].id`, `.name`, `.description`) concatenated into SQL INSERT/UPDATE without parameterization. Malicious MIB XML files could inject SQL.
impact: High — SQL injection via crafted MIB files imported into the Enterprise Alert database.
verify_steps: Craft a MIB XML file with a name containing `'--; DROP TABLE EventParameters; --` and import it.
class: OTHER
asset: derdack-2wayREST-samples/Dynatrace/Main.js:52-69, Logic Monitor/Main.js:52-68, zendesk/Main.js:52-68
confidence: 80
reasoning: `eval()` called on `appContext.state.callbackSaveState`, `appContext.runtimeInfo.callbackSetStatusError`, etc. If these values are attacker-controllable (e.g. via config manipulation), this enables arbitrary code execution on the EA scripting host.
impact: High — RCE on Enterprise Alert scripting host if context values can be influenced.
verify_steps: Manipulate `appContext.state.callbackSaveState` to contain `require('child_process').exec('id')` and observe execution.
class: MISCONFIG
asset: derdack-2wayREST-samples/README.md:147,239,332,421,506 and derdack-plugin-checkmk/2-way/Main.js:94
confidence: 100
reasoning: Internal IPs `192.168.88.88` (5 occurrences in README) and `192.168.88.107` (Main.js:94) leaked in public repo. Reveals internal network topology.
impact: Medium — Aids attacker reconnaissance of Derdack's internal infrastructure.
verify_steps: Check if these IPs respond from the public internet or are firewalled.
class: MISCONFIG
asset: derdack-2wayREST-samples/README.md:195,288,377
confidence: 100
reasoning: Real employee name/email exposed: `rbormann@de.derdack.com`, `Rene Bormann`, username `bormann` — appears 3 times in README example payloads.
impact: Low — PII exposure enabling targeted phishing against Derdack staff.
verify_steps: Confirm rbormann is a current/valid Derdack employee email.
class: MISCONFIG
asset: derdack-alert-forwarding/Alert2Team.js:15, derdack-events-snmp/SNMP-MIB-Importer.js:18
confidence: 85
reasoning: Alert2Team.js:15 reveals `(local)` SQL Server. SNMP-MIB-Importer.js:18 reveals `.\sqlexpress` instance name and `EnterpriseAlert` database name.
impact: Medium — Infrastructure disclosure aiding targeted attacks.
verify_steps: Attempt to connect to the SQL instances from external networks.
class: MISCONFIG
asset: User-Monitoring/User Monitoring.ps1:21
confidence: 80
reasoning: Line 21: `http://<EA_Server>/EAWebService/rest/events?apiKey=<REST_Endpoint_Key>` — uses HTTP, not HTTPS. API key transmitted in cleartext in URL query parameter (logged in server access logs, proxy logs).
impact: Medium — API key interception via network sniffing or log exposure.
verify_steps: Check if EA Server enforces HTTPS redirect; verify if API keys appear in web server access logs.
class: OTHER
asset: derdack-integration-azuremonitor/registerClient.ps1:110, derdack-integration-azuresentinel/registerClient.ps1:119
confidence: 85
reasoning: Both scripts execute `$config | Format-List` which prints the generated Azure `ClientSecret` to stdout in plaintext. Terminal logs, screen captures, or shoulder-surfing can expose it. Sentinel variant also assigns overly broad `"Azure Sentinel Contributor"` role.
impact: Medium — Azure service principal secret exposure; Sentinel variant grants excessive permissions.
verify_steps: Run the script in a test Azure tenant and observe console output for secret leakage.
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-20 07:17:31 UTC
class: SECRET
asset: derdack-oncall-holidayimport/HolidayImport.js:16
confidence: 100
reasoning: >
impact: CRITICAL — if the server is/was internet-exposed or if this repo
verify_steps: >
class: SECRET
asset: derdack-oncall-holidayimport/HolidayDeleteAll.js:22
confidence: 100
reasoning: >
impact: CRITICAL — same as above; duplicate exposure of the same credential.
verify_steps: Same as above.
class: SECRET
asset: derdack-plugin-checkmk/2-way/Main.js:90-94
confidence: 100
reasoning: >
impact: CRITICAL — admin-level CheckMK access. If the internal server
verify_steps: >
class: OTHER (Command Injection)
asset: derdack-alert-augmentation/html-to-text/ps.js:40
confidence: 90
reasoning: >
impact: HIGH — Remote Code Execution on the Enterprise Alert server.
verify_steps: >
class: OTHER (Code Execution Pattern)
asset: derdack-2wayREST-samples/*/Main.js and derdack-plugin-checkmk/2-way/Main.js
confidence: 80
reasoning: >
impact: HIGH — Arbitrary code execution in the EA scripting host
verify_steps: >
class: OTHER (SQL Injection)
asset: derdack-oncall-holidayimport/HolidayImport.js, HolidayDeleteAll.js,
confidence: 85
reasoning: >
impact: HIGH — Database compromise. Depending on the SQL Server
verify_steps: >
class: SSRF
asset: derdack-2wayREST-samples/Dynatrace/Main.js:242-266,
confidence: 75
reasoning: >
impact: HIGH — Internal network scanning, data exfiltration from
verify_steps: >
class: MISCONFIG
asset: derdack-integration-SIGNL4/js/WebhookGateway.js:41
confidence: 95
reasoning: >
impact: MEDIUM — Credential disclosure via log files. If debug
verify_steps: >
class: MISCONFIG
asset: derdack-plugin-checkmk/notifications/derdack:104,
confidence: 85
reasoning: >
impact: MEDIUM — API keys in URLs are logged by web servers,
verify_steps: >
class: MISCONFIG
asset: derdack-plugin-checkmk/2-way/Main.js:94
confidence: 95
reasoning: >
impact: MEDIUM — Credential sniffing on the network segment.
verify_steps: >
class: MISCONFIG
asset: derdack-oncall-holidayimport/HolidayImport.js:16
confidence: 90
reasoning: >
impact: LOW — Reconnaissance value for targeted attacks against
class: OTHER
asset: derdack-alert-augmentation/html-to-text/ps.js:13
confidence: 85
reasoning: >
impact: LOW — Useful for crafting targeted exploits against
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-20 12:23:38 UTC
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-20 16:26:42 UTC
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-20 19:00:57 UTC
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-20 21:34:18 UTC
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-20 23:27:44 UTC
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-21 01:33:04 UTC
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-21 07:01:34 UTC
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-21 14:14:28 UTC
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-21 19:27:54 UTC
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-21 22:46:57 UTC
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-22 01:18:15 UTC
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-22 06:18:10 UTC
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-22 11:44:03 UTC
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-22 15:47:35 UTC
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-22 19:18:13 UTC
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-22 22:14:07 UTC
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-23 00:33:40 UTC
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-23 05:05:35 UTC
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-23 09:59:28 UTC
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-23 14:40:44 UTC
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-23 18:42:01 UTC
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-23 21:50:47 UTC
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-24 00:02:31 UTC
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-24 04:51:15 UTC
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-24 09:35:58 UTC
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-24 14:23:02 UTC
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-24 18:37:38 UTC
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-24 21:45:15 UTC
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-25 00:06:15 UTC
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-25 04:58:41 UTC
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-25 09:57:59 UTC
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-25 14:55:19 UTC
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-25 18:58:40 UTC
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-25 21:57:39 UTC
TARGET_ORG not configured for derdack; skipping public-org deep scan.
## REPOSCAN 2026-09-26 00:18:52 UTC
TARGET_ORG not configured for derdack; skipping public-org deep scan.
