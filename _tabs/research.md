---
title: Research
icon: fas fa-meteor
order: 2
---


**How does dust end up in the circumgalactic medium (CGM)?** Although dust originates in the interstellar medium (ISM) through condensation in stellar winds and supernovae (SNe), it is frequently observed in galaxy CGMs ([Ménard et al. 2010](https://ui.adsabs.harvard.edu/abs/2010MNRAS.405.1025M/abstract)). The means by which dust is transported out of galaxies is debated. Galactic winds seem like a promising explanation, since they are thought to originate from SN feedback in the ISM. However, we know that the hot, dense conditions of these winds are amenable to dust destruction. **Can dust survive in galactic winds?** If winds do carry dust out of the ISM, what effect does that have on star formation, and galaxy evolution as a whole? 

![Global simulation picture](/assets/img/tabs/cholla_comp.png)

Watching the evolution of dusty winds unfold in simulations can help us understand these questions. We have been able to reproduce the winds seen in observations using high resolution numerical simulations, as seen above. This figure shows a side-by-side comparison of a simulation made by the [Cholla hydrodynamics code](https://github.com/cholla-hydro) and a nearby galaxy. Both show filamentary structures flowing out from the disk of the galaxy. Furthermore, in the image of NGC 4217, we can see dust scattered throughout the galaxy. The Cholla simulation, however, only accounts for gas, which is why I am working to develop a model of dust that will allow us to see how dust evolves in these outflows. By directly modeling dust in simulations of galactic winds, we will be able to see how dust evolves in wind conditions, and in particular, whether or not cool clouds that carry dust can shield it from hot wind conditions for long enough to be transported into the CGM.

In the process of building up to a galaxy-scale simulations of dust in outflows, I am running simulations of individual dust clouds in a hot wind. The below simulation 

![Cloud evolution](/assets/img/tabs/cloud_evolution.png)

Cholla is uniquely positioned to answer this question because of its GPU-native construction that allows for parsec-scale resolution, so we can see the dust physics on the scales that it takes place at in real galaxies. Because we don't have to rely on sub-grid models, like many other codes that can't resolve the dust physics, we'll be taking the first look at what happens to dust in the various processes that shape, transform, and transport it in galaxies.
