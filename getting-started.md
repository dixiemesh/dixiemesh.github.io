---
title: Getting Started
layout: default
permalink: /getting-started/
---

# Getting Started with Dixie Mesh

Dixie Mesh is a community-run [LoRa](https://en.wikipedia.org/wiki/LoRa) mesh
network for Southern Utah, built on [MeshCore](https://meshcore.io). This guide
walks you from an unboxed radio to a working node on the mesh in about
**10–20 minutes**.

If you've never touched a LoRa radio before, don't worry — no soldering, no
ham license, and no command line required. If you get stuck, jump to
[Still unsure?](#still-unsure) at the bottom.

## Ways to participate

There are three roles a node can play. You can change roles later, so pick
whatever fits how you'll use it today.

- **Companion** — a portable, battery-powered radio you pair with the MeshCore
  phone app over Bluetooth. This is how you actually send and read messages.
  Most people start here.
- **Repeater** — an always-on node, usually mounted up high, that relays traffic
  for everyone else. Repeaters are the backbone of the mesh; one in a good
  location dramatically extends range for the whole community.
- **Room Server** — an always-on node that hosts a persistent group chat (a
  "room") that members can read back through even if they were offline when a
  message was sent.

> **New here?** Set up a **Companion** first. Once you're comfortable, consider
> putting a **Repeater** somewhere with a clear view of the valley — that's the
> single most valuable thing you can do for Dixie Mesh.

## Encryption and visibility

A quick reality check before you start:

- **Direct messages** between two nodes are end-to-end encrypted.
- **Channels** (group chats, including the default public channel) are encrypted
  with a *shared key*. Anyone who has the key can read the channel — and the
  public channel's key is, by design, public. Treat the public channel like an
  open repeater net: assume others can hear it.
- **Metadata** — who is talking and the rough shape of the network — is visible
  to anyone listening on the frequency, even when message contents are
  encrypted.

For anything sensitive, use direct messages or a private channel with a key you
share only with the people who need it.

## What you need to get started

- A supported **LoRa device** (see below) — this is your node.
- A **USB-C cable** that carries data (not a charge-only cable).
- A **computer with a modern browser** (Chrome or Edge work best — the web
  flasher uses Web Serial).
- A **smartphone** with the MeshCore app, if you're setting up a Companion.
- About **10–20 minutes**.

### Supported hardware

You have two paths: **buy a pre-built node** that's ready to use out of the box,
or **build your own** from a supported board.

**Pre-built / ready-to-use**

These are just two of the many options available for easy purchase:

- **[Seeed Studio Wio Tracker L1 Pro](https://www.seeedstudio.com/Wio-Tracker-L1-Pro-p-6454.html)**
  — a complete handheld with screen, GPS, and battery; great if you'd rather not
  assemble anything. Just confirm you get the **915 MHz (US)** version and flash
  MeshCore.
- **[Elecrow ThinkNode M1](https://www.elecrow.com/thinknode-m1-meshtastic-lora-signal-transceiver-powered-by-nrf52840-with-154-screen-support-gps.html)**
  — an nRF52840-based handheld with a 1.54" screen and GPS. Another solid
  ready-to-go option; pick the **915 MHz (US)** version and flash MeshCore.

**Build your own**

MeshCore runs on a range of inexpensive LoRa boards. For Southern Utah you want
a board for the **US 915 MHz** band. Popular, well-supported choices include:

- **Heltec V3 / Heltec V4** — built-in OLED screen, great starter board.
- **LilyGo T-Deck** — keyboard + screen, usable as a standalone messenger.
- **RAK WisBlock / RAK4631** — low power, good for solar repeaters.
- **Xiao / nRF52 + LoRa** boards — compact companion builds.

> Make sure any board you buy is the **915 MHz (US)** variant. An 868 MHz
> (Europe) board will not work on the Dixie Mesh frequency.

## Antennas and placement

The antenna matters more than almost anything else.

- Use a **915 MHz antenna** — the one that ships with the board is fine to start,
  but a better antenna is the cheapest real upgrade you can make.
- **Never power up a LoRa radio without an antenna attached** — transmitting
  with no antenna can damage the radio.
- **Height and line of sight win.** LoRa loves a clear view. A node in a window
  beats one in a drawer; a node on a hilltop or rooftop beats them all. Southern
  Utah's ridgelines and mesas are excellent repeater sites.
- Keep the antenna **vertical** and away from large metal objects.

## Flashing and initial setup

1. Plug your board into your computer with the USB-C data cable.
2. Open the **MeshCore Web Flasher**: [flasher.meshcore.io](https://flasher.meshcore.io)
3. Select your **board model** from the list.
4. Choose the firmware for the role you want:
   - **Companion (BLE)** for a phone-paired messenger.
   - **Repeater** for an always-on relay.
   - **Room Server** for a hosted group chat.
5. Click **Flash** and follow the browser's prompt to select the serial port.
   Wait for it to finish — don't unplug mid-flash.
6. For a **Companion**, install the MeshCore app
   ([Android](https://play.google.com/store/apps/details?id=com.liamcottle.meshcore)
   / [iOS](https://apps.apple.com/app/meshcore/id6742536298)), then pair with
   your radio over Bluetooth.

## Dixie Mesh conventions

So every node can hear every other node, we all use the **standard MeshCore
USA/Canada preset**. Set these exactly:

| Setting          | Value         |
| ---------------- | ------------- |
| Frequency        | 910.525 MHz   |
| Bandwidth        | 62.5 kHz      |
| Spreading Factor | 7             |
| Coding Rate      | 5             |

In the MeshCore app you can simply pick the **USA/Canada (Recommended)** preset
and it will fill these in for you.

### Public channel

The default public channel is named **`Public`** and uses MeshCore's standard
public key, so it works out of the box on every node:

```
8b3387e9c5cdea6ac9e5edbaa115cd72
```

### Naming your node

Pick a name that helps people find you on the map and tells repeaters from
companions at a glance.

- **Repeaters:** include the location and end the name with **`Repeater`** —
  e.g. `St George Ridge Repeater`, `Hurricane Repeater`. The trailing
  `Repeater` makes infrastructure nodes easy to spot in the node list.
- **Companions:** name it anything familiar to you — your name, callsign, or a
  nickname all work fine.

## Verifying your node works

1. **Say hello on the public channel.** Open the `Public` channel and send a
   message. If someone replies, you're on the mesh.
2. **Check who you can hear.** In the app, look at the contacts/nodes list — any
   nodes that appear are within reach (directly or via a repeater).
3. **Use the built-in tools.** From a repeater or companion you can run a
   **ping** or **trace** to a known node to confirm the path and see how many
   hops away it is.

> **Quick "is my signal getting out?" test:** Join the **`#test`** channel,
> send a test message, and watch the app. It will show whether your message was
> repeated by a repeater — if you see it relayed, your signal is reaching the
> mesh. The `#test` channel is the polite place for this so you're not cluttering
> the public channel.

No responses? Don't panic — see below.

## Still unsure?

That's completely normal. A few things that fix most first-time issues:

- **No one hears you?** Check your frequency/preset matches the table above,
  confirm your antenna is attached, and try moving to a window or going outside.
- **Can't flash?** Use Chrome or Edge, try a different USB-C cable (many are
  charge-only), and make sure no other program (like the Arduino IDE) is holding
  the serial port.
- **Still stuck?** Reach out to the community — we'd rather help you get on the
  air than have you give up.

Welcome to Dixie Mesh. Get a node up, get it high, and help the network grow.

---

*Helpful references: the
[MeshCore documentation](https://docs.meshcore.io) and the
[MeshCore FAQ](https://docs.meshcore.io/faq/).*
