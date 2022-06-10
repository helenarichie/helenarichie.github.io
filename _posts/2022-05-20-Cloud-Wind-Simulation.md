---
title:      Cloud Wind Simulation       # Title
author:     Helena Richie              # Author Name
date:       2022-05-20 12:00:42 -0500  # Date
categories: [Research]     # Catagories, no more than 2
tags:       [Cholla, Dust, Simulations, Hydrodynamics, Winds]  # Tags, any number
pin:        false                      # Should this post be pinned?
toc:        true                       # Table of Contents?
math:       true                      # Does this post contain math?
---
# Simulating Dusty Clouds With Cholla

## Cloud Wind Dynamics


## Cloud Wind Simulations
To study how dust evolves in galactic outflows, we first turn to the simple problem of dust transport in an isolated wind simulation. I started with a cloud of radius 0.1$~\text{kpc}$ in a 2$\times$1$\times$1$~\text{kpc}^3$ tunnel. I used a grid size of 256$\times$128$\times$128$~\text{pix}^3$, so our resolution was around 7.8$~\text{pc}/\text{pix}$.<br>

To emulate the environment of an outflow, the cloud's initial temperature was $T_{cl}=1\times 10^4~\text{K}$ and the background was set to $T_{bg}=3\times 10^6~\text{K}$, which correspond to the typical temperatures of the warm ionized medium and coronal gas in galaxies, respectively. The number densities of the cloud and background were $n_{cl}=5.4\times 10^{-2}~\text{cm}^{-3}$ and $n_{bg}=1.68\times 10^{-4}~\text{cm}^{-3}$, so in the language of Klein et al. (1994), this would put $\chi$ at $10^{-2}$, which is another typically observed value for warm ionized media embedded in coronal gas.<br>

To create the wind tunnel, I applied a velocity of $10~\text{km}/\text{s}$ in the x-direction to the background gas. The upper/lower and side boundaries in this simulation were transmissive and the left and right boundaries were periodic, so after a while you can see the cloud return to the left side of the tunnel. The figures below show a projection of the average gas and dust densities given these initial conditions (and an initial dust-to-gas ratio of 1:100).<br>

![Desktop View](/assets/img/posts/gas.png){: width="589" height="357" style="max-width: 40%" .normal}
![Desktop View](/assets/img/posts/dust.png){: width="589" height="357" style="max-width: 40%" .normal}
<br>
