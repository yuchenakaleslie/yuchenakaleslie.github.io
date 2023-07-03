---
layout: page
title:  Imprecise training
description: Robust learning with imprecise data
img: assets/img/mnist_c.png
redirect:
importance: 3
category: work
---

Building on the universal approximator theory, deep neural network models are trained to construct functional mappings through learning with abundant observed samples. However, in many situations, observations can be imprecise, noisy and even incomplete. These data problems raise challenges in learning the underlying data generating process and also conducting reliable generalisation at testing stage. 

### Interval-valued features

training data may often include interval-valued data, which may be caused by imperfection of measurement tools or imprecision of expert information, or from [missing data](_projects/1_project.md). Interval training sets may also arise in situations of specific grouped representation such as such as daily interval stock prices.



### label noises

In classification tasks, many times human supervision is requried to manually label samples, e.g. experts supervision in domain-specific labelling. Apart from being time-consuming and expensive, this process also suffers from disagreement between experts and sometimes human errors. In fact, just as measurement uncertainty, these "noises" are typically implicit in the training set. 

