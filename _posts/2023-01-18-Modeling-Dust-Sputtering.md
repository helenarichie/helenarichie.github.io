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

To tackle the question of how dust is tranported in galactic winds, I've been thinking about the primary mechanism that destroys dust at high temperatures in galaxies, sputtering. 

In very simple terms, you can think of sputtering as the gradual shrinking of dust grains, as the individual electrons and ions that are bound to dust grains are knocked off by impingent energetic electrions and ions (as is shown in the below cartoon). After enough of these collisions have taken place, dust grains can be destroyed entirely.

![Sputtering Schematic](/assets/img/posts/sputtering.png)

At cooler temperatures ($T\lessim10^4~K$), impinging electrons and ions are more likely to stick to dust grains, so photoemission of electrons from grains by incident UV photons is the only way in which grains shrink. However, when temperatures are higher, energetic charged particles (electrons and ions) are capable of ejecting electrons from the surface of the grain. Eventually, the grain can become so positively or negatively charged that the presence of strong electric fields can cause the emission of electrons or ions from the dust grain (field emission). The sputtering rate for a non-rotating, stationary, spehrical target or radius $a$, potential $U$, in a Maxwellian gas of temperature $T$ is given by:

\\( \frac{da}{dt} = - \frac{m_x}{4\rho} \sum_i n_i \int_{E_{\text{min}}}^\infty \Big(\frac{2E}{m_i}\Big)^{1/2} \Big(1-\frac{Z_ieU}{E}\Big)Y_\text{sput}(E-Z_ieU) \\).

$i$ is the projectile species, $f_E$ is the energy distribution function, $(1-Z_ieU/E)$ is the Coulomb focusing factor, and $Y_\text{sput}$ is the sputtering yield. The sputtering yield depends on the impact energy of the projectile ion, that ion's mass and charge, and the composition of the target. This expression is from [Bruce Draine's ISM book](https://www.astro.princeton.edu/~draine/book/index.html). There's an even more complicated version in [Draine and Salpeter (1979)](https://ui.adsabs.harvard.edu/abs/1979ApJ...231...77D/abstract) for when the grain is moving relative to the gas. The tricky part of using this equation to understand anything about how dust evolves in hot environments is figuring out the potential and the sputtering yields. Calculating the potential is a theory-heavy task that involves some hand-waving and approximation, and the sputtering yields can only be measured empirically.

Much of the work in formulating this theory is done in [Draine and Salpeter (1979)](https://ui.adsabs.harvard.edu/abs/1979ApJ...231...77D/abstract), where they consider the forces acting on a grain of dust in hot gas, and calculate the potentials and sputtering yields for grains of different sizes and compositions. To calculate the potential, they consider drag forces (collision and Coulomb drag) and Loretnz force, and calculate the total potential due to impinging electrons, ions, photons, and field emission. By analyzing how these forces act on dust in regimes of astrophysical interest allowed them to conclude that dust can be considered as dynamically coupled to the magnetic field. They also experimental data to constrain sputtering yields. The result of this work is the first model of sputtering rates as a function of temperature for iron, silicate, graphite, and $H_2O$ dust grains, which are shown in the figure below.

![Draine and Salpeter (1979) Sputtering Rates](/assets/img/posts/sputtering_rates.png)

Note that the rates shown in this figure only apply for stationary grains.