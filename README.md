# WINDOWS 11 STIG HARDENING PROJECT

## OVERVIEW
This project demonstrates the implementation of Security Technical Implementation Guides (STIGs) on a Windows 11 virtual machine using PowerShell.

The objective was to apply system hardening controls, validate compliance using a vulnerability scanner, and document both successful and failed configurations.

---

## ENVIRONMENT
- Operating System: Windows 11  
- Platform: Microsoft Azure Virtual Machine  
- Tools:
  - PowerShell (administrative execution)
  - Nessus (vulnerability scanner)

---

## OBJECTIVES
- Implement STIG controls across multiple categories  
- Automate configurations using PowerShell  
- Perform vulnerability scanning to validate compliance  
- Identify gaps between configuration and scan results  

---

## SCOPE OF IMPLEMENTATION

### ACCOUNT POLICIES (AC)
- Lockout threshold  
- Lockout duration  
- Reset lockout counter  
- Password history  
- Minimum password age  
- Minimum password length  
- Password complexity  

### USER RIGHTS (UR)
- Restriction of “Allow log on locally” to authorized groups  

### SYSTEM OPTIONS (SO)
- Require CTRL+ALT+DEL for logon  
- Configure inactivity timeout  
- Configure legal notice title  
- Enforce NTLM restrictions  
- Enable SMB client signing  
- Enforce audit policy subcategories  

### AUDIT POLICIES (AU)
- Configure Application event log size  
- Configure Security event log size  

### SERVICES AND DEVICE HARDENING
- Disable Secondary Logon service  
- Disable Bluetooth service  

---

## IMPLEMENTATION APPROACH
- PowerShell used for registry and system configuration  
- `net accounts` used for password and lockout policies  
- `secedit` used to configure local security policies  
- Registry edits applied for system and authentication controls  
- Nessus used to validate applied configurations  

---

## RESULTS

### CONTROLS SUCCESSFULLY IMPLEMENTED
- All Account Policy controls (AC series)  
- User Rights control (WN11-UR-000025)  
- Audit policy enforcement (WN11-SO-000030)  
- Inactivity timeout configuration (WN11-SO-000070)  
- SMB client signing (WN11-SO-000100)  
- Secondary Logon service disabled (WN11-00-000175)  

### CONTROLS NOT FULLY COMPLIANT
- WN11-SO-000075 — CTRL+ALT+DEL requirement  
- WN11-SO-000080 — Legal notice title  
- WN11-SO-000180 — NTLM restriction  
- WN11-AU-000500 — Application event log size  
- WN11-AU-000505 — Security event log size  
- WN11-00-000210 — Bluetooth  

---

## KEY CHALLENGE
During implementation, the following control caused a system lockout:

- WN11-SO-000095 — Smart Card removal behavior  

This configuration enforced hardware-based authentication and disabled password-based login, resulting in loss of administrative access. Recovery required rebuilding the environment.

---

## KEY LEARNINGS
- Authentication-related STIGs can impact system accessibility  
- Certain controls require careful sequencing to avoid lockout  
- Vulnerability scanners may require additional configuration beyond registry changes  
- Firewall configurations can affect scan results  
- Incremental validation is critical during hardening  

---

## NESSUS SCANNING CONSIDERATIONS
- Firewall should remain enabled  
- Temporary rules may be required to allow scanner communication  
- Required protocols include SMB, RPC, and WMI  

---

## RECOMMENDATIONS
- Maintain a backup administrative account before applying STIGs  
- Apply high-impact authentication controls cautiously  
- Validate each control incrementally  
- Use snapshots or recovery strategies in controlled environments  

---

## OUTCOME
- Implemented multiple STIG controls using automation  
- Identified discrepancies between applied configurations and scan validation  
- Demonstrated practical challenges in system hardening and compliance enforcement  

---

## REPOSITORY CONTENTS
- PowerShell scripts for STIG implementation  
- Documentation of applied controls  
- Scan validation results  
- Remediation analysis  

---

## NEXT STEPS
- Remediate remaining failed STIG controls  
- Improve automation accuracy  
- Increase compliance score through targeted fixes  
