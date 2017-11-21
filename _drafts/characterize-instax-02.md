---
layout: blog
title:  "Characterizing Instax Mini, part 2: analysis of primary and secondary colors"
tags: 
 - imaging 
 - film
 - instax
category: blog
---

I had a short [tweet exchange](https://twitter.com/steveyedlin/status/931898178214936578) with Steve Yedlin after I posted part one of this project. Seriously, how amazing is it that he even has time to poke holes in my methods?! His criticisms are all valid. Perhaps I should have included an extensive list of caveats before sharing. Or maybe I should just have been more clear about wanting to see how far into the research I can get using the limited material and equipment that I already have. At some point, I would like to do a more faithful reproduction of his research, but for now I'll be keeping it down and dirty.

And, speaking of down and dirty, I've invented my own colorspace. (That cold feeling down my back is Yedlin and Poynton casting long-distance shade about my unscientific methods.) Here's why.

Digital images are data. They're made of pixels, each of which is a group of three numbers, one each for the anount of red, green, and blue the pixel contains. So if I want to graph these color values, a three-dimensional [scatter plot](https://en.wikipedia.org/wiki/Scatter_plot) is my best bet. I'll put red on the x-axis, green on the y-axis, and blue on the z-axis. Why will I do this? Because I'm a compositor, and this is how colors get plotted in Nuke. I'll also be using Nuke's remapping of colors to floating point, so by scan's 0-255 vlaue range will become a 0-1 range. This conveniently represents the full gamut of colors reproducable as a unit cube.

![Unit cube representing black, white, and additive primary and secondary colors in the domain [0, 1].]({{ "/photographs/blog/2017/instax-gamutUnitCube.png" }})

Here we see black at the origin (0,0,0) and white at (1,1,1). All the additive primary (RBG) and secondary (CMY) colors occupy the other six corners on the cube. In the middle, we see a greyscale ramp running from black to white.





Now that we have RGB values as xyz coordinates, from 0,0,0 to 1,1,1 I prefer to have the neutrals run dowmn the z axis, so I rotate -45 degrees around y, then 35.2645 degreen around x (found by experimentation, I didn't do the math), and then scale by 1/1.732 to normalize back into the 0-1 range.





Characterize Instax Mini instant film in order to apply the Instax response to digital photographs.

using X-Rite ColorChecker and Lomo Instant Automat

At the end of this process, I will be able to apply "the Instax look" to digital photographs.

Steps:

1. Build 18% grey board with ColorChecker in the middle. This is the reference.
2. Photograph the reference with the Lomo Instant Automat at camera's automatic exposure, then also at -2 stops, -1 stop, +1 stop, and +2 stops.
3. Let the Instax film develop fully, at least 3 days. [http://www.thepicta.com/media/1430476698750850214_1434391894]
4. Scan the instant film with the ColorChecker.
5. Color-correct the scan to match the ColorChecker patches to known sRGB values.[http://www.poynton.com/notes/color/GretagMacbeth-ColorChecker.html]
6. Plot the Instax color response in 3D (Nuke).
7. Create lookup that takes ColorChecker values and maps them to the Instax data. (Is it even possible to do this step? Nuke ColorMatch?)
8. Apply the lookup to digital photographs.



How have I messed this up?
# I didn't wait three days like ??? suggests for the Instax colors to stabilize.
# I cleaned up the big dust & scratches, but left all the little ones. That means my dark values are going to be slightly inaccurate.
# I don't know the spectrum output of the LED lights I used to shoot the Instax. It probably isn't full spectrum. That probably gives me some color-rendering inaccuracies.