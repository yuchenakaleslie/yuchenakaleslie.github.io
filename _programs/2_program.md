---
layout: page
title: StoEXSIM
description: Stochastic ground motion simulations with variability in model parameters
img: assets/img/command-line interface.png
importance: 2
category: work
---

Stochastic ground motion simulations with variability in model parameters.

>
> - The latest release can be accessed via [![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.8017643.svg)](https://doi.org/10.5281/zenodo.8017643).
> - It has been hosted on [![Repo](https://badgen.net/badge/icon/GitHub?icon=github&label)](https://github.com/leslieDLcy/stoexsim).
>

## Introduction

A CLI interface for the implementation of the `stochastic finite-fault model`. Particularly, we provide extra capabilities in modeling some key parameters as random variables to account for variability.

> *Note: A concise introduction is shown below in the collapsable section while a thorough Python implementation can be found in another [repo](https://github.com/leslieDLcy/eqstochsim). A technical formulation can be found in the section below*. This type of stochastic model is referred to as source-based models. On the other hand, there is another type of site-based stochastic models that are popular in the study of stochastic dynamics, check out [ktnsrm](https://github.com/leslieDLcy/ktnsrm) as a template in implementing those models.

***

## formulation
A stochastic representation that encapsulates the physics of the earthquake process and wave propagation plays the central role, from the seismological perspective, in characterizing the ground motions. One of the most desired advantage is that such type of representations explicitly distill the knowledge of various factors affecting ground motions (e.g. source, path, and site) into a parametric formulation.
In this study, we have adopted a well-validated stochastic seismological model, as given below, whereby source process, attenuation, and site effects are encapsulated in a parameterized form of the amplitude spectrum. A finite fault strategy is particularly employed to represent the geometry of larger ruptures for large earthquakes.

$$A(f; \Theta) = E(f, M; \theta_{E}) \times P(f, R; \theta_{P}) \times S(f; \theta_{S})$$

Particularly, the variability of such effects in the spectral formulation and hence the uncertainty in stochastic simulations are represented by probability distribution over the input parameters $$\Theta=(\theta_{E}, \theta_{P}, \theta_{S}) \sim p(\Theta)$$.

***

## functionalities in short

- [x] A CLI interface facilitating the use of stochastic finite fault model;
- [x] Aleatoric uncertainty on the region-specific parameters
- [x] An easy implementation of generating an ensemble of simulations

***

## how *stochastic* the simulations are ?

`1. standard implementation`

Though bearing the name "*the stochastic method*" for a while, Boore's model[^1] is not the only stochastic implementation in simulating ground motions of certainty earthquake scenarios. It should be, however, more appropritely referred to as *stochastic source method*[^2]. A standard implementation, shown below, will consider random slip distribution and hypocenter location, coupled with random phase in generating time series.  

```shell
$ "mechanism=N;depth=10;Mw=6.5;Repi=10; csh do_exsim.csh $mechanism $depth $Mw $Repi"
```

`2. aleatoric implementation`

One step further, to reflect the aleatoric uncertainty of many region-specific parameters and then the variability of ground motions:

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/alea_single.jpeg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Single aleatoric simulations
</div>


`3. ensemble implementation`

For practical convenience, you will probably want to generate a suite of simulations for a certain earthquake scenario. Input the number of simulations when prompted.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/alea_ensemble.jpeg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    A suite of simulations
</div>

***

[^1]: Atkinson etc. Stochastic Modeling of California Ground Motions
[^2]: Rezaeian etc. Simulation of synthetic ground motions for specified earthquake and site characteristics.


<!-- TODO: Tweak the standart out look of the CLI -->

