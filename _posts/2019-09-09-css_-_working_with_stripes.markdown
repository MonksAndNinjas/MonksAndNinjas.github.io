---
layout: post
title:      "CSS - Working with stripes"
date:       2019-09-09 17:44:18 +0000
permalink:  css_-_working_with_stripes
---


Hey there! We got another installment of working with CSS. This time we are looking at stripes. In the past, whenever I wanted to create stripes I would just create it in photoshop and just convert the image to SVG. In retrospect, this is not the best option as it takes up a lot of memory compared to just using CSS. So today we are going to look at some methods for creating elegant DRY stripes for whatever your purpose. All the examples described below are available to play with in the CodePen at the very bottom of this post. 

## Stripes in Backgrounds

Let's start this example by working with the background property for our div tag. From there let's use the linear-gradient method. So it looks like this.

```
background: linear-gradient(#fb3, #58a);
```

and let's bring the colors closer together by adding some values to the colors in the method.

```
background: linear-gradient(#fb3 20%, #58a 80%);
```

If we bring them even closer together, say 40% and 60%, the actual gradients get even smaller. Now, making the values equal will make the colors suddenly change at that position rather than smoothly change. We no longer have a gradient, but two solid colors.  Because gradients are just background images, we can treat them the same way and adjust their size with background-size.

```
background: linear-gradient(#fb3 50%, #58a 50%);
background-size: 100% 30px;
```

We can also create stripes with unequal widths and simultaneously make the code more DRY by writing it like so:

```
background: linear-gradient(#fb3 30%, #58a 0);
background-size: 100% 30px;
```

We can get a little crazier by making our background three stripes, and the code will not have to change much other than adding four color stops instead of two.

```
background: linear-gradient(#fb3 33.3%, #58a 0, #58a 66.6%, yellowgreen 0);
background-size: 100% 45px;
```

That was easy enough. Let's say, however, we want to make the visually appealing vertical stripes. Our amazing linear-gradient method can also handle this by adding a direction, like so:

```
background: linear-gradient(to right, #fb3 50%, #58a 0);
background-size: 30px 100%;
```

Even cooler, would be making some diagonal stripes, oohhhh yeaaaah!

```
background: linear-gradient(45deg, #fb3 50%, #58a 0);
background-size: 30px 30px;
```

That didn't quite work out, instead it made this, also cool, but not what we want tiling. To correct this, we need to add a couple more color stops.

```
background: linear-gradient(45deg, #fb3 25%, #58a 0, #58a 50%, #fb3 0, #fb3 75%, #58a 0);
background-size: 30px 30px;
```

While this method gives us the desired effect, it isn't quite flexible as changing the angle will make us have to use an irrational number that will make the code look sloppy. A better way, that avoids all this messiness is by using the repeating-linear-gradient method. 

```
background: linear-gradient(60deg, #fb3, #fb3 15px, #58a 0, #58a 30px);
```

Now it's a matter of changing the angle.

Finally, we end with creating flexible sublte stripes. If we would like to use colors that vary subtly in brightness we can use a semi-transparent white instead of figuring out what the code is for those two colors. 

```
background: #58a;
background-image: repeating-linear-gradient(30deg, hsla(0,0,100%,.1),
hsla(0,0%,100%,.1) 15px,
transparent 0, transparent 30px);
```

Now we just have to change one value, instead of two for manipulating our stripe colors.

Well, there you have. Play around with the code in the CodePen below. Thanks for checking out the blog and stay tuned for some more CSS tips down the line.

> Striped Backgrounds -
> //codepen.io/monksandninjas/embed/eYOMYJV/?height=265&theme-id=0&default-tab=css,result
> https://codepen.io/monksandninjas/pen/eYOMYJV/

