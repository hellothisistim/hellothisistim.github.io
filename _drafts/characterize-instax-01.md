---
layout: blog
title:  "Characterizing Instax Mini, part 1: the setup"
tags: 
 - imaging 
 - film
category: blog
---

There's no shortage of info on how to get "that film look" with digital, so [exit now](https://www.google.com/search?q=photo+filter+film+look) if you only have time for a plugin recommendation or a 5-step tutorial. This is going to be a deep dive and I don't believe in easy answers.

Still with me? Good! Here's the plan: We're going to create our own film look based on [Instax film](http://www.fujifilm.com/products/instant_photo/films/instax_mini/) and read Yedlin's excellent article On Color Science.



Here's cinematographer Steve Yedlin, writing about his Film Prep Demo, where he compares finematic images shot on film with digital footage that has been prepared to look like film:

> So, the question is: can we as filmmakers identify, isolate and understand any of these underlying attributes so that we can manipulate them meaningfully for ourselves, or are we forever relegated to the status of shoppers; browsing for pre-packaged solutions and then wearing the badge of brand allegiance to the one we select.





I recently saw the [Display Prep Demo](http://yedlin.net/DisplayPrepDemo/) by cinematographer [Steve Yedlin](http://yedlin.net) ([@steveyedlin](https://twitter.com/steveyedlin)) and read some of the smart stuff on his website about 

This investigation was triggered by [some writing](http://www.yedlin.net/160105_edit.html) that cinematographer [Steve Yedlin](http://yedlin.net) did recently, supporting his [Display Prep Demo](http://yedlin.net/DisplayPrepDemo/). Yedlin doesn't believe in "the mystery of film." He believes film has specific artifacts that can be isolated, modeled, and simulated. According to him, as long as you find all the artifacts and model them accurately, you can then recreate the "look" of film using digital cameras. Yedlin has been working to identify, model, and simulate those artifacts. The 

) is his proof. Have a peek for yourself and see if you can tell what's film and what's digital prepped to look like film. I'm convinced he nailed it. He claims that nobody has been able to pick which is film and which is digital any better than if they'd just guessed.

My reference target is a [ColorChecker Classic](http://xritephoto.com/colorchecker-classic) chart from X-Rite. I'm using it because I already own one, and also because X-Rite and others have published data about how the chart should be represented digitally, so we know how it should look on the screen in an ideal situation.

The camera is an [Instant Automat](https://www.kickstarter.com/projects/lomography/the-lomoinstant-automat-camera) that shoots Instax Mini film.







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



Now that we have RGB values as xyz coordinates, from 0,0,0 to 1,1,1 I prefer to have the neutrals run dowmn the z axis, so I rotate -45 degrees around y, then 35.2645 degreen around x (found by experimentation, I didn't do the math), and then scale by 1/1.732 to normalize back into the 0-1 range.


How have I messed this up?
# I didn't wait three days like ??? suggests for the Instax colors to stabilize.
# I cleaned up the big dust & scratches, but left all the little ones. That means my dark values are going to be slightly inaccurate.
# I don't know the spectrum output of the LED lights I used to shoot the Instax. It probably isn't full spectrum. That probably gives me some color-rendering inaccuracies.