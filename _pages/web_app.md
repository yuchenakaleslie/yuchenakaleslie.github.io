---
layout: page
permalink: /teaching/
title: web application
description: intuitive and integrated web application
nav: true
nav_order: 5
---

We have created an integrated web application for facilitating tunneling squeezing hazard analysis and uncertainty-informed engineering decision making. Currently, it is hosted on PythonAnywhere.

### *front-end* for deploying Bayesian deep learning models

In practice, it is desired to have reliable (uncertainty-informed) prediction in a fast and simple manner. Practioners need tools that work in a pragmatic way. We have discussed about a few ways to [deploy the learned Machine Learning models]({% link _posts/2015-03-15-Deploy-Python-Webapps.md %}). The most convenient and visualised way is through a web-based application where users can interact with anytime anywhere. Shown below, I have created such an web application to display the uncertainty along with the squeezing prediction. 

Two types of prediction are supported, users can either type in the input feaures or directly compute with a grouped data set and additionally obtain more overall insights (i.e. additional metrics and figures.)

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/predict_page.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Two types of prediction and 4 models to choose
</div>

### Integrated interface for understanding the tunnel squeezing hazard

Besides the ease of running uncertatinty-aware models, a lot of relevant resources are also provided "on site" for facilitating the understanding of the research task at hand, the models used, papers published, and the data set available. Overall, the web application works as an one-stop service. Currenly We have another collegue working on a platform that collects and visualizes data (e.g. real-time sensor measurements) along construction. This web app will then be integrated into the platform to have autonomous decision-making ability in a dynamic way as with the excavation of tunnels. 

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/UI_page.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    An enrichment of relevant resources
</div>


### Showcase uncertainty

Uncertainty in predictive distributions are intuitively displayed. Especially, the epistemic uncertainty is considered thanks to the Bayesian neural network model. By comparison, results from other models that lack model uncertainty (e.g. Decision Tree) is also shown.

<div class="row mt-3">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/ensemblePredictions.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/Histogram.png" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/yarinfancyplot.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Uncertainty representation for 10 data points
</div>
