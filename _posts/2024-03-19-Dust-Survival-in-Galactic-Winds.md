---
title:      Dust Survival in Galactic Winds       # Title
author:     Helena Richie              # Author Name
date:       2024-03-19 12:00:42 -0500  # Date
categories: [Research, Dust]     # Catagories, no more than 2
tags:       [Dust, Wind Tunnel Simulations]  # Tags, any number
pin:        false                      # Should this post be pinned?
toc:        true                       # Table of Contents?
math:       true                      # Does this post contain math?
---

[My first paper](https://ui.adsabs.harvard.edu/abs/2024arXiv240303711R/abstract) on dust evolution in outflows is out! In this paper, we used idealized simulations of individual dusty clouds in hot galactic winds to understand how sputtering affects dust in these environments. We ran a suite of simulations to explore how different factors, such as cloud evolution and dust grain size, affect dust survival. In these simulations, we varied cloud size, wind speed, wind temperature, cloud overdensity, and dust grain size. 

In all cases, for large (\\( a\gtrsim0.1~{\mu\text{m}} \\)) grains, we find that a majority of dust survives. Below is a movie of a large (\\(r_\text{cl}=100~\text{pc}\\)) cloud in a slow (\\(500~\text{km}\,\text{s}^{-1}\\)) wind.



<div style="padding:22.89% 0 0 0;position:relative;"><iframe src="https://player.vimeo.com/video/927225139?badge=0&amp;autopause=0&amp;player_id=0&amp;app_id=58479" frameborder="0" allow="autoplay; fullscreen; picture-in-picture; clipboard-write" style="position:absolute;top:0;left:0;width:100%;height:100%;" title="survived_cloud"></iframe></div><script src="https://player.vimeo.com/api/player.js"></script>



In this simulation, the clouds traverses nearly 15 kpc in roughly 80 Myr and exhibits essentially no dust sputtering. The timescale for sputtering in the hot wind is around 10 Myr. Here, dust survival is a direct result of long-term shielding within the cool cloud, where the sputtering time is much longer. 

In this simulation, the mixed phase of gas (which forms as a result of mixing between the cool cloud and the hot wind) is able to cool extremely efficiently (\\(t_\text{cool,mix}\sim40~\text{kyr}\\)). This is short compared to the dynamical timescales for cloud-wind mixing that govern the cloud's evolution. In particular, the shear time (\\(t_\text{shear}=r_\text{cl}/v_\text{w}\\)) is is around \\(200~\text{kyr}\\). [Abruzzo et al. (2023)](https://ui.adsabs.harvard.edu/abs/2023arXiv230703228A/abstract) showed that clouds that satisfy the criterion \\(t_\text{cool, mix} < 7~t_\text{shear} \\) 

![Cloud Survival](/assets/img/posts/cloud_surv.png){: width="589" height="357" style="max-width: 40%" .low}

This ended up being true _even_ when dust is completely exposed to the hot wind (i.e. experiences zero cloud shielding). The total fraction of dust that survives depends on the ability of the mixed phase of gas (which forms at the interface of the cool cloud and hot wind) to rapidly cool and condense onto the cloud.

![Cloud Survival](/assets/img/posts/cloud_dest.png){: width="750" height="357" style="max-width: 60%" .low}