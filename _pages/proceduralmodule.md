---
title: "Procedural Module"
permalink: /pages/proceduralmodule

two_row:
  - image_path: /assets/UniWork/DiamondSquareImproved.PNG
    alt: "placeholder image 0"

  - image_path: /assets/UniWork/DiamondSquareRegularHills2.PNG
    alt: "placeholder image 1"
    
  - image_path: /assets/UniWork/DiamondSquareSand.PNG
    alt: "placeholder image 2"
    
---
*3rd year procedural generation module within Directx11*

I began by creating a simple Perlin noise terrain, by converting Ken Perlin's original algorithm into C++ and then adding environmental texturing through the use of a pixel shader.
The same Perlin noise was also used in conjunction with a compound sine wave to create the water that is seen in all the images.

![PerlinNoise]({{ "/assets/UniWork/PerlinEnviroTex.PNG" | relative_url }})

I then developed a more complex type of terrian, using the Diamond-Square algorithm, which created the outputs seen below.

{% include gallery id="two_row" %}

Finally I used cellular automata to produce the final terrain type, which was my favourite method to implement.

![Cellular Automata]({{ "/assets/UniWork/CellularSmoother.PNG" | relative_url }})

