---
layout: page
title: BioMEMS
description: Microbubble length tracking using image processing
img: /assets/img/BioMEMS_project/bubble_crop1.gif
---

## Introducing a pressure sensor

I spent two years in USC Biomedical Microsystems Laboratory working as an undergraduate researcher. One of the projects aims to treat hydrocephalus via a novel pressure sensor.[^note1] Hydrocephalus occurs when excessive cerebrospinal fluid accumulates in the brain, resulting in an abnormal widening of spaces. Since fluid accumulation poses potentially life-threatening pressure against brain tissues, it is necessary to monitor pressure chronically to drive timely therapeutic interventions. Hence, a new, flexible, MEMS-based, low-powered, biocompatible pressure sensor was being developed. This pressure sensor enables reliable sensing for chronic *in-vivo* implantation and provides immediate access to actionable pressure data. My job is to characterize the transducer's design to maximize its sensitivity. So how does it work?

***

## Principle of pressure sensing using microbubble

A microchannel is carefully fabricated into the device. The channel is connected with four electrodes: two on each side to measure the electrochemical differences (e.g. impedance) and two in the middle to generate a microbubble.

<p>
  <img src="/assets/img/BioMEMS_project/deviceFFC.png" style="width: 28%;"/>
  <img src="/assets/img/BioMEMS_project/device.jpg" style="width: 35%;"/>
  <img src="/assets/img/BioMEMS_project/devicechannel.png" style="width: 35%;"/>
</p>
<div class="caption">
    The design of the pressure transducer: left: A MEMS device connected with a FFC cable; middle: a zoomed image of the microbubble pressure transducer (μBPT); right: a further magnified image of pressure part of the μBPT, with and without a bubble injection in the microchannel.
</div>

----
**Boyle's law** tells us that pressure of a gas is inversely related to its volume ($$ P \varpropto \frac{1}{V} $$).**Henry's law** tells us bubble dissolution rate corresponds to change in pressure linearly.
----

We first completely filled the microchannel with phosphate buffered saline (PBS) that mimics a wet *in-vivo* environment. By a current-induced electrolysis from the nuclear cores, we created a microbubble from the middle of the channel. We chronically measure changes in impedance conducted through the liquid capillaries at the corners. When a microbubble is trapped within a filled chamber with rectangular cross section, the gas tends to fill the middle of the cross sectional area and leave pockets of liquid at the corners. These capillaries allow an ionic conduction path within the channel$^1$. We conclude from [2] that in response to a pressure change, bubble length is more likely to vary than the cross section area.[^footnote1] So I started a project that tracks the bubble length with some simple image processing.

***
## Bubble length tracking program

![bubblelength](/assets/img/BioMEMS_project/bubblelength.png)
<div class="caption">
Top: raw, cropped image of the microchannel; middle: processed B/W image of the bubble; bottom: screenshot of the program that tracks the bubble's length.
</div>


***

[^note1]: It is worth mentioning that this pressure sensor can also be applicable to other common pressure-induced medical conditions, such as hypertension and glaucoma.

[^footnote1]: Ma, S., et al: Effect of Contact Angle on Drainage and Imbibition in Regular Polygonal Tubes. Colloid Surf. A. 117. (1996).
