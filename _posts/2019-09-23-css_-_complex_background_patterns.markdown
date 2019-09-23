---
layout: post
title:      "CSS - Complex Background Patterns"
date:       2019-09-23 05:38:10 +0000
permalink:  css_-_complex_background_patterns
---


In my previous css posts we've been discussing how to display basic patterns like stripes or how to work with borders. For this post I want to talk about background patterns. In the past if I wanted to have a cool looking pattern as a background I would create the shapes in photoshop and then convert it to an svg so it can have responsive behavior. This is pretty time consuming and can take up a lot of memory, so I learned how to create complex shapes all in css. Let's dive right in. 

## Grids

 Many of these complex patterns can be created by combining multiple gradients and having them show through each other'stansparent regions. One example is the tablecloth pattern, which is shown below. Allowing ourselves to adjust the cell size of the grid and have the width of its lines remain constant, will give us more of a guide grid look. In this case the width was set to 1px. By overlaying two grids with different line width and colors will create a more realistic blueprint grid.
 

> Grids -
> //codepen.io/monksandninjas/embed/XWrooZK?height=265&theme-id=0&default-tab=css,result
> https://codepen.io/monksandninjas/pen/XWrooZK


## Polka Dots

Now we move on from linear gradients to radial gradients. We start by creating an array of circles.  However, it looks much better if we add a little spice to the spacing of the dots. We accomplish this by combining two of those gradients and give them different backgroundk positions. For this to work, the second background position must be half of the tile size. This code is just on the verge of being unmaintainable, because four edits would be required to change the tile size. 

> Polka Dots - 
> //codepen.io/monksandninjas/embed/aboPPXw?height=265&theme-id=0&default-tab=css,result
>  https://codepen.io/monksandninjas/pen/aboPPXw

I'm gonna keep this post short but there is still more to be said about complex shapes. Next up we'll talk about checkerboards.
