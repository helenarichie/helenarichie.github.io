---
title:      Modeling Dust Sputtering       # Title
author:     Helena Richie              # Author Name
date:       2023-01-18 12:00:42 -0500  # Date
categories: [Research, Dust Model]     # Catagories, no more than 2
tags:       [Cholla, Dust, Sputtering]  # Tags, any number
pin:        false                      # Should this post be pinned?
toc:        true                       # Table of Contents?
math:       true                      # Does this post contain math?
---

# Sputtering

To tackle the question of how dust is tranported in galactic winds, I've been thinking about the primary mechanism that destroys dust in galaxies, sputtering. Sputtering shrinks dust grains, as the individual atoms that are bound to it are knocked off by incoming energetic ions. After enough of these interactions have taken place, dust grains can be destroyed entirely.

![Sputtering Schematic](/assets/img/posts/sputtering.tiff)

Although the theory of this process is fairly well understood, it is quite complex. As such, modeling sputtering in our hydrodynamics simulation is a challenge. 

\\( \frac{da}{dt} = -\frac{m_x}{4\rho} \sum_i n_i \int_{E_{\text{min}}^\inf \Big(\frac{2E}{m_i}\Big)^{1/2}\Big(1-\frac{Z_ieU}{E}\Big)Y_\text{sput}(E-Z_ieU) \\).