---
layout: post
title:      "CSS - Cutout Corners"
date:       2019-11-18 15:54:16 -0500
permalink:  css_-_cutout_corners
---


In this post we will be talking about CSS as it relates to cutout corners, for example those snazzy little button effects. It's a popular style in both print and web design. Typically they are displayed as cutting out one or more of an element's corners in a 45 degree angle (i.e. beveled corners). When the cutout corners are only on one side and occupy 50% of the element's height  each, it creates an arrow shape used for navigation.

Most designer/developers use background images to achieve this effect, either by obscuring the cutout corners with triangles, or by using one or more images for the entire background, with the corner(s) already cut. This method is not the most efficient as it is difficult to maintain, and add latency. 

This is where we begin. One solution, using CSS, assumes we only want one cutout corner. Working on the bottom-right, we will use a trick to take advantage of the fact that gradients can accept an angle direction and color stop positions in absolute lengths, both of which are not affected by changes in the dimensions of the element the background is on. All we need is one linear gradient, and it will need a transparent color stop for the cutout corner and another color stop in the same position, with the color we want for our background. Our code will start off looking like so:

```
background: #58a;
background:
       linear-gradient(-45deg, transparent 15px, #58a 0);
```

Technically, we don't need the first declaration. We only include it as a fallback: if CSS gradients are not supported, the second declaration will be dropped, so we will want to get at least a solid color background.

Moving on, let's assume we want two cutout corners, say the two bottom ones. We can't do this with just one gradient, we need two! Maybe like this:

```
background: #58a;
background:
       linear-gradient(-45deg, transparent 15px, #58a 0),
			 linear-gradient(-45deg, transparent 15px, #655 0);
```

The problem with this is that they obscure each other. To fix this, we need to make them smaller, by using background-size to make each gradient occupy only half the element:

```
background: #58a;
background:
       linear-gradient(-45deg, transparent 15px, #58a 0)
			        right,
			 linear-gradient(-45deg, transparent 15px, #655 0)
			        left;
background-size: 50% 100%;
```

With this addition, we can see that although background-size was applied, the gradients are still covering each other. This happened because we forgot to turn background-repeat off, so each of our backgrounds is repeated twice. This causes our backgrounds to still obscure each other. To fix this we just add:

```
background-repeat: no-repeat;
```

There we go! Now let's put this all to this test and see if we can make four beveled corners. Check out the pen below.

> CSS - Cutout Corners - 
> //codepen.io/monksandninjas/embed/GRRPaVy?height=265&theme-id=default&default-tab=css,result
> https://codepen.io/monksandninjas/pen/GRRPaVy

The problem with this solution is that it requires five edits to change the background color and four to change the corner size. Using SCSS can help make the code more efficient, but we won't be covering that here. 

That concludes our blog post for today. Tune in next time to read about "Curved Cutour Corners".


