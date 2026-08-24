# 01_Brute-Force-Investigation
## MITRE ATT&CK
- T1110 - Brute Force
## Objective

Investigate repeated failed RDP authentication followed by successful authentication using Wazuh.

## Environment

- Windows endpoint
- Wazuh
- Sysmon
- RDP
- Controlled lab environment

## Scenario

Multiple failed RDP authentication attempts

↓

Successful authentication

↓

L1 investigation

↓

Evidence correlation

↓

Escalation

## Outcome

- **Finding:** Suspicious RDP authentication activity
- **Disposition:** Escalated to L2
- **Key evidence:** Multiple failed RDP logons followed by successful authentication from the same source

## Report

[View the investigation report](investigation-report.md)

## Medium Post

[View the investigation in detail](https://medium.com/@larry.kaheiwong/how-i-investigated-a-suspected-rdp-brute-force-attempt-using-wazuh-ba517a2231be)
