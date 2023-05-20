---
layout: post
title: Cosine Tuning in Motor Cortical Neurons
date: 2018-10-4 06:00
description: Understand neuron's preferred direction of movement and its underlying cosine distribution
published: false
---

Most literature on studying nonstationarity uses nonhuman primates (NHP) model. To translate their work to clinical iBCI, we need to address the important differences in methodology between NHP and human recordings. There are three key differences. First, most NHP research sessions are conducted in a controlled, noise-reduced laboratory setting, whereas BrainGate's research sessions are conducted in the participant’s home - a deliberate choice as our BCI system is intended for at-home use. There are many potential sources of distraction and noise from the environment.

Second, NHP electrode arrays are connected via a short 3-cm wire bundles, whereas BrainGate employs a wireless connection to acquire signals from the electrode arrays. Although the wireless system can achieved high-resolution record broadband intracortical signals over a long period of time, it is still susceptible to picking up noise before amplification and experience signal dropout from receiving antenna interference \cite{Simeral2019-av}.

Third, since human has larger brain and intracranial space (epidural, subdural, and subarachnoid) compared to the NHP, the human brain moves more within the skull. Micro-movements of the implants on the motor cortex can leads to increase of adding or dropping neurons in recordings. These differences are likely to contribute to increase in nonstationarity observed in human intracortical recordings \cite{Jarosiewicz2015-vl}, rendering the same decoder tested on NHP not as effective for human clinical trials.
