---
layout: post
title:  Deploy-Python-Webapps
date:   2022-06-18 16:40:16
description: Best practices in deploying Deep Learning models 
tags: formatting links
categories: sample-posts
---

<blockquote>
    Full-stack web application for deploying a Deep Learning model, with Flask and Docker.
</blockquote>

What happens after having trained and validated your Deep Learinig model? It may be a simple MLP or the more trending Transformer, built by Tensorflow or Pytorch, for your research/application tasks. There will generally be interests for such model to be used by others, say collegues, clients, etc. The following content will give a concise overview about the best practices in deploying your model.

### Deploy the *learnt* model as a REST API

Simply, the model can run with a simple call such as `python inference.py`. But the main interests lay in serving the model to the general public, as opposed to runing it on your own laptop. In this spirit, we can deploy the model as a REST API, such that you can call `curl` to send request to the sever and obtain the response, which will be the results for inference. In doing so, you will probably do the following for an example of image classification task. (Note the host name will be the relevant IP address in real cases. The `localhost` shown below means your own machine for illustration purpose.)

```shell
curl -X POST -F image=@query_image.jpg 'http://localhost:5000/predict'
```

Well, while this works, the caveat is that the call signature seems unnecessarily arcane. Things could be more straightforward.

<hr>

### full-stack web application

By contrast, a user-friendly, intuitive, web application sounds much more attracting. Build a front-end for the API can save a lot of trouble for the end users. Besides, you get to integrate a lot of relevant sources at the same page to enrich the experience.  



<hr>

### Deploy in production 



<ul>
    <li>PythonAnywhere</li>
    <li>AWS</li>
    <li>Google Cloud</li>
    <li>Azure</li>
</ul>
