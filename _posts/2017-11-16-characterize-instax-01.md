---
layout: blog
title:  "Characterizing Instax Mini, part 1: the setup"
tags: 
 - imaging 
 - film
 - instax
category: blog
---

![Instax Mini exposure wedge]( {{ "/photographs/blog/2017/instax-wedge-horiz.jpg" | absolute_url }})

Inspired by [Steve Yedlin]( {% post_url 2017-09-01-yedlin-display-prep %} )'s work with cinema film, I'm going to try to characterize the look of [Instax film](http://www.fujifilm.com/products/instant_photo/films/instax_mini/). I'll then apply the look of that photochemical process to digital photographs. This project will be ongiong as I dig through the data and build a model to simulate the film.

![The ColorChecker and other charts on an 18% grey-painted board]( {{ site.baseurl }}{{ "/photographs/blog/2017/instax-colorChecker.jpg" | absolute_url }} )

In order to understand how Instax represents various colors at various brightnesses, I shot an exposure wedge of an [X-Rite ColorChecker](http://xritephoto.com/colorchecker-classic) target. An exposure wedge is a sequence of images shot at different exposures, ranging from very dark to very light. This is what it looked like when I finished.

![Instax Mini exposure wedge]( {{ "/photographs/blog/2017/instax-wedge.jpg" | absolute_url }} )

The ColorChecker is useful because it provides a consistent ranage of flat color patches. Between the primary (red, green, and blue) and secondary (cyan, magenta, and yellow) patches, lie all the other more more sublte colors. I'm hoping to discover or invent a way to use those primaries and secondaries to reshape the digital colorspace. The grey patches on the bottom row will help track neutral colors. The top two rows represent common colors like skin tones, pastel colors, foliage, and blue sky. They will become useful later as I fine tune the model.

I shot the exposures with a [Lomo Instant Automat](https://www.kickstarter.com/projects/lomography/the-lomoinstant-automat-camera). The Automat's onboard meter assumes that the scene in front of the camera is average because, well, that's how onboard meters work. So I made my scene as average as possible. I made a really big grey card with a piece of plywood and some 18% grey paint. This card fills the camera's field of view and helps the meter set a consistently correct exposure. I taped my ColorChecker and a few other references in the middle of it and chcecked that the lighting was even from top to bottom. That white paper on the desktop is a big bounce card to fill in the bottom half. I ended up only one third of a stop different from top to bottom.

![Setup for shooting the Instax exposure wedge with an Instant Automat and a ColorChecker]( {{ "/photographs/blog/2017/instax-fancySetup.jpg" | absolute_url }})

The camera was pointing right at my big grey card, so it handled the normal exposure with no problem, but without manual exposure controls I had to trick it do the overexposed and underexposed steps. I cut 3" squares from [Rosco](http://us.rosco.com/en) half-stop, full-stop, and two-stop neutral density gels. To get underexposure, I held the gel over the lens to cut the amount of light getting to the film. For overexposure, I held them over the meter's photocell opening to trick into thinking my office was very dark. I layered two gels to get to three and four stops. This gave me an exposure wedge that goes from 3 stop underexposed to four stops overexposed. 

![Instax Mini exposure wedge, animated]( {{ "/photographs/blog/2017/instax-wedge-anim.gif" | absolute_url }} )

Now that I have the prints scanned, it's time for some hard-core numerical analysis. I'll start that in the next post, but we can already see some interesting artifacts as we compare the exposures. 

As we might expect, we see the greatest saturation around normal exposure and it reduces as we go towards underexposure and overexposure. Yellows and oranges (a.k.a. skin-tone hues) seem to be doing pretty well in both underexposure and overexposure. This makes sense in a film tailor-made for selfies. Greens drop out after 1 stop of underexposure and shift toward orange in overexposure. The darkest colors, blues and purples, are taking a beating in underexposure. They don't really show up at all until the normal exposure. These non-linearities that are built into Instax film would be hard to identify in normal photos, but our ColorChecker provides a useful reference for identifying them.
