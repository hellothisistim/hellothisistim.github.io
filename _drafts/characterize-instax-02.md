---
layout: blog
title:  "Characterizing Instax Mini, part 2: analysis of primary and secondary colors"
tags: 
 - imaging 
 - film
 - instax
category: blog
---

![Begining of the tweet exchange with @yedlin.]({{ "/photographs/blog/2017/instax-twitterYedlin.png" }})

I had a short [tweet exchange](https://twitter.com/steveyedlin/status/931898178214936578) with Steve Yedlin after I posted part one of this project. Seriously, how amazing is it that he has the time to poke holes in my methods?! His criticisms are all valid. Perhaps I should have been more clear about wanting to see how far into the research I can get using the limited material and equipment that I already have. At some point, I would like to do a more faithful reproduction of his research, but for now I'll be keeping it down and dirty.

In my defense, I don't have access to a spectrometer, but I did scan all the prints simultaneously in one shot. Even if the scan isn't accurate, the samples are still stable relative to each other. These Instax Mini prints are pretty small. If I had made the chart any smaller, the patches would have been even harder to sample. 

I'll address his number three in the next post. For this project I'm not trying to match the film perfectly as Yedlin did in the [Display Prep Demo](http://yedlin.net/DisplayPrepDemo/). If I can get the general flavor, I'll be satisfied.

When I started this project, I wanted to look at two things. Yes, I did want to emulate Instax film on digital sources. But I also wanted to see how saturation changes with exposure. As a compositor, I had been told that film desaturates as the image gets darker, but I never saw any data about how it happens or why. Yes, my composites looked better when I rolled off saturation in the darks parts of what I was adding. But I never dug into the matter any deeper.

![This is the ColorChecker underexposed by three stops.]({{ "/photographs/blog/2017/instax-rawMinus3.jpg" }})

In the Instax exposure wedge, I can see the lack of saturation as exposure is reduced. Nearly all the color is gone in the minus-three-stops image and the patches register as barely tinted greys. That's a subjective judgement, though so let's dig into it further with numbers.

Digital images are made of pixels. The color of each pixel is determined by three numbers, one each for the anount of red, green, and blue the pixel contains. If I graph those numbers, mapping red on the x-axis, green on the y-axis, and blue on the z-axis, I can represent a digital photograph as a three-dimensional [scatter plot](https://en.wikipedia.org/wiki/Scatter_plot), or as is more common in the VFX business, a point cloud. Usually it looks like a sneeze.

![Most photographs look messy as a point cloud.]({{ "/photographs/blog/2017/instax-pointCloudSneeze.png"}})

[Nuke](https://www.foundry.com/products/nuke), made by [Foundry](http://foundry.com), is the industry-standard image manipulation tool for film and television. I'll be using it for this project because I became very fond of it in [my former life as a compositor](http://www.imdb.com/name/nm2320204/). Nuke offers a few nifty tools for this project. First, it uses a floating-point color pipeline, which means that my 8-bit scans (0 to 255 value range) get remapped to a range from zero to one. This conveniently represents the full gamut of colors reproducable as a [unit cube](https://en.wikipedia.org/wiki/Unit_cube).

![Unit cube representing black, white, and additive primary and secondary colors in the domain [0, 1].]({{ "/photographs/blog/2017/instax-gamutUnitCube.png" }})

Second, it has a handy tool called "PositionToPoints" for turning images into point clouds. That's how I've done all the point clouds in this post. This is much more useful once we start feeding it an image of a test pattern instead of a photograph. Notice how, when we look down the line of midtone values, the outside corners make a nice color wheel.

![Animated RGB unit cube]({{ "/photographs/blog/2017/instax-rgbCubeAni.gif"}})

I'd like to exploit this for my analysis. Lightness is measured along that line. Hue and saturation are determined by how far a point is from the line and in what direction. But that diagonal makes the math part of this a real pain in the butt. I'm not scared of math, but I refuse to do hard work when there's a better option. Instead of looking at the image as RGB data, I can look at it as [YPbPr](https://en.wikipedia.org/wiki/YPbPr) data, which is similar to [Lab](https://en.wikipedia.org/wiki/Lab_color_space) in that it separates lightness and color information, but keeps the shape of the unit cube better.

![Animated Lab unit cube]({{ "/photographs/blog/2017/instax-YPbPrCubeAni.gif"}})

Using YPbPr shifts the greyscale line to the X axis and now I can look at color information as distance and direction from X.

So if I want to graph these color values, a 

 is my best bet. I'll put 

. Why will I do this? Because I'm a compositor, and this is how colors get plotted in Nuke. I'll also be using Nuke's remapping of colors to floating point, so by scan's 0-255 vlaue range will become a 0-1 range. This conveniently represents the full gamut of colors reproducable as a unit cube.

![Unit cube representing black, white, and additive primary and secondary colors in the domain [0, 1].]({{ "/photographs/blog/2017/instax-gamutUnitCube.png" }})


as the exposures get darker, but it seems to reduce differently for different colors.



Like Yedlin, I'm a big fan of visualizing RGB data using the PositionToPoints node in [Nuke](https://www.foundry.com/products/nuke). It's a useful node because you can feed it RGB image data and it will generate a three-dimensional [scatter plot](https://en.wikipedia.org/wiki/Scatter_plot) (a.k.a. point cloud)


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