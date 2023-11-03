---
layout: post
title:  Deploy Python Web apps
date:   2023-06-26 16:40:16
description: Best practices in deploying Deep Learning models 
tags: formatting links
categories: sample-posts
---

<blockquote>
    Full-stack web application for deploying a Deep Learning model, with Flask and Docker.
</blockquote>

What happens after having trained and validated your Deep Learinig model? It may be a simple MLP or the more trending Transformer, built by Tensorflow or Pytorch, for your research/application tasks. There will generally be interests for such model to be used by others, say collegues, clients, etc. The following content will give a concise overview about the best practices in deploying your model.

### Deploy the *learnt* model as a REST API

Simply, the model can run with a simple call such as `python inference.py`. But the main interests lay in serving the model to the general public, as opposed to running only on your own laptop. In this spirit, we can deploy the model as a REST API, such that you can call `curl` to send request to the sever and obtain the response, which will be the results for inference. In doing so, you will probably do the following in the terminal for an example of image classification task. (Note the host name will be the relevant IP address in real cases. The **localhost** shown below means your own machine for illustration purpose.)

```shell
$ curl -X POST -F image=@query_image.jpg 'http://localhost:5000/predict'
```

Well, while this works, the caveat is that the call signature seems unnecessarily arcane. Things could be more straightforward. You don't expect everyone to be a mechanic to drive a car, right?

<hr>

### Full-stack web application

By contrast, a user-friendly, intuitive, responsive, web application sounds much more attracting. Building a front-end for the API can save a lot of trouble for the end users. Besides, you get to integrate a lot of relevant sources at the same page to enrich the experience. The illustrative page below is taken from the [web application](http://18.169.51.60/) I created and hosted by the AWS. Please refer to the [page]({% link _pages/web_app.md %}) for additional details.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.html path="assets/img/predict_page.png" title="example image" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Two types of prediction and 4 models to choose
</div>

<hr>

### Dockerize it !

A tool that can largely stremline the development process is `Docker`. 

<hr>

### Deploy to production 

When deploying in production, the common practice is to use a dedicated combination of WSGI server, with a dedicated HTTP server in front of it (i.e. so-called reverse proxy). Typically, people will use `Gunicorn`, which is a pure Python WSGI server and `nginx`, which is production level HTTP server. How it works is: when serving your application with one of the WSGI servers, it's often good practice to put a dedicated HTTP server in front of it, such that this "reverse proxy" can handle incoming requests, TLS etc. better than the WSGI server.

More conveniently, there are a number of services (e.g. hosting platforms) to facilitate such process. Typical examples include:

<ul>
    <li>PythonAnywhere</li>
    <li>AWS Elastic Beanstalk</li>
    <li>Google Cloud</li>
    <li>Microsoft Azure</li>
</ul>