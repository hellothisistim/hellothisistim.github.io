---
layout: blog
title:  "Characterizing Instax Mini, part 1: the setup"
tags: 
 - imaging 
 - film
category: blog
---

![Instax Mini exposure wedge]( {{ "/photographs/blog/2017/instax-wedge-horiz.jpg" | absolute_url }})

Here's the plan: We're going make our own technique for getting “that film-look” from digital cameras. Specifically, we’ll be trying to recreate the look of [Instax film](http://www.fujifilm.com/products/instant_photo/films/instax_mini/). We're using Instax because I happen to have some on hand. At some point later, we'll run this again using color film.

In order to see how Instax behaves we'll shoot an exposure wedge, a sequence of images of the same subject at differing exposures, from extremely underexposed to extremely overexposed. Our subject will be an [X-Rite ColorChecker](http://xritephoto.com/colorchecker-classic) target. The ColorChecker is handy because it gives us a range of grey patches, primary and secondary color patches, as well as a selection of patches that represent common colors like skin tones, sky, and foliage. We'll be able to see what happens to these colors as the exposure changes.

I'm using a [Lomo Instant Automat](https://www.kickstarter.com/projects/lomography/the-lomoinstant-automat-camera) to make the exposures. The Automat's onboard meter assumes that the scene in front of the camera is average because, well, that's how onboard meters work. So made my scene as average as possible. I made a really big grey card with a piece of plywood and some 18% grey paint. This card fills the camera's field of view and helps the meter set a consistently correct exposure. I'll tape my ColorChecker and a few other references in the middle of it, make sure the lighting is even from top to bottom, and we're all set.

![The ColorChecker and other charts on an 18% grey-painted board]( {{ "/photographs/blog/2017/instax-fancySetup.jpg" | absolute_url }} )

The camera sees a big grey card, so it will handle the normal exposure with no problem, but how do I get it to do the overexposed and underexposed steps? I cut 3" squares from [Rosco](http://us.rosco.com/en) half-stop, full-stop, and two-stop neutral density gels. To get underexposure, I held the gel over the lens to cut the amount of light getting to the film. For overexposure, I held them over the meter's photocell opening. I layered two gels to get to three and four stops. This gave me an exposure wedge that goes from 3 stop underexposed to four stops overexposed. 

![Instax Mini exposure wedge]( {{ "/photographs/blog/2017/instax-wedge.jpg" | absolute_url }} )

![Instax Mini exposure wedge, animated]( {{ "/photographs/blog/2017/instax-wedge-anim.gif" | absolute_url }} )

Next time we'll be doing some hard-core numerical analysis on these, but we can already see some interesting artifacts as we compare the exposures. As we might expect, we see the greatest saturation around normal exposure and it reduces as we go towards underexposure and overexposure. Yellows and oranges (a.k.a. skin-tone hues) seem to be doing pretty well in both underexposure and in overexposure. This makes sense in a film tailor-made for selfies. Greens drop out after 1 stop of underexposure and shift toward orange in overexposure. The darkest colors, blues and purples, are taking a beating in underexposure. 

These non-linearities that are built into Instax film would be hard to identify in normal photos, but our ColorChecker provides a useful reference for identifying them. Next we'll dig into the analysis. We'll use some tools in Nuke to help us visualize these results and also plot saturation graphs for the primary and secondary colors.


