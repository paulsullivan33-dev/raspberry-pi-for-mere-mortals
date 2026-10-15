# Headless Setup

"Headless" means no monitor, no keyboard — you set the Pi up
from your regular computer and talk to it over SSH from then
on. This is how nearly every Pi server runs, and it's easier
than the desktop route.

## What you need

- The Pi board, its official power supply, a case (optional
  but wise)
- A microSD card, **16GB minimum**, 32GB+ better — buy a
  name-brand card (Samsung, SanDisk); counterfeit cards are
  the #1 cause of "my Pi is flaky"
- A computer with an SD card slot (or a $10 USB reader)
- Your Wi-Fi name and password (or an Ethernet cable)

## Flash with Raspberry Pi Imager

[Raspberry Pi Imager](https://www.raspberrypi.com/software/)
is the official tool (Windows, Mac, Linux). It handles the
part everyone used to get wrong:

1. Choose your Pi model → choose **Raspberry Pi OS Lite
   (64-bit)** for a server (no desktop = less RAM, fewer
   updates; choose the full desktop image only if you'll plug
   in a monitor)
2. Choose your SD card
3. Click the **gear icon** (settings) *before* writing:
   - Set hostname (e.g. `pi-server`)
   - **Enable SSH** (this is the step people miss)
   - Set username and password (the default `pi`/`raspberry`
     no longer exists — you create the user here)
   - Configure Wi-Fi with your SSID/password (or skip if
     using Ethernet)
4. Write, eject, insert into the Pi, power on

The gear-icon settings are the whole trick: hostname, user,
SSH, and Wi-Fi are baked into the card before first boot.
Two minutes of clicking saves twenty minutes of fumbling.

## First connection

Give it a minute to boot, then from your computer:

```bash
ssh paul@pi-server.local
```

(`.local` uses mDNS — it usually just works on home
networks. If not, check your router's client list for the
Pi's IP address.)

**Check:**

```
Linux pi-server 6.6.XX ... aarch64 GNU/Linux
```

`aarch64` confirms you're on the 64-bit OS. (If it says
`armv7l`, you flashed the 32-bit image — reflash; 64-bit
matters for Docker and modern software.)

## Why 64-bit

The Pi 4 and 5 are 64-bit machines; the 32-bit OS exists for
the oldest boards. On 64-bit you get: Docker images that
actually exist, more than 3GB usable RAM, and software built
this decade. There is no reason to run 32-bit on a Pi 4 or 5
in 2026.

## Going further

- Give the Pi a **static DHCP lease** in your router so its
  IP never changes — future-you will thank present-you.
- For the essential first-hour configuration (`raspi-config`,
  updates, the must-change settings), see
  [Pi OS Essentials](pi-os-essentials.md).
