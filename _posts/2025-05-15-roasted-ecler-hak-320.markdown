---
layout: post
title:  "Roasted Ecler"
excerpt: Repairing burned Ecler Hak 320 mixer
date:   2025-05-15
categories: blog
author: Ilia Frolov
tags: Ecler Hak Mixer
thumbnail: /assets/posts/roasted-ecler-hak-320/thumbnail.jpeg
---

Ecler still makes nice analog DJ mixers, which are kind of old-scool nowadays. I personally use NUO 2.0 in my setup. As pretty much all my stories begin, I've found a non-working vintage Ecler Hak 320 battle mixer in a good visual condition on Kleinanzeigen and decided to take a look what's inside.

In the description was stated that the mixer was working perfectly, but when the previous owner connected it to some new decks and speakers, a loud crack was heard and no sound since then. So looks like it should be an easy fix, isn't it?

<div class="blogPostImage">
<img src="/assets/posts/roasted-ecler-hak-320/ecler-hak-320.jpeg" />
<div class="blogPostImageTitle">Ecler HAK 320 Mixer</div>
</div>

So after powering it in and inspecting the verdict was the following - nothing works. Both channels, Line/Phono inputs, level indicators, headphones, faders - everything is dead. Let's look inside:

<div class="blogPostImage">
<img src="/assets/posts/roasted-ecler-hak-320/burned-connector.jpeg" />
<div class="blogPostImageTitle">Burned PCB</div>
</div>

Apparently I wasn't the first to be inside the mixer. Burned connector to the output PCB was disconnected and one of the TL074 opamps on the main board was replaced.

# Power Supply

Even though the reason seemed obvious, I decided to disconnect everything and check the power supply first. It's a classical one that should give two + and - 18V rails for opamps to work. Here's what it was supplying instead:

<div class="blogPostImage">
<img src="/assets/posts/roasted-ecler-hak-320/power-supply-plus-defekt.jpeg" />
<div class="blogPostImageTitle">+30V instead of +18V</div>
</div>

<div class="blogPostImage">
<img src="/assets/posts/roasted-ecler-hak-320/power-supply-minus-defekt.jpeg" />
<div class="blogPostImageTitle">0V instead of -18V</div>
</div>

It's using popular 7918 and 7818 voltage regulators, which both were defektive. That was the first fix in this repair project. But let's leave the power supply for a while and try to supply the boards with a bench power supply with a current limit. Otherwise the voltage regulators may die again.

# OpAmps

By doing so and powering the faders PCB with +/-18V supply, I felt the nice smell of a burning TL074.

<div class="blogPostImage">
<img src="/assets/posts/roasted-ecler-hak-320/burned-tl072.jpeg" />
<div class="blogPostImageTitle">Burned TL072 Operation Amplifier</div>
</div>

Quad TL074 and it's dual version TL072 are both very popular opamps used in sound devices and designed to work with +/-18V max. And apparently they didn't survive our 0/30V power supply.

_None of them._

What a nice SMD soldering exercise it was (trying to stay positive)! At first I've had a hope and tried to test every operation amplifier, but after five or so I've given up and decided, that desoldering and soldering all 19 ICs is faster.

<div class="blogPostImage">
<img src="/assets/posts/roasted-ecler-hak-320/testing-opamps.jpeg" />
<div class="blogPostImageTitle">Testing Operation Amplifiers with a Sine Wave Signal</div>
</div>

The test is quite easy by the way. I was using a self made [signal generator](https://github.com/frolovilya/stm32-signal-generator) out of STM32 development board to produce Line level sine signals and feed into the PCB. Then check either output or input of each OpAmp. In most cases either no voltage was on the output or virtual ground on the input wasn't zero.


# Voltage Controlled Amplifier

When you move your faders or a crossfader, the sound signal doesn't really come physically through them. Instead, a combination of those volume controls produce a voltage which is used by a special integrated circuit Voltage Controlled Amplifier.

<div class="blogPostImage">
<img src="/assets/posts/roasted-ecler-hak-320/vca-ic.jpeg" />
<div class="blogPostImageTitle">Voltage Controlled Amplifier</div>
</div>

So as the name hints, VCA is an amplifier that varies it's gain based on the control voltage and does it in an efficient and low-distortion way. Ecler Hak 320 uses SSM2164 from Analog Devices, which has four VCAs in a single IC with control voltage around 2.9V acorrding to the available service manual schematics.

In my case there was 18V on the IC control pins out of nowhere, which isn't normal. This suggests, that the IC was also burned. And the original SSM2164 is no longer in production, but there're a few alternatives.

* [THAT2162](https://thatcorp.com/that-alternatives-to-the-analog-devices-ssm2164/) even though it's advertised as a replacement for SSM2164 it has two amps instead of four, so it should work for your own designs but doesn't suit the repair case.
* [V2164D](https://www.coolaudio.com/features-page.php?product=V2164D), a direct clone from the Coolaudio company. Should work just well when swapped with SSM2164.
* [AS2164](https://www.alfarzpp.lv/eng/sc/AS2164.php) from a Latvia based company has similar characteristics to the original IC but with twice the input impendance of 10kΩ.
* [SSI2164](https://www.soundsemiconductor.com/) just as AS2164 has 10kΩ input impendance.

So I decided to try AS2164 as it was easier to find in the EU and it works well.

# Summary

Just to note what was done to bring the mixer back to life:

1. 7918 and 7818 voltage regulators replaced in the power supply
2. 19x TL074/TL072 opamps were replaced
3. Burned SSM2164 VCA was replaced with AS2164
4. Two 0Ω resistors leading to the ground were also burned and replaced
5. Burned PCB traces were repaired

Not sure it it's worth economically to repair such a mixer, but it was a challenge to me and great time spent with a hot air station :)