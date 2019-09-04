---
layout: post
title:      "CSS - Nuances in Backgrounds and Borders"
date:       2019-09-03 16:49:33 -0400
permalink:  css_-_nuances_in_backgrounds_and_borders
---


As a designer, my specialty will lie on the front side of the full-stack. With that in mind, I've decided to dedicate some of my blog posts cleaning up my css skills. Having a strong understanding of border and background manipulation has been important to me as much of what I do and enjoy is making borders and their contents behave in reliable ways. Whether it be multiple borders, changing colors, shadows, or inserting svg's, I have developed an appreciation of the difficulty of creating responsive websites. In this blog posts you will learn some basic options to correcting some pain in the butt problems involving css, borders, and backgrounds. So let's jump in and tackle some problems! 

## Translucent Border

Let's say we want to create a white background with a semi-transparent white border and have our body background visible. With the example shown below, our first attempt would be the box displayed on the top. With the correct method displayed on the bottom. As you can see, the first attempt, has made our border disapear. Despite the border seeming to disapear, it is still there and by default, backgrounds extend underneath the border area. Instead of having a semi-transparent white border through which our nice body background is shown, we ended up having semi-transparent white borders on opaque white, which are indistinguishable from plain white borders.

To correct this unholy mess, we want our background to not extend underneath the border, all we have to do is give it the value padding-box, which tells the browser to clip the background at the padding edge. That looks way better!

```
 See the Pen <a href='https://codepen.io/monksandninjas/pen/PoYJLGE/' data='5'>Translucent Borders</a> by MonksAndNinjas
  (<a href='https://codepen.io/monksandninjas'>@monksandninjas</a>) on <a href='https://codepen.io'>CodePen</a>.
```
## Multiple Borders

So when dealing with multiple borders one type of solution is the over-used box-shadow to create shadows. What was new to me was that it accepts a fourth parameter called the "spread radius", which makes the shadow larger (positive lengths) or smaller (negative lengths) by the amount specified. A positive spread radius combined with zero offsets and zero blur creates a "shadow" that looks more like a solid border. This is not the most ideal method, as you can create the same kind of border by using the border property. What's also pretty neat is that we can have as many box-shadows that we want, all we need to do is separate them with a comma as shown below. Some things should be pointed out using this method. 

* First, shadows don't exactly work like borders, as they don't affect layout and are oblivious to the box-sizing property. However, you can emulate the extra space a border would occupy via padding or margins depending on whether the shadow is inset or not.

* Second, the method creates fake "borders" on the outside of elements. These do not capture mouse events such as hovering or clicking. If this is important, you can add the inset keyword to make the shadows be drawn on the inside of the element.

Let's say, however, we only need two borders, we can use a regular border and the outline property for the outer one. This will also give us flexibility with the border style, whereas the shadow method, we can only emulate solid borders. This method also has some limitations.

* First, it only works for two borders, as outline does not accept a comma-seperated list of outlines. 

* Second, outlines do not have to follow rounding, so even if your corners are round, the outline may have straight corners.

* Lastly, outlines may be non-rectangular. Although make sure to test the result in different browsers.

```
  See the Pen <a href='https://codepen.io/monksandninjas/pen/BaBwEyb/' data='1'>Multiple Borders</a> by MonksAndNinjas
  (<a href='https://codepen.io/monksandninjas'>@monksandninjas</a>) on <a href='https://codepen.io'>CodePen</a>.
```

## Flexible Background

It is often that we want to position a background image with offsets from a different corner than the top-left one, such as the bottom right. In the example below we want our background image to have a 10px offset from the right side and a 10px offset from the bottom side. We also want to provide a decent fallback, as some browsers that don't support the extended background-position will place the background image on the top-left corner (default position) ruining everything. To provide a fallback all we have to do is include a bottom right position in the background shorthand as displayed below in the top image. Much better!

A common way to apply offsets from a corner is to make the background image follow padding. Because we would need to update in three different places every time there was a change, this method is not DRY. To fix this we can use the background-origin property set to content-box. Now the side and corner keywords we use in background-position will refer to the edge of the content box. This means that any background images will be offset from the sides or corners as much as our padding is.

Finally, the last method to create the same effect is the calc() solution. We want to position our background image 10px from the bottom and 10px from the right side. If we think of it in terms of offsets from the top-left corner, we basically want an offset of 100%-10px horizontally and 100%-10px vertically. With the calc() function we can do exactly that.

So that concludes our topic for the day! Tune in next time as we look at some more css options for typical problems. 
