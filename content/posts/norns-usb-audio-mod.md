+++
title = "Four months chasing noise on my Norns (and a USB audio mod)"
date = "2026-10-15T12:00:00+01:00"
tags = ["norns", "audio", "raspberry-pi", "supercollider", "diy"]
description = "Tracking down a weird noise on my DIY Norns DAC outputs, and the mod I ended up writing to send audio to a USB sound card instead."
showFullContent = false
readingTime = true
hideComments = false
draft = true
color = "" #color from the theme settings
+++

It started with a weird noise on the outputs of my DIY Norns (a Raspberry Pi with a DAC board on top). I'd heard the hum you get when something isn't grounded properly, and this was a bit different. Here's what it sounded like with the Norns running on a battery:

<audio controls preload="none" src="/img/posts/norns-usb-audio-mod/noisebattery.mp3"></audio>

And the spectrum of that recording:

![Spectrum of the noise, with the biggest peak around 374 Hz and a series of narrow spikes above it](/img/posts/norns-usb-audio-mod/spectrumanalyzenoise.png)

The strongest peak sits around 374 Hz, followed by a row of narrow spikes higher up, so it didn't look like mains hum to me.

I spent about four months on and off trying to figure out where it came from, and it turned out to be power.

## What was actually wrong

I had two full builds with a ![shieldXL](https://denki-oto.com/pages/shieldxl) , each a Pi 4B, but on different revisions of the Pi 4B. Both had the noise, and one was a lot worse than the other. The difference came down to the power management chip on the Pi. On a line power supply, the Pi with the MXL7704 chip had the noise and the one with the Dialog chip didn't. On a battery, both had it every time.

In the end I found two causes, and fixing only one of them didn't change much. That's mostly why it took so long.

The first was the header pins between the Pi and the DAC board. They had a thin layer of oxidation on them, invisible at a glance but enough to make the contact worse. Cleaning them with alcool helped a bit.

The second was my power supply. I was running the thing either from a battery or from a wall adapter that couldn't deliver enough current. The Pi pulls more when it's working hard, the voltage sags, and the DAC happily turns all of that into noise on the outputs.

The kernel was telling me this the whole time, and I didn't pay enough attention to it. `dmesg` kept showing lines like these:

```
Under-voltage detected!
Voltage normalised
```

What finally fixed it was using the Pi 4 with the Dialog chip (revision 1.5), which regulates the current properly, and feeding it with a decent line supply instead of a battery. After that the outputs got quiet.

## Skipping the DAC altogether

While I was in the middle of all this I wanted a way around the problem. So I wrote a Norns mod that sends the SuperCollider output straight to a USB sound card:

[github.com/Magicking/norns-usb-audio-mod](https://github.com/Magicking/norns-usb-audio-mod)

It started as a small shell script with my card name hardcoded in it. The mod is the cleaned-up version of that. It lists the USB sound cards that are plugged in, and you pick one (or several) from `SYSTEM > MODS > USB AUDIO` and connect it with K3. E3 changes the volume on a connected card. The list rescans every couple of seconds, so you can hotplug a card while the menu is open.

Under the hood it's pretty simple. For each card it starts an `alsa_out` process that bridges the ALSA device into JACK, then wires its playback ports to `crone:output_1` and `crone:output_2`. Disconnecting kills the `alsa_out` process and JACK cleans up the connections by itself.

## Install

### Maiden

Navigate to the Maiden interface, put `;install https://github.com/Magicking/norns-usb-audio-mod` in the console, restart, enable it in `system > mods`, and restart again.

### SSH

Copy the repo to `~/dust/code/usb-audio-mod` on your Norns, restart, enable it in `system > mods`, and restart again.

## Known issue

Sometimes there's a small bug in the sound. If you run into it and find the cause, issues and PRs are welcome, overall it's better than having a constant noisy sound over the analog output when using a battery!
