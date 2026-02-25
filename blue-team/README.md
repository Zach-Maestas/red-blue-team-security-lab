# 🔵 Blue Team: Incident Response (CS456 Lab)

**Author:** Zach Maestas
**Incident ID:** ZachM-20251205
**Report Date:** 2025-12-07

This folder documents a blue team **incident-response investigation** for an authorized CS456 lab environment (Podman services + host firewall logging + packet capture).

## Important Note (Simulation Dataset)

My assigned red team partner didn't generate attack traffic against my deployed lab, so my original incident report documents "no observed attack" for the live environment. To still demonstrate a realistic IR workflow, I analyzed an **instructor-provided log + packet-capture dataset** that *does* contain attack activity. The findings below reflect **that simulated incident**, not my live environment.

## What's in this folder

- `podman-compose.yml` (environment artifacts: services + layout)
- `services.pdf` (diagram/descriptions of the Podman services)
- `logs/` (service/system logs from the dataset)
- `report/` (full write-up)

## Executive Summary

| | |
|---|---|
| **Observed activity** | Recon/scanning + SSH authentication pressure |
| **Confirmed compromise** | Not proven from available evidence |

At a high level, the dataset shows:
- Broad **TCP SYN probing** across many internal targets/ports (classic recon behavior)
- **SSH authentication failures** (failed login attempts recorded)
- No recorded HTTP or PostgreSQL activity — those logs are empty in this dataset

Still a valuable blue-team exercise: it shows how to triage scanning, validate auth activity, and document what the evidence does (and doesn't) support.

---

## Detection and Analysis

### 1) Recon / Port Scanning (Firewall Evidence)

`ufw.log` shows repeated TCP SYN traffic consistent with scanning:
- Large volume of SYN attempts from a single internal source
- Targets spread across dozens of internal destinations
- Frequent probing of **SSH (TCP/22)** plus additional high ports

**Why it matters:** This is a common precursor to exploitation. Even without confirmed compromise, this is "raise a flag and investigate" activity.

### 2) SSH Authentication Pressure (Container/System Evidence)

Failed SSH login activity (btmp/failed-login records) shows:
- Repeated login attempts against a single username
- Attempts originating from a small set of internal attacker IPs

**Why it matters:** This indicates credential guessing / brute-force behavior. In production, this would trigger immediate alerting and hardening (rate limiting, key-only auth, IP restrictions).

### 3) Web & Database Decoys (No Interaction Recorded)

Logs for `nginx` and `postgresql` are empty in this dataset — no evidence of web exploitation or database auth attempts.

**Interpretation:** Attack activity was concentrated on recon + SSH, not web/DB interaction (or logging didn't capture it).

### 4) Packet Capture Validation

`capture.pcap` serves as the "ground truth" dataset to:
- Confirm scanning patterns and targeted services
- Check whether SSH sessions fully established
- Look for post-auth activity (callbacks, downloads, lateral movement)

---

## Timeline

| Window | Activity |
|--------|----------|
| **2025-11-30 00:00 – ~07:26** | Firewall log coverage |
| **Nov 29–30** | SSH failed login attempts observed |

Attack-like activity spans **multiple hours** — not a one-off probe.

## Scope & Impact Assessment

Based on available evidence:
- ✅ Recon and credential pressure **occurred**
- ❌ No confirmed privileged session, data access, or persistence

**Verdict:** Attempted intrusion / suspicious activity — insufficient evidence to declare a successful breach from this dataset alone.

## Containment, Eradication & Recovery (Recommended)

If this were a live environment, here's the playbook:

**Containment**
- Restrict SSH exposure (allowlist source IPs or require VPN/bastion)
- Block offending IPs from failed-auth + scan telemetry
- Increase logging verbosity for auth + network events

**Eradication / Hardening**
- Disable password auth — enforce key-only SSH
- Disable direct root login (`PermitRootLogin no`)
- Add rate limiting (fail2ban or equivalent)
- Validate UFW rules — only required ports should be reachable

**Recovery**
- Review accounts, rotate credentials/keys
- Confirm integrity of configs and containers
- Preserve logs + pcap as evidence

## Lessons Learned

- Even when your live lab doesn't get attacked, you can still demonstrate IR skills by investigating a realistic dataset — just be transparent about what's simulated vs. real
- Good defensive work includes stating what you **can't** prove from evidence, not just what you can

## Responsible Use Statement

All activity and artifacts in this repository are from an **authorized university lab** and are shared for educational/portfolio purposes only.
