---
layout: distill
title: Imputation is no picnic
description: Uncertainty quantification over spectral representation of stochastic processes in the presence of missing data
img: assets/img/incomplete_puzzle.jpg
giscus_comments: true
date: 2023-06-26
importance: 1
category: work

authors:
  - name: Yu Chen
    url: "https://riskinstitute.uk"
    affiliations:
      name: Risk institute, Univ of Liverpool

bibliography: 2018-12-22-distill.bib

# see `bin/2018-12-22-distill.md` for the origianl version

# Optionally, you can add a table of contents to your post.
# NOTES:
#   - make sure that TOC names match the actual section names
#     for hyperlinks within the post to work correctly.
#   - we may want to automate TOC generation in the future using
#     jekyll-toc plugin (https://github.com/toshimaru/jekyll-toc).
toc:
  - name: Introduction
    # if a section has subsections, you can add them as follows:
    # subsections:
    #   - name: Example Child Subsection 1
    #   - name: Example Child Subsection 2
  - name: Three challenges
  - name: Our proposed solution and two frameworks 
  - name: Conclusion
  - name: Interactive Plots
  - name: Layouts
  - name: Other Typography?

# Below is an example of injecting additional post-specific styles.
# If you use this post as a template, delete this _styles block.
_styles: >
  .fake-img {
    background: #bbb;
    border: 1px solid rgba(0, 0, 0, 0.1);
    box-shadow: 0 0px 4px rgba(0, 0, 0, 0.1);
    margin-bottom: 12px;
  }
  .fake-img p {
    font-family: monospace;
    color: white;
    text-align: left;
    margin: 12px 0;
    text-align: center;
    font-size: 16px;
  }

---

## Introduction

Missing data is an ubiquitous problem of various engineering and physical fields, in which incompleness may present in the observational recordings or engineering monitoring data. In fact, it is pervasive in virtually any discipline where *in situ* measurements are collected and transferred, as a result of abundant practical reasons causing intermittent failure, such as sensor failure or incompetence, temporary transmission loss for real-time data, plus numerous other reasons including sensor maintenance, usage, data acquisition restrictions and or data-corruption, see <d-cite key="chen4405534bayesian"></d-cite> for a thorough discussion. `It is therefore vital for safety-critical systems operated by decision-makings on the basis of real-time data streams (e.g. autonomous driving) to be robust under unexpected sensor failure.`

## Three challenges

Stochastic processes are widely adopted to characterise time-dependent data which are random in nature and involve strong nonstationarity, as well as to model  system responses that involve highly nonstationarity and uncertain system parameters. We seek a probabilistic spectral representation of the underlying stochastic processes even in the presense of missing data, and investigate the propagation of uncertainties from imperfect observations all the way through the computational pipeline. 

However, we note there are **three main challenges** in this noble cause: 
**(I)** It's practically impossible for the certain event/scenario/incident under recording to be reevaluated (*let bygones be bygones* :pensive:) hence almost impossible to reconstruct the missing samples not measured with certainty. **Uncertainty quantification** plays a key role in reflecting the inherent uncertainty of the missing data and the downstream models. 
**(II)** most of current approaches are developed on the stationary assumption hence inadequate to reflect the **nonstationary properties** of most real world processes. 
**(III)** most importantly, most of current approaches are still significantly bounded by a ceiling in performance since they are merely **driven by the very limited information** contained in the incomplete data.


## Our proposed solution and two frameworks 

Due to the limit of data quality, fully data-driven methods are bounded to a ceiling performance. As such, our idea is rooted in the incorporation of prior domain knowledge to guide the learning/inference and mitigate the impacts of data problems, thereby producing robust and informed models. 

Particularly, in response to the three challenges, we propose knowledge-guided Bayesian frameworks that `(i)` takes advantage of a-priori knowledge of the underlying process, enabling to incorporate additional information (physics-based knowledge) into the modelling. `(ii)` accounts for uncertainty throughout the framework, allowing to provide a host of outputs in a probabilistic manner (e.g. reconstructions, spectral representations, and stochastic-process sample generations). `(iii)` applicable to nonstationary processes.

Depending on the level of information incorporated, two frameworks are proposed.

### Augmented-Learning 

<div class="fake-img l-body">
  {% include figure.html path="assets/img/Framework2_latest.png" class="img-fluid rounded z-depth-1" %}
</div>

We build on the premise that prior knowledge could provide general yet insightful prior expectations of the observation (with variaibility) of the physical process.
The *a-priori* information is addressed by generating simulations based on the domain knowledge represented by $$\boldsymbol{\theta}_{g}$$. 

specifically, $$\boldsymbol{\theta}_{g} = (\theta_{1}, \dots, \theta_{n})$$ represents a random vector of relevant physical parameters, each component of which stands for a random variable. $$g(\cdot)$$ represents a generator function, which may just be a model with physics aspects capable of generating stochastic simulations accordingly. Collectively the corresponding probability distribution $$p(\boldsymbol{\theta}_{g})$$ would reflect the variability of the simulations embedded in our prior belief.

Given the data represented by those physics-informed simulations, Bayesian recurrent neural network models $$\mathcal{M}$$ are trained as probabilistic model representations of the underlying process, whereby the imputation of missing data is conducted as predictions in a recursive manner.
Importantly, the epistemic uncertainties of the learned model representations are addressed by putting probability distributions over the model parameters $$\boldsymbol{\omega}$$ of neural nets, thus giving rise to the posterior distribution $$p(\boldsymbol{\omega}| \mathcal{S}, \mathcal{M})$$ through the Bayesian inference, as given below:

$$
    p(\boldsymbol{\omega}|\mathcal{S}, \mathcal{M}) = \frac{p(\mathcal{S}|\boldsymbol{\omega}, \mathcal{M}) p(\boldsymbol{\omega}|\mathcal{M})}{p(\mathcal{S}|\mathcal{M})} \propto p(\mathcal{S}|\boldsymbol{\omega}, \mathcal{M}) p(\boldsymbol{\omega}|\mathcal{M})
$$

This marks a key step of the proposed framework, where a probabilistic representation of the underlying processes is learned by recurrent neural network models and further used to reconstruct the incomplete observations. 
Besides, in this study we also present investigations and comparisons of 
a few neural network architectures in this regard. With the posterior distribution, an ensemble of recurrent imputations can be obtained by marginalizing out the parameter space, as follows:

$$
    \mathcal{R} = \int p(\tilde{\mathbf{y}} | \tilde{\mathbf{x}}, \boldsymbol{\omega}) p(\boldsymbol{\omega}| \mathcal{S}) \text{d} \boldsymbol{\omega}
    \label{eq:predictive_distribution}
$$

where $\tilde{\mathbf{x}}$ represents the missing samples in a specific recording;
$\mathcal{R}$ denotes the reconstructed process, practically through an ensemble of reconstructions, which contain both the recurrent imputations $\tilde{\mathbf{y}}$ and existing observations.

***

## Results


<div class="row justify-content-sm-center">
    <div class="col-sm-8 mt-3 mt-md-0">
        {% include figure.html path="assets/img/waveletEPSD3D.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm-4 mt-3 mt-md-0">
        {% include figure.html path="assets/img/EPSD_uncertainty_plot.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    You can also have artistically styled 2/3 + 1/3 images, like these.
</div>

***












## Conclusion

Syntax highlighting is provided within `<d-code>` tags.
An example of inline code snippets: `<d-code language="html">let x = 10;</d-code>`.
For larger blocks of code, add a `block` attribute:

<d-code block language="javascript">
  var x = 25;
  function(x) {
    return x * x;
  }
</d-code>

**Note:** `<d-code>` blocks do not look good in the dark mode.
You can always use the default code-highlight using the `highlight` liquid tag:

{% highlight javascript %}
var x = 25;
function(x) {
  return x * x;
}
{% endhighlight %}

***

## Interactive Plots

You can add interative plots using plotly + iframes :framed_picture:

<div class="l-page">
  <iframe src="{{ '/assets/plotly/demo.html' | relative_url }}" frameborder='0' scrolling='no' height="500px" width="100%" style="border: 1px dashed grey;"></iframe>
</div>

The plot must be generated separately and saved into an HTML file.
To generate the plot that you see above, you can use the following code snippet:

{% highlight python %}
import pandas as pd
import plotly.express as px
df = pd.read_csv(
  'https://raw.githubusercontent.com/plotly/datasets/master/earthquakes-23k.csv'
)
fig = px.density_mapbox(
  df,
  lat='Latitude',
  lon='Longitude',
  z='Magnitude',
  radius=10,
  center=dict(lat=0, lon=180),
  zoom=0,
  mapbox_style="stamen-terrain",
)
fig.show()
fig.write_html('assets/plotly/demo.html')
{% endhighlight %}

***

<!-- ## Details boxes 

Details boxes are collapsible boxes which hide additional information from the user. They can be added with the `details` liquid tag:

{% details Click here to know more %}
Additional details, where math $$ 2x - 1 $$ and `code` is rendered correctly.
{% enddetails %} -->


## Layouts

The main text column is referred to as the body.
It is the assumed layout of any direct descendants of the `d-article` element.

<div class="fake-img l-body">
  <p>.l-body</p>
</div>

For images you want to display a little larger, try `.l-page`:

<div class="fake-img l-page">
  <p>.l-page</p>
</div>

All of these have an outset variant if you want to poke out from the body text a little bit.
For instance:

<div class="fake-img l-body-outset">
  <p>.l-body-outset</p>
</div>

<div class="fake-img l-page-outset">
  <p>.l-page-outset</p>
</div>

Occasionally you’ll want to use the full browser width.
For this, use `.l-screen`.
You can also inset the element a little from the edge of the browser by using the inset variant.

<div class="fake-img l-screen">
  <p>.l-screen</p>
</div>
<div class="fake-img l-screen-inset">
  <p>.l-screen-inset</p>
</div>

The final layout is for marginalia, asides, and footnotes.
It does not interrupt the normal flow of `.l-body` sized text except on mobile screen sizes.

<div class="fake-img l-gutter">
  <p>.l-gutter</p>
</div>

***

## Other Typography?

Emphasis, aka italics, with *asterisks* (`*asterisks*`) or _underscores_ (`_underscores_`).

Strong emphasis, aka bold, with **asterisks** or __underscores__.

Combined emphasis with **asterisks and _underscores_**.

Strikethrough uses two tildes. ~~Scratch this.~~

1. First ordered list item
2. Another item
⋅⋅* Unordered sub-list.
1. Actual numbers don't matter, just that it's a number
⋅⋅1. Ordered sub-list
4. And another item.

⋅⋅⋅You can have properly indented paragraphs within list items. Notice the blank line above, and the leading spaces (at least one, but we'll use three here to also align the raw Markdown).

⋅⋅⋅To have a line break without a paragraph, you will need to use two trailing spaces.⋅⋅
⋅⋅⋅Note that this line is separate, but within the same paragraph.⋅⋅
⋅⋅⋅(This is contrary to the typical GFM line break behaviour, where trailing spaces are not required.)

* Unordered list can use asterisks
- Or minuses
+ Or pluses

[I'm an inline-style link](https://www.google.com)

[I'm an inline-style link with title](https://www.google.com "Google's Homepage")

[I'm a reference-style link][Arbitrary case-insensitive reference text]

[I'm a relative reference to a repository file](../blob/master/LICENSE)

[You can use numbers for reference-style link definitions][1]

Or leave it empty and use the [link text itself].

URLs and URLs in angle brackets will automatically get turned into links.
http://www.example.com or <http://www.example.com> and sometimes
example.com (but not on Github, for example).

Some text to show that the reference links can follow later.

[arbitrary case-insensitive reference text]: https://www.mozilla.org
[1]: http://slashdot.org
[link text itself]: http://www.reddit.com

Here's our logo (hover to see the title text):

Inline-style:
![alt text](https://github.com/adam-p/markdown-here/raw/master/src/common/images/icon48.png "Logo Title Text 1")

Reference-style:
![alt text][logo]

[logo]: https://github.com/adam-p/markdown-here/raw/master/src/common/images/icon48.png "Logo Title Text 2"

Inline `code` has `back-ticks around` it.

```javascript
var s = "JavaScript syntax highlighting";
alert(s);
```

```python
s = "Python syntax highlighting"
print s
```

```
No language indicated, so no syntax highlighting.
But let's throw in a <b>tag</b>.
```

Colons can be used to align columns.

| Tables        | Are           | Cool  |
| ------------- |:-------------:| -----:|
| col 3 is      | right-aligned | $1600 |
| col 2 is      | centered      |   $12 |
| zebra stripes | are neat      |    $1 |

There must be at least 3 dashes separating each header cell.
The outer pipes (|) are optional, and you don't need to make the
raw Markdown line up prettily. You can also use inline Markdown.

Markdown | Less | Pretty
--- | --- | ---
*Still* | `renders` | **nicely**
1 | 2 | 3

> Blockquotes are very handy in email to emulate reply text.
> This line is part of the same quote.

Quote break.

> This is a very long line that will still be quoted properly when it wraps. Oh boy let's keep writing to make sure this is long enough to actually wrap for everyone. Oh, you can *put* **Markdown** into a blockquote.


Here's a line for us to start with.

This line is separated from the one above by two newlines, so it will be a *separate paragraph*.

This line is also a separate paragraph, but...
This line is only separated by a single newline, so it's a separate line in the *same paragraph*.
