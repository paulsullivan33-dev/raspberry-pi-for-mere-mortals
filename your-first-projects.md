# Your First Projects

One project per Pi class — each teaches a real skill, each
finishes in an evening.

## Pi 4/5: Pi-hole (network-wide ad blocking)

The classic first server project, and genuinely useful
forever after.

```bash
curl -sSL https://install.pi-hole.net | bash
```

(The installer is interactive and walks you through it.)
Then point your router's DNS at the Pi's IP. Every device on
your network stops seeing most ads, and the Pi-hole dashboard
shows you *which* devices phone home the most — an education
in itself.

**Skill learned:** DNS, DHCP integration, running a real
network service.

## Zero 2 W: temperature logger

A $15 computer, a $5 sensor, and the smallest useful IoT
device:

```bash
sudo apt install python3-pip
pip3 install adafruit-circuitpython-dht --break-system-packages
```

(Use `--break-system-packages` here deliberately — it's a
single-purpose Pi, not a shared Python environment. On a
Pi you *develop* on, prefer a venv; see the
[Python guide](https://paulsullivan33-dev.github.io/python-for-mere-mortals/).)

Wire a DHT22 to the GPIO pins, log readings to a file every
minute via cron, and you've built a thing that *senses the
physical world* — the whole point of the GPIO header.

**Skill learned:** GPIO, cron, the sensor-to-data pipeline.

## Pi 5: NVMe boot (kill the SD card)

The project that makes every later project better:

1. Attach an M.2 HAT+ and NVMe SSD
2. Flash Raspberry Pi OS directly to the NVMe (Imager
   supports it)
3. Set the boot order: `sudo raspi-config` → Advanced →
   Boot Order → NVMe first

**Check:**

```bash
lsblk -d -o NAME,TRAN | grep nvme
```

```
nvme0n1  nvme
```

and confirm root is on it: `findmnt -n -o SOURCE /` shows
`/dev/nvme0n1p2`.

**Skill learned:** bootloaders, storage hierarchy, why
"disk" stopped meaning one thing.

## Pico 2 W: the blink-to-Wi-Fi ladder

On a microcontroller, the ladder is: blink an LED (GPIO
works) → read a button (input works) → connect to Wi-Fi
(network works) → publish a sensor reading over MQTT (it's
a real IoT device). Each rung is ten lines of MicroPython.
The [Arduino guide](https://paulsullivan33-dev.github.io/arduino-for-mere-mortals/)
covers this mindset in depth — the Pico is just the Pi
family's entry in that world.

## Pi 4: the fleet monitor

Dedicate the whole box to watching your other machines: a
cron job that pings each host, checks SSH, and messages you
when something's down. One computer, one job, boring and
reliable — the Pi philosophy at its best. (A second Pi as
monitor-for-the-monitor is not paranoia; it's the logical
conclusion.)
