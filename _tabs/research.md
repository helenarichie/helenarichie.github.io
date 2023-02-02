---
title: Research
icon: fas fa-meteor
order: 2
---


*How does dust end up in the circumgalactic medium (CGM)?* Although dust originates in the interstellar medium (ISM) through condensation in stellar winds and supernovae (SNe), it is frequently observed in galaxy CGMs ([Ménard et al. (2010)](https://ui.adsabs.harvard.edu/abs/2010MNRAS.405.1025M/abstract)). The means by which dust is transported out of galaxies is debated. Galactic winds seem like a promising explanation, since they are thought to originate from SN feedback in the ISM. However, we know that the hot, dense conditions of these winds are amenable to dust destruction. *Can dust survive in galactic winds?* If winds do carry dust out of the ISM, what effect does that have on star formation, and galaxy evolution as a whole? Watching the evolution of dusty winds unfold in simulations can help us understand these questions. By directly modeling dust in simulations of galactic winds, we will be able to see how dust evolves in wind conditions, and in particular, whether or not cool clouds that carry dust can shield it from hot wind conditions for long enough to be transported into the CGM.

![Global simulation picture](/assets/img/tabs/cholla_comp.jpg)


My research focuses on using numerical simulations to study galaxy evolution. Right now, I'm working with Evan Schneider on developing her hydrodynamics code, [Cholla](https://github.com/cholla-hydro/cholla), to make state-of-the-art isolated galaxy simulations. In particular, I'm adding a dust model to Cholla that will allow us to study how the dust content of galaxies evolves over time and the interactions between dust and other galaxy components. Cholla is uniquely positioned to answer this question because of its GPU-native construction that allows for parsec-scale resolution, so we can see the dust physics on the scales that it takes place at in real galaxies. Because we don't have to rely on sub-grid models, like many other codes that can't resolve the dust physics, we'll be taking the first look at what happens to dust in the various processes that shape, transform, and transport it in galaxies.
