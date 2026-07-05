---
title: Troubleshooting
layout: default
permalink: /troubleshooting/
---

# Troubleshooting Dixie Mesh

Before you dig into settings or suspect your hardware, start here:

> **Most problems are not hardware or configuration problems — they're antenna
> placement and RF-environment problems.** LoRa needs a clear path. In Southern
> Utah's terrain, a ridgeline, a mesa, or even a building between you and the
> nearest repeater can be the difference between solid coverage and silence.

A huge help when diagnosing anything is the **[Dixie Mesh Analyzer](https://live.dixiemesh.com/#/home)**.
You can:

- **Find your node** — type your node name into the
  [Analyzer home](https://live.dixiemesh.com/#/home) to see if (and how) the
  network is hearing you.
- **Inspect packets** — watch live traffic on the
  [packets view](https://live.dixiemesh.com/#/packets?timeWindow=360) to see what's
  actually making it onto the mesh.
- **Check the live map** — see active nodes and coverage on the
  [live map](https://live.dixiemesh.com/#/live).

Make sure you're running **MeshCore** firmware, not Meshtastic — they are not
compatible and won't talk to each other.

## Check who's hearing you with the Health Check

The **[Dixie Mesh Health Check](https://healthcheck.dixiemesh.com)** answers the
single most useful question directly: *is my signal actually being heard out on
the mesh?* Several **observers** — nodes scattered across the network that report
what they hear — listen for a test message from you and tell you exactly who
picked it up. It's the fastest way to gauge how effective your signal really is.

How it works:

1. Open the [Health Check](https://healthcheck.dixiemesh.com). It generates a
   short **test code** for you.
2. Send that code as a message on the **`#dixie-hc`** channel — the same idea as
   the [`#test` channel check](/getting-started/#verifying-your-node-works) from
   setup, on the channel the observers watch.
3. The tool watches for observers reporting your packet and scores your
   **coverage** — how many of them heard you.

For every observer that received your message you'll see **RSSI and SNR** (how
strong and clean your signal was), the **path** it took and which repeaters
relayed it, timing details, and a **map** of who heard you and roughly how far
your packet traveled. That makes it easy to tell a solid, well-heard signal from
one that's barely scraping in — and to see which directions your coverage is
strong or weak.

## "I can hear others, but they can't hear me"

This is the most common issue, and it almost always means your *transmit* path
isn't reaching a repeater.

1. **Run the [Health Check](https://healthcheck.dixiemesh.com).** Send a test
   code and see whether any observers hear you. No receipts is a clear sign your
   TX path isn't reaching the mesh; weak RSSI/SNR points to a marginal one.
2. **Look yourself up in the Analyzer.** Search your node name on the
   [Analyzer](https://live.dixiemesh.com/#/home). If the network isn't seeing your
   transmissions, that points squarely at your TX path.
3. **Watch for "repeats heard."** When you send a message, the app indicates if a
   repeater relayed it. No repeat = your signal isn't getting out.
4. **Check the path on messages you receive.** Note which repeater they came
   through, and test whether you can reach that repeater directly.
5. **Review geography.** Use the [live map](https://live.dixiemesh.com/#/live) or
   the in-app line-of-sight tools to see what's between you and the nearest
   repeater.
6. If none of that helps, the likely culprits are **antenna placement, an indoor
   setup, or hardware limits.** Get the antenna higher and outdoors.

## "It used to work"

Usually a configuration drift or a change at a repeater — less often hardware.

1. **Trace your local repeater** to confirm the link is still there.
2. **Test a known nearby repeater**, and watch for your message being repeated.
3. **Check the Analyzer** to confirm your packets are still landing on the mesh.
4. **Review recent changes** — did you adjust settings, swap an antenna, or update
   firmware? Reapply the [standard US preset](/getting-started/#dixie-mesh-conventions)
   and check your antenna connection.

## "I'm not hearing anything at all"

1. Confirm you're on **MeshCore**, on the correct **frequency/preset**
   (910.525 MHz, SF7, BW 62.5, CR5).
2. Treat it as a link problem: check the
   [live map](https://live.dixiemesh.com/#/live) to see whether any repeater is
   even within reach of your location.
3. Get outdoors and elevate the antenna, then try again.

## "Messages are inconsistent or random"

This is the classic signature of a **weak or marginal signal** — you're at the
edge of range.

- Raise the antenna and remove obstructions.
- Aim for a **stable path to one repeater** rather than barely reaching a distant
  one.
- Use the [packets view](https://live.dixiemesh.com/#/packets?timeWindow=360) to
  see how reliably your traffic is landing.

## "I only connect sometimes"

Same root cause as inconsistent messages: an edge-of-range link that shifts with
weather, foliage, and who's transmitting. **Prioritize a stable connection over
maximum distance.**

## "I see activity, but nothing useful"

You may be hearing distant nodes without having a usable *path* to them. Seeing
traffic isn't the same as having a working two-way link.

- Focus on reliably reaching **one specific nearby repeater**.
- Confirm in the [Analyzer](https://live.dixiemesh.com/#/home) that your own
  packets — not just everyone else's — are being relayed.

## Common gotchas

- **Line of sight beats power.** Height and a clear path matter more than turning
  TX power up.
- **Indoors badly underperforms outdoors.** A window helps; outside helps more.
- **Below the roofline, the horizon is blocked.** Get above it where you can.
- **Reception can be one-directional** — hearing a node doesn't guarantee it
  hears you.
- **"It worked once" ≠ stable.** A single successful message isn't proof of a
  reliable link.

## Getting help

When you ask the community for help, share:

- Your **hardware** (board and antenna).
- Your **general location** (and antenna height / indoor vs. outdoor).
- **Signal metrics** — RSSI / SNR if you have them.
- What you've **already tried**.

Change one variable at a time, test temporary setups, and remember: when in
doubt, **get the antenna higher and outdoors**.
