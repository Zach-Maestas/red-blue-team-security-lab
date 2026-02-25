# 🔴 Red Team: Penetration Test (CS456 Lab)

**Author:** Zach Maestas
**Date of Assessment:** 2025-12-03
**Target (Authorized Lab):** `192.168.0.153`

This section documents an **authorized penetration test** against a student VM. The engagement identified a **critical SSH misconfiguration** that enabled **immediate root access** — full system compromise, no brute force needed. 💥

## 📁 What's in this folder

- **Full report (PDF):** [`./report/CS456_Pen_Test_Report_Zach_Maestas.pdf`](./report/CS456_Pen_Test_Report_Zach_Maestas.pdf)
- **Scan outputs:** `./scans/`
- **Screenshots / evidence:** `./screenshots/`

## 🎯 Scope + Rules

- **In-scope:** `192.168.0.153`
- **Out-of-scope:** any other devices on the network — **no DoS** activities performed
- Additional exploitation beyond the identified compromise path was not pursued

## 🔍 Methodology (High Level)

1. Enumerated exposed services with **Nmap** and evaluated each for realistic exploitability
2. Investigated SMB, NoMachine NX, and DVWA as potential paths — none produced viable routes
3. Identified and validated a **critical SSH configuration issue** on a non-standard port, leading to privileged access

## 🚨 Key Result

**Overall risk rating: CRITICAL** 🔥

### Finding 1: Unauthorized Root Access via Weak SSH Configuration (Critical)

- **Impact:** Immediate privileged access without brute force or privilege escalation — total system compromise
- **Affected service:** SSH on TCP **port 2222** (`192.168.0.153`)

**Recommended remediation:**
- ❌ Disable root login in `sshd_config` (`PermitRootLogin no`)
- 🔐 Enforce strong passwords
- 🔑 Prefer key-based authentication
- 🌐 Restrict SSH exposure (authorized IPs only)
- 🔄 Rotate passwords + audit accounts

## 🚫 Non-Viable Attack Paths (Attempted)

| Service | Port | Result |
|---------|------|--------|
| **SMB** | 445 | Only default admin shares; no anonymous/writable access |
| **DVWA** | 8081 | Database not initialized — web exploitation blocked |

## 🗺️ Attack Path Summary

Service enumeration → SSH on port 2222 flagged as high-value → validated critical auth misconfiguration → **root access achieved** → full VM control.

## 🧰 Tools Used

- Nmap
- smbclient
- SSH client
- Web browser (DVWA validation)

## ⚖️ Responsible Disclosure

This work was performed **only** in an authorized university lab environment and is shared for educational/portfolio purposes.
