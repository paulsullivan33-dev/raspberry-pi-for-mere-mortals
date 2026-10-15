# Glossary

**Compute Module (CM4/CM5)** — a Pi without ports, on a
small board meant to be built into custom products. For
manufacturing, not hobbyists.

**GPIO** — General-Purpose Input/Output: the 40-pin header
for connecting buttons, sensors, LEDs, and HATs. The Pi's
superpower over a regular PC.

**HAT** — Hardware Attached on Top: an expansion board that
plugs into the GPIO header (NVMe HATs, sensor HATs, DAC
HATs...). The Pi 5's PCIe HATs are the current hot zone.

**headless** — running without monitor or keyboard,
administered over SSH. How nearly every Pi server runs.

**microcontroller (MCU)** — a chip that runs one program
directly on hardware: no OS, kilobytes of RAM, milliwatts
of power. The Pico, not the Pi.

**Raspberry Pi Imager** — the official SD-card flashing tool
(Windows/Mac/Linux). Handles OS selection, SSH enablement,
Wi-Fi, and user setup before first boot.

**Raspberry Pi OS** — the official OS: Debian Linux tuned
for Pi hardware. Comes in full (desktop), Lite (no desktop),
and 64-bit variants.

**raspi-config** — the Pi's text-menu configuration tool
(`sudo raspi-config`): hostname, SSH, GPU memory, boot
order, localization.

**single-board computer (SBC)** — a complete computer on
one board: CPU, RAM, USB, networking. The Pi 5/4/Zero are
SBCs; the Pico is not.

**throttling** — the Pi slowing itself down to avoid
overheating (at 80°C) or undervoltage. Check history with
`vcgencmd get_throttled`.

**undervoltage** — the power supply sagging below what the
Pi needs, causing random crashes. The lightning-bolt icon,
or a nonzero `vcgencmd get_throttled`.
