# Troubleshooting

Symptom → fix, in the order you'll hit them.

## Red light on, no green activity light

**Symptom:** power LED lit, ACT LED dark, nothing on screen.

**Cause:** the Pi can't read the SD card — bad flash, bad
card, or bad card slot contact.

**Fix:** reflash with Raspberry Pi Imager (verify the write
when it offers). Try a different card — preferably a
name-brand one. Reseat the card firmly; the click matters.

## Boots, then random crashes or reboots

**Symptom:** works for minutes or hours, then dies —
especially under load.

**Cause:** 9 times out of 10, the power supply. Phone
chargers and long thin cables can't hold 5V when the CPU
spikes.

**Fix:** the official supply for your model (5V/5A Pi 5,
5V/3A Pi 4). Check for the lightning-bolt (undervoltage)
icon, or `vcgencmd get_throttled` — a nonzero result means
it's happened since boot:
```bash
vcgencmd get_throttled
```
```
throttled=0x0
```
`0x0` is clean. Anything else, fix the power first and
suspect everything else second.

## Wi-Fi connects, then drops

**Symptom:** SSH works, then hangs; the Pi vanishes from the
network intermittently.

**Cause:** power management putting the Wi-Fi chip to sleep,
or (again) marginal power.

**Fix:** disable Wi-Fi power management:
```bash
sudo iw dev wlan0 set power_save off
```
Make it permanent via a udev rule or a systemd unit. If it
still drops, suspect power before drivers.

## "No space left" with space to spare

**Symptom:** `df -h` shows free space, but writes fail.

**Cause:** the filesystem was never expanded to fill the
card — or you're out of *inodes* (millions of tiny files).

**Fix:** `sudo raspi-config` → Advanced → Expand Filesystem
(Imager does this automatically now, but old cards bite).
For inodes: `df -i` — if it's 100% full, find the culprit
with `du`.

## Runs hot and throttles

**Symptom:** sluggish under sustained load; `vcgencmd
measure_temp` reads 80°C+.

**Cause:** the Pi 5 especially needs active cooling for
sustained work; the Pi 4 mostly doesn't, until you hammer it.

**Fix:** a fan (the official Pi 5 active cooler is $5 and
excellent) or at least a heatsink case. Check current temp
anytime:
```bash
vcgencmd measure_temp
```
```
temp=57.5'C
```
Design for your workload: a Pi-hole never breaks a sweat; a
Pi running Ollama will cook without airflow.

## SD card corrupted after power loss

**Symptom:** won't boot after an outage; filesystem errors.

**Cause:** SD cards hate sudden power loss mid-write.

**Fix:** short term, reflash from your backup (you have one —
see [Pi OS Essentials](pi-os-essentials.md)). Long term: a
UPS for the Pi, or boot from NVMe/USB-SSD which tolerates
abuse far better.

## SSH "connection refused" on a fresh flash

**Symptom:** ping works, SSH doesn't.

**Cause:** SSH wasn't enabled in the Imager settings.

**Fix:** power off, put the card back in your computer, and
create an empty file named `ssh` (no extension) in the boot
partition — or just reflash with the gear-icon SSH option
checked. The file method works without reflashing.

## apt is painfully slow

**Symptom:** updates crawl.

**Cause:** the default mirror is far away, or the SD card is
slow at random writes (all of them are, relatively).

**Fix:** `sudo raspi-config` → Localisation → pick a nearby
mirror. And accept that `apt upgrade` on SD storage takes a
while — it's the card, not your network.
