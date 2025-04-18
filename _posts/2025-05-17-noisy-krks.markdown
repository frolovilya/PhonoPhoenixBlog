---
layout: post
title:  "Noisy KRKs"
excerpt: Fixing KRK RP5 G2 noise problem
date:   2025-04-17
categories: blog
author: Ilia Frolov
tags: KRK RP5G2 Monitors
thumbnail: /assets/posts/noisy-krks/thumbnail.jpeg
---

KRK monitors are a popular choise for DJ setups, especially for bass-heavy music lovers. They are relatively cheap and sound great. At the same time, when you look on Kleinanzeigen or eBay, there're many used KRKs on sale with various problems. I decided to buy a pair and check myself what it's like inside and if they're easy to fix. In my case there was an audible cracking noise mixed with a kind of white noise waves and hiss in one of the monitors when they're are on stand by and no audio signal coming in.

<div class="blogPostImage">
<img src="/assets/posts/noisy-krks/krk-rp5-g2.jpeg" alt="KRK RP5 G2"/>
<div class="blogPostImageTitle">KRK RP5 G2</div>
</div>

Here's how it looks from inside. Split power supply, pre-amp for the incoming signal and two amplifiers for low and high frequency speakers.

<div class="blogPostImage">
<img src="/assets/posts/noisy-krks/inside-the-monitor.jpeg" alt="KRKs from inside"/>
<div class="blogPostImageTitle">KRKs from inside</div>
</div>

In the RP5 G2 version there're two TDA2052 amps driving the high frequency tweeter and low frequency speaker both connected to a huge heat sink. The amps are powered separately so that there're two rectifiers sections and four capacitors, two for each speaker. Speaker wires are soldered right into the board and fixed with a black substance, which is present all over the PCB.

<div class="blogPostImage">
<img src="/assets/posts/noisy-krks/power-and-amp-board-old-caps.jpeg" alt="Power supply and amplifiers"/>
<div class="blogPostImageTitle">Power supply and amplifiers</div>
</div>

If you can hear the noise, then you can see it with your oscilloscope - that's the case where you really need one. The audible noise was coming from the high frequency tweeter. On the picture below the probe is touching pin 1 (output) of the TDA2052 responsible for the high frequency amplification. Every time I hear a cracking sound, it's also visualised on that pin. 

<div class="blogPostImage">
<img src="/assets/posts/noisy-krks/noise-with-the-osci.jpeg" alt="Observing noise with the oscilloscope"/>
<div class="blogPostImageTitle">Observing noise with the oscilloscope</div>
</div>

The noise was present even if the pre-amp board is disconnected, so I decided to check the power supply section first. DC coming after rectifier diodes must be smoothed by the capacitors to have a certain stable level. But the small ripple can still be expected. On the pictures below, I check the positive and negative voltages after the smoothing caps. Those are the two caps in the middle of the PCB.

<div class="blogPostImage">
<img src="/assets/posts/noisy-krks/capacitor-positive-good-smoothing-p2p.jpeg" alt="Positive voltage, 19V DC, 400mV peak-to-peak ripple"/>
<div class="blogPostImageTitle">Positive voltage, 19V DC, 400mV peak-to-peak ripple</div>
</div>

<div class="blogPostImage">
<img src="/assets/posts/noisy-krks/capacitor-negative-bad-smoothing-p2p.jpeg" alt="Observing noise with the oscilloscope"/>
<div class="blogPostImageTitle">Negative voltage, -19V DC, 1200mV peak-to-peak ripple</div>
</div>

So the -19V voltage has 1.2V voltage fluctiations after the smoothing capacitor, that doesn't look good in comparison to all other power supply 400mV differences on that board. Unsoldering and checking it with a tester shows degraded capacitance: 788uF actual vs 1000uF expected. 

<div class="blogPostImage">
<img src="/assets/posts/noisy-krks/bad-capacitor-check.jpeg" alt="Degraded capacitance"/>
<div class="blogPostImageTitle">Degraded capacitance</div>
</div>

Here's how check results look in comparison for the new 1000uF Panasonic capacitor:

<div class="blogPostImage">
<img src="/assets/posts/noisy-krks/new-capacitor-check.jpeg" alt="New capacitor check results"/>
<div class="blogPostImageTitle">New capacitor check results</div>
</div>

Both caps were changed to the new ones:

<div class="blogPostImage">
<img src="/assets/posts/noisy-krks/power-and-amp-board-new-caps.jpeg" alt="Soldered in new capacitors"/>
<div class="blogPostImageTitle">Soldered in new capacitors</div>
</div>

The peak-to-peak voltage fluctuation is now like for all other caps, around 400mV:

<div class="blogPostImage">
<img src="/assets/posts/noisy-krks/new-capacitor-negative-good-smoothing-p2p.jpeg" alt="Degraded capacitance"/>
<div class="blogPostImageTitle">Degraded capacitance</div>
</div>

This +/- 19V voltage directly drives the TDA2052 amplifier and all changes in the voltage level also seen and heard on the amplifier output. After fixing the caps, the hiss noise problem was solved, but still there were random quiet cracks on the tweeter.

All PCB were covered with a black substance to reduce vibrations impact, I believe, but with the time it become stiff and started to conduct electricity. You can find lots of similar problem reports and videos on YouTube. I decided to follow the advices and remove this black dirt completely. 

<div class="blogPostImage">
<img src="/assets/posts/noisy-krks/dirt-connectivity-1.jpeg" />
<div class="blogPostImageTitle">There's a small connectivity between two random points through this dirt, still can impact the noise</div>
</div>

After cleaning the dirt, one capacitor and one resistor were completely rusted and were replaced. So this dirt not only conductive, but also resulted to a rust problem all over the PCB.

<div class="blogPostImage">
<img src="/assets/posts/noisy-krks/dirty-pcb-1.jpeg" />
<div class="blogPostImageTitle">R103 resistor turned into a peace of rust under the dirt</div>
</div>

<div class="blogPostImage">
<img src="/assets/posts/noisy-krks/dirty-pcb-2.jpeg" />
<div class="blogPostImageTitle">CL107 capacitor legs rusted out</div>
</div>

The dirt was removed from all boards including pre-amp and what a surprise, the noise problem has completely gone. 

<div class="blogPostImage">
<img src="/assets/posts/noisy-krks/replaced-components.jpeg" />
<div class="blogPostImageTitle">Replaced components</div>
</div>

So seems like it's a mass problem with old KRKs. Even though they are great DJ monitors, you need to be carefull when buying used ones and be ready to service them.