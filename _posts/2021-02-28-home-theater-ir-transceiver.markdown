---
layout: post
title:  "Home Theater IR Transceiver"
date:   2021-02-28 01:00:00 -0600
categories: projects electronics
---

I’ve been programming for a long time now, but I’ve always wanted to learn how to build my own electronics. I’ve wanted to automate a few of my home theater components that are only controllable via infrared remotes. Mainly my cheap-o 1080p projector I got off Amazon, and my very old, second hand Sony audio receiver. These are both powered by IR based remotes. I wondered, could I build something that could send these IR signals from a Raspberry PI? Then I could hook those IR commands to a web API and create voice commands. The gears really started turning.

After looking at some other DIY projects online, the design looked fairly simple and the opportunity arose to try my hand at building my first circuit schematic and design my first piece of circuitry.

I’ve worked with the Raspberry Pi since it was first introduced. And I think I have more than a dozen various models now floating around my house now. But I’ve always been a little intimidated by the GPIO. But no more. I ordered a few spools of wire, some breadboards, and a soldering station, and facing my fears head on.

I’ll continue to update as the project progresses. So far, I’ve drawn up a wiring diagram and currently awaiting some components I’ve ordered.

#### Wiring Diagram

![AWS Lambda](/assets/ir-remote.png)

#### Parts List
- 940nm IR LED
- 220 ohm Resistor
- 10k ohm Resistor
- NPN Transistor (PN2222)
- IR Receiver (TSOP38238)
- Half Size Breadboard
- Male to Female Jumpers
- 22 AWG single strand wire

>  <small>Note: Make sure you get an NPN (and not a PNP) transistor like I did with my first order</small>
