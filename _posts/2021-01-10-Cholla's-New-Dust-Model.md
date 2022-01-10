---
title:      Cholla's New Dust Model        # Title
author:     Helena Richie              # Author Name
date:       2021-01-10 09:55:42 -0500  # Date
categories: [Research]     # Catagories, no more than 2
tags:       [Dust, Numerical Methods, Hydrodynamics, Winds]  # Tags, any number
pin:        false                      # Should this post be pinned?
toc:        true                       # Table of Contents?
math:       true                      # Does this post contain math?
---
# Background
Lately, I've been working on adding a dust model to the [Cholla hydrodynamics code](https://github.com/cholla-hydro/cholla). Cholla currently uses its hydro capabilities to model gas, which is the largest fluid component of most galaxies. Dust, however, is another important fluid in galaxies that we can use hydrodynamics to study. As I'll discuss in more detail later in this post, the impacts of including dust in simulations can be huge. At the moment, Cholla does not make any attempt to model dust in its simulations, but it can be incorporated in a fairly straightforward way by treating dust density as a passive scalar with its dynamics fully coupled to the gas. With this, we can study how the density evolves per cell based on local gas characteristics such as temperature and density. In reality, dust does not strictly follow the dynamics of gas in galaxies, so a later improvement of this model would be to create a particle-based treatment of dust that is free to flow independently. For now, though, we can learn a lot about how dust affects galaxies from this simple model.

## Why Dust?
Although dust is a relatively small contribution to the overall fluid content of galaxies, it is deeply intertwined with some of the most important processes that shape galaxy evolution. After forming in the late stages of stellar evolution, dust enriches a galaxy's interstellar medium (ISM) and interacts with the gas in that medium. One significant property of galaxies that the presence of dust strongly affects is the gas cooling rate ([Vogelsberger et al. 2019](https://ui.adsabs.harvard.edu/abs/2019MNRAS.487.4870V/abstract) and references therein). Metal-line cooling is one of the most significant ways in which molecular gas cools enough for star formation to take place. However, the presence of dust reduces the gas' overall capacity for metal-line cooling by accreting its gas-phase metals. On the other hand, dust itself catalyzes the formation of HII, so it enhances the cooling rate at the same time. The balance between these two effects is one of the many important processes that an improved understanding of dust can inform on. In particular, knowing how the spatial distribution of dust evolves as it is created, destroyed, grown, and transported in galaxies would lead to major improvements in our understanding of these processes.

For a while, the spatial distribution of dust in and around galaxies has been a puzzle to astronomers. One source of confusion comes from our observations of dust in the circumgalactic medium (CGM) of galaxies. Although we know that dust does not originate in these regions, we have unmistakable evidence of significant amounts of dust in the CGMs of many galaxies (e.g. [Ménard et al. 2010](https://ui.adsabs.harvard.edu/abs/2010MNRAS.405.1025M/abstract)). This tells us that there must be some mechanism that is responsible for transporting dust from where it is originally formed in the ISM into the CGM, and some popular explanations for this process are outflows driven by stellar feedback and/or active galactic nuclei (AGN) ([Kannan et al. 2020](https://ui.adsabs.harvard.edu/abs/2020MNRAS.499.5732K/abstract)). These outflows, however, are very energetic and seem like they would destroy any dust contained in an outflow through thermal sputtering.

It's hard to determine what's going on from observations alone, so simulations are being used to address this question, and some have even shown that these outflows are a viable transport mechanisms ([Aoyama et al. 2018](https://ui.adsabs.harvard.edu/abs/2018MNRAS.478.4905A/abstract)). Galactic winds, however, are known to be multi-phase, with structure existing on scales smaller than the resolutions of most simulation codes, so simulation results are often not entirely consistent with observations (e.g. [Hirashita et al. 2021](https://ui.adsabs.harvard.edu/abs/2021MNRAS.505.1794H/abstract)). Cholla is uniquely positioned to answer this question because of its massively parallel nature, which allows us to resolve physics that takes place on parsec-scales. Using this new dust model, Cholla simulations will give us our first real insight into what happens to dust when it's transported in a galactic wind.

# Our Dust Model
To understand how dust would behave in a galactic wind, the dust model that I'm writing for Cholla will account only for the processes that would be significant to dust in this environment: gas-phase metal accretion and thermal sputtering. These two processes cause dust to grow and get destroyed, respectively. To model these mechanisms, I'm using differential equations for dust density that are adapted from the [McKinnon et al. (2016)](https://ui.adsabs.harvard.edu/abs/2016MNRAS.457.3775M/abstract) and [McKinnon et al. (2017)](https://ui.adsabs.harvard.edu/abs/2017MNRAS.468.1505M/abstract) papers that introduce a dust model to the [Arepo code](https://ui.adsabs.harvard.edu/abs/2010MNRAS.401..791S/abstract).

## Gas-Phase Metal Accretion
Dust grows in size by accreting gas-phase metals of the same species, \\( i \\), according to the following equation:

\\( \frac{d\rho_{i,\text{dust}}}{dt} = \Big(1-\frac{\rho_{i,\text{dust}}}{\rho_{i,\text{metal}}}\Big)\Big(\frac{\rho_{i,\text{dust}}}{\tau_g}\Big) \\).

Here, \\( \tau_g \\) is the growth timescale for dust, and scales inversely with total density and temperature. The accretion rate depends on the dust-to-metal ratio of the cell, and slows as metals are depleted onto dust. This eventually causes accretion to come to a halt. For now, we're assuming constant solar metallicity, so we'll just calculate the total percentage of metals in the gas based on that and forego the index \\( i \\).

## Thermal Sputtering
The other main process that dust undergoes in a wind is thermal sputtering, which is when an energetic particle collides with a dust molecule and destroys it. This process is modeled by the following equation:

 \\( \frac{d\rho_{i,\text{dust}}}{dt} = -\frac{\rho_{i,\text{dust}}}{\tau_\text{sp}/3} \\).

The sputtering timescale, \\( \tau_\text{sp} \\), depends only on gas temperature, and decreases as gas temperature increases. In this model, dust sputters away exponentially over time until it has been depleted entirely.

# Model Testing
To test this model, I wanted create a Python version of the numerical method I'll be applying to these equations in Cholla. The code that I wrote for this can be found [here](https://github.com/helenarichie/research/tree/master/cholla/dust_model). To integrate the dust model equations, I used the forward-Euler method,

\\( \rho_{n+1}=\rho_n+dt\cdot f(\rho_n, t) \\),

where \\( dt \\) is the integration time-step and \\( f(\rho_n, t) \\) is the right hand side of the accretion or sputtering differential equations given above. The sputtering equation has a well-known analytical solution, so I was able to compare the numerical and analytical solutions directly, as is shown in the following figure:

![Sputtering Analytic Solution](/assets/img/posts/sputtering_numerical.png)

Here, the solid lines show the analytical solution and the dashed lines show the numerical solution. The timescale for sputtering to occur depends on gas temperature, so for cooler gas sputtering has little effect on the dust content of a fluid. However, in higher temperature gas (like \\( T=10^5~K \\) and up), sputtering becomes important at around \\( T=10^8~\text{kyr} \\) and even sooner for higher temperatures. In general, on the time-scales we're interested in, sputtering only takes place in the hottest gas, as expected.

For gas-phase metal accretion, the forward-Euler solution gave the following evolution of density:

![Accretion Analytic Solution](/assets/img/posts/accretion_numerical.png)


With gas-phase metal accretion, the picture is not as simple. In general, gas-phase metal accretion is a non-linear process that depends on a balance of processes. [Draine et al. (1990)](https://ui.adsabs.harvard.edu/abs/1990ASPC...12..193D/abstract) describes accretion as a process 