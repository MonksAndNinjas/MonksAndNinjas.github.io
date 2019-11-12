---
layout: post
title:      "CSS - Diamonds"
date:       2019-11-12 18:29:25 +0000
permalink:  css_-_diamonds
---


Hello and welcome back to another css blog post by Monks and Ninjas. Today we will be talking about working with diamonds and images in CSS. So the problem we have is cropping images into a diamond shape, which isn't obvious. One previous solution, not that long ago, was to just cut the image into a diamond shape before putting it into HTML. In the modern age we now have a couple of ways of tackling this problem. The first is called the transform-based solution.

## Transform-Based

This solution is similar in some ways to our secret parallelograms solution in the previous post. We needed to wrap our image with a div tag, then apply opposite rotate() transforms to them, like this:

```
<div class="picture">
      <img src="adam-catlace.jpg" alt="..." />
<div>

.picture {
     width: 400px;
		 transform: rotate(45deg);
		 overflow: hidden;
}
.picture > img {
      max-width: 100%;
			transform: rotate(-45deg);
}
```

If you test the code out yourself, you wil see that this doesn't quite work, as we get an octagon shape.  The missing piece here is some math! The problem is the max-width: 100% declaration 100% refers to the side of our .picture container. However, we want our image to be as wide as its diagonal, not its side. Using the pythagorean theorem will give use some insight. Skipping the math, the theorem tells us that the diagonal of a squre is equal to its side multiplied by 1.414213562. Thus we get the number 142% after rounding up and multiplying by 100%. We want to be slightly larger than this number when using max-width.

Instead of doing this though, we will want the size of the image to remain 100%, in case CSS transforms are not supported. Thus we will scale() the image, like so:

```
.picture {
      width: 400px;
      transform: rotate(45deg);
			overflow: hidden;
}
.picture > img {
       max-width: 100%;
			 transform: rotate(-45deg) scale(1.45);
}
```

## Clipping Path

The next method is called the clipping path solution. Clipping paths allow us to clip the element in the shape that we please. In this case, we're going to use a polygon() shape to specify a diamond.

```
clip-path: plygon(50% 0, 100% 50%, 50% 100%, 0 50%);
```

And with fewer code, we have what we want. This method is also animatable, as long as we animate between the same shape functions( polygon()) with the same number of points. 

And there you have it, working with Diamonds! Next CSS post will cover cutout corners.
