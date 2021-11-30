---
title:      Dust Model Testing        # Title
author:     Helena Richie              # Author Name
date:       2021-11-30 09:55:42 -0500  # Date
categories: [Research]     # Catagories, no more than 2
tags:       [Dust]  # Tags, any number
pin:        false                      # Should this post be pinned?
toc:        true                       # Table of Contents?
math:       true                      # Does this post contain math?
---
I have been working on adding a dust model to our group's hydrodynamics code, Cholla. As is stands, Cholla models the fluid dynamics of the gas in galaxies, but gas is not the only fluid that galaxies contain. Dust is the other major fluid component of galaxies, and it plays an important role in many of the processes that shape a galaxy's evolution. To incorporate these effects into our isolated galaxies simulations, I am developing a model that is adapted from the [McKinnon et al. (2016) paper](https://ui.adsabs.harvard.edu/abs/2016MNRAS.457.3775M/abstract) that introduces a simple dust model to the [Arepo](https://ui.adsabs.harvard.edu/abs/2010MNRAS.401..791S/abstract) code. In our adaptation, we are treating dust as a fluid that is fully coupled to the dynamics of the existing gas. Treating dust density as a passive scalar that depends on the gas density and temperature.  
This model accounts for how dust density changes due to the processes of thermal sputtering and gas-phase metal accretion and are modeled by the following equations: $$\frac{d\rho_{i,\text{dust}}{dt} = \Bigg(1-\frac{\rho_{i,\text{dust}}{\rho_{i,\text{metal}}\Bigg)\Bigg(frac{\rho_{i,\text{dust}}{\tau_g} $$
