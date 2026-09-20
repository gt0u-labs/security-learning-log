# 🔧 Proxmox GPU passthrough — VFIO troubleshooting

**Goal:** run a Kali Linux VM on Proxmox VE with a monitor, keyboard and mouse
attached directly through GPU passthrough, instead of going through Proxmox's
web console — Burp Suite and other GUI-heavy tools were unusable over the
browser console.

**Hardware:** MSI GTX 1080 Gaming X · Proxmox VE host · Kali Linux guest

---

## What broke, and how each part was fixed

### 1. No video output at all

`dmesg` pointed straight at it:

```
vfio-pci 0000:01:00.0: Invalid PCI ROM header signature: expecting 0xaa55, got 0xffff
```

The card's ROM couldn't be read live from
`/sys/bus/pci/devices/0000:01:00.0/rom` — I/O error even with the VM fully
stopped.

**Fix:** obtained the correct vendor-specific VBIOS for this exact card from a
public VBIOS archive and pointed the VM at it with `romfile=` in the PCI device
configuration.

### 2. Keyboard and mouse dead on the physical display

GPU passthrough does not carry USB with it — that caught me out.

**Fix:** added the keyboard and mouse as individual USB devices, by
vendor/device ID, in the VM's hardware configuration.

### 3. Still no output after the ROM fix

The install ISO was still mounted and the disk sat ahead of the CD-ROM in the
boot order, so the VM kept trying to boot an unfinished install instead of
continuing setup.

**Fix:** unmounted the ISO, corrected the boot order, and set the virtual
Display to `none` so the passed-through GPU wasn't competing with Proxmox's own
virtual VGA output.

### 4. The mistake — installing `nvidia-driver` inside the guest

Passthrough was already working. I installed `nvidia-driver` inside Kali anyway,
and it broke the whole install: no video, no VNC fallback, full rebuild from
scratch.

**What I got wrong:** passthrough gives the guest working video without
installing GPU drivers inside it at all. The driver was solving a problem that
no longer existed, and it took out the only working display path in the process.

---

## Result

Kali now runs through the passed-through GPU with a real monitor, keyboard and
mouse — substantially faster than the web console for anything GUI-heavy.

---

## What this exercise covered

`VFIO` · `PCI/GPU passthrough` · `dmesg log diagnosis` · `VBIOS and romfile` ·
`USB device mapping` · `VM boot order` · `structured troubleshooting under an
unclear failure`
