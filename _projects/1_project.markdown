---
layout: page
title: BioMEMS
description: Microbubble length tracking using image processing
img: /assets/img/BioMEMS_project/bubble_crop1.gif
---

# Introducing a novel pressure sensor

I spent two years in USC Biomedical Microsystems Laboratory working as an undergraduate researcher. One of the projects aims to treat hydrocephalus via a novel pressure sensor. Hydrocephalus occurs when excessive cerebrospinal fluid accumulates in the brain, resulting in an abnormal widening of spaces. Since such fluid accumulation poses potentially life-threatening pressure against brain tissues, it is necessary to monitor pressure chronically to drive timely therapeutic interventions. Hence, a new, flexible MEMS-based, low-powered and biocompatible pressure sensor was being developed. This pressure sensor enables reliable sensing for chronic \textit{in-vivo} implantation and provides immediate access to actionable pressure data. My job is to characterize the transducer's design to maximize its sensitivity. It is worth mentioning that this pressure sensor is also applicable to other common pressure-induced medical conditions, such as hypertension and glaucoma.

<div class="img_row">
    <img class="col one left" src="{{ site.baseurl }}/assets/img/BioMEMS_project/deviceFFC.png" alt="" title="example image"/>img/1
    <img class="col one left" src="{{ site.baseurl }}/assets/img/BioMEMS_project/device.jpg" alt="" title="example image"/>
    <img class="col one left" src="{{ site.baseurl }}/assets/img/BioMEMS_project/devicechannel.png" alt="" title="example image"/>
</div>
<div class="col three caption">
    Images of a device. left: the MEMS device connected with a FFC cable; middle: a zoomed image of the microbubble pressure transducer (\muBPT); right: a further magnified image of pressure part of \muBPT, with and without bubble generation.
</div>

***

# Measure pressure with microbubble

We completely filled the microchannel with phosphate buffered saline (PBS) that mimics a wet \textit{in-vivo} environment. By a current-induced electrolysis from the nuclear cores, we created a microbubble from the middle of the channel. We chronically measure changes in impedance conducted through the liquid capillaries at the corners. We conclude from [2] that in response to a pressure change, bubble length is more likely to vary than the cross section area.[^footnote1]

Boyle's law: inversely relates pressure of a gas to its volume by $P \varpropto \frac{1}{V}$


![bubblelength]/assets/img/BioMEMS_project/bubblelength.png">
*Top: raw, cropped image; middle: processed B/W image of the bubble; bottom: screen shot of the program tracking the bubble's length.*

[^footnote1]: Ma, S., et al: Effect of Contact Angle on Drainage and Imbibition in Regular Polygonal Tubes. Colloid Surf. A. 117. (1996).
