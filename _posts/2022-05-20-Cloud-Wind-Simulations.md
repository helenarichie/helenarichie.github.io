---
title:      Cloud-Wind Simulations       # Title
author:     Helena Richie              # Author Name
date:       2022-05-20 12:00:42 -0500  # Date
categories: [Research, Wind Tunnel Simulations]     # Catagories, no more than 2
tags:       [Cholla, Dust, Wind Tunnel Simulations, Hydrodynamics]  # Tags, any number
pin:        false                      # Should this post be pinned?
toc:        true                       # Table of Contents?
math:       true                      # Does this post contain math?
---
# Simulating Dusty Clouds With Cholla

## Cloud-Wind Dynamics
The dynamics of an interaction between a cool, dense, spherical cloud and a warmer or hot planar shock is a well-studied problem. The seminal paper by [Klein et al. (1994)](http://adsabs.harvard.edu/doi/10.1086/173554) outlines a study of this problem in two dimensions, ignoring radiative losses, thermal conduction, magnetic fields, and gravitational forces. While certainly an oversimplification for astrophysical applications, this formulation provides useful insight into the problem of cloud-wind interactions.<br>

This work showed that small clouds are destroyed in several "cloud crushing times," $t_{cc}$. A cloud crushing time is defined as the amount of time it takes for a shock to cross through a cloud, $t_{cc}=\chi^{1/2}a/v$, where $a$ is the initial radius of the spherical cloud and $v$ is the speed of the shock wave in the intercloud medium. $\chi$ is the ratio between the densities of the cloud and medium in which it sits. The Mach number can be used to characterize the strength of a shock, which is defined as the ratio of the local flow velocity in the intercloud medium and the speed of sound in the medium, $M=v/c$. For a strong shock, $M\gg1$. The speed of sound depends on the pressure, $P$, the density, $\rho$, and the ratio of specific heats in the cloud, $\gamma$;  $c=(\gamma P/\rho)^{1/2}$. That said, before a shock enters the cloud, its local sound speed is smaller than the intercloud medium by a factor of $\chi^{1/2}$. The constraint that this result applies to small clouds assumes that the pressure behind the shock wave in the intercloud medium is constant. In particular, small clouds are defined by $t_{cc}\ll t_P$, which is the timescale for pressure to change substantially.<br>

Looking at the largest level of detail of this interaction, the cloud is accelerated in two stages. First, the cloud shock accelerates the cloud to the "typical value" of the speed of propagation of the shock within the cloud, $v_s$. Then the intercloud gas accelerates the cloud further until it is comoving with the shocked intercloud gas. The finer details that occur are lateral expansion of the cloud after being shocked, Kelvin-Helmholtz and Rayleigh-Taylor instabilities between the cloud and the medium that grow with time. By relating the growth timescales of these instabilities to the cloud crushing time, we are able to determine that cloud destruction time can be characterized by cloud crushing time, and that the total amount of time for the cloud to be destroyed will be a few times $t_{cc}$.<br>

## Cloud-Wind Simulations

I am working to understand the ability of galactic outflows to transport dust out of galaxies, so I am interested in the evolution of individual dusty clouds as they're accelerated by galactic winds. In particular, if dust can remain shielded by clouds as they become entrained in galactic winds, its survivability can benefit from shielding from the hot gas that comrpises winds. We can use these idealized wind tunnel simulations to gain insight into this problem. I am running a series of cloud-wind simulations using the dust sputtering model described in a [previous post](https://helenarichie.github.io/posts/Dust-in-Cholla/), with a range of cloud sizes, wind speeds, wind temperature, dust grain sizes, etc. to understand the factors that dust survival in outflows depend on. Here, I'll describe a few of the test simulations that I ran to explore this setup. Unlike in the adiabatic case described above, these simulations include radiative cooling, which has been shown to extend the lifetimes of clodus from a few times $t_{cc}$ (see e.g. [Gronke et al. 2018](https://ui.adsabs.harvard.edu/abs/2018MNRAS.480L.111G/abstract)). I'm also using a relatively small box and periodic boundaries, which can cause the cloud to get jumbled up at late times.


I started with a cloud of radius 0.1$~\text{kpc}$ in a 2$\times$1$\times$1$~\text{kpc}^3$ tunnel. I used a grid size of 256$\times$128$\times$128$~\text{pix}^3$, so our resolution was around 7.8$~\text{pc}/\text{pix}$. To emulate the environment of an outflow, the cloud's initial temperature was $T_{cl}=1\times 10^4~\text{K}$ and the background was set to $T_{bg}=3\times 10^6~\text{K}$, which correspond to the typical temperatures of the warm ionized medium and coronal gas in galaxies, respectively. The number densities of the cloud and background were $n_{cl}=5.4\times 10^{-2}~\text{cm}^{-3}$ and $n_{bg}=1.68\times 10^{-4}~\text{cm}^{-3}$, which puts $\chi$ at $10^{2}$. To create the wind tunnel, I applied a velocity of $10~\text{km}/\text{s}$ in the x-direction to the background gas, which is quite slow for galactic contexts. The figures below show a projection of the average gas and dust densities given these initial conditions (and an initial dust-to-gas ratio of 1:100).<br>

![Desktop View](/assets/img/posts/gas.png){: width="589" height="357" style="max-width: 40%" .normal}
![Desktop View](/assets/img/posts/dust.png){: width="589" height="357" style="max-width: 40%" .normal}

For this cloud, the cloud crushing time is $t_{cc}=\chi^{1/2}a_0/v_b=9.8\times10^{7}~\text{yr}$, with $a_0=0.1~\text{kpc}$ being the radius of the cloud and $v_b=10~\text{km}/\text{s}$ is the speed of the wind. The below plot shows the evolution of dust-to-gas ratio throughout the simulation.<br>

![Desktop View](/assets/img/posts/dtgr.png){: width="589" height="357" style="max-width: 40%" .normal}

Here, we see some change in dust-to-gas ratio over time at the boundaries, but not a ton. Looking at a slice of the temperature of the simulation could shed some light on how the dust density should be changing.<br>

![Desktop View](/assets/img/posts/temp.png){: width="589" height="357" style="max-width: 40%" .normal}

Here, we can see that the central temperature of the cloud isn't changing too rapidly, so the inside of the cloud is staying at a of around $10^4~\text{K}$. At this temperature, dust has a sputtering timescale that is comparable to or longer than the time of the simulation, so it makes sense that we wouldn't see too much change in the dust density.