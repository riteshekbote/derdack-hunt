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
