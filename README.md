# RTSPoofing — Write-Up

**Trust Me, I'm a Camera** — a technical paper on a man-in-the-middle and RTP replay attack against RTSP video-surveillance streams.

By Martín López Aranburu · Presented at the Barcelona Cybersecurity Congress, November 2026.

## About

This repository contains the write-up ([`rtspoofing-paper.pdf`](rtspoofing-paper.pdf)) for **RTSPoofing**, a working man-in-the-middle tool against the RTSP/RTP pipeline used by most consumer and small-business IP cameras and network video recorders (NVRs).

By combining ARP-based positioning, a byte-transparent RTSP relay, and RTP-level frame substitution, an on-path attacker can quietly replace a live camera feed with pre-recorded footage while the NVR keeps logging a stream that looks entirely valid — sequence numbers, timestamps, sender identity, and even the RTCP wall-clock all line up.

## Contents of the paper

- **Background** — RTSP, RTP/RTCP, and the three unauthenticated header fields the attack relies on
- **Threat model and architecture** — a three-stage attack running through an async Rust/Tokio proxy
  - Phase I — network-layer positioning (ARP spoofing)
  - Phase II — transparent interception (byte-transparent RTSP relay + live parameter detection)
  - Phase III — media substitution (continuity-preserving, paced RTP frame injection)
- **Extending to UDP transport**
- **Empirical scope**, detection, countermeasures, and limitations
- **Ethics and responsible disclosure**

## Scope and ethics

> All testing described in the paper was performed in isolated lab environments or under explicit written authorization.

This material is provided for **educational and authorized-testing use only**. Do not use these techniques against systems you do not own or have explicit written permission to test.

## License / contact

Author: Martín López Aranburu — [LinkedIn](https://www.linkedin.com/in/martín-lópez-aranburu)
