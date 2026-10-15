# Which Pi for What

The question isn't "which Pi is best" — it's "which Pi fits
*this job*." Here's the honest matching, including where a Pi
is the wrong tool entirely.

## The quick answers

| Job | Pick | Why |
|---|---|---|
| Home server / NAS | **Pi 5 4–8GB + NVMe HAT** | PCIe kills the SD bottleneck; ~400 MB/s over GigE |
| Budget home server | **Pi 4 4GB + USB SSD** | Half the price, fine for files and media at 1080p |
| Pi-hole / DNS / ad-blocking | **Zero 2 W** | Sips power, runs 24/7 for pennies |
| MQTT broker, tiny services | **Zero 2 W** | 512MB is plenty; ~0.4W idle |
| Small-AI / Ollama tinkering | **Pi 4 4–8GB** (or Pi 5 8GB) | See the honest notes below |
| Desktop replacement | **Pi 500+** (or Pi 5 8GB) | 16GB + NVMe is the only true daily-driver |
| Learning Linux | **Pi 4 2GB** or **Pi 5 2GB** | Cheapest full Linux computer |
| Sensors, buttons, LEDs | **Zero 2 W** (Linux) or **Pico 2 W** (real-time) | Linux+GPIO vs microcontroller — pick by the job |
| Camera projects | **Pi 5** | Dual camera ports, CPU to process frames |
| Retro gaming | **Pi 5** | The extra CPU headroom matters for emulation |
| K8s cluster learning | **3–4× Pi 4 or 5** | One per node; the classic use case |

## Small AI on a Pi: the honest version

This is where hype outruns reality, so here's what actually
happens, measured on a Pi 4 (4GB):

- **1–2B models work** (qwen3:1.7b, smollm2:1.7b) at a few
  tokens/second. Fine for experiments, duels, and learning —
  not for chat you enjoy.
- **Two models loaded at once OOM'd the 4GB board.** The fix
  was unloading between uses (`OLLAMA_KEEP_ALIVE=0`), at the
  cost of slow model swaps.
- **It runs hot.** Sustained inference pushed past 80°C and
  into thermal throttling — active cooling isn't optional for
  this workload.
- **The Pi 5 is meaningfully faster** (~2× on CPU-bound
  inference) but still a toy next to any used GPU box.

If your goal is *learning* how local LLMs work, a Pi 4 is a
great cheap lab. If your goal is *using* LLMs daily, put the
money toward the AI-PC build instead (see the
[Local AI guide](https://paulsullivan33-dev.github.io/local-ai-for-mere-mortals/)).

## When it's not a Pi job

- **Needs >8GB RAM or real speed** — a used mini-PC (Intel
  N100-class) often costs the same as a kitted-out Pi 5 and
  runs circles around it. The Pi wins on power draw and GPIO,
  not raw compute per dollar.
- **Battery-powered sensing** — a Pico sipping milliwatts
  beats any Linux Pi. Booting Linux to blink an LED is
  burning money.
- **Real-time control** — Linux isn't real-time. Motors,
  precise timing, bit-banging protocols: Pico.
- **Serious NAS with redundancy** — one USB disk on a Pi is
  a file server, not a NAS. For RAID and real data safety,
  that's the [ZFS conversation](https://paulsullivan33-dev.github.io/proxmox-for-mere-mortals/)
  on bigger hardware.

## The fleet angle

Pis make excellent *infrastructure* precisely because they're
cheap and boring: one Pi 4 as a fleet monitor watching your
other machines, a Zero 2 W as a serial console server, another
as the MQTT broker everything reports to. At $15–60 each,
dedicating a whole computer to one job stops feeling
extravagant — and a dead-simple box per job is easier to
reason about than one big server doing twelve things.
