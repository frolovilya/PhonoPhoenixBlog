---
layout: post
title:  "Mysterious MN1400PA"
excerpt: Microcontroller that drives Technics turntable automatics
date:   2025-03-18
categories: blog
author: Ilia Frolov
---

The MN1400PA is a 28-pin proprietary microcontroller developed by Technics, responsible for controlling the automatic functions of their turntables, including tonearm movement, start/stop and cueing mechanisms.

<div class="blogPostImage">
<img src="/assets/mysterious-mn1400pa/mn1400pa.jpeg" alt="MN1400PA Microcontroller"/>
<div class="blogPostImageTitle">MN1400PA Microcontroller</div>
</div>

This post is focused on the Technics SL-10 model, but the MN1400PA microcontroller is also used in other models, such as the SL-1600MK2. I had to dive deep into the microcontroller's pinout and conditional logic to troubleshoot the start/stop functions and tonearm operations. Unfortunately, the SL-10 service manual doesn’t provide detailed information about the MN1400PA. I'm writing these notes as a cheatsheet for future myself and anyone else who might encounter similar issues—because, honestly, I just can’t keep all this in my head!

<div class="blogPostImage">
<img src="/assets/mysterious-mn1400pa/ports.png" alt="MN1400PA Microcontroller Ports" style="width: 200px"/>
<div class="blogPostImageTitle">Microcontroller pins</div>
</div>

Reference values are given with the S201 pushed, S401 pushed, Q403-5 covered with a tape. So that for the tonearm to start moving, pin 3 must be H, pin 11 - H, pin 12 - L and pin 21 - grounded.

| Pin    | Port   | Value  | Description |
| :----- | :----- | :-----| :---------- |
| 1      | Vss    | 0     | Ground      |
| 2      | C09    | H - enabled, <br>L - disabled      | Connected to D475 "Repeat" LED <br> ![D475 Reset LED](/assets/mysterious-mn1400pa/D475.jpeg)    |
|  __3__      | __C08__    | __H - started__, <br>L - stopped     |  Start/Stop switch. Connected to the S201 switch <br> ![S201 Switch](/assets/mysterious-mn1400pa/S201.jpeg)    |
| 4      | C07    | H - started, <br>L - stopped      | Connected to the Base of Q407 (stylus illuminator)      |
| 5      | C06    |       | When connected to pin 9 - Cueing, to pin 10 - Repeat     |
| 6      | C05    |       | When connected to pin 9 - Start, to pin 10 - Stop     |
| 7      | A13    | L when true, H otherwise      | Tonearm is in the leftmost position (end of a record), S403 switch is On. <br> ![S403 and S402 Switches](/assets/mysterious-mn1400pa/S402_S403.jpeg)      |
| 8      | A12    | L when true, H otherwise      | Tonearm is in the rightmost position (beginning of a record), S402 switch is On. See image for A13 port.    |
| 9      | A11    |       | Input from pins 5 and 6     |
| 10     | A10    |       | Input from pins 5 and 6     |
| __11__     | __B13__    | __H__     | Should be constantly H to indicate that the platter is spinning. Make sure that the mainboard is correctly assembled and the platter doesn't touch anything while rotating.     |
| __12__     | __B12__    | __L__ for 17cm record.     | Size detection, H for 17cm records. At least this Port must be H for the tonearm to start moving. Connected to the Q403 photo transistor. You may cover it with an electrical tape for troubleshooting while the top part of the turntable is open. <br> ![Q403, Q404 and Q405 Photo Transistors](/assets/mysterious-mn1400pa/Q403_Q404_Q405.jpeg) |
| 13     | B11    | L for 25cm record.      | Size detection, H for 25cm records. Input from Q404, see B12 image. |
| 14     | B10    | L for 30cm record.     | Size detection, H for 30cm records. Input from Q405, see B12 image. |
| 15     | E00    |       | Tonearm motor drive output signals |
| 16     | E01    |       | Tonearm motor drive output signals     |
| 17     | E02    |       | Tonearm motor drive output signals     |
| 18     | E03    |       | Tonearm motor drive output signals     |
| 19     | -      |       |      |
| 20     | RESET  | H     | When L, then the MCU state is reset  |
| __21__     | __SNS0__   | __Ground__     | Connected to the ground via S401 switch, that controls that the top part of the turntable is closed. You may solder top left and middle left pins of the S401 to have it always on for troubleshooting. <br> ![S401 Switch](/assets/mysterious-mn1400pa/S401.jpeg) |
| 22     | SNS1   |       | Impuls from a PC401 photo sensor, when the tonearm motor is rotating. <br> ![PC401](/assets/mysterious-mn1400pa/PC401.jpeg) |
| 23     | -      |       |      |
| 24     | -      |       |      |
| 25     | D02    |       | Goes to S202 speed selector switch    | 
| 26     | -      |       |      |
| 27     | Vdd    | 5V    | Power input |
| 28     | OSC    |       | Clock signal |
