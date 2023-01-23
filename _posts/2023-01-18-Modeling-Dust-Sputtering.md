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

To tackle the question of how dust is tranported in galactic winds, I've been thinking about the primary mechanism that destroys dust at high temperatures in galaxies, sputtering. 

In very simple terms, you can think of sputtering as the gradual shrinking of dust grains, as individual electrons and ions that are bound to dust grains are knocked off by impingent energetic electrons and ions (as is shown in the below cartoon). After enough of these collisions have taken place, dust grains can be destroyed entirely.

![Sputtering Schematic](/assets/img/posts/sputtering.png)

The mechanism isn't quite as simple as an ion bumping into a bound atom and knocking it off, it's really a [linear cascade process](https://en.wikipedia.org/wiki/Collision_cascade#:~:text=In%20linear%20cascades%20the%20set,atoms%20(TKA)%2C%20etc.), but this simple mental image suffices for our purposes. 

Sputtering only occurs at sufficiently high temperatures, because at cooler temperatures ($T\lesssim10^4~K$), impingent electrons and ions are more likely to stick to dust grains. In this regime, photoemission of electrons from grains by incident UV photons is the main way by which grains shrink, but it's sub-dominant in overall grain evolution. However, when the temperature is high enough, charged particles (electrons and ions) are energetic enough that they are capable of ejecting atoms from the surface of the grain through the transfer of kinetic energy. Eventually, the grain can become so positively or negatively charged that the presence of strong electric fields can cause the emission of atoms from the dust grain (field emission). Both of these effects are included in the general definition of sputtering. The sputtering rate for a non-rotating, stationary, spehrical target of radius $a$, potential $U$, in a Maxwellian gas of temperature $T$ is given by:

\\( \frac{da}{dt} = - \frac{m_x}{4\rho} \sum_i n_i \int_{E_{\text{min}}}^\infty \Big(\frac{2E}{m_i}\Big)^{1/2} \Big(1-\frac{Z_ieU}{E}\Big)Y_\text{sput}(E-Z_ieU) \\).

$i$ is the projectile species, $f_E$ is the energy distribution function, $(1-Z_ieU/E)$ is the Coulomb focusing factor, and $Y_\text{sput}$ is the sputtering yield. The sputtering yield is defined as the mean number of emitted atoms per incident particle, and it depends on the impact energy of the projectile ion, that ion's mass and charge, and the composition of the target. This expression is from [Bruce Draine's ISM book](https://www.astro.princeton.edu/~draine/book/index.html). There's an even more complicated version in [Draine and Salpeter (1979)](https://ui.adsabs.harvard.edu/abs/1979ApJ...231...77D/abstract) for when the grain is not stationary relative to the gas. The generalized formulation uses a skewed Maxwellian velocity distribution, which accounts for dust drift velocity and gas thermal motions. The tricky part of using either of these formulations is figuring out the grain potential and sputtering yields. Calculating the potential is a theory-heavy task (described below) that involves some hand-waving and approximation, and the sputtering yields can only be measured empirically.


Much of the work in formulating this theory is done in [Draine and Salpeter (1979)](https://ui.adsabs.harvard.edu/abs/1979ApJ...231...77D/abstract), where they consider the forces acting on a grain of dust in hot gas, and calculate the potentials and sputtering yields for grains of different sizes and compositions. To calculate the potential, they consider drag forces (collision and Coulomb drag) and Loretnz force, and calculate the total potential due to impingent electrons, ions, photons, and field emission. By analyzing how these forces act on dust in regimes of astrophysical interest they were able to conclude that dust can be considered as dynamically coupled to the magnetic field (i.e. that drag forces are not usually not significant compared to Lorentz force). They also use experimental data to constrain sputtering yields. The result of this paper is the first model of sputtering rates as a function of temperature for iron, silicate, graphite, and $H_2O$ dust grains, which are shown in the figure below.

<img src="/assets/img/posts/sputtering_rates.png" alt="Draine and Salpeter (1979) Sputtering Rates" width="400"/>

Note that the rates shown in this figure only apply for stationary grains. For continuous distributions of hot ionized gas, this prescription is perfectly acceptable under the assumption that dust grains are dynamically coupled to gas through magnetic fields. When you need to deal with shocks, however, things can get complicated. In shocks, dust can't be treated as stationary with respect to gas, because the relative velocities between gas and dust can be quite high. This is because grains are not betatron accelerated like they are under non-shock conditions, they're dragged to rest with respect to gas. Thus, our simplified treatment of sputtering breaks down. A skewed Maxwellian distribution can be used to average the sputtering yield in the above version of the sputtering rate equation from [Draine and Salpeter (1979)](https://ui.adsabs.harvard.edu/abs/1979ApJ...231...77D/abstract). Alternatively, you can treat the two different regimes ($v_\text{rel}=0$ and $v_\text{rel}\neq0$) as two different types of sputtering: thermal and non-thermal (or inertial), respectively.


This concept was first introduced by [Tielens et al. (1994)](https://ui.adsabs.harvard.edu/abs/1994ApJ...431..321T/abstract). Aside from introducing this useful formalism, this study also gave sputtering yields as a function of incident projectile energy and mass for different compositions of dust grains: graphite, silicates, silicon carbide, iron, and specific grain mantle materials (icy and organic refractory). Note that this model shifts from the consideration of unique species of ions to a "universal" law for sputtering yields, which was first introduced by 
[Bohdansky (1984)](https://ui.adsabs.harvard.edu/abs/1984NIMPB...2..587B/abstract). The end result of this work are simple polynomial fits to sputtering yields as a function of temperature that only depend on grain species, which is the basis of most modern sputtering models seen in the literature today. The equations for sputtering rates are given below:

\\( \frac{dN_\text{sp}}{dt}=2\pi a^2v_g\Sigma n_i Y_i(E=0.5m_i v_g^2) (\text{non-thermal}) )\\
\\( \frac{dN_\text{sp}}{dt}=2\pi a^2\Sigma n_i \langel Y_iv\rangel (\text{thermal}))\\