---
title:      Dust Model Testing        # Title
author:     Helena Richie              # Author Name
date:       2021-11-30 09:55:42 -0500  # Date
categories: [Research]     # Catagories, no more than 2
tags:       [Dust, Numerical Methods, Hydrodynamics]  # Tags, any number
pin:        false                      # Should this post be pinned?
toc:        true                       # Table of Contents?
math:       true                      # Does this post contain math?
---
# Background
Lately, I've been working on adding a dust model to the [Cholla hydrodynamics code](https://github.com/cholla-hydro/cholla). Cholla currently uses its hydro capabilities to model gas, which is the largest fluid component of most galaxies. Dust, however, is another important fluid component in galaxies that we can use hydrodynamics codes to study. At the moment, Cholla does not make any attempt to model dust in its simulations, but we can incorporate it in a fairly straightforward way by treating dust as a passive scalar with its dynamics fully coupled to the gas. Then, we can study how the scalar dust density evolves per cell based on other cell quantities such as temperature and gas density. In reality, dust does not strictly follow the dynamics of gas in galaxies, so a later improvement of this model would be to create a particle-based treatment of dust that is free to flow on its own. For now, though, we can learn a lot about how dust affects galaxies from this simple model.

Although dust is a relatively small contribution to the overall fluid content of galaxies, it is deeply intertwined in many of the most important processes that shape galaxy evolution. After forming in the late stages of stellar evolution, dust enriches the insterstellar medium (ISM) and interacts with the other components of the galaxy. One very significant property of galaxies that the presence of dust affects is the gas cooling rate. Metal-line cooling is one of the most significant ways in which molecular gas cools enough for star formation to occur. However, dust accretes gas-phase metals, reducing the capacity for gas to cool. On the other hand, dust itself catalyzes the cooling of HII regions. Understanding the distribution of dust in galaxies will inform our understanding of this balance and its affects on star formation. To make predictions of the spatial distribution of dust in galaxies, we must account for the various processes that create, destroy, grow, and transport dust in galaxies. Once dust gets in the ISM, it interacts with and affects processes in galaxies, like star formation.

Despite its importance in galaxy evolution, there are many open questions pertaining to dust among astronomers. In particular, we have extensive observations of large amounts of dust in the circumgalactic media (CGMs) of galaxies (e.g. [Ménard et al. 2010](https://ui.adsabs.harvard.edu/abs/2010MNRAS.405.1025M/abstract)), which is puzzling because we know that dust does not originate from these regions. Some plausible ways in which dust could be transported from the ISM where it originates into the CGM is through outflows driven by stellar radiation pressure or active galactic nuclei (AGN).
There are some proposals that stellar radiation pressure can drive some amounts of dust outside of galaxy ISMs, where it is formed, as well as nuclear outflows. These outflows, however, are very energetic and seem like they would destroy any constituent dust through thermal sputtering. 

# Our Dust Model
To incorporate these effects into our isolated galaxy simulations, I'm developing a model that is adapted from the [McKinnon et al. (2016) paper](https://ui.adsabs.harvard.edu/abs/2016MNRAS.457.3775M/abstract) that introduces a simple dust model to the [Arepo](https://ui.adsabs.harvard.edu/abs/2010MNRAS.401..791S/abstract) code. In this model, we are treating dust as a fluid that is fully coupled to the dynamics of the existing gas, so dust density is simply a passive scalar that depends on the gas density and temperature. 
This model accounts for how dust density changes due to the processes of gas-phase metal accretion and thermal sputtering and are modeled by the following equations:  
\\( \frac{d\rho_{i,\text{dust}}}{dt} = \Big(1-\frac{\rho_{i,\text{dust}}}{\rho_{i,\text{metal}}}\Big)\Big(\frac{\rho_{i,\text{dust}}}{\tau_g}\Big) \\)
and \\( \frac{d\rho_{i,\text{dust}}}{dt} = \frac{\rho_{i,\text{dust}}}{\tau_\text{sp}/3}. \\) A major difference between our handling of dust and that of the McKinnon et al. (2016) study cited above, and many other hydrodynamics codes used to model galaxy evolution, is that we are not using a sub-grid model to simulate supernova shocks. Cholla was designed to run on massively parallel, GPU-based architecures, allowing us to create simulations resolved down to parsec scales, where we can resolve the dust physics that many other simulations miss.

Because of this, Cholla is uniqely positioned to address many of the open questions perataining to the effects of dust on galaxy evolution. For example, it is well known through observation that dust exists in the circumgalactic medium (CGM) of galaxies. However, simulations suggest that the mechanisms that transport dust from within galaxies where it is formed to the CGM should destroy dust. Since Cholla can observe the scales at which dust is expected to be destroyed through thermal sputtering, I will address this question by creating a simple simulation of a galactic wind an studying how dust evolves.

# Model Testing
To test this model, I'm creating a Python version of the numerical solutions to the differential equations we're using to model the processes of gas-phase metal accretion and thermal sputtering shown above. The sputtering equation has a simple analytic solution that we can compare with our numerical solution, as is shown below.

![Sputtering Analytic Solution](/assets/img/posts/sputtering_numerical.png)

The timescale for sputtering to occur depends on gas temperature, so for cooler gas sputtering has little effect on the dust content of a fluid. However, in higher temperature gas (like \\(T=10^5~K\\) and up), sputtering becomes important at around \\(T=10^8~\text{kyr}\\) and even sooner for higher temperatures.

With gas-phase metal accretion, the picture is not as simple. In general, gas-phase metal accretion is a non-linear process that depends on a balance of processes. [Draine et al. (1990)](https://ui.adsabs.harvard.edu/abs/1990ASPC...12..193D/abstract) describes accretion as a process 