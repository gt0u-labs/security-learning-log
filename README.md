# 🔐 Security Learning Log

Ongoing, self-directed defensive security training — HTB Academy, HTB Labs and
TryHackMe — with notes on what each module actually covered.

Kept as a running record so the work is traceable, and connected back to the
infrastructure I already run in my own homelab.

---

## Where I'm at

**64 modules, rooms and machines completed** across HTB Academy, HTB Labs and
TryHackMe (Aug – Sep 2026).

Organized by role rather than by platform:

| Area | Covers |
| --- | --- |
| **Blue team / SOC** | Alert triage, log analysis, phishing and email header analysis (SPF/DKIM/DMARC), traffic analysis, defensive security workflow |
| **Systems & networking** | Linux fundamentals, Windows fundamentals, OSI/TCP-IP, subnetting, network architecture |
| **Identity & access** | IAAA model, MFA, SSO (Kerberos/LDAP), RADIUS/TACACS+, OAuth 2.0, OpenID Connect, SAML |
| **Web & application security** | SQL injection, file inclusion, JavaScript deobfuscation, OWASP Top 10 |
| **Offensive fundamentals** | Pentesting methodology, Metasploit, reconnaissance, threat intel |
| **Cloud & DevSecOps** | CI/CD pipeline security, containerisation, Kubernetes hardening, IaC |

📄 **[Full module-by-module log →](PROGRESS.md)**

---

## Write-ups

Longer pieces where something broke and I had to work out why.

**[Proxmox GPU passthrough — VFIO troubleshooting →](writeups/proxmox-gpu-passthrough.md)**
Diagnosing a PCI ROM signature error through `dmesg`, resolving it with a
card-specific VBIOS, and the driver mistake that cost me a full rebuild.

---

## How this connects to the lab

The training here isn't separate from the infrastructure I run. Network
reconnaissance practice targets the Kali and Ubuntu VMs on my own
[Proxmox homelab](https://github.com/gt0u-labs/homelab-notes), and the log
analysis modules feed directly into the Grafana/Loki/Promtail stack I maintain
on the same setup.

---

## Next

- Wazuh deployment with custom detection rules
- Sigma rules mapped to MITRE ATT&CK
- CompTIA Security+

---

🌐 Full profile: [gt0u-labs.github.io](https://gt0u-labs.github.io/)
