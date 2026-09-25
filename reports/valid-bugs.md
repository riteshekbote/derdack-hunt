# Validated findings (running count 0)

- 2 lead(s) marked VALID at 2026-09-03 23:20:09 UTC
  - **Verdict: VALID**
  - **Verdict: VALID**

- 3 lead(s) marked VALID at 2026-09-04 17:46:22 UTC
  - | Q7 Reasonable triager? | **Yes** | Information disclosure of sensitive file paths on a live dev host is a valid finding |
  - **Verdict: VALID**
  - | dev.derdack.com MultiViews path disclosure | **VALID** | 5.3 | Report to bugs.olivermaicher.eu |

- 1 lead(s) marked VALID at 2026-09-05 13:31:45 UTC
  - Please paste the lead(s) you want me to triage, and I'll run each through the 7-Question Gate with verdict, reasoning, and (if VALID) proof steps, impact, CVSS 3.1, and reporting channel.

- 2 lead(s) marked VALID at 2026-09-06 06:28:40 UTC
  - **Verdict: VALID**
  - **Verdict: VALID**

- 2 lead(s) marked VALID at 2026-09-08 10:34:26 UTC
  - **VERDICT: VALID**
  - **VERDICT: VALID**

- 4 lead(s) marked VALID at 2026-09-09 06:38:04 UTC
  - **VERDICT: VALID**
  - **VERDICT: VALID**
  - | 1 | Cross-Env JWKS Key + Client/Scope Reuse | **VALID** | 7.4 |
  - | 6 | Staging IdP Directly Reachable | **VALID** | 6.5 |

- 4 lead(s) marked VALID at 2026-09-10 10:37:58 UTC
  - **Verdict: VALID**
  - **Verdict: VALID**
  - | Q7 Reasonable triager? | Yes — hardcoded real secrets in public code is a standard valid finding |
  - **Verdict: VALID**

- 14 lead(s) marked VALID at 2026-09-11 05:08:59 UTC
  - **Verdict: VALID**
  - **Verdict: VALID**
  - **Verdict: HOLD** — valid code defect, but impact gated on EA Scripting Host deployment and attacker ability to control event parameters; needs confirmatory evidence of production deployment
  - **Verdict: HOLD** — valid code defect, but impact requires confirmation that parameters originate from external/user input in production
  - **Verdict: VALID**
  - **Verdict: VALID**
  - **Verdict: VALID**
  - **Verdict: VALID**
  - | 1 | Cross-env JWKS key reuse (4 hosts) | **VALID** | 7.4 | HIGH |
  - | 2 | Hardcoded SQL Server SA creds | **VALID** | 8.1 | HIGH |
  - | 5 | Hardcoded Checkmk creds + internal IP | **VALID** | 7.5 | MEDIUM |
  - | 6 | SIGNL4 secret logged at INFO (ioBroker) | **VALID** | 5.3 | MEDIUM |
  - | 7 | Team secrets in public repos | **VALID** | 5.3 | MEDIUM |
  - | 8 | PII in public CSV export | **VALID** | 5.3 | MEDIUM |

- 7 lead(s) marked VALID at 2026-09-13 21:11:57 UTC
  - | 1 | Cross-env JWKS key + client/scope reuse (devconnect + connect.signl4.com) | VALID | 7.4 | Reported |
  - | 2 | Staging IdentityServer directly reachable (devconnect.signl4.com, password grant) | VALID | 6.5 | Reported |
  - | 3 | Hardcoded SQL Server SA creds (`Derdack!`) in public EA plugin | VALID | 8.1 | Reported |
  - | 4 | Hardcoded Checkmk admin creds + internal IP in public plugin | VALID | 7.5 | Reported |
  - | 5 | SIGNL4 team secrets in public repos (Google IoT, Postman, DevTools) | VALID | 5.3 | Reported |
  - | 6 | SIGNL4 secret logged at INFO level in ioBroker adapter | VALID | 5.3 | Reported |
  - | 7 | PII + internal infra URLs in public CSV export | VALID | 5.3 | Reported |

- 6 lead(s) marked VALID at 2026-09-14 21:52:08 UTC
  - **Verdict: VALID**
  - **Verdict: VALID**
  - **Verdict: VALID**
  - | 1 | Cross-env JWKS key reuse | **VALID** | 8.1 |
  - | 2 | Password grant on staging IdP | **VALID** | 7.3 |
  - | 5 | /de/ XML-RPC exposed | **VALID** | 7.5 |

- 2 lead(s) marked VALID at 2026-09-18 23:43:24 UTC
  - **VERDICT: VALID**
  - | devconnect↔prod signing key + client reuse | **VALID** | 8.1 High | Yes — bugs.olivermaicher.eu |

- 26 lead(s) marked VALID at 2026-09-20 01:52:55 UTC
  - | Q5 Novel? | **No** — already reported in valid-bugs.md (multiple entries: 2026-09-09, 09-11, 09-13, 09-14, 09-18) |
  - **Verdict: ALREADY REPORTED** — Prior VALID, CVSS 7.4 HIGH. No new action needed.
  - | Q5 Novel? | **No** — already reported in valid-bugs.md |
  - **Verdict: ALREADY REPORTED** — Prior VALID, CVSS 6.5 MEDIUM.
  - **Verdict: ALREADY REPORTED** — Prior VALID, CVSS 8.1 HIGH.
  - **Verdict: ALREADY REPORTED** — Prior VALID, CVSS 7.5 MEDIUM.
  - **Verdict: ALREADY REPORTED** — Prior VALID, CVSS 5.3 MEDIUM.
  - **Verdict: ALREADY REPORTED** — Prior VALID, CVSS 5.3 MEDIUM.
  - **Verdict: ALREADY REPORTED** — Prior VALID, CVSS 5.3 MEDIUM.
  - **Verdict: ALREADY REPORTED** — Prior VALID, CVSS 7.5 HIGH.
  - | Q5 Novel? | **Yes** — not in valid-bugs.md; distinct from the eval() finding (different file, different mechanism — shell interpolation vs eval) |
  - **Verdict: VALID**
  - | Q5 Novel? | **Yes** — not in valid-bugs.md as a standalone finding; distinct from the hardcoded SA creds finding |
  - **Verdict: VALID**
  - | Q5 Novel? | **Uncertain** — may overlap with prior VALID entries in valid-bugs.md that mention "eval" |
  - | Q7 Reasonable triager? | **Conditional** — valid code defect, but impact requires EA SDK documentation to confirm trust boundary |
  - **Verdict: HOLD** — Valid code defect but impact gated on whether EA SDK provides attacker-controllable data to these callback fields. Needs: (1) EA Scripting Host SDK documentation review, (2) confir
  - | Q5 Novel? | **Yes** — not in valid-bugs.md |
  - **Verdict: VALID**
  - | Q5 Novel? | **Yes** — not in valid-bugs.md |

- 4 lead(s) marked VALID at 2026-09-21 22:48:59 UTC
  - **Verdict: VALID**
  - **Verdict: VALID**
  - | 1 | SIGNL4 staging OIDC + cross-env JWKS key reuse | **VALID** | 7.4 |
  - | 2 | Hardcoded SA/Checkmk creds + command injection in EA scripts | **VALID** | 9.8 |

- 8 lead(s) marked VALID at 2026-09-25 05:00:44 UTC
  - **Verdict: VALID**
  - **Verdict: VALID**
  - **Verdict: VALID**
  - **Verdict: VALID**
  - | 1 | SIGNL4 staging IdP shares prod signing key + OAuth client | **VALID** | 7.4 |
  - | 2 | Hardcoded SA/Checkmk creds + command injection in EA scripts | **VALID** | 9.8 |
  - | 9 | Hardcoded SIGNL4 team secrets in public repos | **VALID** | 5.3 |
  - | 10 | PII + internal URLs in public CSV exports | **VALID** | 5.3 |
