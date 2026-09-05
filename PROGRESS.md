# 🔐 Full Progress Log

Everything I've completed so far, in order, with a quick note on what actually stuck from each one.

---

## 📚 HTB Academy

| Module | Tier | Date | Notes |
|---|---|---|---|
| Intro to Academy | Tier 0 | Aug 2026 | Basically onboarding — how the platform and learning paths work |
| Linux Fundamentals | Tier 0 | Aug 2026 | Mostly stuff I already do daily in my own homelab, but good to have it formalized |
| Web Requests | Tier 0 | Aug 2026 | HTTP methods, headers, response codes, curl and browser devtools for poking at APIs |
| Learning Process | Tier 0 | Aug 2026 | Less technical, more about staying focused and treating mistakes as part of the process |
| Identity and Access Management | Tier 1 | Aug 2026 | IAAA model, MFA, SSO (Kerberos/LDAP), RADIUS/TACACS+, OAuth 2.0, OpenID Connect, SAML |
| SQL Injection Fundamentals | Tier 0 | Aug 2026 | Union-based SQLi, using it for OS interaction, mitigations — this one was rough, needed a walkthrough for a couple of the later flags |
| JavaScript Deobfuscation | Tier 0 | Aug 2026 | Got stuck looking in the wrong place for a while before it clicked |
| Phishing Email Analysis (LetsDefend) | Tier 0 | Aug 2026 | Header analysis, SPF/DKIM/DMARC, static + dynamic analysis of attachments, WHOIS/MX attribution |
| Introduction to Networking | Tier 0 | Aug 2026 | Internet structure, topologies, OSI/TCP-IP, IPv4/IPv6, subnetting |
| File Inclusion | Tier 0 | Aug 2026 | LFI, path traversal, filter bypasses, RCE through PHP wrappers/RFI/log poisoning — one of the harder ones so far, had to lean on outside references for the last few flags |
| Introduction to Web Applications | Tier 0 | Aug 2026 | Front-end/back-end basics, HTML/CSS/JS, XSS/CSRF intro, web servers, databases, OWASP Top 10 |
| Introduction to Information Security | Tier 0 | Aug 2026 | InfoSec structure, threat types, red/blue/purple teams, career paths up to CISO |
| Getting Started | Tier 0 | Aug 2026 | Pentesting overview + a real skills assessment at the end — one guided box, one without. Took me about 4 hours, got stuck on a port 9443 issue for a while, but finished my first unguided box |

---

## 🎯 HTB Labs (unguided machines)

| Machine | Difficulty | OS | Date | Notes |
|---|---|---|---|---|
| Meow | Very Easy | Linux | Aug 2026 | First Labs machine |
| Fawn | Very Easy | Linux | Aug 2026 | Second one, same session |
| Dancing | Very Easy | Windows | Aug 2026 | First Windows box |
| Redeemer | Very Easy | Linux | Aug 2026 | Very Easy Labs machines are noticeably lighter than the denser Academy modules |
| Cap | Easy | Linux | Aug 2026 | Harder than the Very Easy ones — needed one hint to understand what a step was actually asking for |
| Appointment | Very Easy | Linux | Aug 2026 | |
| Sequel | Very Easy | Linux | Aug 2026 | |
| Crocodile | Very Easy | Linux | Aug 2026 | Pretty entertaining, very light difficulty |
| Responder | Very Easy | Windows | Aug 2026 | |
| Archetype | Very Easy | Windows | Aug 2026 | |
| Three | Very Easy | Linux | Aug 2026 | |
| Vaccine | Very Easy | Linux | Sep 2026 | |
| Oopsie | Very Easy | Linux | Sep 2026 | |
| Unified | Very Easy | Linux | Sep 2026 | Got stuck on one question — turned out to be an HTB platform bug, a power cut and retry with the exact same answer fixed it |
| Orion | Very Easy | Linux | Sep 2026 | |

---

## 📚 TryHackMe

| Room | Difficulty | Date | Notes |
|---|---|---|---|
| Windows Fundamentals 1 | Easy | Aug 2026 | Desktop, NTFS, UAC, Control Panel |
| Windows Fundamentals 2 | Easy | Aug 2026 | System config, registry, resource monitoring |
| Security Principles | Easy | Aug 2026 | CIA triad and common security models |
| Secure Network Architecture | Medium | Aug 2026 | Network segmentation and design |
| Governance & Regulation | Easy | Aug 2026 | Policies and frameworks behind org-level security |
| Security Engineer Intro | Easy | Aug 2026 | What the role actually looks like day to day |
| Search Skills | Easy | Aug 2026 | Searching docs/technical sources efficiently instead of guessing |
| Defensive Security Intro | Easy | Aug 2026 | Investigating an ongoing attack — blue team basics |
| Linux Fundamentals (Pt1) | Easy | Aug 2026 | First interactive terminal commands |
| Pentesting Fundamentals | Easy | Aug 2026 | Ethics and methodology of a pentest engagement |
| Metasploit: Introduction | Easy | Aug 2026 | Core components of the framework |
| Intro to Pipeline Automation | Easy | Aug 2026 | CI/CD pipelines and where security fits in (part of the DevSecOps path) |
| Red Team Fundamentals | Easy | Aug 2026 | Basics of a red team engagement and how it differs from other security work |
| Red Team Threat Intel | Medium | Aug 2026 | Applying threat intel to adversary emulation |
| Red Team OPSEC | Easy | Aug 2026 | Operational security process for red team work |
| Senior Security Analyst Intro | Easy | Aug 2026 | What a SOC L2 analyst does day to day |
| SOC L1 Alert Triage | Easy | Aug 2026 | Building a systematic approach to triaging alerts |
| The CIA Triad | Easy | Aug 2026 | Confidentiality, Integrity, Availability as the base of most security decisions |
| Encryption - Crypto 101 | Medium | Aug 2026 | Fundamentals of encryption — genuinely enjoyed this one |
| MS Sentinel: Introduction | Easy | Aug 2026 | What Sentinel is and where it fits in a SOC analyst's workflow |
| Introductory Networking | Easy | Aug 2026 | More tedious than hard — needed close attention to detail |
| Cluster Hardening | Easy | Aug 2026 | Finished in about 15 minutes |
| K8s Best Security Practices | Medium | Aug 2026 | Kubernetes security at the cluster level |
| History of Malware | Easy | Aug 2026 | Actually fun — the first computer virus dates back to 1971 |
| Intro to Containerisation | Easy | Aug 2026 | Estimated 30 min, finished in under 10 |
| Custom Tooling Using Python | Easy | Aug 2026 | |
| Intro to Logs | Easy | Aug 2026 | |
| Web Application Security | Easy | Sep 2026 | |
| Passive Reconnaissance | Easy | Sep 2026 | |
| Traffic Analysis Essentials | Easy | Sep 2026 | |
| TryHack3M: Bricks Heist | Easy | Sep 2026 | |

---

[← Back to summary](./README.md)

---

## 🔧 Infrastructure troubleshooting: GPU passthrough with a physical display

Set up a Kali Linux VM on Proxmox VE with a monitor, keyboard, and mouse connected directly through GPU passthrough, instead of relying on Proxmox's web console — the goal was to stop Burp Suite and other GUI-heavy tools from crawling through the browser console.

**What actually happened, and how each part got fixed:**

1. **No video output at all.** `dmesg` pointed to `vfio-pci 0000:01:00.0: Invalid PCI ROM header signature: expecting 0xaa55, got 0xffff`. Couldn't read the card's ROM live from `/sys/bus/pci/devices/.../rom` (I/O error even with the VM fully stopped), so I grabbed the correct vendor-specific VBIOS for my exact card (MSI GTX 1080 Gaming X) from a public VBIOS archive and pointed the VM at it with `romfile=` in the PCI device config.
2. **Keyboard and mouse doing nothing** on the physical display — GPU passthrough doesn't bring USB along with it automatically. Added the keyboard and mouse as their own USB devices (by vendor/device ID) in the VM's hardware config.
3. **Still nothing on screen after the ROM fix.** Turned out the install ISO was still mounted and the disk was ahead of the CD-ROM in the boot order, so the VM kept trying to boot into an unfinished install instead of continuing setup. Unmounted the ISO, fixed the boot order, and set the virtual Display to `none` so the passthrough GPU wasn't competing with Proxmox's own virtual VGA output.
4. **Mistake I won't repeat:** installed `nvidia-driver` manually inside Kali after passthrough was already working fine, and it broke the whole install — no video, no VNC fallback, had to rebuild from scratch. Passthrough gives you working video without installing GPU drivers inside the guest at all.

**End result:** Kali now runs through the passed-through GPU with a real monitor, keyboard, and mouse — noticeably faster than the web console for anything GUI-heavy.
