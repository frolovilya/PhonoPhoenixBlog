---
layout: post
title:  "Technics SL10 Blows 800mA Fuse"
excerpt: Investigating high current draw problem
date:   2025-03-15
categories: blog
author: Ilia Frolov
---

I recently bought an SL10 in seemingly mint condition from Kleinanzeigen. I received the package, opened it, and eagerly connected the turntable, excited to hear the original Technics MC cartridge. I turned it on and quickly went to grab a vinyl record. But when I returned, the turntable was dead—no buttons were working, and no lights were flashing. What a disappointment.


<div class="blogPostImage">
<img src="/assets/technics-sl10-blows-800ma-fuse/sl10.jpg" alt="Technics SL10"/>
<div class="blogPostImageTitle">Technics SL10 linear tracking turntable</div>
</div>


The deck was consistently blowing the F2 800mA fuse within approximately 3 seconds of powering on (it’s a Träge fuse). It wasn’t an immediate blow, like when something is shorted.


<div class="blogPostImage">
<img src="/assets/technics-sl10-blows-800ma-fuse/fuse.jpg" alt="F2 800mA Fuse"/>
<div class="blogPostImageTitle">F2 800mA fuse</div>
</div>


I checked the power supply, main board, MC amplifier, and control board—no signs of a short or faulty components. I then hooked up my lab power supply and discovered that it was drawing around 1300mA. By the way, the SL10 can also be powered by an external 12V 800mA DC adapter, so 1300mA is quite unexpected and explains why the F2 fuse can’t handle this load.

The answer to the issue was fairly simple. The deck is trying to move the tonearm to its rightmost position when powered on. The tonearm is moved by a small electric motor, which appeared to be rusted or just stuck after years of inactivity. The motor, identified as KCN-22AS4A (4V), was drawing excess current in this rusted state—well above the designed limit.


<div class="blogPostImage">
<img src="/assets/technics-sl10-blows-800ma-fuse/motor.jpg" alt="Tonearm Motor"/>
<div class="blogPostImageTitle">Tonearm motor</div>
</div>


After cleaning it up and lubricating it with SAE 20 motor oil, the SL10 now draws around 800mA. I hope this small tip proves useful and saves time for others. I searched through many similar questions online but didn’t come across an answer like this.
