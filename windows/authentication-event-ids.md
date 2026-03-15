# Windows Authentication Event IDs

Windows records authentication activity in the **Security Event Log**.  
SOC analysts monitor these events to detect brute-force attacks, credential abuse, and unauthorized access.

---

## Event ID 4624 — Successful Logon

Description:
User successfully logged into the system.

Important fields:
- Username
- Source IP address
- Logon type
- Timestamp

Common Logon Types:

2 → Interactive login (local login)  
3 → Network login  
10 → Remote Desktop (RDP)

SOC Relevance:
Used to identify **who logged in and from where**.

---

## Event ID 4625 — Failed Logon

Description:
Login attempt failed.

Common reasons:
- Incorrect password
- Invalid username
- Disabled account

SOC Relevance:
Multiple 4625 events may indicate **brute force attacks**.

---

## Event ID 4634 — Logoff

Description:
User logged off from a system.

SOC Relevance:
Helps analysts track **session activity timelines**.

---

## Event ID 4648 — Logon with Explicit Credentials

Description:
User attempted login using explicit credentials.

Example command:

runas /user:administrator cmd.exe

SOC Relevance:
Possible **credential misuse or lateral movement**.

---

## Event ID 4740 — Account Lockout

Description:
Account locked after multiple failed login attempts.

SOC Relevance:
Strong indicator of **password guessing or brute force attacks**.

---

## Event ID 4672 — Special Privileges Assigned

Description:
User logged in with **administrator privileges**.

Examples:
- Administrator
- Domain Admin

SOC Relevance:
Monitor privileged account activity.

---

## Brute Force Attack Pattern

SOC analysts detect brute-force attacks by observing event patterns.

Example sequence:

4625 → 4625 → 4625 → multiple failed login attempts  
4624 → successful login  
4672 → administrator privileges assigned

Explanation:

1. Attacker attempts multiple passwords (4625)
2. Eventually logs in successfully (4624)
3. If the account has admin privileges, event 4672 appears

This pattern may indicate **successful brute-force compromise**.
