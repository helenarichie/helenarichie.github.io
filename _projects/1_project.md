---
layout: page
title: Galactic Outflow Simulations
description: large-scale, high-resolution simulations of dusty galactic outflows
img: assets/img/nuclear-burst.png
importance: 1
category: research
related_publications: false
---

This post is a summary of [Richie & Schneider (2026)](https://doi.org/10.3847/1538-4357/ae12e8), where we modeled dust evolution in simulations of entire star-forming disk galaxies with multi-phase outflows driven by stellar feedback. Building on our [cloud-wind simulations]({% link _projects/2_project.md %}), we wanted to know whether dust can survive in a realistic outflow, where clouds are not idealized and dust is exposed to a wide range of gas conditions as it leaves the galaxy.

Using [Cholla](https://github.com/cholla-hydro/cholla), we ran two simulations at $$\sim5~\text{pc}$$ resolution in a $$10\times10\times20~\text{kpc}^3$$ box. The **nuclear-burst** model is an M82-like starburst with a star formation rate of $$5~M_\odot\,\text{yr}^{-1}$$ and centrally concentrated star clusters, and the **high-z** model has a higher star formation rate ($$20~M_\odot\,\text{yr}^{-1}$$) with clusters spread throughout the disk. In each, we tracked dust grains with radii of 1, 0.1, 0.01, and 0.001 $$\mu\text{m}$$ as they are carried out of the disk subject to thermal sputtering.

Our main conclusions are:

- **Outflows are an efficient way to move dust into galaxy halos.** Multi-phase outflows safely carry the majority of their dust out to $$\sim10$$ kpc, which could help explain the large amounts of dust observed in the circumgalactic medium (CGM).
- **More (and more distributed) star formation means dustier halos.** The high-z model loads the CGM with dust more efficiently, thanks to its higher outflow rates and larger mass of cool gas, which shields dust from sputtering.
- **The hot phase may be a source of CGM dust.** The cool phase is ultimately the dustiest, but it takes tens of Myr to build up its dust mass. Early on, the hot phase dominates the outflow's dust budget, simply because it moves the fastest. Large ($$a\gtrsim0.1~\mu\text{m}$$) grains in the hot phase experience very little sputtering, and thus can survive to populate the CGM.
- **Small grains don't survive in hot gas.** Grains with $$a\lesssim0.01~\mu\text{m}$$ are efficiently sputtered in gas hotter than $$\sim2\times10^4$$ K, so the grain size distribution in the halo likely differs from that in the disk. PAH-sized grains need shielding in cool gas to travel significant distances, which suggests that the small grains and PAHs observed in nearby outflows may be (at least partly) produced in situ, for example by shattering of larger grains.
- **Implications for cosmological simulations.** Because the average gas properties of an outflow don't fully predict how its dust evolves, and because cosmological simulations don't resolve the hot phase, they may underestimate dust outflow rates. This motivates updated sub-grid dust models.

### high-z model
<div style="padding:49.38% 0 0 0;position:relative;"><iframe loading="lazy" src="https://player.vimeo.com/video/1037395367?badge=0&amp;autopause=0&amp;player_id=0&amp;app_id=58479" frameborder="0" allow="autoplay; fullscreen; picture-in-picture; clipboard-write" style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;border-radius: 10px; overflow: hidden;" title="high_z"></iframe></div>
<div class="caption">
    Evolution of 1, 0.1, 0.01, and 0.001 micron radius dust grains (from left to right) under sputtering in a multi-phase galactic outflow. The galaxy has a star formation rate of 20 solar masses per year, with clusters distribuetd throughout the disk at a scale radius of 800 pc.
</div>

### nuclear-burst model
<div style="padding:49.38% 0 0 0;position:relative;"><iframe loading="lazy" src="https://player.vimeo.com/video/1037618258?badge=0&amp;autopause=0&amp;player_id=0&amp;app_id=58479" frameborder="0" allow="autoplay; fullscreen; picture-in-picture; clipboard-write" style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;border-radius: 10px; overflow: hidden;" title="m82"></iframe></div>
<div class="caption">
    Evolution of 1, 0.1, 0.01, and 0.001 micron radius dust grains (from left to right) under sputtering in a multi-phase galactic outflow. The galaxy has a star formation rate of 5 solar masses per year and centrally concentrated star clusters, distrbuted at a scale radius of 300 pc in the disk.
</div>
