---
layout: page
title: Cloud-Wind Simulations
description: a project with a background image and giscus comments
img: assets/img/cloud-wind.png
importance: 2
category: research
giscus_comments: false
---

This post is a summary of [Richie et al. 2024](https://ui.adsabs.harvard.edu/abs/2024arXiv240303711R/abstract), my first paper on dust evolution in galactic outflows. In this paper, we used idealized simulations of individual dusty clouds in hot galactic winds to understand how sputtering affects dust in these environments. We ran a suite of simulations to explore how different factors, such as cloud evolution and dust grain size, affect dust survival. In these simulations, we varied cloud size, wind speed, wind temperature, cloud overdensity, and dust grain size. 

In all cases, for large ($$a\gtrsim0.1~{\mu\text{m}}$$) grains, we find that a majority of dust survives. Below is a movie of a large ($$ r_\text{cl}=100~\text{pc} $$) cloud in a slow ($$500~\text{km}\,\text{s}^{-1}$$) wind.

<div style="padding:22.89% 0 0 0;position:relative;"><iframe src="https://player.vimeo.com/video/927225139?badge=0&amp;autopause=0&amp;player_id=0&amp;app_id=58479" frameborder="0" allow="autoplay; fullscreen; picture-in-picture; clipboard-write" style="position:absolute;top:0;left:0;width:100%;height:100%;" title="survived_cloud"></iframe></div><script src="https://player.vimeo.com/api/player.js"></script>
<div class="caption">
    Survived cloud simulation.
</div>

In this simulation, the cloud traverses nearly 15 kpc in roughly 80 Myr and exhibits essentially no dust sputtering. The timescale for sputtering in the hot wind is short compared to the simulation length--around 10 Myr. Here, dust survival is a direct result of long-term shielding within the cool cloud, where the sputtering time is much longer. 

The mixed phase of gas (which forms as a result of mixing between the cool cloud and the hot wind) has a temperature of $$\sim10^5~\text{K}$$, allowing it to cool extremely efficiently ($$t_\text{cool,mix}\sim$$40 kyr). This is short compared to the dynamical timescales for cloud-wind mixing that govern the cloud's evolution. In particular, the shear time $$t_\text{shear}=r_\text{cl}/v_\text{w}$$ is is around 200 kyr. [Abruzzo et al. (2023)](https://ui.adsabs.harvard.edu/abs/2023arXiv230703228A/abstract) showed that clouds that satisfy the criterion $$t_\text{cool, mix} < 7~t_\text{shear}$$ can survive for long periods.

<div class="row justify-content-sm-center">
    <div class="col-sm-7 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/cloud_dest.png" title="cloud destruction" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm-5 mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/cloud_surv.png" title="cloud survival" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Cartoons illustrating cloud destruction and survival (credit: Matthew Abruzzo).
</div>

In this scenario, the mixed-phase gas can cool and accrete onto the cloud's tail before the momentum it gains from the hot phase carries it away from the cloud. Extremely efficient cloud shielding enabled near-total dust survival in the survived cloud case, but a majority of dust ended up surviving _even_ when it was completely exposed to the hot wind. We saw this when we repeated the above simulation for a cloud in the destruction regime, defined by $$t_\text{cool, mix} \gg t_\text{shear}$$.

<div style="padding:32.32% 0 0 0;position:relative;"><iframe src="https://player.vimeo.com/video/1018752642?badge=0&amp;autopause=0&amp;player_id=0&amp;app_id=58479" frameborder="0" allow="autoplay; fullscreen; picture-in-picture; clipboard-write" style="position:absolute;top:0;left:0;width:100%;height:100%;" title="destroyed_cloud"></iframe></div><script src="https://player.vimeo.com/api/player.js"></script>
<div class="caption">
    Destroyed cloud simulation.
</div>

Several factors are responsible for this cloud's destruction--it has a smaller radius (5 pc), it is accelerated by a faster wind ($$10^3~\text{km}\,\text{s}^{-1}$$), and the higher mixed-phase temperature results in a longer cooling time ($$t_\text{cool,mix}\sim$$160 kyr). The smaller cloud radius and faster wind velocity drive down the shear time, so the mixed cloud material moves away from the cloud before it can cool, and it eventually gets heated to the wind temperature.

By the end of the destroyed cloud simulation, the cloud is almost completely mixed into the wind, but $$ \sim80\% $$ of the dust remains intact, having traveled 0.5 kpc. In this case, dust survival can be explained by the rapid wind speed. Once the dust is transferred from the cloud into the hot gas, it moves at the wind speed away from the galaxy, where the wind is at its hottest and densest. Further away from the galaxy, sputtering times in the hot phase lengthen as the wind drops in density and temperature as it expands adiabatically.

![Sputtering Contours](/assets/img/sputtering_contours.jpg){: width="750" height="357" style="max-width: 60%" .low}
<div class="caption">
    Sputtering times for ($$a=0.1~{\mu\text{m}}$$) grains as a function of gas density and temperature.
</div>

The above figure shows the sputtering times for ($$a=0.1~{\mu\text{m}}$$) grains as a function of density and temperature. Overlaid are the densities and temperatures of the hot, cool, and mixed phases of an outflow at various distances away from the galactic midplane, taken from a theoretical model of a starburst-driven galactic outflow ([Schneider et al. 2020](https://ui.adsabs.harvard.edu/abs/2020ApJ...895...43S/abstract)). This shows that the only region of the outflow where the wind is hot and dense enough to sputter dust on timescales that are short compared to the outflow dynamical time ($$\sim$$10 Myr) is roughly $$r\lesssim$$1 kpc. So, for large dust grains, cloud shielding is not necessary to enable dust survival.

These results provide a viable explanation for the vast amounts of dust observed in the CGMs of galaxies and beyond. In the future, we plan to apply this model to simulations of entire galaxies with self-consistently driven outflows to understand dust survival in non-idealized environments.
