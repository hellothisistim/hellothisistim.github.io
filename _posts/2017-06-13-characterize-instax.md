---
layout: post
title:  "Characterizing Instax Mini Film"
date:   2017-06-13 9:00:00 -0400
categories: imaging film
published: false
---

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
