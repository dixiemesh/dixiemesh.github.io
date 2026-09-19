---
title: How To
layout: default
permalink: /how-to/
---

# How To & Tips

Practical tips for getting the most out of Dixie Mesh once you're on the air.
This page grows over time — if there's something you'd like to see covered,
[let us know](mailto:contact@dixiemesh.com).

## Hashtag channels

Hashtag channels are shared public channels named with a hashtag (like
`#weather`). They're how the community organizes conversation by topic. A
channel's key is derived from its name, so **anyone who adds a channel with the
same name is in the same channel** — no invites or key-swapping needed. Like the
default public channel, treat these as open: assume anyone on the mesh can read
them.

**To join one in the MeshCore app:**

1. Open the **three-dot menu** and tap **Add Channel**.
2. Choose **Join a Hashtag Channel**.
3. Enter the channel name including the `#` (for example, `#weather`).

That's it — you'll start seeing traffic on that channel and can post to it.

### Dixie Mesh channels

These are the common hashtag channels on Dixie Mesh. This isn't an exhaustive
list, and you're welcome to spin up your own for a topic or area.

| Channel | What it's for |
| --- | --- |
| **`#alerts`** | Community-wide announcements and heads-up notices: mesh news, planned outages, events, and other things worth broadcasting. Not for emergencies — see `#emergency`. |
| **`#dixiemesh`** | Local Washington County area chat. Use it for day-to-day conversation, questions, events, and coordination with other people on the mesh in Washington County. |
| **`#emergency`** | Real-time emergency and life-safety communications **only**. Keep this channel clear so urgent traffic gets through; take non-urgent chatter elsewhere. |
| **`#hamradio`** | Amateur radio talk: licensing, nets, gear, repeaters, and general ham discussion. |
| **`#repeater-ops`** | For folks running mesh infrastructure — coordinate repeater placement and config, announce maintenance or outages, and compare notes on keeping nodes healthy. |
| **`#test`** | The "can anyone hear me?" channel. Send test messages here to check your signal and confirm a new node is getting out. See [Verifying your node](/getting-started/#verifying-your-node-works). |
| **`#weather`** | Local weather updates and conditions around Southern Utah. |
| **`#weekly-net`** | Check-ins for the Wednesday night weekly net. See [net.dixiemesh.com](https://net.dixiemesh.com) for details. |

> **Channel etiquette:** post on the channel that fits your topic, keep
> `#emergency` reserved for real emergencies, and remember everything on a public
> channel is readable by anyone on the mesh. For anything sensitive, use a direct
> message or a private channel.

## Configuring Repeaters

Recommended advert, loop detection, and delay settings for repeaters on the
Intermountain West mesh — these keep airtime efficient and cut down on
duplicate/looped traffic as the mesh grows. Full details:
[Advert, Loop Detection, and Delay Settings (PDF)](/assets/docs/advert-loop-detection-delays.pdf).

<video controls preload="metadata" style="max-width: 100%;">
  <source src="/assets/video/repeater-advanced-settings.mp4" type="video/mp4">
  Your browser doesn't support embedded video.
  <a href="/assets/video/repeater-advanced-settings.mp4">Download the video</a>.
</video>

*Video walkthrough: setting these values on a repeater from the MeshCore app.*

### Advert interval

Set your advert interval to **47 hours**. That's often enough to stay
discoverable, but not so often — or so regular — that adverts pile up at the
same time every day.

### Loop detection

On any repeater that supports it, run:

```
set loop.detect moderate
```

With `loop.detect` set to `moderate`:

- **1-byte path** — rejects the packet if its own ID appears 2 times.
- **2-byte & 3-byte path** — rejects the packet if its own ID appears 1 time.

### Delays

- **`txdelay`** — the random wait before retransmitting flood packets. A
  higher value gives nearby nodes more time to transmit first, reducing
  collisions.
- **`direct.txdelay`** — the same idea for direct packets, usually set lower
  for faster delivery.
- **`rxdelay`** — prioritizes stronger copies of a packet and can discard
  weaker duplicates.

These can be set via CLI or when flashing a repeater. Pick the row that
matches your neighbor count:

| Neighbors | `txdelay` | `direct.txdelay` | `rxdelay` |
| --- | --- | --- | --- |
| 20+ | 2 | 2 | 3 |
| 10–19 | 1.5 | 1 | 3 |
| 5–9 | 0.8 | 0.4 | 3 |
| 1–4 | 0.3 | 0.1 | 3 |
| Mobile repeaters (vehicle nodes) | 2 | 2 | 3 |

## Presentations

These presentations are available to view and share:

- [Texting Without Towers: Off-Grid Messaging with MeshCore](/presentations/texting-without-towers/): An introduction to LoRa, MeshCore, and the Dixie Mesh network.

## Frequently asked questions

**Do I need a license to use Dixie Mesh?**
No. LoRa here operates on the license-free 915 MHz ISM band, so anyone can join.
(If you *are* a licensed ham, `#hamradio` is the place for licensed-radio
topics.)

**Are my messages private?**
Direct messages are end-to-end encrypted. Channels — including hashtag channels
and the default public channel — are encrypted with a shared key, but anyone who
has that key (which, for public channels, is everyone) can read them. Use a
direct message or a private channel for anything sensitive.

**People can't hear me / I can't hear anyone. What do I do?**
Start with the [Troubleshooting guide](/troubleshooting/). Most issues come down
to antenna placement and line of sight — getting your antenna higher and outdoors
fixes the majority of them.

**How do I know if my signal is actually getting out?**
Send a message on `#test` and watch for it being repeated, or run the
[Health Check](/troubleshooting/#check-whos-hearing-you-with-the-health-check) to
see exactly which nodes hear you.

**How can I help the network grow?**
Put up a repeater. A well-placed, always-on node — especially somewhere high with
a clear view of the valley — extends range for everyone. See
[Ways to participate](/getting-started/#ways-to-participate).
