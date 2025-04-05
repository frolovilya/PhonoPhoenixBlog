---
layout: post
title:  "Technics Needle Highlight LED"
excerpt: Replacing bulb with a warm white LED
date:   2025-04-04
categories: blog
author: Ilia Frolov
tags: Technics SL1200 SL1600 SL1700 SL1800 Repair Video
---

Replacing the original bulb with an LED is a popular modification for Technics turntables. The original bulbs burn out quite often, and the replacement part can be expensive, while the LED option is significantly cheaper (günstiger!), brighter, and will last for the rest of the turntable's life. Here’s my video showing the full modification process:

VIDEO

# Finding The Right Resistor

The Technics SL1210 supplies around 21V DC to the needle lamp, which is too much for many LEDs. For example, the warm white LED I use is designed for a 3.6V forward voltage and draws around 18mA of current.

An elementary calculation for the resistor to drop another 17.4V:

```
I = 0.018
U = 17.4
R = U / I = 17.4 / 0.018 ~= 967 Ohm
```

And the right wattage:

```
P = UI = 17.4 * 0.018 ~= 0.32 W
```

I've seen a guide with adding an extra voltage regulator, but based on the calculations a single __1kOhm 0.5W__ resistor should work just fine in this case.

It’s important to note that ohms and watts are not the only properties to consider. Even with a 0.32W load, the resistor might get very hot. Some resistor datasheets provide temperature rise plots. Below is an example of the temperature characteristics of a good-quality resistor, showing around 40°C for a 0.4W load:

<div class="blogPostImage">
<img src="/assets/posts/technics-needle-highlight-led/TemperatureRise.png" alt="Rise of surface temperature"/>
<div class="blogPostImageTitle">Rise of surface temperature</div>
</div>

I did a comparison of 1kOhm resistors of different types and price-ranges out of interest and got the following table:

| Part Number        | Type | Price, € | Temperature, °C |
| --- | --- | --- | --- |
| MBE04140C1001FC100 | Thin film resistor, 1 W, 1% | 0.21 | 45 |
| PO593-05T1K | Metal oxide film resistor, 2 W, 5%  | 0.18 | 43 |
| ERG12SJ102 | Metal oxide film resistor, 0.5 W, 5% | 0.14 | 53 |
| 201711P004 | Metal film resistor, 0.5 W, 1% | 0.04 | 73 |

<div class="blogPostImage">
<img src="/assets/posts/technics-needle-highlight-led/SurfaceTemperatureTest.jpg" alt="Measuring 52°C of ERG12SJ102 with a multimeter"/>
<div class="blogPostImageTitle">Measuring 52°C of ERG12SJ102 with a multimeter</div>
</div>

So that the cheap 201711P004, sold as a set of 400 resistors, got the worst temperature results. PO593-05T1K was the best, but noticable larger in size than MBE04140C1001FC100, so that I chose the later one for my projects.