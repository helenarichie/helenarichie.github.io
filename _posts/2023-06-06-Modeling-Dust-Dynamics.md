---
title:      Modeling Dust Dynamics       # Title
author:     Helena Richie              # Author Name
date:       2023-06-06 12:00:42 -0500  # Date
categories: [Research, Dust]     # Catagories, no more than 2
tags:       [Dust, Dynamics, Dust destruction]  # Tags, any number
pin:        false                      # Should this post be pinned?
toc:        true                       # Table of Contents?
math:       true                      # Does this post contain math?
---

When simulating dust, a major simplification in modeling can be made through assumptions about dust dynamics. Namely, dust dynamics (which are hard to calculate in Eulerian hydrodynamics simulations) can be ignored under the assumption that they are fully coupled to the dynamics of gas. This assumption can be made because dust grains are often charged, causing them to closely follow the ISM's magnetic fields, much like gas. Dust and gas are spatially coincident as long as the radius at which dust gyrates around magnetic fields is small. This radius is just the Larmor radius, and is defined as:

\\( r_\textrm{L} = \frac{m_\textrm{gr}v_\textrm{rel}}{Z_\textrm{gr}eB} \\).

This can also be written as 

\\( r_\textrm{L} \approx 8.5 \times 10^{-3}\,\textrm{pc}\,Z_\textrm{gr}^{-1} \Big(\frac{a}{0.1~\mu\textrm{m}}\Big)^3 \Big(\frac{v_\textrm{rel}}{\textrm{km}\,\textrm{s}^{-1}}\Big) \Big(\frac{B}{3~\mu\textrm{G}}\Big)^{-1}  \\)        ([Hu et al. 2019](https://ui.adsabs.harvard.edu/abs/2019MNRAS.487.3252H/abstract)).

$v_\textrm{rel}$ is the relative velocity between gas and dust and $a$ is the grain radius. From this we can see that for large grains and/or grains with a high relative velocity, the Larmor radius can become quite high and this assumption can break down.

This leads to several questions: _when do dust grains decouple_, _when does_ $v_\textrm{rel}$ _become large_, and _how common are large grains_?

Briefly answering the first question---[Slavin et al. (2004)](https://ui.adsabs.harvard.edu/abs/2004ApJ...614..796S/abstract) found that for grains with sizes $\gtrsim0.1~\mu\textrm{m}$ in shocks faster than $\sim50~\textrm{km}\,\textrm{s}^{-1}$ decoupling of gas and dust is usually important. 

To answer the second question, we can look at an example of an empirically calculated formula for the grain velocity. [Hirashita & Aoyama (2019)](https://ui.adsabs.harvard.edu/abs/2019MNRAS.482.2555H/abstract) give the following:

\\( v_\textrm{gr}(a) = 1.1\mathcal{M}^{3/2}\Big(\frac{a}{0.1~\mu\textrm{m}}\Big)^{1/2} \Big(\frac{T_\textrm{gas}}{10^4~\textrm{K}}\Big)^{1/4}  \Big(\frac{n_\textrm{H}}{1~\textrm{cm}^{-3}}\Big)^{-1/4} \Big(\frac{s}{3.5~\textrm{g}\,\textrm{cm}^{-3}}\Big)^{1/2}~\textrm{km}\,\textrm{s}^{-1}\\),

where $\mathcal{M}$ is the Mach number of the largest eddy velocity in the turbulent ISM (which they practically use as an adjusting parameter for the grain velocity) and $s$ is the material density of dust. The idea here is that under normal circumstances dust is spatially coincident wtih gas due to magnetic fields and moves along with gas as gas pushes on it (gas drag). So, this formula is derived by equating the gas drag timescale and the eddy turnover time due to turbulent velocities in the ISM. This formula captures the qualitative properties of grain velocities: larger grains have larger velocities because of their larger Larmor radii, grain velocities are larger in a higher temperature environment because of the higher characteristic velocity, grain velocities are larger in a less dense medium because of weaker gas drag, and more massive grains have higher velocities because of their larger inertia ([Hirashita & Aoyama 2019](https://ui.adsabs.harvard.edu/abs/2019MNRAS.482.2555H/abstract)). According to [Hirashita & Aoyama (2019)](https://ui.adsabs.harvard.edu/abs/2019MNRAS.482.2555H/abstract), in the diffuse ISM ($n_\textrm{H}\sim0.1--0.3~\textrm{cm}^{-3}$) large grains have a velocity of $\sim10~\textrm{km}\,\textrm{s}^{-1}$.

So, in short, it's hard to get a precise answer to this question, but we can get an idea of typical relative velocities in a continuous medium from these types of formulas.

Lastly, we need to know how common large (i.e. $a\gtrsim0.1~\mu\textrm{m}$) grains are to understand whether or not ignoring them in dynamically coupled dust models will have a significant effect on their accuracy.