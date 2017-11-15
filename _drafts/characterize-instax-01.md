---
layout: blog
title:  "Characterizing Instax Mini, part 1: the setup"
tags: 
 - imaging 
 - film
category: blog
---

![Instax Mini exposure wedge]( {{ "/photographs/blog/2017/instax-wedge-horiz.jpg" | absolute_url }})

Here's the plan: We're going make our own technique for getting “that film-look” from digital cameras. Specifically, we’ll be trying to recreate the look of [Instax film](http://www.fujifilm.com/products/instant_photo/films/instax_mini/).

We're going to do it by following in cinematographer Steve Yedlin's footsteps. Maybe you've heard of him? He shot Brick, Looper, and the new Star Wars movie that's coming out soon. Here’s a [brief introduction](https://storify.com/tvaziri/steve-yedlin) (in tweets, natch) to him and what he’s up to with film modeling.

Yedlin doesn't believe in "the mystery of film." He believes film has specific artifacts that can be isolated, modeled, and simulated. According to him, as long as you find all the artifacts and model them accurately, you can then recreate the "look" of film using digital cameras.

Yedlin's [Display Prep Demo](http://yedlin.net/DisplayPrepDemo/) compares cinematic images shot on film with digital footage that he modified to look like film using the techniques he's developed. Have a look at the Demo. See if you can pick which clips are film and which are digital. I sure can't. He claims that nobody has been able to pick which is film and which is digital any better than if they'd just guessed.

He's done a bunch of writing on [his web site](http://yedlin.net/OnColorScience/) and on Twitter ([@steveyedlin](https://twitter.com/steveyedlin)) about film and color. There's a lot of detail that that I'm glossing over here. Here's a quote from him about why this matters ([Via Twitter](https://twitter.com/steveyedlin/status/686314296679219201?ref_src=twsrc%5Etfw&ref_url=https%3A%2F%2Fstorify.com%2Ftvaziri%2Fsteve-yedlin))

> The reason I got interested in color science is not that I don't like film. It's that [I] love film and don't want [its] tradition to vanish.


For this project, we will focus on the color response of film. When Yedlin was developing this part of his display prep technique, he used an Arri SkyPanel to display lots and lots of different colors to two cameras, one film-based and one with a digital sensor. This allowed him to build a [LUT](http://nofilmschool.com/2011/05/what-is-a-look-up-table-lut-anyway) for applying the film response to the digital capture.

[SkyPanels are expensive.](https://www.bhphotovideo.com/c/product/1139001-REG/arri_l0_0007063_skypanel_s60_c_led_softlight.html)

But I do happen to have a ColorChecker that we can use. We only get 16 color patches with it, and they're not evenly spaced through the color spectrum. We won’t be able to make a LUT directly, but we can at least start our investigation about what happens to color at different exposures.

I'm using a [Lomo Instant Automat](https://www.kickstarter.com/projects/lomography/the-lomoinstant-automat-camera) to make the exposures. The Automat's onboard meter assumes that the scene in front of the camera is average because, well, that's how onboard meters work. So made my scene as average as possible. I took my 18% grey card to the paint store, had them color match it, and painted a piece of plywood. This gives me a really big grey card that the meter can see and set a consistently correct exposure. I'll tape my ColorChecker and a few other references in the middle of it, make sure the lighting is even from top to bottom, and we're all set.

![The ColorChecker and other charts on an 18% grey-painted board]( {{ "/photographs/blog/2017/instax-fancySetup.jpg" | absolute_url }} )

The camera sees a big grey card, so it will handle the normal exposure with no problem, but how do I get it to do the overexposed and underexposed steps? I cut 3" squares from [Rosco](http://us.rosco.com/en) half-stop, full-stop, and two-stop neutral density gels. To get underexposure, I held the gel over the lens to cut the amount of light getting to the film. For overexposure, I held them over the meter's photocell opening. I layered two gels to get to three and four stops. This gave me an exposure wedge that goes from 3 stop underexposed to four stops overexposed. 

![Instax Mini exposure wedge]( {{ "/photographs/blog/2017/instax-wedge.jpg" | absolute_url }} )

![Instax Mini exposure wedge, animated]( {{ "/photographs/blog/2017/instax-wedge-anim.gif" | absolute_url }} )

Next time we'll be doing some hard-core numerical analysis on these, but we can already see some interesting artifacts as we compare the exposures. As we might expect, we see the greatest saturation around normal exposure and it reduces as we go towards underexposure and overexposure. Yellows and oranges (a.k.a. skin-tone hues) seem to be doing pretty well in both underexposure and in overexposure. This makes sense in a film tailor-made for selfies. Greens drop out after 1 stop of underexposure and shift toward orange in overexposure. The darkest colors, blues and purples, are taking a beating in underexposure. 

These non-linearities that are built into Instax film would be hard to identify in normal photos, but our ColorChecker provides a useful reference for identifying them. Next we'll dig into the analysis. We'll use some tools in Nuke to help us visualize these results and also plot saturation graphs for the primary and secondary colors.


