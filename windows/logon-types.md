# Windows Logon Types

Logon types indicate **how a user authenticated to a system**.  
They are commonly found in **Event ID 4624 (Successful Logon)**.

SOC analysts use logon types to understand:
- Login method
- Potential attack behavior
- Suspicious access patterns

---

## Important Logon Types

### Type 2 — Interactive

Description:
User logs in locally using keyboard and screen.

Example:
- Physical login on workstation

SOC Relevance:
- Normal user activity

---

### Type 3 — Network

Description:
Login over the network.

Examples:
- Accessing shared folders (SMB)
- Remote system access

SOC Relevance:
- Indicates possible **lateral movement**
- Common in internal network activity

---

### Type 5 — Service

Description:
Login performed by a service account.

Examples:
- Background services
- Scheduled tasks

SOC Relevance:
- Can indicate **persistence mechanisms**
- Service accounts are often targeted by attackers

---

### Type 10 — Remote Interactive (RDP)

Description:
Login via Remote Desktop Protocol (RDP).

SOC Relevance:
- High-risk login type
- Common entry point for attackers and ransomware

Red Flags:
- Login at unusual hours
- Login from unknown or external IP addresses
- Multiple failed attempts followed by success

---

### Type 11 — Cached Interactive

Description:
Login using cached credentials when domain controller is unavailable.

Examples:
- Offline login on domain-joined machine

SOC Relevance:
- Usually normal behavior
- Should be monitored for anomalies

---

## SOC Detection Notes

Primary event to monitor:

Event ID: 4624

Key field:
- Logon Type

---

## Suspicious Patterns

- Type 3 → Potential lateral movement
- Type 5 → Possible persistence via service accounts
- Type 10 → High-risk (RDP access)

---

## Example Detection (Splunk)

Search for successful logins:

