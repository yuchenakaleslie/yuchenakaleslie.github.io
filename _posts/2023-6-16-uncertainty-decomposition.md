---
layout: post
title: uncertainty decomposition
date: 2023-6-26 11:12:00-0400
description: explain the language of uncertainty in Machine Learning
tags: formatting math
categories: sample-posts
related_posts: false
---

Advances in Deep Learning bring further investigation into credibility and robustness, especially for safety-critical applications. Trustworthy AI which aims to critically investigate the fairness (biasness), interpretability, and robustness of Deep Learning algorithms and applications, has attracted significant attention recently. 

<blockquote>
    All models are wrong, but models that know when they don't know are useful.
</blockquote>

It is desired that Machine Leanring or Deep Learning models should know when they don't know. In most cases, people create or use a neural network model in order to predict a certain quantify of interest (QoI). However, there is no gurrantee that the model prediction is correct, especially under the situations of generalization to out-of-distribution data. People would like to know the predictive distribution instead to understand the uncertainty of the prediction, and further the risks associated with the downstream decisions. This post will clarify the concepts and techniques proposed in recent years on how the Deep Learning models account for the different sources of uncertainty.

### sources of uncertainty

Different sources of uncertainty are involved within the training pipeline, which are generally classified between two categories: aleatoric and epistemic uncertainty [37, 44]. aleatoric is the uncertainty inherent in the data and irreducible, which may comprise measurement error, noisy labels or inherent stochasticity in the data generating process. Depending on the assumption that whether the data noise is dependent on the input features, methods vary in accounting for heteroscedastic or homoscedastic variance. epistemic uncertainty, on the other hand, refers to the model uncertainty, which is reducible with more data. That is, it reflects the fact that there may exist a set of model configurations that can explain the observed data, hence we are probably uncertain about the model parameters given the limited data. Most Deep Learning models, despite being probabilistic in some sense, do not capture model uncertainty. For example, consider a classification task, a model can still be uncertain even with a high softmax output. An example of regression can be found at [Probabilistic regression](https://blog.tensorflow.org/2019/03/regression-with-probabilistic-layers-in.html).


### Probabilistic noise estimation

Most likely the real world data contain noise. Without losing generality, consider a regression problem with gaussian noise, it is desired to account for the variance of the conditional distribution given the feature vector, which represents the *aleatoric* uncertainty. 
That is, to estimate the second moment (variance) of the target conditional distribution in addition to the usual estimation of the first moment (mean).
Note that such uncertainty is irreducible even with increasing data samples as the underlying data collection/measurement process is still noisy, which merely leads to increased number of noisy data. 
Especially, efforts are pursued for modelling the input-dependent variance *heteroscedastic noise*.
A unified structure of a neural network model, where two output units are separately mapped to the mean and variance through independent sets of weights, is constructed to simutaneously estimate the conditional distribution. 
Under the Gaussian noise assumption, the loss objective (*negative log likelihood NLL*) is given as:

\begin{equation}
- \log p(y_{i} | \mathbf{x}_{i}) = \frac{\log \sigma^2(\mathbf{x}_{i})}{2} + \frac{(y_{i} - f_{\omega}(\mathbf{x}_{i}))^2}{2 \sigma^2(\mathbf{x}_{i})} + \frac{\log 2 \pi}{2}
\end{equation}


### Bayesian inference in Deep Learning

Implicit in the above MLE procedure is the ignorance of model uncertainties (*epistemic* uncertainty). The model weights are themselves uncertain due to the imperfect training data. Significant uncertainties may exist on the model configurations that could have generated the data. Especially in the context of limited data, deterministic models, unless properly regularised, are prone to learn too much noise (overfitting) and become overconfident due to the unawareness of model uncertainties. Note that such uncertainty can be reduced with more data and hence referred to as *reducible uncertainty*.
Probability theory provides a framework for reasoning with uncertainty. As such, in accounting for the model uncertainty  in neural network models, probability distributions are assigned to model parameters $$\boldsymbol{\omega}$$, whereby *learning* is characterised with the transformation of the prior knowledge or belief, via the observed data $$\mathcal{D}:\{\mathbf{X}, \mathbf{Y}\}$$, into the posterior knowledge.
Particularly, by formulating such uncertainty, Bayesian models achieves a regularising effect against overfitting, which may otherwise be a serious problem in terms of limited and noisy data.

In the training stage, given a dataset $$\mathbf{X}, \mathbf{Y}$$, we then look for the *posterior distribution* over the parameter space:

\begin{equation}
p(\boldsymbol{\omega}|\mathbf{X}, \mathbf{Y}) = \frac{p(\mathbf{Y|\mathbf{X}, \boldsymbol{\omega}})p(\boldsymbol{\omega})}{p({\mathbf{Y}|\mathbf{X}})}
\end{equation}

This distribution captures the most probable function parameters given our observed data. $$p(\mathbf{Y|\mathbf{X}, \boldsymbol{\omega}})$$ is the *likelihood*, and the *evidence*, $$p({\mathbf{Y}|\mathbf{X}})$$, is given by:

\begin{equation}
p({\mathbf{Y}|\mathbf{X}}) = \int{p(\mathbf{Y|\mathbf{X}, \boldsymbol{\omega}}) p(\boldsymbol{\omega}) \text{d}{\boldsymbol{\omega}}}
\end{equation}

In the testing stage, with the parameters the output given a new input $$\mathbf{x^*}$$ can be predicted:

\begin{equation}
p(\mathbf{y^*}|\mathbf{x^*, \mathbf{X}, \mathbf{Y}}) = \int{p(\mathbf{y^*}|\mathbf{x^*, \boldsymbol{\omega}})p(\boldsymbol{\omega}|\mathbf{X}, \mathbf{Y}) \text{d}{\boldsymbol{\omega}}}
\end{equation}

Compactly, for an i.i.d dataset of $$N$$ observations $$\mathcal{D}$$, the likelihood function can be compactly rewritten as:

\begin{equation}
p(\mathcal{D}|\boldsymbol{\omega}, \beta) = \prod_{i=1}^{N} \mathcal{N} (y_{i}|f_{\boldsymbol{\omega}}(\mathbf{x}), \beta^{-1})
\end{equation}

Similarly, choose a prior distribution over the weights, for example Gaussian:

\begin{equation}
p(\boldsymbol{\omega}|\alpha) = \mathcal{N} (\boldsymbol{\omega}|\mathbf{0}, \alpha^{-1} \mathbf{I})
\end{equation}

the resulting posterior distribution is then:

\begin{equation}
p(\boldsymbol{\omega}| \mathcal{D}, \alpha, \beta)  \propto p(\boldsymbol{\omega}|\alpha) p(\mathcal{D}|\boldsymbol{\omega}, \beta)
\end{equation}

Despite conceptually straightforward, the above inference problem is practically challenging to solve. The integral $$p(\mathcal{D})=\int p(\mathcal{D}|\boldsymbol{\omega}) p(\boldsymbol{\omega}) d \boldsymbol{\omega}$$ is intractable due to the high dimensionality of weights $$\boldsymbol{\omega}$$.


<!-- ### predictive distribution

Predictive uncertainty can be propagated from the uncertain model given the input, which may be of out-of-sample distribution.
Two sources of uncertainty can be combined to account for the predictive uncertainty.
Assuming Gaussian noise $$p(\mathbf{y}|\mathbf{x}, \omega) = \mathcal{N}(f_{\omega}(\mathbf{x}), \tau^{-1} \mathbf{I})$$ where the model precision estimated as $$\tau^{-1} = g_{\boldsymbol{\omega}}(\mathbf{x}^{*})$$, the model's predictive variance given a new data point can be given as:

\begin{equation}
	\text{Var}(y^{*}) = \frac{1}{T} \sum_{t=1}^{T} g_{\boldsymbol{\omega}_{t}}(\mathbf{x}^{*}) \mathbf{I} + \frac{1}{T} \sum_{t=1}^{T} f_{\omega_{t}}(\mathbf{x}^{*})^{T} f_{\omega_{t}}(\mathbf{x}^{*}) - \mathbb{E} (\mathbf{y}^{*})^{T} \mathbb{E} (\mathbf{y}^{*})
\end{equation}

With the Gaussian assumption, the predictive distribution, the integral in Eq.~(\ref{eq:testing_inference}), is indeed approximated by an ensemble of conditional gaussians for $$y^{*}$$, with each gaussian represented by a neural network model parameterised by a sample from the variational posterior.
On the basis of this ensemble of Gaussians, a mixture of Gaussian model further approximates the estimation of mean and variance of the considered predictive distribution:

\begin{aligned}
	\mu(\mathbf{x}^{*}) &= T^{-1} \sum_{t=1}^{T} \mu_{\omega_{t}}(\mathbf{x})  \\
	\sigma(\mathbf{x}^{*}) &= T^{-1} \sum_{t=1}^{T} [\sigma^{2}_{\omega_{t}}(\mathbf{x}^{*}) + \mu^{2}_{\omega_{t}}(\mathbf{x}^{*})] - \mu^{2}(\mathbf{x}^{*})
\end{aligned}

In addition, a further approximation of considering homoscedastic noise could be simpler to estimate, by empirical estimation from the validation set, as given below:

\begin{equation}
	\text{Var}(\mathbf{y}^{*}) \approx \tau^{-1}\mathbf{I} + \frac{1}{T} \sum_{t=1}^{T} f_{\omega_{t}}(\mathbf{x}^{*})^{T} f_{\omega_{t}}(\mathbf{x}^{*}) - \mathbb{E} (\mathbf{y}^{*})^{T} \mathbb{E} (\mathbf{y}^{*})
\end{equation}

Assuming constant, the model imprecision can be estimated as:

\begin{equation}
	\tau = \frac{(1-p) l_{i}^{2}}{2N \lambda_{i}}
\end{equation}

where the weight decay $$\lambda_{i}$$ and prior length scale $$l_{i}$$ are hyperparameters tuned from the separate validation data set. Alternatively, a naive estimate based on the sample variance of the validation set is also sometimes employed. -->