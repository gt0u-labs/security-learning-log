# 🔐 Full Progress Log

Every module and room completed, in order, with a short note on what I actually took from each one.

---

## 📚 HTB Academy

| Module | Tier | Date | Key takeaway |
|---|---|---|---|
| Intro to Academy | Tier 0 | Aug 2026 | How the platform and learning path work |
| Linux Fundamentals | Tier 0 | Aug 2026 | Shell navigation, permissions, service management — mostly reinforced what I already use daily in my homelab |
| Web Requests | Tier 0 | Aug 2026 | HTTP methods, headers, response codes, using curl and browser devtools to interact with APIs |
| Learning Process | Tier 0 | Aug 2026 | Less technical, more about how to actually learn — staying focused, treating mistakes as part of the process |
| Identity and Access Management | Tier 1 | Aug 2026 | IAAA model, MFA factor types, SSO (Kerberos/LDAP), RADIUS/TACACS+, OAuth 2.0, OpenID Connect, SAML federation |
| SQL Injection Fundamentals | Tier 0 | Aug 2026 | DBMS/SQL basics, union-based SQL injection, exploiting SQLi for OS interaction, mitigations — genuinely hard, needed a walkthrough for parts of it |
| JavaScript Deobfuscation | Tier 0 | Aug 2026 | Reading through obfuscated JS to find what it's actually doing — got stuck looking in the wrong place before it clicked |
| Phishing Email Analysis (LetsDefend) | Tier 0 | Aug 2026 | Email header analysis, SPF/DKIM/DMARC, static and dynamic analysis of malicious attachments, WHOIS/MX attribution |
| Introduction to Networking | Tier 0 | Aug 2026 | Internet structure, proxies, topologies, OSI/TCP-IP, IPv4/IPv6, subnetting |
| File Inclusion | Tier 0 | Aug 2026 | LFI, path traversal, filter bypasses, RCE via PHP wrappers/RFI/log poisoning — genuinely hard, needed outside references to get through the last flags |
| Introduction to Web Applications | Tier 0 | Aug 2026 | Front-end/back-end architecture, HTML/CSS/JS basics, HTML Injection/XSS/CSRF intro, web servers, databases, OWASP Top 10 overview |
| Introduction to Information Security | Tier 0 | Aug 2026 | InfoSec structure, threat types (malware, phishing, APTs), red/blue/purple team roles, career paths up to CISO |
| Getting Started | Tier 0 | Aug 2026 | Pentesting overview, scanning/enumeration, public exploits, file transfers, priv esc primer — finished with a real skills assessment (one guided box, one unguided). Took ~4 hours and got stuck at 80% on a port 9443 issue before figuring it out — first box completed without a walkthrough |

---

## 🎯 HTB Labs (unguided machines)

| Machine | Difficulty | OS | Date | Notes |
|---|---|---|---|---|
| Meow | Very Easy | Linux | Aug 2026 | First Labs machine — straightforward after the Academy fundamentals |
| Fawn | Very Easy | Linux | Aug 2026 | Second Labs machine, same day |
| Dancing | Very Easy | Windows | Aug 2026 | First Windows machine on Labs |
| Redeemer | Very Easy | Linux | Aug 2026 | Straightforward — Labs Very Easy machines are noticeably simpler than the denser Academy modules like File Inclusion |
| Cap | Easy | Linux | Aug 2026 | Noticeably harder than the Very Easy machines — needed one AI-assisted hint to understand what a specific step was asking for |

---

## 📚 TryHackMe

| Room | Difficulty | Date | Key takeaway |
|---|---|---|---|
| Windows Fundamentals 1 | Easy | Aug 2026 | Desktop, NTFS, UAC, Control Panel basics |
| Windows Fundamentals 2 | Easy | Aug 2026 | System config, registry, resource monitoring |
| Security Principles | Easy | Aug 2026 | CIA triad and common security models |
| Secure Network Architecture | Medium | Aug 2026 | Network segmentation and design best practices |
| Governance & Regulation | Easy | Aug 2026 | Policies and frameworks behind organizational cybersecurity |
| Security Engineer Intro | Easy | Aug 2026 | What a day-to-day security engineering role actually looks like |
| Search Skills | Easy | Aug 2026 | Efficiently searching docs and technical sources instead of guessing |
| Defensive Security Intro | Easy | Aug 2026 | Investigating an ongoing attack scenario — blue team basics |
| Linux Fundamentals (Pt1) | Easy | Aug 2026 | First interactive terminal commands |
| Pentesting Fundamentals | Easy | Aug 2026 | Ethics and methodology behind a pentest engagement |
| Metasploit: Introduction | Easy | Aug 2026 | Core components of the Metasploit Framework |
| Intro to Pipeline Automation | Easy | Aug 2026 | DevOps CI/CD pipelines and where security concerns show up in them (part of the DevSecOps path) |
| Red Team Fundamentals | Easy | Aug 2026 | Basics of a red team engagement, stakeholders, how it differs from other security engagements |
| Red Team Threat Intel | Medium | Aug 2026 | Applying threat intel to red team engagements and adversary emulation |
| Red Team OPSEC | Easy | Aug 2026 | Operations security process for red team engagements |
| Senior Security Analyst Intro | Easy | Aug 2026 | What a SOC Level 2 analyst actually does day to day |
| SOC L1 Alert Triage | — | Aug 2026 | Building a systematic approach to triaging SOC alerts |
| The CIA Triad | — | Aug 2026 | Confidentiality, Integrity, Availability as the foundation of security decision-making |
| Encryption - Crypto 101 | Medium | Aug 2026 | Fundamentals of encryption/cryptography — genuinely enjoyed this one |
| MS Sentinel: Introduction | Easy | Aug 2026 | What Microsoft Sentinel is and how it fits into a SOC analyst's day-to-day work |
| Introductory Networking | Easy | Aug 2026 | Networking theory and basic tools — more tedious than hard, needed close attention to detail |

---

[← Back to summary](./README.md)

---

## 🔧 Infrastructure troubleshooting: GPU passthrough with a physical display

Set up a dedicated Kali Linux VM on Proxmox VE with a physical monitor, keyboard, and mouse connected directly (via GPU passthrough), instead of relying on Proxmox's web console — to fix the sluggish performance of running Burp Suite and other heavier tools through the browser-based console.

**What went wrong, in order, and how each was diagnosed:**

1. **No video output at all** — traced through `dmesg` to `vfio-pci 0000:01:00.0: Invalid PCI ROM header signature: expecting 0xaa55, got 0xffff`. The card's ROM couldn't be read live from `/sys/bus/pci/devices/.../rom` (I/O error even with the VM stopped), so I downloaded the correct vendor-specific VBIOS (MSI GTX 1080 Gaming X) from a public VBIOS archive and pointed the VM at it via `romfile=` in the PCI device config.
2. **Keyboard/mouse not responding** on the physical display — the GPU being passed through doesn't automatically bring USB with it. Added the keyboard and mouse as separate USB devices (by vendor/device ID) in the VM hardware config.
3. **Still no display after the ROM fix** — turned out the ISO was still mounted and the boot order had the disk before the CD-ROM, so the VM kept trying (and failing) to reboot into an incomplete install instead of finishing setup. Removed the mounted ISO, fixed the boot order, and set the virtual Display device to `none` (letting the passthrough GPU be the only display output instead of competing with Proxmox's virtual VGA).
4. **A later mistake to avoid repeating:** manually installing `nvidia-driver` inside Kali after passthrough was already working broke the install entirely (no video, no VNC fallback) — had to rebuild the VM from scratch. Passthrough already provides working video output without installing GPU drivers manually inside the guest.

**Result:** Kali now runs through the passed-through GPU with a real monitor/keyboard/mouse, noticeably faster than the web console for anything GUI-heavy like Burp Suite.
