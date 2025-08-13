---
layout: post
title: Unity Tutorial Test
date: 2025-08-12 14:24:00
description: this is what included plotly.js code could look like
tags: code
categories: sample-posts
featured: true
disqus_comments: true
chart:
  plotly: true
images:
  compare: true
  slider: true
---

This is a test to showcase some example code. This example will showcase C#.

```c#
using UnityEngine;
 
public class CheckButtonPress : MonoBehaviour
{
 
    void Update()
    {
        if (Input.GetKeyDown(KeyCode.Space)) 
           Debug.Log("Space was pressed this frame");
 
    }
 
}
```
<swiper-container keyboard="true" navigation="true" pagination="true" pagination-clickable="true" pagination-dynamic-bullets="true" rewind="true">
  <swiper-slide>{% include figure.liquid loading="eager" path="assets/img/9.jpg" class="img-fluid rounded z-depth-1" %}</swiper-slide>
  <swiper-slide>{% include figure.liquid loading="eager" path="assets/img/7.jpg" class="img-fluid rounded z-depth-1" %}</swiper-slide>
  <swiper-slide>{% include figure.liquid loading="eager" path="assets/img/8.jpg" class="img-fluid rounded z-depth-1" %}</swiper-slide>
  <swiper-slide>{% include figure.liquid loading="eager" path="assets/img/10.jpg" class="img-fluid rounded z-depth-1" %}</swiper-slide>
  <swiper-slide>{% include figure.liquid loading="eager" path="assets/img/12.jpg" class="img-fluid rounded z-depth-1" %}</swiper-slide>
</swiper-container>

## Image Comparison Slider

This is a simple image comparison slider. It uses the [img-comparison-slider](https://img-comparison-slider.sneas.io/) library. Check the [examples page](https://img-comparison-slider.sneas.io/examples.html) for more information of what you can achieve with it.

<img-comparison-slider>
  {% include figure.liquid path="assets/img/prof_pic.jpg" class="img-fluid rounded z-depth-1" slot="first" %}
  {% include figure.liquid path="assets/img/prof_pic_color.png" class="img-fluid rounded z-depth-1" slot="second" %}
</img-comparison-slider>
