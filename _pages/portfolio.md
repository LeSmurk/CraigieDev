---
title: "Portfolio"
layout: splash
permalink: /portfolio/
header:
  overlay_color: "#000"
  overlay_filter: "0.5"
  overlay_image: 
  # cta_label: "Download"
  # cta_url: "https://github.com/mmistakes/minimal-mistakes/"
  # caption: "Photo credit: [**Unsplash**](https://unsplash.com)"
excerpt: "My Work."
intro: 
  - excerpt: 'Here are some of the bigger scale projects that I am currently developing.'
  
feature_row1:
  - image_path: /assets/Voxracers/voxSplash.jpg
    alt: "placeholder image 2"
    title: "Voxracers"
    excerpt: 'Currently my biggest project creating a voxel-based racing game.'
    url: "/pages/voxracers"
    btn_label: "Read More"
    btn_class: "btn--primary"
feature_row2:
  - image_path: /assets/UniWork/temp.jpg
    alt: "placeholder image 2"
    title: "Professional Project"
    excerpt: 'A group project for university working with a client.'
    url: "/pages/profproj"
    btn_label: "Read More"
    btn_class: "btn--primary"
    
intro1: 
  - excerpt: 'Here are some of my smaller solo projects that I have completed.'
  
feature_row:
  - image_path: assets/images/unsplash-gallery-image-1-th.jpg
    alt: "placeholder image 1"
    title: "Shadow Walker"
    excerpt: "48 hour Unity shadow controlling puzzle game."
    url: "/pages/shadowwalker"
    btn_label: "Read More"
    btn_class: "btn--primary"
    
  - image_path: /assets/UniWork/IceCreamRushSplash.JPG
    alt: "placeholder image 2"
    title: "Ice Cream Rush"
    excerpt: "An OpenGL PSVita ice cream stacking game."
    url: "/pages/icecreamrush"
    btn_label: "Read More"
    btn_class: "btn--primary"
    
  - image_path: /assets/UniWork/LemmingsGBA.JPG
    title: "Lemmings"
    excerpt: "A lemmings demo on GBA."
    url: "/pages/lemmings"
    btn_label: "Read More"
    btn_class: "btn--primary"
---

{% include feature_row id="intro" type="center" %}

{% include feature_row id="feature_row1" type="center" %}

{% include feature_row id="feature_row2" type="center" %}

{% include feature_row id="intro1" type="center" %}

{% include feature_row %}
