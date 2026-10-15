# The Lineup

Every current Raspberry Pi model, compared on the specs that
actually change what you can build. Prices are approximate
October 2026 USD — a DRAM shortage has raised Pi prices
several times since late 2025, so check before buying.

## The full-size boards

| | **Pi 5** | **Pi 4 Model B** |
|---|---|---|
| CPU | Quad Cortex-A76 @ 2.4 GHz | Quad Cortex-A72 @ 1.5 GHz |
| Real speed | ~2–3× a Pi 4 | The baseline |
| RAM | 1 / 2 / 4 / 8 / 16 GB | 1 / 2 / 4 / 8 GB |
| Storage | microSD **+ PCIe for NVMe** | microSD (or USB SSD) |
| Video | 2× micro HDMI, 4Kp60 | 2× micro HDMI, 4Kp60 |
| USB | 2× USB 3.0, 2× USB 2.0 | 2× USB 3.0, 2× USB 2.0 |
| Network | Gigabit Ethernet, Wi-Fi 5 | Gigabit Ethernet, Wi-Fi 5 |
| Extras | RTC, power button, fan header | 3.5mm audio jack |
| Power | 5V/5A recommended (25W) | 5V/3A (15W) |
| Idle power | ~2.7W | ~1.0W |
| Board price ≈ | $45 (1GB) – $145 (16GB) | $60 (4GB) / $85 (8GB) |

The Pi 5's headline features: the much faster A76 CPU, the
**PCIe slot** (NVMe SSDs via an M.2 HAT — no more SD-card
bottleneck), and a real-time clock. Its hidden costs: the
bigger power supply and active cooling for sustained loads.

The Pi 4's case: still fast enough for most server jobs,
sips power, runs cooler, and the huge existing accessory
ecosystem all fits it.

## The keyboard PCs

| | **Pi 500** | **Pi 500+** |
|---|---|---|
| What | Pi 5 inside a keyboard | Pi 5 inside a *nice* keyboard |
| RAM | 8 GB | 16 GB |
| Storage | microSD | 256 GB NVMe built in |
| Price ≈ | $90 | $200 |

A complete desktop with no separate board/case/keyboard to
buy. The 500+ (16GB + NVMe) is the only Pi I'd call a genuine
daily-driver desktop.

## The tiny ones

| | **Zero 2 W** | **Pico 2 W** |
|---|---|---|
| Kind | Computer (runs Linux) | Microcontroller (no OS) |
| CPU | Quad Cortex-A53 @ 1 GHz | Dual Cortex-M33 @ 150 MHz |
| RAM | 512 MB | 520 KB |
| Wi-Fi | Yes (Wi-Fi 4) | Yes (Wi-Fi 4) |
| Size | 65 × 30 mm | 51 × 21 mm |
| Power | ~1–2.5W | Milliwatts |
| Price ≈ | $15 | ~$7 |

The Zero 2 W is a *real Linux computer* the size of a stick
of gum — astonishing for $15. The Pico 2 W is for
microcontroller jobs (see [What Is a Pi?](what-is-a-pi.md)).

## Compute Modules (CM4 / CM5)

Bare boards without ports, meant to be soldered into custom
products. Unless you're manufacturing something, skip them —
every CM project starts with "first prototype it on a Pi 5."

## The true cost

The board price is never the project price. A realistic
minimum kit:

- Board + official power supply + case + decent microSD card
  + micro-HDMI cable ≈ **board price + $35–50**
- Pi 5 with NVMe: add an M.2 HAT+ (~$15–30) and the SSD

**The #1 beginner mistake** is powering a Pi 5 from a random
phone charger. Undervoltage causes random crashes that look
like software bugs. The official 5V/5A supply for the Pi 5
(5V/3A for the Pi 4) is the cheapest reliability upgrade
there is.
