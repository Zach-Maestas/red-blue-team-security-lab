# 🔴🔵 Red & Blue Team Security Lab

**Zach Maestas | CS 456 — Fall 2025**

This repo is my full cybersecurity lab portfolio — covering both sides of the fight. I built and broke into systems as the **attacker (Red Team)** 🗡️ and investigated + defended against attacks as the **responder (Blue Team)** 🛡️, all in a controlled university lab environment.

> ⚠️ **Ethics & Authorization Notice**
> All testing was performed against intentionally vulnerable lab systems with full authorization. No real-world systems or data were targeted. Ever.

---

## 🔴 Red Team Project

**Penetration Test — SSH Misconfiguration → Full Root Compromise**

- 🔍 Enumerated exposed services across the target VM (Nmap, SMB, DVWA, SSH)
- 🔑 Discovered a critical SSH config flaw on a non-standard port — weak creds + root login enabled
- 💥 Achieved **immediate root access** without brute force or privilege escalation
- 📊 Assessed overall risk as **CRITICAL** and provided remediation recommendations

📄 **Full Report:** [`CS456_Pen_Test_Report_Zach_Maestas.pdf`](./red-team/report/CS456_Pen_Test_Report_Zach_Maestas.pdf)

---

## 🔵 Blue Team Project

**Incident Response — Recon & SSH Auth Pressure Investigation**

- 🕵️ Investigated suspicious scanning and login activity across an instructor-provided dataset
- 📋 Correlated UFW firewall logs, SSH auth records, and packet captures
- 🗓️ Constructed an attack timeline and impact assessment
- 🔒 Proposed detection rules and hardening improvements

📄 **Full Report:** [`blue-team/README.md`](./blue-team/README.md)

---

## 🧰 Skills Demonstrated

- 🌐 Network reconnaissance & service enumeration
- 🔑 Credential exposure and access validation
- 🧪 Evidence-based penetration testing
- 📊 Log analysis & attack timeline reconstruction
- 🚨 Incident impact assessment
- 🛡️ Security hardening & mitigation strategies
- 📝 Professional technical reporting

## 🖥️ Lab Environment

- 🐳 Containerized vulnerable services (Podman)
- 🎯 Student VMs as authorized targets
- 🌍 Web application security testing (DVWA)
- 📂 Centralized log collection for forensic analysis

## 💡 Takeaway

These projects demonstrate not only **how systems get compromised**, but **how defenders detect, analyze, and respond** — a full lifecycle view valued in security engineering, SOC, and infrastructure roles.
