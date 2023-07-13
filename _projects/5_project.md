---
layout: page
title: SHM 
description: Anomaly detection in structural health monitoring - a collaboration with Isterre UGA
img: assets/img/earthquake_annotated.png
importance: 3
category: collaboration
---

> This study embodies the research efforts in automatically detecting out-of-distribution data outlier in real-time for autonomous decision making for complex systems. 

This an ungoing collaboration work with Isterre UGA, to propose an environment-informed approach to probabilistically detect the potential structural damage. Several environmental factors, shown below and three vibrational modes are considered in this anlysis. Each mode is associated with its natural frequancy $\omega$ and damping ratio. 

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/target_n_features.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    A glimpse of Environmental factors.
</div>

We will detect the potential structural damage based on the 95% prediction interval. Three examples with respect to three modes are shown below:

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/PI95_fntran.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/PI95_fnt.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/PI95_fnlong.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Three examples with respect to three modes
</div>



