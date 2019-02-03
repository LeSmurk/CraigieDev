---
title: "Helpers"
permalink: /pages/proceduralmodule
excerpt: "Jekyll `_includes` and other helpers to use as shortcuts for creating archives, galleries, table of contents, and more."
gallery:
  - url: /assets/images/unsplash-gallery-image-1.jpg
    image_path: /assets/images/unsplash-gallery-image-1-th.jpg
    alt: "placeholder image 1"
    title: "Image 1 title caption"
  - url: /assets/images/unsplash-gallery-image-2.jpg
    image_path: /assets/images/unsplash-gallery-image-2-th.jpg
    alt: "placeholder image 2"
    title: "Image 2 title caption"
  - url: /assets/images/unsplash-gallery-image-3.jpg
    image_path: /assets/images/unsplash-gallery-image-3-th.jpg
    alt: "placeholder image 3"
    title: "Image 3 title caption"
feature_row:
  - image_path: /assets/images/unsplash-gallery-image-1-th.jpg
    alt: "placeholder image 1"
    title: "Placeholder 1"
    excerpt: "This is some sample content that goes here with **Markdown** formatting."
  - image_path: /assets/images/unsplash-gallery-image-2-th.jpg
    alt: "placeholder image 2"
    title: "Placeholder 2"
    excerpt: "This is some sample content that goes here with **Markdown** formatting."
    url: "#test-link"
    btn_label: "Read More"
    btn_class: "btn--inverse"
  - image_path: /assets/images/unsplash-gallery-image-3-th.jpg
    title: "Placeholder 3"
    excerpt: "This is some sample content that goes here with **Markdown** formatting."
last_modified_at: 2018-11-25T20:47:01-05:00
toc: true
toc_label: "Helpers"
toc_icon: "cogs"
---




title: "Procedural Module"
permalink: /pages/proceduralmodule
three_rowDS:
  - image_path: /assets/UniWork/DiamondSquareImproved.PNG
    alt: "placeholder image 0"
  - image_path: /assets/UniWork/DiamondSquareRegularHills2.PNG
    alt: "placeholder image 1"    
  - image_path: /assets/UniWork/DiamondSquareSand.PNG
    alt: "placeholder image 2"
two_rowSnipDS:
  - image_path: /assets/Code Snips/DiaSquCodeLoop.PNG
    alt: "placeholder image 0"
  - image_path: /assets/Code Snips/DiaStepCode.PNG
    alt: "placeholder image 1" 
two_rowSnipDS1:
  - image_path: /assets/Code Snips/RandomStep.PNG
    alt: "placeholder image 0"
  - image_path: /assets/Code Snips/SquStepCode.PNG
    alt: "placeholder image 1"  
 two_rowSnipCA:
  - image_path: /assets/Code Snips/CellularCodeRule1.PNG
    alt: "placeholder image 0"
  - image_path: /assets/Code Snips/CellularCodeRule2.PNG
    alt: "placeholder image 1"


*3rd year procedural generation module within Directx11*

I began by creating a simple Perlin noise terrain, by converting Ken Perlin's original algorithm into C++ and then adding environmental texturing through the use of a pixel shader.
The same Perlin noise was also used in conjunction with a compound sine wave to create the water that is seen in all the images.

![PerlinNoise]({{ "/assets/UniWork/PerlinEnviroTex.PNG" | relative_url }})

I then developed a more complex type of terrian, using the Diamond-Square algorithm, which created the outputs seen below.

{% include gallery id="three_rowDS" %}

Here are a couple of snippets of the Diamond Square

{% include gallery id="two_rowSnipDS" %}
{% include gallery id="two_rowSnipDS1" %}

Finally I used cellular automata to produce the final terrain type, which was my favourite method to implement.

![Cellular Automata]({{ "/assets/UniWork/CellularSmoother.PNG" | relative_url }})

Here are a couple of snippets of the Cellular Automata

{% include gallery id="two_rowSnipCA" %}


![DiaSqu]({{ "/assets/UniWork/DiamondSquareImproved.PNG" | relative_url }})
![DiaSqu]({{ "/assets/UniWork/DiamondSquareRegularHills2.PNG" | relative_url }})
![DiaSqu]({{ "/assets/UniWork/DiamondSquareSand.PNG" | relative_url }})

