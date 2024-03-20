---
title:      Dust in Cholla       # Title
author:     Helena Richie              # Author Name
date:       2022-01-10 09:55:42 -0500  # Date
categories: [Research, Dust]     # Catagories, no more than 2
tags:       [Cholla, Dust, Numerical Methods, CGM]  # Tags, any number
pin:        false                      # Should this post be pinned?
toc:        true                       # Table of Contents?
math:       true                      # Does this post contain math?
---
# Background
I am working on adding a dust model to the grid-based [Cholla hydrodynamics code](https://github.com/cholla-hydro/cholla). Cholla currently uses its hydro capabilities to model gas, which is the primary fluid component of galaxies. Dust, however, is another important element in galaxies that we can use hydrodynamics to study. At the moment, Cholla is dust-free. However, dust can be incorporated in a fairly straightforward way by taking advantage of Cholla's passive scalar feature. By modeling dust as a scalar fluid element that is advected with gas we are treating dust as a fluid that is fully dynamically coupled to gas. This is a good assumption time when the drag time is short, resulting in a small Stokes number ( \\( \text{Stk}\ll1 \\) ). In cases where \\( \text{Stk}\gg1 \\) (when the grain radius is large, the sound speed is slow, etc.), a two-fluid treatment of dust is necessary. With this model, we can study the effects of outflow gas properties, such a density and temperature, on the evolution dust.

## Why Dust?
Although dust is a small component of the overall masses of galaxies, it is deeply entwined with some of the most important processes that shape galaxy evolution. After forming in the late stages of stellar evolution, dust enriches the interstellar medium (ISM). Once in the ISM, dust interacts with the gas that stars form from in a number of ways. For example, the gas cooling rate is affected by the presence of dust (see e.g. [Vogelsberger et al. 2019](https://ui.adsabs.harvard.edu/abs/2019MNRAS.487.4870V/abstract) and references therein). Metal-line cooling allows molecular gas to become cold enough for stars to form, but dust regulates the total available gas-phase metals in the ISM, therefore regulating the cooling rate. On the other hand, dust catalyzes the formation of \\( H_2 \\), helping to create more fuel for stars to form. These are just two of the many key processeses in galaxy evolution that an improved understanding of dust evolution in galaxies can help us understand. From an observational standpoint, dust is also extremely significant. Dust freqently shows up in our observations in the form of redenning, extinction, and emission. An understanding of how the spatial distribution of dust evolves as it is created, destroyed, grown, and transported thoughout galaxies is needed to understand these phenomena.

The distribution of dust in and around galaxies has been a puzzle to astronomers. One reason for this is the observed ubiquity of dust in the circumgalactic medium (CGM). Although we know that dust does not originate in these regions, we have unmistakable evidence of significant amounts of dust in the CGMs of numerous galaxies (e.g. [Ménard et al. 2010](https://ui.adsabs.harvard.edu/abs/2010MNRAS.405.1025M/abstract)). This tells us that there must be some mechanism that is responsible for transporting dust from where it is originally formed in the ISM into the CGM. Explanations for this process include outflows driven by stellar feedback and/or active galactic nuclei (AGN) ([Kannan et al. 2020](https://ui.adsabs.harvard.edu/abs/2020MNRAS.499.5732K/abstract)), which are well-known as sinks of the overall gas content in galaxies. These outflows, however, consist (by volume) largely of hot gas--conditions which are not amenable to dust survival.

It's hard to understand the ability of outflows to trasnport dust out of galaxies since they only show us a snapshot in time of dusty outflows. Simulations are valuable tools to address this question, since they allow us to watch dust's evolution as it unfolds. Some simulations have begun to explore dust as a transport mechanism ([Aoyama et al. 2018](https://ui.adsabs.harvard.edu/abs/2018MNRAS.478.4905A/abstract)). Galactic winds, however, are known to be multi-phase, with structure existing on scales smaller than the simulation resolution, which can lead to results that are inconsistent with observations. Cholla is uniquely positioned to answer this question because it is used to simulate relatively small scales at high resolution. Simulating the evolution of dust in a resolved, multi-phase outflow can enable improvements in sub-grid models for dust evolutions in simulations that do not fully resolve the phase strucutre of outflows.

# Our Dust Model
To understand how dust would behave in a galactic wind, the dust model that I am implementing in Cholla accounts for gas-phase metal accretion and thermal sputtering. These two processes cause dust to grow and get destroyed, respectively. The model equations I am using are adapted from the [McKinnon et al. (2016)](https://ui.adsabs.harvard.edu/abs/2016MNRAS.457.3775M/abstract) and [McKinnon et al. (2017)](https://ui.adsabs.harvard.edu/abs/2017MNRAS.468.1505M/abstract) papers that introduce a dust model to the [Arepo code](https://ui.adsabs.harvard.edu/abs/2010MNRAS.401..791S/abstract).

## Gas-Phase Metal Accretion
Dust grows in size by accreting gas-phase metals of the same species, \\( i \\), according to the following equation:

\\( \frac{d\rho_{i,\text{dust}}}{dt} = \Big(1-\frac{\rho_{i,\text{dust}}}{\rho_{i,\text{metal}}}\Big)\Big(\frac{\rho_{i,\text{dust}}}{\tau_g}\Big) \\).

Here, \\( \tau_g \\) is the growth timescale for dust, and scales inversely with total density and temperature. The accretion rate depends on the dust-to-metal ratio of the cell, and slows as metals are depleted onto dust. This eventually causes accretion to come to a halt. For now, we're assuming constant solar metallicity, so we'll just calculate the total percentage of metals in the gas based on that and forego the index \\( i \\).

**Useful references:** 
Density-dependent time-scale: [Draine et al. (1990)](https://ui.adsabs.harvard.edu/abs/1990ASPC...12..193D/abstract), [Hirashita (2000)](https://ui.adsabs.harvard.edu/abs/2000PASJ...52..585H/abstract)

Density and temperature-dependent time-scale: [Yozin & Bekki (2014)](https://ui.adsabs.harvard.edu/abs/2014MNRAS.443..522Y/abstract)

Metal depletion due to dust grains: [Dwek & Scalo (1980)](https://ui.adsabs.harvard.edu/abs/1980ApJ...239..193D/abstract), [McKee (1989)](https://ui.adsabs.harvard.edu/abs/1989IAUS..135..431M/abstract)

## Thermal Sputtering
The other main process that dust undergoes in a wind is thermal sputtering, which is when an energetic particle collides with a dust molecule and destroys it. This process is modeled by the following equation:

 \\( \frac{d\rho_{i,\text{dust}}}{dt} = -\frac{\rho_{i,\text{dust}}}{\tau_\text{sp}/3} \\).

The sputtering timescale, \\( \tau_\text{sp} \\) , depends only on gas temperature, and decreases as gas temperature increases. In this model, dust sputters away exponentially over time until it has been depleted entirely.

**Useful references:** [Draine & Salpeter (1979a)](https://ui.adsabs.harvard.edu/abs/1979ApJ...231...77D/abstract), [Draine & Salpeter (1979b)](https://ui.adsabs.harvard.edu/abs/1979ApJ...231..438D/abstract)

# Model Testing
To test this model, I wanted create a Python version of the numerical method I'll be applying to these equations in Cholla. The code that I wrote for this can be found [here](https://github.com/helenarichie/research/tree/master/cholla/dust_model). The plots below assume a gas number density of \\( n=10^{-2}\\). To integrate the dust model equations, I used the forward-Euler method,

\\( \rho_{n+1}=\rho_n+dt\cdot f(\rho_n, t) \\),

where \\( dt \\) is the integration time-step and \\( f(\rho_n, t) \\) is the right hand side of the accretion or sputtering differential equations given above. 

## Sputtering
The sputtering equation has a well-known analytical solution, so I was able to compare the numerical and analytical solutions directly, as is shown in the following figure:

![Sputtering Analytic Solution](/assets/img/posts/sputtering_numerical.png)

Here, the solid lines show the analytical solution and the dashed lines show the numerical solution. The timescale for sputtering to occur depends on gas temperature, so for cooler gas, sputtering has little effect on the dust content of a fluid. However, in higher temperature gas (\\( \sim T=10^5~K \\) and up), sputtering becomes important at around \\( T=10^4~\text{yr} \\) and later for lower temperatures. In general, on the time-scales that we're interested in, sputtering only takes place in the hottest gas.

## Accretion
For gas-phase metal accretion, the forward-Euler solution gave the following evolution of density:

![Accretion Analytic Solution](/assets/img/posts/accretion_numerical.png)

In general, we see that higher temperature gases tend to have dust that grows more quickly. If we were to compare gases of different densities, we would see the trend that higher-density gases also accrete more quickly. These trends are both a result of the growth time-scale, originally introduced by [Draine et al. (1990)](https://ui.adsabs.harvard.edu/abs/1990ASPC...12..193D/abstract), and approximated by [Hirashita (2000)](https://ui.adsabs.harvard.edu/abs/2000PASJ...52..585H/abstract) to reflect typical values of atom-grain collision sticking efficiency and grain cross-section. Further studies, such as [Yozin & Bekki (2014)](https://ui.adsabs.harvard.edu/abs/2014MNRAS.443..522Y/abstract) have modified this time-scale to account for temperature in addition to density, giving the form we see in [McKinnon et al. (2016)](https://ui.adsabs.harvard.edu/abs/2016MNRAS.457.3775M/abstract). These curves all converge to a dust density that is \\( \sim60\% \\) of the initial dust density, following the result of [Dwek & Scalo (1990)](https://ui.adsabs.harvard.edu/abs/1980ApJ...239..193D/abstract).