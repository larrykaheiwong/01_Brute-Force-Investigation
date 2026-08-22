# RDP Brute-Force Investigation

Severity: Medium

Verdict: Suspicious — Escalate to L2

Tooling: Wazuh, Windows Security Logs, Sysmon

## Summary

Investigated repeated RDP authentication failures against a Windows endpoint. Six failed authentication attempts were followed by a successful login from the same source against the same account.

Six failed authentication attempts occurred within approximately 7 seconds, followed by a successful authentication 6.6 seconds after the first failure. This pattern is consistent with possible brute-force activity.


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

## Authentication Evidence
<img width="1905" height="746" alt="Screenshot 2026-08-22 013146" src="https://github.com/user-attachments/assets/9056a4cf-b61d-4d9c-9e63-3407e6f690fd" />
<img width="1916" height="740" alt="Screenshot 2026-08-22 013153" src="https://github.com/user-attachments/assets/d58eb042-fd7e-4a87-92e7-7334b02351db" />



## Post-Authentication Activity

Following the successful authentication, a test executable named malicious.exe was created on the endpoint as part of the controlled lab scenario.

The file creation was identified through Sysmon Event ID 11 (FileCreate).

<img width="1906" height="671" alt="Screenshot 2026-08-22 005614" src="https://github.com/user-attachments/assets/245dbbc6-e9e6-4447-8bbf-b0b224e03e8a" />


## Investigation

I correlated the failed and successful authentication events using the source IP, destination host, account and timestamps.

I then reviewed available endpoint telemetry following the successful login to determine whether additional suspicious activity occurred.

## Assessment

The sequence of repeated authentication failures followed by successful authentication is suspicious and consistent with possible brute-force activity. The subsequent creation of an executable was identified as post-authentication activity. In this controlled lab scenario, `malicious.exe` was intentionally created to simulate suspicious file creation.

## L1 Disposition

Escalate to L2

Further investigation should determine whether the successful authentication was authorized and whether the post-authentication executable creation was legitimate. Additional endpoint telemetry should be reviewed to determine whether further activity occurred.
