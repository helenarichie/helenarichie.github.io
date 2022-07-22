---
title:      Wind Boundary Testing       # Title
author:     Helena Richie              # Author Name
date:       2022-07-22 12:00:42 -0500  # Date
categories: [Research, Dusty Cloud Wind Simulation]     # Catagories, no more than 2
tags:       [Cholla, Clouds, Simulations, Hydrodynamics, Winds]  # Tags, any number
pin:        false                      # Should this post be pinned?
toc:        true                       # Table of Contents?
math:       true                      # Does this post contain math?
---

<div style="padding:100% 0 0 0;position:relative;"><iframe src="https://player.vimeo.com/video/732549755?h=9a05329233&amp;badge=0&amp;autopause=0&amp;player_id=0&amp;app_id=58479" frameborder="0" allow="autoplay; fullscreen; picture-in-picture" allowfullscreen style="position:absolute;top:0;left:0;width:100%;height:100%;" title="cloud-wind-072222"></iframe></div><script src="https://player.vimeo.com/api/player.js"></script>

<br>I'm working on developing code for a boundary condition that sets the -x boundary of my simulation to a wind of constant velocity. This video shows slices of a simulation I made with this wind boundary set to 100$~\text{km}\text{s}^{-1}$ in the +x direction. The cloud has a radius of 0.1$~\text{kpc}$ and sits in a 2$\times$1$\times$1$~\text{kpc}^3$ tunnel. The grid size is 256$\times$128$\times$128$~\text{pix}^3$, so the resolution is around 7.8$~\text{pc}/\text{pix}$.