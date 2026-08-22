# RDP Brute-Force Investigation

Severity: Medium

Disposition: Escalate to L2

Tools: Wazuh, Windows Security Logs, Sysmon

## Alert

Multiple failed RDP authentication attempts were observed against DESKTOP-96GH4UH.

## Evidence

| Event | Event ID | Finding |
| -------- | -------- | -------- |
| Failed authentication | 4625 | 6 failed attempts |
| Successful authentication | 4624 | Successful login |
| File creation | Sysmon 11 | `malicious.exe` created |
| Source IP | — | `192.168.141.1` |
| Target | — | `DESKTOP-96GH4UH` |
| Account | — | `cyberlab` |
| First failure | — | Aug 22, 2026 @ 00:50:10.047 |
| Successful login | — | Aug 22, 2026 @ 00:50:16.647 |

Six failed authentication attempts occurred within approximately 7 seconds, followed by a successful authentication 6.6 seconds after the first failure. This pattern is suspicious and may indicate RDP brute-force activity.

The executable was intentionally created as part of the controlled lab scenario to simulate suspicious post-authentication activity.

## Authentication Evidence
### Failed Authentication — Event ID 4625
<img width="1905" height="746" alt="Screenshot 2026-08-22 013146" src="https://github.com/user-attachments/assets/9056a4cf-b61d-4d9c-9e63-3407e6f690fd" />
### Successful Authentication — Event ID 4624
<img width="1916" height="740" alt="Screenshot 2026-08-22 013153" src="https://github.com/user-attachments/assets/d58eb042-fd7e-4a87-92e7-7334b02351db" />
### File Creation — Sysmon Event ID 11
<img width="1906" height="671" alt="sysmon-file-create" src="https://github.com/user-attachments/assets/4e26fa91-af8d-4aaf-ab25-ed8cce908e0a" />

## Assessment

The repeated authentication failures followed by successful access from the same source are suspicious.

Based on the available evidence, I escalated the case to L2 for further investigation. I escalated the case to L2 for further investigation.

## Disposition

*Escalate to L2*

### Recommended L2 actions:

- Validate whether the successful authentication was authorized.
- Investigate the source IP and account for additional suspicious activity.
- Review endpoint activity following authentication.
- Determine whether the executable creation was authorized.
- Take appropriate containment/credential-reset actions if compromise is confirmed.
