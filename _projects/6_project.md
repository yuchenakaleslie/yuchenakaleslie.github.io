---
layout: page
title: SiteAmp
description: Uncertainty-aware frequency-dependent predictions for single site amplification
img: assets/img/kde_example.png
importance: 4
category: collaboration
---
This in an ungoing collarboartion with Dr. Chuanbin Zhu from Univ of Canterbury, New Zealand. Stay tuned for more in-depth findings. 

Currently Bayesian deep recurrent models are adopted for single-site amplification prediction. Specifically, both sources of uncertainties, aleatoric and epistemic, are considered and reflected in the predictive uncertainties. Refer to the post [uncertainty decomposition]({% link _posts/2023-6-16-uncertainty-decomposition.md %}) for a discussion in differentiating aleatoric and epistemic uncertainty in constructing predictive intervals. Importanly, in this research, accurate predictions are obtained by the model and we show the frequency-dependent variances. 

Various frequency patterns have been learnt and reasonable uncertainty bounds have been estimated. The ground truth has been well captured.

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/61.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/144.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>
<div class="caption">
    Varying frequency patterns at different sites
</div>

For uncertainty measures, Fig. 6 shows the width measure (i.e. width between upper and lower bounds) of the 95% predictive interval with respect to each frequency, as an indication of the magnitude of uncertainty. Apparently, high frequency ranges have shown comparatively larger widths, suggesting
the model’s uncertainty when predicting at high frequency ranges. Also, it can be seen that only very few times, mostly in the middle frequency range, that the PI has missed the ground truth value. 

<div class="row">
    <div class="text-center">
        {% include figure.html path="assets/img/PIwidthpercentage.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    The PI width metric for each frequency value for the test set. Blue points
    indicate the PI has contained the ground truth while the orange points suggest otherwise.
</div>

The residuals with respect to different frequencies can be seen below.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/uncer_residual_at_f016.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/uncer_residual_at_f574.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/uncer_residual_at_f1046.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Residual plots with respect to certain frequencies
</div>