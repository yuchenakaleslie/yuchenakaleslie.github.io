---
layout: page
title: dbNets
description: Concurrent seismic events identification - a collaboration with GFZ
img: assets/img/multi_event_combo.png
importance: 3
category: collaboration
---

 The exponential increase in seismic recording srecently, facilitated by abundant dense monitoring networks, demands systematic approaches to deal with continuous data-streams, such as pipelines for data downloading as well as pre-processing. However, implicit in much of these automated procedures is the reality that often a multi-event segment may arise once a station simultaneously records a near event as well as other events (i.e. teleseismic events or aftershocks), contaminating the main earthquake recording of interest. Significant consequences might occur should this error be unidentified and propagated into subsequent spectral analyses. 
 
 This study presents a novel approach to identify multiple seismic events using Deep Learning techniques in an end-to-end and uncertainty-aware fashion. In particular, we transform the waveforms into time-frequency representations, thereby applying Bayesian Convnets (CNN) to automatically pick out and separate the multi-events, without manual feature design. 

Importantly, a Bayesian Convnet, having considered model uncertainty, is trained to probabilistically detect the seismic evnents in a typical segment from continuous streams. If multiple events are present, our model further yields the location estimates of each event and therefore separating them out.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/separation.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    An automated probabilistic procedure in detecting seismic events
</div>

We have reasoned about the uncertainty regarding the multi events detection as well as the decision in the dividing points throughout a probabilistic pipeline. 

<div class="container">
  <div class="row">
    <div class="col">
        {% include figure.html path="assets/img/1.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col">
        {% include figure.html path="assets/img/3.jpg" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
  </div>
