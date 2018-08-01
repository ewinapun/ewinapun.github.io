---
layout: page
title: SubID simulations
description: Adaptive subspace identification algorithm for dynamic tracking
img: /assets/img/dynamic_tracking_project/auto(1)-eig-99.png
---

On this page, I briefly go over what I wrote for my senior thesis. I only cover key research ideas and figures that are extracted from my thesis.

<!-- To view the full version of my senior thesis, <a href='http://ewinapun.tk/assets/pdf/thesis.pdf'>*click here*</a>. -->

***

#### abstract

In this work, we implement an adaptive subspace identification algorithm developed by[^yang] and test it on simulated time-invariant and time-varying state-space models. We run some simulations to prove that the algorithm can track the poles trajectories of the time-varying State-space models in an adaptive manner with high accuracy. By quantifying the performance with prediction error and tracking error, experimental results indicate the proposed adaptive identification algorithm could better predict and track poles of the true time-varying system, as compared to the traditional non-adaptive identification algorithm.

## results

For each case, we visually evaluate the pole tracking ability of the adaptive algorithm and compare the output estimation in the test set. We also quantitatively compare PE and TE of both algorithms.

<p>
    <img src="/assets/img/dynamic_tracking_project/all5waveforms.png" style="width: 99%;"/>
    <div class="caption">
        Waveforms of poles of system matrix A: (a) a time-invariant system, (b-e) time-varying systems with random walk, ascending linearly, changing abruptly with a step function, and ascending linearly with a step function, respectively.
    </div>
</p>

### Time-invariant system

<p>
    <img src="/assets/img/dynamic_tracking_project/non(3)_eig_test_enlarged.png" style="width: 49%;"/>
    <img src="/assets/img/dynamic_tracking_project/non-test-1.png" style="width: 49%;"/>
    <div class="caption">
        Performance on time-invariant system: (a) Poles trajectories (b) Estimated outputs in test set.
    </div>
</p>

Since this is a time-invariant system, we set *β* = 1 to show that the adaptive algorithm can perform equally well when all past data are used. The pole estimation using the non-adaptive algorithm can perfectly track the true time-invariant poles and the estimated poles using adaptive algorithm can converge quickly to the true poles as well.

### Time-varying systems

<p>
    <img src="/assets/img/dynamic_tracking_project/auto(1)-eig-99.png" style="width: 49%;"/>
    <img src="/assets/img/dynamic_tracking_project/auto(1)-test-99.png" style="width: 49%;"/>
    <div class="caption">
        Performance on random walk time-varying system: (a) Poles trajectories (b) Estimated outputs in test set. Each pole trajectory of the A matrix has different random walk patterns.
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

For all time-varying cases, we can point out that the non-adaptive algorithm fails to track the poles trajectories over time. Even when the non-adaptive algorithm uses all past data, since only one estimated system is produced, it is impossible to track poles in an adaptive manner. On the other hand, the adaptive algorithm can effectively track the true poles of the time-varying system. In figure (b), the estimated outputs of the test set using the adaptive algorithm are also closer to the true outputs compared to the non-adaptive algorithm. Judging visually, we can already conclude that the adaptive algorithm has a higher estimation power in the simulated time-varying cases.

## Simulations summary

We also want to compare the algorithms quantitatively using our defined error measures. For all time-varying cases, we obtain TE_adpt < TE_non-adpt and PE_baseline < PE_adpt < PE_non-adpt, proving that the performance of the adaptive algorithm is indeed better than the non-adaptive algorithm. Meanwhile, adaptive algorithm can perform equally well as the non-adaptive algorithm in the time-invariant case.

| cases | TE_adpt | TE_non-adpt | PE_adpt | PE_non-adpt | PE_baseline |
| --- | --- | --- | ---  | --- | --- | --- |
| TI | 1.01±0.33% | 0.079±0.062% | 30.18±0.05% | 30.19±0.05% | 25.81±0.02% |
| random walk | 0.99 | 3.76±0.14% | 10.85±5.03% | 20.50±0.21% | 28.26±0.05% | 13.47±0.01% |
| linear | 1.96±0.13% | 6.96±0.70% | 15.85±0.19% | 19.77±0.05% | 11.10±0.001% |
| step-up | 2.68±0.75% | 14.48±0.35% | 13.36±0.17% | 15.23±0.04% | 9.59±0.001% |
| lin+step-up | 3.78±0.05% | 7.06±0.75% | 17.80±0.19% | 20.77±0.05% | 13.70±0.002% |

<p>
    <div class="caption">
        A summary table of the PEs and TEs for each case.
    </div>
</p>


## Influence of the forgetting factor

One goal of the project is to determine the best value of the forgetting factor, *β* . Here I display the pole trajectories of some time-varying cases as *β* increase from 0.8 to 1. Remember, larger the value of *β*, heavier the past data are weighted. A *β* = 1 means that the entire dataset are weighted equally.

<p>
    <img src="/assets/img/dynamic_tracking_project/beta_allwith1.png" style="width: 99%;"/>
    <div class="caption">
        The progressions of poles trajectories of (a) random walk, (b) step function (c) linearly ascending cases with different forgetting factor values.
    </div>
</p>

For *β* = 0.8, the pole trajectories of all cases are poorly estimated with large estimate variance. As the value of *β* increases from 0.8 to 0.98, the algorithm starts to perform more accurately in tracking poles. The estimate variance is also reduced as the value of *β* gets close to 1. When *β* = 1, the algorithm cannot track any time-varying part of the system in all cases, because the weights on past data equal to the weights on the recent data.

The performance of the algorithm with *β* = 0.98, 0.99, and 0.995 is very similar in terms of pole tracking, but there is a difference in terms of rate of convergence to the true poles. Closer the value of *β* to 1, more recent data are weighted in the algorithm, so longer it takes to converge to the true poles. As the value of *β* increases from 0.98 to 0.995, we can see an increasing delay in pole convergence in the random walk case and a slower convergence in the step function case. In real-life scenarios, maintaining a quick rate of convergence is surely something scientist concerns.

### Additional Work

My thesis has more contents that I didn't get to cover here. To be specific, we investigate the effect of the forgetting factor and training set length empirically (with error measures) to best optimize our simulations.

***

[^yang]: Y. Yang, E. Chang, and M. Shanechi, “Dynamic tracking of non-stationarity in human ECoG activity,” Proc. IEEE Engineering in Medicine and Biology Society Conference(EMBC), Jeju Island, Korea, pp. 1660–1663, 2017.

