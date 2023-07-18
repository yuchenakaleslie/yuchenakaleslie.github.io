---
layout: page
title: tunnel squeezing intensity
description: Dynamic and Uncertainty-informed squeezing intensity prediction
img: assets/img/two_moon.png
importance: 2
category: work
toc:
  sidebar: left
---

> Part of the results herein are published. Pls refer to [RMRE](https://doi.org/10.1007/s00603-020-02138-8) and [ESREL2020](https://www.researchgate.net/publication/349715719_Decision_Making_for_Optimal_Primary-Support_Selection_to_Minimise_Tunnel-_Squeezing_Risk) for additional details.
> some other parts are currently under review.
> A web-application is provided for uncertainty-informed prediction of squeezing intensity.

Tunnel squeezing is a time-dependent process that typically occurs in weak or over-stressed rock masses, significantly influencing the budget and time of tunnel construction. Given that only limited databases of case histories are documented in literature, many supervised-learning based probabilistic models, naturally probabilistic or not, are prone to provide over confident (some even distorted) probability estimates of squeezing intensity, due to the ignorance of model uncertainties.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/existing_methods.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    List of existing Machine Learning methods for tunnel squeezing intensity prediction
</div>

### Uncertainty informed

The absence of enough data has restricted Machine Learning models from effectively learning the true relationship between features and labels (i.e. the underlying data generating process). Significant uncertainties exist on the model configurations that may have explained such limited data. Consequently, such uncertainties further compromise the generalization power of learned models in that predictions from uncertain/unrepresentative models can still be unreliable and over confident, especially when doing extrapolation on unseen geologic conditions. These unreliable probabilistic predictions will propagate errors (e.g. misclassification costs) into risk analysis of the hazard, further leading to biased construction strategies.

### Dynamically updated

In addition, another challenge in terms of reliable predictions in underground space is that geologic conditions of surrounding rocks obtained in the investigation stage are often incomplete and unreliable. Therefore, such inconsistencies between investigation and construction significantly reduce the accuracy of those aforementioned methods. As such, a **dynamic** scheme based on excavated grounds to predict the squeezing hazard is vital as it can reasonably boost the reliability and practicality of the prediction of squeezing. Mathematically, a Markov process is used to simulate the random process in which the probability distribution of the representative geologic parameters are changing over locations. As such, probabilistic prediction of squeezing is **continuously updated** in light of newly excavated rockmass conditions during construction phase.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/updating_scheme.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Updating of probabilistic predictions along excavation
</div>


### Decision making under uncertainty

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/1.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/3.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/5.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Caption photos easily. On the left, a road goes through a tunnel. Middle, leaves artistically fall in a hipster photoshoot. Right, in another hipster photoshoot, a lumberjack grasps a handful of pine needles.
</div>

In tunneling practices, it’s of great engineering importance to avoid overconfident yet incorrect predictions, as such biased predictions will lead to faulty construction strategies. To better understand the risks associated with squeezing and thus guiding construction strategies, for example designing support system schemes, adjusting the excavation rate, enhancing monitoring frequencies, etc, tunnel practitioners would desire that they can be confident about the probabilistic hazard prediction. This motivates the use of uncertainty measures to make uncertainty-informed engineering decision. 


<hr>

> Footnote: thumbnail image credit: [Purvanshi Mehta](https://towardsdatascience.com/am-i-sure-or-unsure-talks-with-a-neural-network-fc0e14d31373)