# Pi OS Essentials

Raspberry Pi OS is Debian with Pi-specific tuning. If you
know Debian/Ubuntu, you know 95% of it. This chapter covers
the Pi-specific 5% and the first-hour setup.

## First boot checklist

```bash
sudo apt update && sudo apt full-upgrade -y
```

Then reboot if the kernel updated (`uname -r` before and
after tells you). After that:

```bash
sudo raspi-config
```

The settings worth touching:

- **System → Hostname** — if you didn't set it in Imager
- **Interface Options → SSH** — confirm it's on (headless
  depends on it)
- **Performance → GPU Memory** — on a headless server, drop
  this to **16MB**. The default reserves 76MB+ for a desktop
  you'll never see; that's RAM back for your services
- **Localisation** — timezone and Wi-Fi country (the wrong
  Wi-Fi country can disable 5GHz channels)

## The 64-bit check (again, because it matters)

```bash
uname -m
```

```
aarch64
```

And confirm you're actually *using* the RAM you paid for:

```bash
free -h
```

```
               total        used        free      shared  buff/cache   available
Mem:           3.7Gi       ...
```

A "4GB" Pi shows ~3.7GiB (some goes to the GPU/CPU
reservation). If you see ~1GB on a 4GB board, something's
wrong — usually the GPU memory split set absurdly high.

## Storage: treat the SD card as fragile

SD cards wear out and corrupt on power loss. Two habits:

1. **Back up the card** before big changes:
   ```bash
   # from your regular computer, with the card inserted:
   sudo dd if=/dev/sdX of=pi-backup.img bs=4M status=progress
   ```
   (Replace `/dev/sdX` with the card's device — `lsblk` to
   find it. Getting this wrong overwrites the wrong disk.)
2. **For anything you care about, boot from better storage:**
   Pi 5 → NVMe via the PCIe HAT; Pi 4 → USB 3.0 SSD. Both
   are an order of magnitude more reliable than SD.

## Keep it updated, automatically

```bash
sudo apt install unattended-upgrades
```

It installs security updates on its own. Check occasionally
that it's actually running (`systemctl status
unattended-upgrades`) — "set and forget" only works if the
"set" part happened.

## What Raspberry Pi OS is not

It's not a rolling release and not minimal — it's stable
Debian with a friendly face. For containers and servers that
means: slightly older packages, rock-solid behavior. If you
need the newest everything, that's what the
[Docker guide](https://paulsullivan33-dev.github.io/docker-for-mere-mortals/)
is for — run new software in containers on a boring,
stable host.
