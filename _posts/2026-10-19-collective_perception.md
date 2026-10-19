---
layout: default
title: "Demonstrate collective perception improving safety"
date: 2026-10-18
---

![Collective Perception Main](/assets/img/collective_perception_main.jpg)

This post demonstrates the idea of Collective Perception in CARLA simulator.
Collective perception here works by sensor fusion from multiple vehicles
uses **pose graph** to reduce the sensor noise. A visualization of the sensor
fusion is showing in the "PGO" window in the demo.

In the first scenario, the pedestrian crossed the intersection from the blind
spot of the bottom vehicle, but fully visible from the top vehicle. With
collective perception enabled, both vehicle shares the view to avoid a potential
traffic accident.

[Scenario0](https://youtu.be/YPdnukJ_96M)


[Scenario1](https://youtu.be/YPdnukJ_96M)

[Scenario2](https://youtu.be/YPdnukJ_96M)


## Paper

To check the full detail see my [original
paper](https://ualberta.scholaris.ca/items/90413d7a-b9fb-4895-af9f-cf6dc32b531e).
