---
title:      Dust Dynamics       # Title
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