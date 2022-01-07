---
title:      Cholla's New Dust Model        # Title
author:     Helena Richie              # Author Name
date:       2021-11-30 09:55:42 -0500  # Date
categories: [Research]     # Catagories, no more than 2
tags:       [Dust, Numerical Methods, Hydrodynamics]  # Tags, any number
pin:        false                      # Should this post be pinned?
toc:        true                       # Table of Contents?
math:       true                      # Does this post contain math?
---
# Background
Lately, I've been working on adding a dust model to the [Cholla hydrodynamics code](https://github.com/cholla-hydro/cholla). Cholla currently uses its hydro capabilities to model gas, which is the largest fluid component of most galaxies. Dust, however, is another important fluid in galaxies that we can use hydrodynamics codes to study. At the moment, Cholla does not make any attempt to model dust in its simulations, but it can be incorporated it in a fairly straightforward way by treating dust as a passive scalar with its dynamics fully coupled to the gas. With this we can study how the scalar dust density evolves per cell based on local gas characteristics such as temperature and density. In reality, dust does not strictly follow the dynamics of gas in galaxies, so a later improvement of this model would be to create a particle-based treatment of dust that is free to flow independently. For now, though, we can learn a lot about how dust affects galaxies from this simple model.

Although dust is a relatively small contribution to the overall fluid content of galaxies, it is deeply intertwined with some of the most important processes that shape galaxy evolution. After forming in the late stages of stellar evolution, dust enriches a galaxy's insterstellar medium (ISM) and interacts with the gas in the medium. One significant property of galaxies that the presence of dust strongly affects is the gas cooling rate. Metal-line cooling is one of the most significant ways in which molecular gas cools enough for star formation to take place. However, dust accretes gas-phase metals, reducing the overall capacity for metal-line cooling. On the other hand, dust itself catalyzes the cooling rate of HII regions, so growth through gas-phase metal accretion enhances cooling in this sense. The balance between these two effects is one of the many important processes that an improved understanding of dust can inform on. In particular, knowing how the spatial distribution of dust evolves as it is created, destroyed, grown, and transported in galaxies would lead to major improvements in our understanding of these processes.

For a while, the spatial distribution of dust in and around galaxies has been a puzzle to astronomers. One source of confusion comes from our observations of dust in the circumgalactic medium (CGM). Although we know that dust does not originate in these regions, we have unmistakable evidence of significant amounts of dust in the CGMs of many galaxies (e.g. [Ménard et al. 2010](https://ui.adsabs.harvard.edu/abs/2010MNRAS.405.1025M/abstract)). This tels us that there must be some process that is responsible for transporting dust from where it is originally formed in the ISM into the CGM, and some popular explanations for this mechanism are outflows driven by stellar feedback and active galactic nuclei (AGN). These outflows, however, are very energetic and seem like they would destroy any dust contained in an outflow through a process called thermal sputtering. 

# Our Dust Model
To understand how dust would behave in a galactic outflow, the dust model that I'm adding to Cholla will account for the processes that would be signficant to dust in a wind, gas-phase metal accretion and thermal sputtering. These two processes cause dust to grow and get destroyed, respectively. To model these processes, I'm using differential equations for dust density that are adapted from the [McKinnon et al. (2016) paper](https://ui.adsabs.harvard.edu/abs/2016MNRAS.457.3775M/abstract) that introduces a dust model to the [Arepo](https://ui.adsabs.harvard.edu/abs/2010MNRAS.401..791S/abstract) code.

Dust can grow in size by accreting gas-phase metals of the same species, according to the following equation:
\\( \frac{d\rho_{i,\text{dust}}}{dt} = \Big(1-\frac{\rho_{i,\text{dust}}}{\rho_{i,\text{metal}}}\Big)\Big(\frac{\rho_{i,\text{dust}}}{\tau_g}\Big) \\).

 \\( \frac{d\rho_{i,\text{dust}}}{dt} = \frac{\rho_{i,\text{dust}}}{\tau_\text{sp}/3}. \\) A major difference between our handling of dust and that of the McKinnon et al. (2016) study cited above, and many other hydrodynamics codes used to model galaxy evolution, is that we are not using a sub-grid model to simulate supernova shocks. Cholla was designed to run on massively parallel, GPU-based architecures, allowing us to create simulations resolved down to parsec scales, where we can resolve the dust physics that many other simulations miss.

Because of this, Cholla is uniqely positioned to address many of the open questions perataining to the effects of dust on galaxy evolution. For example, it is well known through observation that dust exists in the circumgalactic medium (CGM) of galaxies. However, simulations suggest that the mechanisms that transport dust from within galaxies where it is formed to the CGM should destroy dust. Since Cholla can observe the scales at which dust is expected to be destroyed through thermal sputtering, I will address this question by creating a simple simulation of a galactic wind an studying how dust evolves.

# Model Testing
To test this model, I'm creating a Python version of the numerical solutions to the differential equations we're using to model the processes of gas-phase metal accretion and thermal sputtering shown above. The sputtering equation has a simple analytic solution that we can compare with our numerical solution, as is shown below.

![Sputtering Analytic Solution](/assets/img/posts/sputtering_numerical.png)

The timescale for sputtering to occur depends on gas temperature, so for cooler gas sputtering has little effect on the dust content of a fluid. However, in higher temperature gas (like \\(T=10^5~K\\) and up), sputtering becomes important at around \\(T=10^8~\text{kyr}\\) and even sooner for higher temperatures.

With gas-phase metal accretion, the picture is not as simple. In general, gas-phase metal accretion is a non-linear process that depends on a balance of processes. [Draine et al. (1990)](https://ui.adsabs.harvard.edu/abs/1990ASPC...12..193D/abstract) describes accretion as a process 