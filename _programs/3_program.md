---
layout: page
title: KTnSRM
description: 
img: assets/img/separableEPSD.png
redirect:
importance: 3
category: work
---

Spectral power density models and Spectral Representation Method

> The latest release can be accessed via [![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.7979812.svg)](https://doi.org/10.5281/zenodo.7979812).

> It has been hosted on [![Repo](https://badgen.net/badge/icon/GitHub?icon=github&label)](https://github.com/leslieDLcy/ktnsrm).


***

## Introduction
Stochastic process models are responsible for characterising ground motions, representing the stochastic excitations applied upon engineering structures[^1]. To this end, a series of power spectral density models are developed and employed in stochastic dynamic analysis[^2]. Notably, Kanai Tajimi model plays a foundational role[^3]. Beyond which, nonstationary model attract more attention in recent years.

***

## *functionality*

- [x] Define a base Kanai Tajimi model;
- [x] Define both **separable** and **non-separable** evolutionary power spectral density models;
- [x] Generate sample realizations via the Spectral Representation Method;
- [x] A general framework enabling easy addition of more nonstationary models via subclassing.

***

## Examples

`1. Kanai Tajimi PSD model`

$$S(\omega) = S_{0} \frac{1+[2 \zeta (\omega/\omega_{g})]^2}{[1-(\omega/\omega_{g})^2]^2+[2 \zeta (\omega/\omega_{g})]^2}$$

where $$w_{g}=5 \pi$$ rad/s; $$\zeta$$ = 0.63; $$S_{0}$$ = 0.011;

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/KanaiTajimi_PSD.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Kanai Tajimi PSD
</div>


`2. separable EPSD`

Define an evolutionary spectrum in the form $$S(\omega, t)=g(t)^2S(\omega)$$

with an example of modulating function:
$$g(t)=b(e^{-ct} - e^{-2ct})$$
where $b$=4, $c$=0.8

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/nonseparableEPSD.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Example non-separable evolutionary power spectral function
</div>


`3. non-separable EPSD`

An evolutionary spectrum with fully coupled time and frequency nonstationarity. Define an example EPS:
$$S(\omega, t) =\frac{\omega^2}{5 \pi} e^{-0.15t} t^{2} e^{-(\frac{\omega}{5 \pi})^2 t}$$ 

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/separableEPSD.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Example separable evolutionary power spectral function
</div>


4. Spectral Representation Method

***

[^1]: Kiureghian etc. Nonlinear stochastic dynamic analysis for performance-basedearthquake engineering. 
[^2]: Conte and Peng. Fully nonstationary analytical earthquake ground-motion model.
[^3]: Lai etc. Statistical characterization of strong ground motions using power spectral density function.
