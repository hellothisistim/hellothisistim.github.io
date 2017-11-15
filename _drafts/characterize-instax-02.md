---
layout: blog
title:  "Characterizing Instax Mini, part 2: analysis of primary and secondary colors"
tags: 
 - imaging 
 - film
category: blog
---

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