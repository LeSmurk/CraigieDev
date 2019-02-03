---
title: "Procedural Module"
permalink: /pages/proceduralmodule/
galleryDS:
  - image_path: /assets/UniWork/DiamondSquareImproved.PNG
    alt: "placeholder image 0"
  - image_path: /assets/UniWork/DiamondSquareRegularHills2.PNG
    alt: "placeholder image 1"    
  - image_path: /assets/UniWork/DiamondSquareSand.PNG
    alt: "placeholder image 2"
---


title: "Helpers"
permalink: /pages/proceduralmodule/
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

