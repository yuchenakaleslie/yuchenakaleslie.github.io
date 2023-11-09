---
layout: post
title: Out-of-box Python decorators
date: 2023-05-19 15:09:00
description: some go-to decorator examples
tags: code
categories: implementation
---

Decorator has always been my favorite feature of Python, not only because of the nice look of a colorful `@function` symbol, but more because of it as an elegant construct to dynamically enrich the wrapped function. In this post I would like to share some of my favorite use cases. I will also mention some real-world uses and leave interested reader to dig more. Some other common examples include the `@app.route()` decorator in Flask, etc.

<hr>

### 1. Timer

Perhaps the most simple case. But it is a definitly a frequent go-to use case where you may need to know the run time of your function or code block. Just simply wrap up the code bloack into a function and add this simple `@function` symbol, quick and elegant.

```python
def timer(func):
    """Print the runtime of the decorated function"""
    @functools.wraps(func)
    def wrapper_timer(*args, **kwargs):
        start_time = time.perf_counter()    # 1
        value = func(*args, **kwargs)
        end_time = time.perf_counter()      # 2
        run_time = end_time - start_time    # 3
        print(f"Finished {func.__name__!r} in {run_time:.4f} secs")
        return value
    return wrapper_timer

@timer
def waste_some_time(num_times):
    for _ in range(num_times):
        sum([i**2 for i in range(10000)])
```

For Jupyter notebook users, you may be familiar with the `%%time` magic command, then you get the idea.

<hr>

### 2. Runtime plot style change

Customize the plotting styles when plotting with matplotlib at runtime. Note that this type of runtime changes takes precedance than stylesheets. I personally find it super useful when polishing your most fancy plot. It enables you to just focus on the style, without worrying about the data content part as it is all wrapped in the `plotting_function`.

```python
@mpl.rc_context({'lines.linewidth': 3, 'lines.linestyle': '-'})
def plotting_function():
    plt.plot(data)

plotting_function()
```

<hr>

### 3. Tensorflow **Function**

This should be quite familiar with Tensorflow users. This allows the switch from **eager excution** to **graph execution**. In Tensorflow 2, computations are running eagerly by default, suggesting Tensorflow operations are executed by Python, one by one, and return results back to Python. By contrast, graph execution means the tensor computations are executed as a Tensorflow graph, represented by `tf.Graph`. Graphs are data structures that contain a set of tf.Operation objects, which represent units of computation; and tf.Tensor objects, which represent the units of data that flow between operations. They are defined in a `tf.Graph` context. Since these graphs are data structures, they can be saved, run, and restored all without the original Python code.

Most commonly, you will use it when writing your own low-level training/test pipeline, such as

```python
@tf.function
def test_step(x, y):
    val_logits = model(x, training=False)
    val_acc_metric.update_state(y, val_logits)
```

<hr>