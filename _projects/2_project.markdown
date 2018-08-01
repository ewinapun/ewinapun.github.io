---
layout: page
title: SubID simulations
description: Adaptive subspace identification algorithm for dynamic tracking
img: /assets/img/dynamic_tracking_project/auto(1)-eig-99.png
---

On this page, I briefly covers what I wrote for my senior thesis. I only cover key research ideas and figures that are extracted from my thesis.

To view the full version of my senior thesis, <a href='http://ewinapun.tk/assets/pdf/thesis.pdf'>*click here*</a>.

***

### abstract
<p style="font-size: $small-font-size; width: 80%; text-align: center;">
    In this work, we implement an adaptive subspace identification algorithm developed by[^note1] and test it on simulated time-invariant and time-varying state-space models. We run some simulations to prove that the algorithm can track the poles trajectories of the time-varying State-space models in an adaptive manner with high accuracy. By quantifying the performance with prediction error and tracking error, experi- mental results indicate the proposed adaptive identification algorithm could better predict and track poles of the true time-varying system, as compared to the tradi- tional non-adaptive identification algorithm. In addition, we investigate the effect of the forgetting factor and training set length to empirically find their best values in our simulations.
</p>

## result

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
| cases | *β* | TE_adpt | TE_non-adpt | PE_adpt | PE_non-adpt | PE_baseline |
| --- | --- | --- | ---  | --- | --- | --- |
| TI | 1 | 1.01±0.33% | 0.079±0.062% | 30.18±0.05% | 30.19±0.05% | 25.81±0.02% |
| random walk | 0.99 | 3.76±0.14% | 10.85±5.03% | 20.50±0.21% | 28.26±0.05% | 13.47±0.01% |
| linear | 0.99 | 1.96±0.13% | 6.96±0.70% | 15.85±0.19% | 19.77±0.05% | 11.10±0.001% |
| step-up | 0.99 | 2.68±0.75% | 14.48±0.35% | 13.36±0.17% | 15.23±0.04% | 9.59±0.001% |
| lin+step-up | 0.99 | 3.78±0.05% | 7.06±0.75% | 17.80±0.19% | 20.77±0.05% | 13.70±0.002% |

<p>
    <div class="caption">
        A summary table of the PE and TE for each case.
    </div>
</p>

Overall, TE_adpt  TE_non-adpt

What difference does β make?

<p>
    <img src="/assets/img/dynamic_tracking_project/beta_allwith1.png" style="width: 99%;"/>
    <div class="caption">
    </div>
</p>

The progressions of poles trajectories of each time-varying case are presented in figure 3.9. For β = 0.8, the pole trajectories of all cases are poorly estimated with large estimate variance. As the value of β increases from 0.8 to 0.98, the algorithm starts to perform more accurately in tracking poles, which affirms the drops of TE in figure 3.8. The estimate variance is also reduced as the value of β gets close to 1. When β = 1, the algorithm cannot track any time-varying part of the system in all cases, because the weights on past data equal to the weights on the recent data.
The performance of the algorithm with β = 0.98, 0.99, and 0.995 is very similar in terms of pole tracking, but there is a difference in their rate of convergence to the true poles. Closer the value of β to 1, more recent data are weighted in the algorithm, so longer it takes to converge to the true poles. As the value of β increases from 0.98 to 0.995, we can see an increasing delay in pole convergence in the random walk case in figure 3.9a and a slower convergence in the step function case in figure 3.9b. There is change in poles at Ttrain/2 in the step function case. If we calculate the number of time steps needed to converge, denote as tconv, the data at tconv is weighted in approximately 1.5% in SSMadpt for β = 0.98, 0.99, and 0.995. This means that the last data needed will approximately be weighted in by 1.5%. So greater the value of β, longer it takes to converge. Based on the averaged pole trajectories, β = 0.99 appears to be an optimal value that gives a small estimation error while maintaining a quick rate of convergence.

***

[^note1]: Y. Yang, E. Chang, and M. Shanechi, “Dynamic tracking of non-stationarity in human ECoG activity,” Proc. IEEE Engineering in Medicine and Biology Society Conference(EMBC), Jeju Island, Korea, pp. 1660–1663, 2017.
