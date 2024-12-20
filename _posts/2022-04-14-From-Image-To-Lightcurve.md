---
title:      From Image to Lightcurve      # Title
author:     Helena Richie              # Author Name
date:       2022-04-14 09:55:42 -0500  # Date
categories: [Outreach]     # Catagories, no more than 2
tags:       [Photometry, Data Visualization]  # Tags, any number
pin:        false                      # Should this post be pinned?
toc:        true                       # Table of Contents?
math:       true                      # Does this post contain math?
---
# Visualizing Photometric Data
As an assignment in my graduate galaxies course this spring, I was tasked with making a visualization of some sort of astronomical data or concept using an interactive display or animation that might eventually be useful in a research or public talk. I decided to make a figure that I had frequently reached for when explaining what lightcurves of exoplanet transits represent during my time in my undergraduate research group, [STEPUP](https://sites.pitt.edu/~stepup/). The resulting animation can be seen below:

<span style="display:block;text-align:center">
[![Photometry Demo](https://img.youtube.com/vi/T4mSG8iG4xY/0.jpg)](https://youtu.be/T4mSG8iG4xY)
</span>

This video shows a slideshow of the ~hundred collected of the star WASP-52 as the planet WASP-52b transited in front of it over the course of about two hours. Then, it demonstrates how the brightness of that star can be quantified in each image using its point spread function, and finally it shows how that point spread function ultimately tells us that the star WASP-52 briefly became dimmer as WASP-52b passed in front of it while we were collecting this data.

I like this visualization because it can be used as a tool for both the general public and new researchers working with photometric data to understand what photometric data is actually measuring, and what factors might affect those measurements. A 3D histogram is one of the easiest ways to see that a brighter star will have higher levels of _something_ that they can think of as light, and how data points in a light curve are just a result of totaling up those levels in the spots where the star's light hit the sensor of a camera.

At different points of this video, we can see instrumental noise in the image, tracking errors in both the image and its resulting point spread function, how the telescope's focus degrades throughout the night, and how that adds scatter to the light curve. It also demonstrates some of the human touch that goes into collecting astronomical image data--we almost didn't get WASP-52 in the telescope's field of view because we were wrong about which star in the image actually was WASP-52 when we were setting up the telescope, which is why the star is so close to the edge of the image! 

There are definitely improvements that I'd like to make to this short visualization, but I already turned in my assignment, so I'm just gonna leave it here as is :-) The (very clunky and disorganized) code that I used to create these figures can be found in [this GitHub repo](https://github.com/helenarichie/photometry-visualization).