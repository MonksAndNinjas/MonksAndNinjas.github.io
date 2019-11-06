---
layout: post
title:      "CSS - Parallelograms"
date:       2019-11-06 23:31:45 +0000
permalink:  css_-_parallelograms
---


Welcome back! We're at it again with CSS, and this time we are making parallelograms. The rectangular superset gives a more dynamic look for your website. In this post we will start things off by making a button-style link. Our first bit of code is shown below. We also use the skew() function to create the parallelogram look.

```
transform: skewX(-45deg);
```

The problem with this is that it also skews the content within the shape. To fix the problem we could add an extra HTML element to wrap around teh content, such as a div. The code for that is:

```
<a href="#yolo" class="button">
      <div>Click me</div>
</a>

.button { transform: skewX(-45deg); }
.button > div { transform: skewX(45deg);  }
```

This almost satisfies our needs but it would be better to have an only CSS solution. Tada!! Check out the codepen below.

> Parallelograms - 
> //codepen.io/monksandninjas/embed/yLLKoxg?height=265&theme-id=0&default-tab=css,result
> https://codepen.io/monksandninjas/pen/yLLKoxg

Another way of creating a parallelogram is to use a pseudo-element to apply all styling to backgrounds, borders, etc., and then transform that. Becuase the conent is not contained in the pseudo-element, it is not affected by the transformation. 

To perform this action we need the pseudo-element box to remain flexible and automatically inherit the dimensions of its parent. To do this we will need to apply position relative to the parent, make the position absolute to the generated content, and set all offsets to zero so that it stretches horizontally and vertically to the size of the parent. The code will look as such:

```
.button { position: relative; } // text color, paddings, etc. 

.button::before {
     content: '';
		 position: absolute;
		 top: 0; right: 0; bottom: 0; left: 0;
}
```

The generated box is above our content and will obscure the contents once we apply some background to it. To fix this, we can apply z-index: -1 to the pseudo-element, so that it moves underneath its parents. The new code will look like this:

```
.button { position: relative; } // text color, paddings, etc. 

.button::before {
     content: ''; // to generate the box
		 position: absolute;
		 top: 0; right: 0; bottom: 0; left: 0;
		 z-index: -1;
		 background: #58a;
		 transform: skew(45deg);
}
```

This technique, not only works with skew(), but also for techniques such as rotate(). Other cases include: multiple backgrounds, Inner Rounding; applying opacity to background, and to emulate multiple borders in a more flexible way. Codepen for this technique is shown below.

> Pseudo-element parallelogram - 
>  //codepen.io/monksandninjas/embed/ZEEoOZz?height=265&theme-id=0&default-tab=css,result
>  https://codepen.io/monksandninjas/pen/ZEEoOZz

Thanks for checking us out!!
