---
layout: blog
title:  TimeBlur for concatenating motion blur 
tags: 
 - compositing
category: blog
---

![Nuke node graph]( {{ "/assets/posts/2014-08-18-concatenating-motion-blur/nuke-node-graph.gif" | relative_url }})

Last week I needed to concatenate the motion blur for a SplineWarp, a Transform, and two CornerPins in [Nuke](https://www.foundry.com/products/nuke). The Transform and the CornerPins, of course, concatenate beautifully once you make sure they are all using the same filter and motion blur settings. But the SplineWarp doesn’t. In fact, it doesn’t even have a motion blur option. Bummer.

I worked around this problem by using a TimeBlur node. Wrapping the stack of transforms in a NoTimeBlur/TimeBlur sandwich gave me motion blur concatenation for all four nodes. It also let me turn off motion blur on the Transform and CornerPin nodes. This made me happy because motion blur on the CornerPin is slow. The default of 10 divisions was a little overkill for my application, so I turned it down to 5 and got a bit of a performance boost.

Don’t forget to add the NoTimeBlur directly upstream from the nodes you want to TimeBlur. If you don’t, you’ll be doing expensive fractional frame processing for the entire node tree up to that point!