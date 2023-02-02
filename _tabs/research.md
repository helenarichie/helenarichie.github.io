---
title: Research
icon: fas fa-meteor
order: 2
---


**How does dust end up in the circumgalactic medium (CGM)?** Although dust originates in the interstellar medium (ISM) through condensation in stellar winds and supernovae (SNe), it is frequently observed in galaxy CGMs ([Ménard et al. 2010](https://ui.adsabs.harvard.edu/abs/2010MNRAS.405.1025M/abstract)). The means by which dust is transported out of galaxies is debated. Galactic winds seem like a promising explanation, since they are thought to originate from SN feedback in the ISM. However, we know that the hot, dense conditions of these winds are amenable to dust destruction. **Can dust survive in galactic winds?** If winds do carry dust out of the ISM, what effect does that have on star formation, and galaxy evolution as a whole? 

![Global simulation picture](/assets/img/tabs/cholla_comp.png)

Watching the evolution of dusty winds unfold in simulations can help us understand these questions. High resolution numerical simulations have reproduced the winds observed in galaxies, as is shown above. Here we see a side-by-side comparison of a simulation made by the [Cholla hydrodynamics code](https://github.com/cholla-hydro) and a nearby galaxy. Both show filamentary structures flowing out from the disk of the galaxy. Furthermore, in the image of NGC 4217, we can see dust scattered throughout the galaxy. Cholla, however, only simulates gas, which is why I am working to develop a model of dust that will allow us to see how dust evolves in these outflows. By directly modeling dust in simulations of galactic winds, we will be able to see how dust evolves in wind conditions, and in particular, whether or not cool clouds that carry dust can shield it from hot wind conditions for long enough to be transported into the CGM.

In the process of building up to a galaxy-scale simulations of dust in outflows, I am running simulations of individual dust clouds in a hot wind. The below simulation shows this scenario for relatively large cloud (but the scale of the simulation is still much smaller than galaxy-scale), with an itial radius of $\text{50}~\text{pc}$, and a gas density of $\text{n}=\text{1}~\text{cm}^\text{-3}$ and temperature of $\text{T}=\text{10}^\text{4}~\text{K}$ per cell. Using an initial dust-to-gas ratio of 1:100, the cloud is given a distribution of dust and we are able to watch how it evolves as the cloud is accelerated by a $\text{10}^\text{6}~\text{K}$, $\text{100}~\text{km}\,\text{s}^\text{-1}$ wind. In this simulation very little dust is destroyed, suggesting that winds are a viable mechanism for transporting dust out of galaxies.

![Cloud evolution](/assets/img/tabs/cloud_evolution.png)

Cholla is uniquely positioned to answer these types of questions because of its ability to create extremely high resolution simulations. Because Cholla is a GPU-based code, it can simulate volumes that fit entire galaxies while maintaining a fixed resolution of less than a few parsecs. Cholla's resolving power has been used to show that the small-scale dynamical coupling of mass and momentum between hot and cool phases of winds are responsible for the survival of cool clouds in hot outflows. Now, Cholla's resolving power will be put to use to directly resolve dust in these dynamical interactions to show us if they are important to dust's overall evolution. Because we don't have to rely on sub-grid models, we'll be taking the first look at what happens to dust in the various processes that shape, transform, and transport it in galaxies.
