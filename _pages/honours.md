---
title: "Soft Body Dynamics - Honours"
permalink: /pages/honours
---

*My 4th year Honours project researching simulating soft-body dynamics in real-time.*

[Example Scripts]({{"https://github.com/LeSmurk/ExampleCode/tree/master/SoftBodiesHons"}}){: .btn .btn--primary .btn--large}

Using Spring/Mass principles, I attempted to simulate soft-body physics within a games context and therefore placing a focus on the performance of the simulation within real-time. While I used the Unity3D engine, I only used the collision and transform components that come with the engine to create the current Spring/Mass system as I then went onto researching how Entity Component Systems could be used to improve the performance of this soft body system. The dissertation I wrote can be found at the bottom of this page.

The video below demonstrates the feasibility of the Sping/Mass system, using a nearest neighbours approach to determine which masses are connected.
<iframe width="560" height="315" src="https://www.youtube.com/embed/e-H2lSZaFJc" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

This video shows the final product of the soft-body system using ECS to simulate the spring/mass principle, along with fixed neighbours.
<iframe width="560" height="315" src="https://www.youtube.com/embed/NaVvGqzRaIw" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

Full Dissertation Paper
<embed src="/assets/UniWork/Mark_Craigie_ECSSoftBodyDissertation.pdf" type="application/pdf" />
