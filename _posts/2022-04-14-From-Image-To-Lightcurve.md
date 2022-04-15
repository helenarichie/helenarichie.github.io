---
title:      From Image to Lightcurve      # Title
author:     Helena Richie              # Author Name
date:       2022-04-14 09:55:42 -0500  # Date
categories: [Research, Outreach]     # Catagories, no more than 2
tags:       [Photometry, Data Visualization]  # Tags, any number
pin:        false                      # Should this post be pinned?
toc:        true                       # Table of Contents?
math:       true                      # Does this post contain math?
---
# Visualizing Photometric Data
As an assignment in my graduate galaxies course this spring, I was tasked with making a visualization of some sort of astronomical data or concept using an interactive display or animation that might eventually be useful in a research or public talk. I decided to make a figure that I had frequently reached for when explaining what lightcurves of exoplanet transits actually represent during public talks about my undergraduate research group, [STEPUP](https://sites.pitt.edu/~stepup/).

<span style="display:block;text-align:center">
[![Photometry Demo](https://img.youtube.com/vi/T4mSG8iG4xY/0.jpg)](https://youtu.be/T4mSG8iG4xY)
</span>

This video shows a slideshow of the 100 or so images collected of the star WASP-52 as the planet WASP-52b transits in front of it. Then, it demonstrates how the brightness of that star can be quantified in each image using its point spread function, and finally it shows how that point spread function ultimately tells us that the star got briefly dimmer as WASP-52b passed in front of it during the 2 hours during which this data was collected. 

I like this visualization because it can be used as a tool for both the general public and new researchers working with photometric data to get an understanding of what photometric data is measuring, exactly, and what factors might affect it. A 3D histogram is one of the easiest ways to see that measurements of a brighter star will have higher levels of _something_ that they can think of as light, and that data points in a light curve are just a result of totaling up the levels in the spots where the star's light hit the sensor of a camera.

At different points of this video, you can see instrumental noise in the image, tracking errors in both the image and its resulting point spread function, how the telescope's focus degrades throughout the night, and how that adds scatter to the light curve. It also demonstrates some of the human touch that goes into collecting astronomical image data--we almost didn't get WASP-52 in the telescope's field of view, because we were wrong about which star in the image actually was WASP-52 when we were setting up the telescope, which is why the star is so close to the edge of the image! 

There are details aside from the ones that I've pointed out that one could pore over, and there are definitely improvements that I'd like to make to this short visualization, but I already turned in my assignment, so I'm just gonna leave it here as is :-) Anyone looking to use this animation should feel free to do so, as long as they're sure to credit myself and the STEPUP team! The (very clunky and disorganized) code that I used to create these figures can be found in [this GitHub repo](https://github.com/helenarichie/photometry-visualization). I'm happy to share our data on WASP-52 as well, so if you want to play around with it send me an email!