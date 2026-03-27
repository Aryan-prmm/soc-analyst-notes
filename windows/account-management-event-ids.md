# Windows Account Management Event IDs

Account management events track changes to user accounts and group memberships.  
These events are critical for detecting **privilege escalation, persistence, and unauthorized access**.

---

## Event ID 4720 — New User Account Created

Description:
A new user account is created.

SOC Relevance:
- Possible creation of a backdoor account
- Indicator of unauthorized access

---

## Event ID 4726 — User Account Deleted

Description:
A user account is deleted.

SOC Relevance:
- May indicate attacker attempting to remove evidence

---

## Event ID 4722 — Account Enabled

Description:
A previously disabled account is enabled.

SOC Relevance:
- Attackers may re-enable dormant accounts

---

## Event ID 4725 — Account Disabled

Description:
A user account is disabled.

SOC Relevance:
- May be legitimate or attacker disabling accounts

---

## Event ID 4732 — User Added to Group

Description:
A user is added to a group.

SOC Relevance:
- If added to privileged groups (e.g., Administrators), indicates privilege escalation

---

## Event ID 4733 — User Removed from Group

Description:
A user is removed from a group.

SOC Relevance:
- May indicate permission changes or cleanup activity

---

## Attack Pattern — Privilege Escalation

Example sequence:

4720 → New user account created  
4732 → User added to Administrators group  
4672 → Administrative privileges assigned  

Explanation:

1. Attacker creates a new account (4720)
2. Adds account to privileged group (4732)
3. Logs in with administrative privileges (4672)

This pattern indicates a **full system compromise**.

---

## Splunk Detection Example

Search for account creation and privilege assignment:

