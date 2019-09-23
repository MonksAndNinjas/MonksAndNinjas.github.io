---
layout: post
title:      "CSS - Complex Backgrounds Part 2"
date:       2019-09-23 17:10:38 +0000
permalink:  css_-_complex_backgrounds_part_2
---


In part 1 of complex backgrounds we discussed creating grids, and polka dots in css. Moving on, we now wll look at checkerboard patterns. Despite the familiarity and simplicity of checkboard patterns in real life, it proves to be harder than expected to recreate this pattern using css.

## Checkerboard

One might think that all one has to do to create the pattern would be to create two squares with different background positions, but with no spacing around them, the result will look like a solid color. The actual method requires one to compose the square from two right triangles. The first part of our code will create a repeating pattern of squares with space around it.

```
background: #eee;
background-image:
       linear-gradient(45deg, #bbb 50%, transparent 0);
background-size: 30px 30px;
```

This bit of code might not seem useful at first, but if we reduce the legs of these triangles to half their original size, they will occupy 1/8 of the tile instead of 1/2. This adjustment will give as an array of right triangles with a lot of spacing around them.

```
background: #eee;
background-image:
       linear-gradient(45deg, #bbb 25%, transparent 0);
background-size: 30px 30px;
```

And if we flip the color stops, we get triangles in opposite directions.

```
background: #eee;
background-image:
       linear-gradient(45deg, #bbb 75%, transparent 0);
background-size: 30px 30px;
```

And if we combine the two, and move the second gradient by half the tile size like so:

```
background: #eee;
background-image:
       linear-gradient(45deg, #bbb 25%, transparent 0);
			 linear-gradient(45deg, transparent 75%, #bbb 0);
background-position: 0 0, 15px, 15px;
background-size: 30px 30px;
```

we get even closer. It now looks like half a checkerboard. To finish the job, we repeat the two gradients to create another set of squares and offset their positions again. Taddaaa! 

> Checkerboard - 
>  //codepen.io/monksandninjas/embed/eYOxZEE?height=265&theme-id=0&default-tab=css,result
> https://codepen.io/monksandninjas/pen/eYOxZEE

It's not very DRY, and so this might be a situation where an SVG will get the job done in an efficient way. 

## Psuedo random backgrounds

So far we've been working with very strict patterns that are not random, but nature doesn't really look quite like that. In nature objects appear to form in a consistent pattern, but if you look closely they tend to have a patten and then veer off from it and perhaps start another similar pattern.

Recreating this in code can be challenging, mostly because CSS does not have this capability. Going back to our stripes knowledge we'll start four stripes represent by four different colors. We'll create this by using a linear gradient for all four stripes.

```
background:
       linear-gradient (90deg, 
			       #fb3 15%, #655 0, #655 40%, 
			       #ab4 0, #ab4 65%, hsl(20, 40%, 90%) 0);
background-size: 80px 100%;
```

This bit of code is without a doubt a repeating pattern. To enhance the effect of randomness we will next split the flat stripe tile into layers: one base color and three layers of stripes, repeating in different intervals. Using color stops and background-size we end up with the following:

```
background: hsl (20, 40%, 90%);
background-image:
       linear-gradient (90deg, #fb3 10px, transparent 0),
			 linear-gradient (90deg, #ab4 20px, transparent 0),
			 linear-gradient( 90deb, #655 20px, transparent 0);
background-size: 80px 100%, 60px 100%, 40px 100%;
```

This pattern is better, but if you look closely it repeats every 240px. To increase the sense of randomness we need to maximize the size of the repeating tile. I won't go into the details of it but it involves math and prime numbers. The final code is show below:

> Pseudo Randomness - 
>  //codepen.io/monksandninjas/embed/zYOeBOJ?height=265&theme-id=0&default-tab=css,result
>  https://codepen.io/monksandninjas/pen/zYOeBOJ

And so, while it's not DRY, we have been able to make the tiles repeat in such a way that the pattern pixel width is larger than any screen resolution one could find. This idea of using prime numbers is an established way to create a sense of randomness for anything that repeats. 

Hope this was helpful and be on the look out for my next post. 
