---
layout: page
title: Identify Volitional States via Intracortical BCI
description: describe my poster at SfN 2019
img: /assets/img/SfN2019/thumbnail.gif
published: false
---

On October 19 - 23, 2019, I attended Society for Neuroscience (SfN) Annual meeting in Chicago, IL, USA. I presented our research with a poster, titled ***Identifying changes in volitional state and task engagement based on the intrinsic structure of neural ensemble activity patterns in motor cortex of people with tetraplegia during daily activities and BCI use***. You can view the poster <a href='/assets/pdf/SfN_poster_2019.pdf'>here.</a>
*Keywords:* Motor Cortex, Brain Computer Interface, tetraplegia, neural state space

***



## Overview

* Brain-computer interfaces (BCIs) are designed to bypass damaged motor pathways and provide new links to assistive technologies for people with neuromotor deficits. It is widely accepted that motor cortex incorporates a mix of incoming sensory, cognitive, and motor planning information, reflecting latent variables that are not directly related to kinematic motor output.
* There is a need to reliably identify neural activity patterns indicative of a set of latent factors affected by task and cognitive context changes to build BCI systems that support continuous, multi-effector use.
* Studies previously showed successful decoding of contextual changes in idle vs. active states [^Lesenfants], and controlling different end effectors [^Fasoli].
* We present clustering of the projections of neural data representing different context-dependent volitional states using an approach that visualizes data by generating low-dimensional state spaces based solely on the intrinsic similarity of single unit ensemble recordings.

## Introduction

Neuromotor deficits resulting from conditions such as amyotrophic lateral sclerosis (ALS), brainstem stroke, and spinal cord injury (SCI) result in loss of volitional movement reducing independence. Brain-computer interfaces (BCI) bypass damaged motor pathways and provide new links to assistive technologies. Voluntary action engages vast networks of neurons performing complex calculations which are still not fully understood. It is widely accepted that motor cortex incorporates a mix of incoming sensory, cognitive, and motor planning information, reflecting latent variables that are not directly related to kinematic motor output. Reliably identifying neural activity patterns indicative of a set of latent factors impacted by task and cognitive context is a challenge for developing BCI systems that support continuous, multi-effector use.

Here we present a new approach to generate state spaces based solely on the intrinsic properties of single unit ensemble recordings. We used Spike train SIMilarity Space (SSIMS) analysis to map neural activity patterns into low dimensional state spaces (based on spike train metrics combined with dimensionality reduction). These state space projections can be used to identify clusters of similar, recurring activity patterns, without the need to define task-related tuning models for individual neurons. We applied this method to data collected from two participants enrolled in the BrainGate2 clinical trial - T10, an adult male with tetraplegia due to SCI (C4 AIS-A), and T9, an adult male with tetraplegia due to ALS (ALSFRS-R of 8). T10 had two 96 microeletrode arrays (Blackrock Microsystem, Inc) implanted on the left middle frontal gyrus (MFG) and precentral gyrus (PCG), and T9 on the left PCG. We collected data during sessions where T10 & T9 controlled either a computer cursor or a JACO robotic arm to perform a 2D target acquisition task via intracortical BCI. We demonstrate that our approach can be used to generate state spaces that differentiate between effectors (cursor vs. robotic arm) in both T10 & T9 (81.4±8.0%, 99.5±0.58% accuracy). Additionally, we recorded data from T10 over a 24 hour period; we can identify 5 partially overlapping states related to session tasks, interaction with caretakers and others, engagement with a sip-and-puff computer system, eating, and sleeping (Nearest Neighbor Classifier: 46.5±0.6%, p<.01; against chance classification: 23.5±0.8%). Our findings suggest that state space models based on intrinsic similarity can be used to detect context-dependent changes in volitional state, providing a useful indicator of when BCI control modes should be adjusted.

## Background



## Methods

## Participants and Implants

Two participants (enrolled in BrainGate2 pilot clinical trial): T9 is 52 years old with tetraplegia due to amyotrophic lateral sclerosis (ALSFRS-R of 8), and T10 is 35 years old with tetraplegia due to spinal cord injury (C4 AIS-A). Two 96-channel Utah microelectrode arrays implanted both on left precentral gyrus (PCG) for T9, and one array on the left middle frontal gyrus (MFG) and one on the left PCG for T10.


<p>
<img src="/assets/img/SfN2019/setup.png"/>
    <div class="caption">
        blah blah blah
    </div>
</p>

### Spike Train SIMilarity Space (SSIMS)

[^SSIMS]

Step 1: compute similarity metrics between pairs of spike trains by calculating the cost to transform one spike train to another with inserting, deleting, or shifting spikes[^Victor]

Step 2: perform dimensionality reduction using t-Distributed Stochastic Neighbor Embedding [^tsne]

These state space projections can be used to identify clusters of similar, recurring activity patterns, without the need to define task-related tuning models for individual

### Data Acquisition

## I. Full day continuous neural recording of BCI use and daily activities

26-hour continuous wireless recording from T10 performing center out task, grid task, and other usual daily activities.
<p>
  <img src="/assets/img/SfN2019/R8.png" style="float: right; width:30%;"/>
</p>

<p>
  <img src="/assets/img/SfN2019/GRID.png" style="float: right; width:30%;"/>
</p>

### Data Selection

Tasks: from 1s after the ‘go’ cue in each trial

each event denotes a 1 second long spike train

<p>
  <img src="/assets/img/SfN2019/snippet.png" style="float: right; width:40%;"/>
</p>

Other categories: events in top percentile of change in smoothed mean threshold crossings after outlier elimination (to avoid signal dropout and electronic noise)



<p>
  <img src="/assets/img/SfN2019/events.png" style="width:80%;"/>
  <img src="/assets/img/SfN2019/label_event_long.png" style="width:20%;"/>
</p>

### Results



<p>
<img src="/assets/img/SfN2019/24hBehaviorial.gif" style="width:50%;vertical-align: middle;"/>
    <div class="caption">
        cool SSIMS
    </div>
</p>

10-fold cross validated 5-Nearest-Neighbor (KNN) of 7 states: 81.18% ± 2.38% (chance: 17.82% ± 2.95% ) • Eating and watching TV difficult to separate; potentially because T10 was watching TV while eating

<p>
<img src="/assets/img/SfN2019/result1.png"/>
    <div class="caption">
        blah blah blah
    </div>
</p>



## II. Cursor vs robotic arm control

In each recording session (8 for T9 and 4 for T10), the decoder was first calibrated on one effector using open-loop imagery and then closed-loop decoder calibration. The decoder then ran on blocks (each consisting of many trials of the same task) that alternated between the two effectors.

Participants were instructed to move either a computer cursor or a JACO robotic arm to a cued target with no instructed delay in a center-out task.

<p>
  <img src="/assets/img/SfN2019/JACO.jpg" style="float: right; width:35%;"/>
</p>
<p>
<div class="caption">
    A center-out task controlled with a JACO robotic arm.
</div>
</p>


### Data Selection

each point repersents one trial; use spike trains 2.5s before target is acquired

### Results
Engaging different effectors elicits different neural activity patterns

<p>
<img src="/assets/img/SfN2019/T9_SSIMS.gif" style="width:45%"/>
<img src="/assets/img/SfN2019/T10_SSIMS.gif" style="width:45%"/>
<div class="caption">
3D SSIMS spaces of a session of T9 and T10.
</div>
</p>

A 10-fold cross validated KNN (K=3) accuracy averaged across all sessions:
direction classification - T9 : 63.52 ± 9.20% and T10 : 43.57 ± 7.63%
effector classification - T9 : 97.58 ± 1.55% and T10 : 87.94 ± 5.17%

<p>
<img src="/assets/img/SfN2019/result2.png" style="width:60%;vertical-align: middle;"/>
    <div class="caption">
    The above 3D SSIMS spaces of T9 and T10 view from 2 orientations. One presents the clustering between directions, while another shows separation of tasks using different effectors.
    </div>
</p>


## Discussions



## Conclusion and Future Work


• State space models based on intrinsic activity pattern similarity can be used to:
(1) detect context-dependent changes in volitional state across daily activities
(2) differentiate between the intention to engage different effectors (cursor vs. robot)
• Motor cortex contains information about volitional states, in addition to intended movements. • Future work includes
- comparing various dimensionality reduction techniques;
- investigating non-stationarity across days, obtaining more than one day of continuous data;
- using these data to support the development of a highly interactive BCI system that enables continuous, multi-effector use for people with tetraplegia.


This work is supported by Office of Research and Development, Rehabilitation R&D Service, Department of Veterans Affairs, NIH and Massachusetts General Hospital.


***

[^Lesenfants et al., SfN, 2016]:
[^Fasoli et. al., APMR, 2017]:
[^SSIMS]:
[^Victor]: Victor and Purpura, 2011
[^tsne]: van der Maaten, 2008
