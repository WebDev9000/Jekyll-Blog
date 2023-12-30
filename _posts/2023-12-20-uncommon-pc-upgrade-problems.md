---
layout: post
title: Uncommon PC Upgrade Problems
date: 2023-12-20 16:32 -0800
description: Development related tips and tricks from an experienced developer.
categories:
- pc
---

A recently, relatively simple, PC RAM upgrade came with some expected challenges, for which Googling produced no results matching the (eventually discovered) problems. I'm posting the issues here in the hopes that someone with a similar issue doing a search might find an answer.

### A squeak/beep is heard frequently but the computer otherwise boots after a long boot time

I noticed one of my drives was missing. It turns out that a cable came loose on an old HDD drive that came with the PC. The noise and the long boot time was the drive trying, and failing, to spin up properly and be read. Once I reseated the cables, the drive was silent again and the boot time was back to normal.

### The computer turns on and boots up normally, but there's no display on the monitors

This was seemingly due to my video card *also* somehow becoming just slightly unseated.  It's a heavy, two bracket card and turning the computer on its side to change the RAM seems to have jolted it slightly. I reseated it, tightened the bracket screws, and everything was fine.

### The computer's fans are extremely loud after the PC upgrade

This one stumped me for a few hours. I checked every temperature reading I could find and everything seemed normal. I eventually tracked the fan noise down to the PSU by ear. The result was, surprisingly enough, I had accidentally flipped a "Silent Mode" (sometimes called Eco Mode) switch directly next to the PSU power switch. After years of owning this PC, I didn't even know it was there. I changed it back to silent mode and everything was normal again.