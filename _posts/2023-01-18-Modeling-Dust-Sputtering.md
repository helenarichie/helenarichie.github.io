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

# Overview

To understand how dust is transported in galactic winds, I've been thinking about the primary mechanism that destroys dust at high temperatures in galaxies, sputtering. 

In very simple terms, you can think of sputtering as the gradual shrinking of dust grains, as individual electrons and ions that are bound to dust grains are knocked off by impingent energetic electrons and ions (as is shown in the below cartoon). After enough of these collisions have taken place, dust grains can be destroyed entirely.

![Sputtering Schematic](/assets/img/posts/sputtering.png)

The mechanism isn't quite as simple as an ion bumping into a bound atom and knocking it off, it's really a [linear cascade process](https://en.wikipedia.org/wiki/Collision_cascade#:~:text=In%20linear%20cascades%20the%20set,atoms%20(TKA)%2C%20etc.), but this simple mental image will suffice for our purposes. 

Sputtering only occurs at sufficiently high temperatures, because at cooler temperatures ($T\lesssim10^4~K$), impingent electrons and ions are more likely to stick to dust grains. In this regime, photoemission of electrons from grains by incident UV photons is the main way by which grains shrink, but it's sub-dominant in overall grain evolution. However, when the temperature is high enough, charged particles (electrons and ions) are energetic enough that they are capable of ejecting atoms from the surface of the grain through the transfer of kinetic energy. Eventually, the grain can become so positively or negatively charged that the presence of strong electric fields can cause the emission of atoms from the dust grain (field emission). Both of these effects are included in the general definition of sputtering. The sputtering rate for a non-rotating, stationary, spehrical target of radius $a$, potential $U$, in a Maxwellian gas of temperature $T$ is given by:

\\( \frac{\text{d}a}{\text{d}t} = - \frac{m_x}{4\rho} \sum_i n_i \int_{E_{\text{min}}}^\infty \Big(\frac{2E}{m_i}\Big)^{1/2} \Big(1-\frac{Z_ieU}{E}\Big)Y_\text{sput}(E-Z_ieU) \\).

$i$ is the projectile species, $f_E$ is the energy distribution function, $(1-Z_ieU/E)$ is the Coulomb focusing factor, and $Y_\text{sput}$ is the sputtering yield. The sputtering yield is defined as the mean number of emitted atoms per incident particle, and it depends on the impact energy of the projectile ion, that ion's mass and charge, and the composition of the target. This expression is from [Bruce Draine's ISM book](https://www.astro.princeton.edu/~draine/book/index.html). There's an even more complicated version in [Draine and Salpeter (1979)](https://ui.adsabs.harvard.edu/abs/1979ApJ...231...77D/abstract) for when the grain is not stationary relative to the gas. The generalized formulation uses a skewed Maxwellian velocity distribution, which accounts for dust drift velocity and gas thermal motions. The tricky part of using either of these formulations is figuring out the grain potential and sputtering yields. Calculating the potential is a theory-heavy task (described below) that involves some hand-waving and approximation, and the sputtering yields can only be measured empirically. Once we have all of this information, though, it's possible to write a formula for the rate of change of dust mass for a particular species of dust as a function of gas density and temperature.

# Formulation History

Much of the work in formulating sputtering theory is done in Draine and Salpeter (1979), where they consider the forces acting on a grain of dust in hot gas, and calculate the potentials and sputtering yields for grains of different sizes and compositions. To calculate the potential, they consider drag forces (collision and Coulomb drag) and Loretnz force, and calculate the total potential due to impingent electrons, ions, photons, and field emission. By analyzing how these forces act on dust in regimes of astrophysical interest they were able to conclude that dust can be considered as dynamically coupled to the magnetic field (i.e. that drag forces are not usually not significant compared to Lorentz force). They also use experimental data to constrain sputtering yields. The result of this paper is the first model of sputtering rates as a function of temperature for iron, silicate, graphite, and $H_2O$ dust grains, which are shown in the figure below.

<img src="/assets/img/posts/sputtering_rates.png" alt="Draine and Salpeter (1979) Sputtering Rates" width="400"/>

Note that the rates shown in this figure only apply for stationary grains. For continuous distributions of hot ionized gas, this prescription is perfectly acceptable under the assumption that dust grains are dynamically coupled to gas through magnetic fields. When you need to deal with shocks, however, things can get complicated. In shocks, dust can't be treated as stationary with respect to gas, because the relative velocities between gas and dust can be quite high. This is because grains are not betatron accelerated like they are under non-shock conditions. Instead, they're accelerated by drag forces until they're once again at rest with respect to gas. Thus, our simplified treatment of sputtering breaks down. A less generalized version of the sputtering rate (that uses a skewed Maxwellian distribution, accounting for relative velocities and gas thermal motions) can ben used, and is given in Draine and Salpeter (1979). Alternatively, you can treat the two different regimes ($v_\text{rel}=0$ and $v_\text{rel}\neq0$) as two different types of sputtering: thermal and non-thermal (or inertial), respectively.

This concept was first introduced by [Tielens et al. (1994)](https://ui.adsabs.harvard.edu/abs/1994ApJ...431..321T/abstract). Aside from introducing this useful formalism (in the form of the two equations below), their study also gave sputtering yields as a function of incident projectile energy and mass for different compositions of dust grains: graphite, silicates, silicon carbide, iron, and specific grain mantle materials (icy and organic refractory). Note that this model shifts from the consideration of unique species of ions to a "universal" law for sputtering yields, which was first introduced by 
[Bohdansky (1984)](https://ui.adsabs.harvard.edu/abs/1984NIMPB...2..587B/abstract). The end result of this work are simple polynomial fits to thermal sputtering yields as a function of temperature averaged over all ion impact angles that only depend on grain species, which is the basis for most modern sputtering models seen in the literature today. The equations for sputtering rates are given below:

\\( \frac{\text{d}N_\text{sp}}{\text{d}t}=2\pi a^2v_g\sum n_i Y_i(E=0.5m_i v_g^2)\,\,(\text{non-thermal}) \\)

\\( \frac{\text{d}N_\text{sp}}{\text{d}t}=2\pi a^2\sum n_i \langle Y_iv\rangle \,\, (\text{thermal}) \\) 

The primary difference between these two equations is the velocity dependence that the non-thermal form has. Both depend on gas temperature and density. 

The universal yields for thermal sputtering resulting from this paper are shown below. (Yields for non-thermal sputtering are not given in this study.)

<img src="/assets/img/posts/tielens_yields.png" alt="Tielens (1994) Universal Sputtering Yields" width="400"/>

These curves are given in units of $\text{cm}^{3} \text{Å} \text{yr}^{-1}$ and are described numerically in Tielens et al. (1994) in Table 4, which gives coefficients for the fith-order polynomial fit for five types of dust grains. Preceding sections of this paper detail how the yield for each material was calculated.

[Tsai and Mathews (1995)](https://ui.adsabs.harvard.edu/abs/1996ApJ...468..571T/abstract) derived a commonly-used analytic form of the thermal sputtering rate based on the work of Tielens et al. (1994):

\\( \frac{\text{d}a}{\text{d}t}=-\tilde{h}\Big(\frac{\rho}{m_p}\Big)\Big[\Big(\frac{T_d}{T}\Big)^\omega+1\Big]^{-1} \\)

This formula is a good approximation for both graphite and silicate when $\tilde{h}=3.2\times10^{-18}~\text{cm}^4\text{s}^{-1}$, $\omega=2.5$, and $T_d=2\times10^6~\text{K}$. They also introduce the "local sputtering time" (now more frequently known as the sputtering timescale) as:

\\( t_\text{sp}=a\Big\|\frac{\text{d}a}{\text{d}t}\Big\|^{-1} \\).

[Nozawa, Kozada, and Habe (2006)](https://ui.adsabs.harvard.edu/abs/2006ApJ...648..435N/abstract) built on the work of Tielens et al. (1994) by calculating sputtering rates both for thermal sputtering and non-thermal sputtering for an even wider range of dust species. They do this by introducing newly determined sputtering yields using a method similar to Tielens et al. (1994), but used a slightly improved version of the Bohdansky (1984) universal sputtering relation, with an improved fitting method for the free parameter in this model, and using the EDDY code ([Ohya and Kawata, 1997](https://ui.adsabs.harvard.edu/abs/1997JaJAP..36L.298O/abstract)) to constrain species for which no experimental data exists. They used these yields to give sputtering rates as a function of temperature for thermal sputtering, and as function of relative velocity for non-thermal sputtering, shown below.

<p float="left">
  <img src="/assets/img/posts/rate_thermal.jpeg" width="250" />
  <img src="/assets/img/posts/rate_nonthermal.jpeg" width="250" />
</p>

# Modern Sputtering Modeling

In this section, I'll give three different examples to show how the theory of sputtering modeling developed above is being implemented to model dust evolution in modern simulations.

## [McKinnon et al. (2017)](https://ui.adsabs.harvard.edu/abs/2017MNRAS.468.1505M/abstract)

This paper treats dust as dynamically coupled to gas, and tracks the evolution in dust mass as:

\\( \Big(\frac{\text{d}M_\text{i,dust}}{\text{d}t}\Big)_\text{sp}=-\frac{M_\text{i,dust}}{\tau_\text{sp}/3} \\).

Here, $tau_\text{sp}$ comes from the formula given by Tsai and Mathews (1995):

\\( \tau_\text{sp}=a\Big\|\frac{\text{d}a}{\text{d}t}\Big\|^{-1}\approx(0.17~\text{Gyr})\Big(\frac{a_{-1}}{\rho_{-27}}\Big)\Big[\Big(\frac{T_0}{T}\Big)^\omega+1\Big] \\).

This does not give a complete treatment of sputtering, however, because the above only accounts for thermal sputtering. To account for the effects of non-thermal sputtering, which takes place primarily in supernova shocks, this paper uses a subgrid grain destruction model that was introduced in [McKinnon et al. (2016)](https://ui.adsabs.harvard.edu/abs/2016MNRAS.457.3775M/abstract). This model indirectly treats non-thermal sputtering using an overall destruction timescale,

\\( \tau_\text{d}=\frac{M_\text{g}}{\epsilon\gamma M_\text{s}(100)} \\),

where $M_\text{g}$ is the gas mass within a cell, $\epsilon$ is the efficiency with which grains are destroyed by SN shocks, $\gamma$ is the local Type II SN rate, and $M_\text{s}(100)$ is the mass of gas shocked to at least $100~\text{km}\text{s}^{-1}$. In general, this prescription is not as flexible, since it requires more assumptions about SN shocks and grain physics.

## [Hu et al. (2019)](https://ui.adsabs.harvard.edu/abs/2019MNRAS.487.3252H/abstract)

This paper also treats dust as dynamically coupled to gas, but it directly treats thermal and non-thermal sputtering. Their overall sputtering rate is given by

\\( \frac{\text{d}m_\text{dust}}{\text{d}t}=N_\text{gr}\frac{\text{d}m_\text{gr}}{\text{d}t}=3N_\text{gr}m_\text{gr}\frac{\dot{a}}{a}=\frac{3n_\text{H}m_\text{dust}}{a}Y_\text{tot}\\)

where $m_\text{dust}$ is the dust mass of a cell, $N_\text{gr}=m_\text{dust}/m_\text{gr}$ is the number of grains, and $Y_\text{tot}$ is the total erosion rate (or sputtering yield). This paper uses the sputtering yields from Nozawa, Kozasa, and Habe (2006), and Table 1 in their paper gives the polynomial coefficients to describe the rates for thermal and non-thermal sputtering for carbon and silicon grains. For non-thermal sputtering, though, $Y_\text{nth}$ is a function of the relative velocity between dust and gas, so they also have a way to track dust dynamics. They derive the dust equation of motion and use a sub-cycling technique to solve it for the relative velocity when it is nonzero:

\\( \frac{\text{d}\bf{v}_\text{rel}}{\text{d}t}=-\frac{\bf{v}_\text{rel}}{t_\text{rel}}-\bf{a}_\text{hydro} \\),

where $t_\text{rel}\equiv(t_\text{drag}^{-1}-(\nabla\cdot\bf{v}_\text{gas})/2)^{-1}$.

## [Bocchio et al. (2014)](https://ui.adsabs.harvard.edu/abs/2014A%26A...570A..32B/abstract)

Instead of using the aritficial distinction of thermal and non-thermal sputtering, this paper uses a skewed Maxwellian distribution to calculate its sputtering rates. The equation for sputtering rate is exactly the same as the formula introduced for non-thermal sputtering in Tielens et al. (1994) (given above), but it uses a skewed Maxwellian velocity distribution, shown in the figure below.

<img src="/assets/img/posts/skm_dist.jpeg" alt="Bocchio Skewed Maxwellian" width="400"/>

The solid lines show the case when the drift velocity is zero, the dotted lines show a drift velocity of $35~\text{km}\text{s}^{-1}$, and the dashed lines show $V_\text{drift}=200~\text{km}\text{s}^{-1}$. This figure demonstrates one of the shortcomings of the non-thermal sputtering formulation--the relative velocity between gas and dust is really a combination of gas thermal motions and dust drift velocities. As such, the non-thermal sputtering treatment isn't as good of an approximation for higher gas temperatures. Indeed, for $V_\text{drift}=30~\text{km}\text{s}^{-1}$, the blue inertial sputtering velocity lines up well with $10^4~\text{K}$ gas, but not for $10^5~\text{K}$ gas, and there is a much wider spread in the $10^5~\text{K}$ gas velocity distribution. In general, at higher velocities inertial sputtering is a reasonable approximation. Using this approach eliminates the need to track dust dynamics in order to calculate the total sputtering rate.