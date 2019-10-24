---
layout: post
title:      "CSS - Shapes"
date:       2019-10-24 19:29:57 +0000
permalink:  css_-_shapes
---


So we are back for some more CSS, and we will be discussing shapes. 

## Flexible Ellipses

You may have noticed that any square created in css and with a sufficiently large enough border-radius can turn into a circle. Just like this:

```
background: #fb3;
width: 200px;
height: 200px;
border-radius: 100px; /* >= half the side */
```

On top of that we can also specify any radius larger than 100px and it will still result in a circle. This happens because when the sum of any two adjacent border radii exceeds the size of the border box, user agents must proportionally reduce the used values of all border radii until none of them overlap.

However, we often cannot provide a specific width and height of an element, because of the need to adjust to its content, which may not be known. The question then becomes, can we use border-radius to make an ellipse, let alone a flexible one?

To start off, it is not often known that border-radius accepts different horizontal and vertical radii, if you use a slash(/) to seperate the two. This little bit of syntax allows us to create elliptical rounding at the corners. However, this results in a major flaw. If the dimensions change, the border-radius values need to change as well. When the dimensions vary depending on content, it seems we may have a problem. Fortunately, another lesser known feature of border-radius is that it accepts percentages, not just lengths. This feature means the same percentage can compute to different horizontal and vertical radii. Check out the codepen below for an example.

> Flexible Ellipses - 
> //codepen.io/monksandninjas/embed/NWWjXxL?height=265&theme-id=0&default-tab=css,result
> https://codepen.io/monksandninjas/pen/NWWjXxL

## Half Ellipses

Armed with a descent understanding of making an ellipse we can now tackle making half ellipses or half circles. Just like before we can use border-radius, but this time we will seperate out each corner of the square so we can control the shape and then make the code DRY by using shorthand. For example, border-radius value of 10px/ 5px 20px is equivalent to 10px 10px 10px 10px/ 5px 20px 5px 20px. 

Before writing code, let's make some observations.

* The shape is symmetrical horizontally => top left and top right radii should be the same. Also bottom left and bottom right radii should also match.
* There are no straight horizontal edges at the top => the top left and top right radii together should total 100% of the shape's width.
* Horizontal left and horizontal right radii should be 50%.
* The vertical part of the border-radius would be 100% 100% 0 0, since the height of the shape is in the top half.
* Lastly bottom vertical rounding is zero.

All together, our possibilities are shown below.

> Half Ellipses - 
>  //codepen.io/monksandninjas/embed/OJJmzgw?height=265&theme-id=0&default-tab=css,result
>  https://codepen.io/monksandninjas/pen/OJJmzgw

## Quarter Ellipses
We end this post with making quarter ellipses. What we need to know is that one of the corners needs to have a 100% radius both horizontally and vertially, and the other four will have no rounding. 

> Quarter Ellipses - 
> //codepen.io/monksandninjas/embed/QWWvaOP?height=265&theme-id=0&default-tab=css,result
> https://codepen.io/monksandninjas/pen/QWWvaOP

That concludes this topic and stay tuned for another installment.

