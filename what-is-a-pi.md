# What Is a Raspberry Pi?

A Raspberry Pi is a **single-board computer (SBC)**: a whole
computer — processor, memory, USB, networking, video output —
on one circuit board, running real Linux. Plug in power and a
microSD card and it boots like any PC, just smaller, cheaper,
and sipping power instead of gulping it.

The original 2012 pitch was "a $35 computer for teaching kids
to program." A decade-plus later, the family spans $4
microcontrollers to $150 desktop-class boards, with millions
of projects and the best hobbyist documentation of any
hardware platform.

## The one distinction that matters: Pi vs Pico

The lineup splits into two fundamentally different kinds of
device, and mixing them up is the #1 beginner mistake:

**Raspberry Pi (5, 4, Zero 2 W...)** — a *computer*. Runs
Linux (Raspberry Pi OS). Has gigabytes of RAM, USB, HDMI,
Wi-Fi. You SSH into it, install packages, run Python, Docker,
servers. If it sounds like a tiny PC, that's because it is.

**Raspberry Pi Pico (Pico, Pico W, Pico 2)** — a
*microcontroller*. No Linux, no HDMI, kilobytes of RAM. Runs
one program, written in MicroPython or C++, talking directly
to pins and sensors. It's closer to an Arduino than to a Pi 5
— see the [Arduino guide](https://paulsullivan33-dev.github.io/arduino-for-mere-mortals/)
for that mindset.

| | Pi (SBC) | Pico (MCU) |
|---|---|---|
| Runs | Full Linux | One program, no OS |
| RAM | 512MB–16GB | 264–520KB |
| Good at | servers, desktop, AI tinkering | sensors, LEDs, real-time control |
| Power | watts | milliwatts |
| Price | ~$15–150 | ~$4–7 |

**Rule of thumb:** if the job involves Linux, networking
services, or running *programs*, you want a Pi. If it
involves reading a sensor every 100ms on battery power, you
want a Pico.

## What you actually get

Every full-size Pi (5, 4) gives you:

- **40 GPIO pins** — the row of pins along the edge, for
  buttons, sensors, LEDs, HATs
- **USB ports** — 2× USB 3.0 + 2× USB 2.0 on Pi 5/4
- **Networking** — Gigabit Ethernet + Wi-Fi + Bluetooth
- **Video** — dual micro-HDMI (4K on Pi 5/4)
- **Storage** — microSD card slot (Pi 5 adds PCIe for NVMe)

What you *don't* get in the box: a power supply, a case, a
microSD card, or cables. Budget for those — a "$60 board" is
really a ~$100 project once kitted out. (More on true costs in
[The Lineup](the-lineup.md).)

## Why people keep buying them

- **The software just works.** Raspberry Pi OS is Debian with
  the rough edges sanded off; `apt install` anything.
- **The community is enormous.** Whatever you want to build,
  someone documented it.
- **GPIO on a real computer.** Arduino gives you pins without
  Linux; a PC gives you Linux without pins. The Pi gives you
  both at once.
- **Honest pricing.** No subscriptions, no cloud required, no
  account to run your own hardware.
