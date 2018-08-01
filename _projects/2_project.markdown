---
layout: page
title: SubID simulations
description: Adaptive subspace identification algorithm for dynamic tracking
img: /assets/img/dynamic_tracking_project/auto(1)-eig-99.png
---



<p>
    <img src="/assets/img/dynamic_tracking_project/all5waveforms.png" style="width: 99%;"/>
    <div class="caption">
        Waveforms of poles of system matrix A: (a) a time-invariant system, (b-e) time-varying systems with random walk, ascending linearly, changing abruptly with a step function, and ascending linearly with a step function, respectively.
    </div>
</p>

<p>
    <img src="/assets/img/dynamic_tracking_project/non(3)_eig_test_enlarged.png" style="width: 49%;"/>
    <img src="/assets/img/dynamic_tracking_project/non-test-1.png" style="width: 49%;"/>
    <div class="caption">
        Performance on time-invariant system: (a) Poles trajectories (b) Estimated outputs in test set.
    </div>
</p>

<p>
    <img src="/assets/img/dynamic_tracking_project/auto(1)-eig-99.png" style="width: 49%;"/>
    <img src="/assets/img/dynamic_tracking_project/auto(1)-test-99.png" style="width: 49%;"/>
    <div class="caption">
        Performance on random walk time-varying system: (a) Poles trajectories (b) Estimated outputs in test set.
    </div>
</p>


<p>
    <img src="/assets/img/dynamic_tracking_project/lin(1)-eig-99.png" style="width: 49%;"/>
    <img src="/assets/img/dynamic_tracking_project/lin(1)-test-99.png" style="width: 49%;"/>
    <div class="caption">
        Performance on linearly ascending time-varying system: (a) Poles trajectories (b) Estimated outputs in test set.
    </div>
</p>

<p>
    <img src="/assets/img/dynamic_tracking_project/stepup(1)-eig-99.png" style="width: 49%;"/>
    <img src="/assets/img/dynamic_tracking_project/stepup(1)-test-99.png" style="width: 49%;"/>
    <div class="caption">
        Performance on time-varying system with step up function: (a) Poles trajectories (b) Estimated outputs in test set.
    </div>
</p>

<p>
    <img src="/assets/img/dynamic_tracking_project/stlin(2)-eig-99.png" style="width: 49%;"/>
    <img src="/assets/img/dynamic_tracking_project/stlin(2)-test-99.png" style="width: 49%;"/>
    <div class="caption">
        Performance on linearly ascending time-varying system with step function: (a) Poles trajectories (b) Estimated outputs in test set.
    </div>
</p>

## Simulations summary

cases | $\beta$ *β* | TE_adpt | TE_non-adpt | PE_adpt | PE_non-adpt | PE_baseline
--- | --- | --- | ---  | --- | --- | ---
TI | 1 | 1.01±0.33% | 0.079±0.062% | 30.18±0.05% | 30.19±0.05% | 25.81±0.02%
random walk | 0.99 | 3.76±0.14% | 10.85±5.03% | 20.50±0.21% | 28.26±0.05% | 13.47±0.01%
linear | 0.99 | 1.96±0.13% | 6.96±0.70% | 15.85±0.19% | 19.77±0.05% | 11.10±0.001%
step-up | 0.99 | 2.68±0.75% | 14.48±0.35% | 13.36±0.17% | 15.23±0.04% | 9.59±0.001%
lin+step-up | 0.99 | 3.78±0.05% | 7.06±0.75% | 17.80±0.19% | 20.77±0.05% |
13.70±0.002%
<p>
    <img src="/assets/img/dynamic_tracking_project/beta_allwith1.png" style="width: 99%;"/>
    <div class="caption">
    </div>
</p>

<!-- To view the full version of my senior thesis, <a href='http://ewinapun.tk/assets/pdf/thesis.pdf'>click here</a>. -->
