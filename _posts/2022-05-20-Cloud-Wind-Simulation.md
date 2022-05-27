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
Observations and simulations have both shown us that galactic outflows contain individual "clouds", or small, dense regions of relatively cool material. In general, galactic winds are composed of several phases of gas, with a "hot" phase of $n\approx10^{-2.5}~\text{cm}^{-3}$ and $T\approx 10^{6.5}~\text{K}$ and a "cold" phase of $n\approx10^{2}~\text{cm}^{-3}$ and $T\approx 10^{2}~\text{K}$.

At face value, observations do not give us a clear picture of how clouds end up in outflows. Small, cool clouds moving at high velocities in a hot medium is an interesting picture from a dynamical point of view, considering that 
*Pressure equilibrium putting constraints on densities, however cold gas density profiles tend to follow hot gas profiles from observations for thermal pressure.*

Much work has been done to understand just how these cool clouds end up in the CGM, and how they're transported through outflows without being destroyed. Observations have shown cold clouds moving out of galaxies at high speeds, which is puzzling because of the timescales dense clouds of gas should be destroyed by hydrodynamic instabilities on. Using simulations, we're able to see how individual clouds are affected by their 

## Cloud Wind Dynamics
A simple process that we can study to use to understand how clouds evolve in outflows is an interaction between a shock wave and a spherical cloud. This study was originally done by the seminal work [Klein et al. (1994)](https://ui.adsabs.harvard.edu/abs/1994ApJ...420..213K/abstract), where 2D simulations were done for a variety of temperatures and densities, assuming no radiative losses, thermal conduction, magnetic fields, and gravity. While an over-simplistic study, this work was able to show that this problem could be fully characterized by the Mach number of the shock, and the ratio of cloud to background densities. The Mach number is simply the ratio of flow velocity to the speed of sound in the medium. The amount of time for a shock to cross through a cloud is called the cloud crushing time, and is defined as $t_{cc}=\chi^{1/2}a_0/v_b$, where $a_0$ is the cloud size and $v_b$ is the velocity of the shock. The key result of this work is that it takes several cloud crushing times for small clouds to be destroyed by shocks, so shocks are able to accelerate clouds to high velocities without destroying them, thus providing a model for cloud acceleration in winds.

## Cloud Wind Simulations
To study the process of dust evolution in winds, I'm making a simple simulation of a dusty cloud in a wind tunnel. The setup of that simulation will be a stationary, spherical cloud in a $1\times1\times2~\text{kpc}$ box with a wind boundary at the end closest to the cloud. This is a figure from a preliminary simulation I ran that is a simpler version of this setup, where instead of using a wind boundary, I added a background velocity of $200~\text{km/s}$ to medium.
![Desktop View](/assets/img/posts/gas.png){: width="589" height="357" style="max-width: 40%" .normal}
_Gas number density._
![Desktop View](/assets/img/posts/dust.png){: width="589" height="357" style="max-width: 40%" .normal}
_Dust number density._
![Desktop View](/assets/img/posts/velocity.png){: width="589" height="357" style="max-width: 40%" .normal}
_Gas velocity._