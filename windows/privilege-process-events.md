# Windows Privilege, Process, Persistence, and Cleanup Event IDs

These event IDs are critical for detecting:
- Malware execution
- Privilege escalation
- Persistence mechanisms
- Attacker cleanup activities

---

## Event ID 4672 — Special Privileges Assigned

Description:
User logged in with administrative privileges.

SOC Relevance:
- Indicates privileged account activity
- High-risk login event

---

## Event ID 4688 — New Process Created

Description:
A new process is created on the system.

Examples:
- powershell.exe
- cmd.exe

SOC Relevance:
- Detect malware execution
- Identify suspicious commands

Important:
Check the **parent process**.

Example:
WINWORD.EXE → powershell.exe → suspicious behavior

---

## Event ID 4698 — Scheduled Task Created

Description:
A scheduled task is created.

SOC Relevance:
- Indicates persistence mechanism
- Malware may use scheduled tasks to maintain access

---

## Event ID 1102 — Audit Log Cleared

Description:
Security audit logs are cleared.

SOC Relevance:
- Strong indicator of attacker attempting to cover tracks

Important:
Investigate all activity **before this event occurs**

---

## Attack Scenarios

### Malware Execution

4688 → powershell.exe launched  
Parent process → WINWORD.EXE  

Explanation:
A malicious document triggers PowerShell execution.

---

### Persistence Mechanism

4688 → process executed  
4698 → scheduled task created  

Explanation:
Malware creates a scheduled task for persistence.

---

### Cleanup Activity

1102 → audit logs cleared  

Explanation:
Attacker deletes logs to hide activity.  
Investigate all events before this timestamp.

---



