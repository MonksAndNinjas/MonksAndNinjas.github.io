---
layout: post
title:      "Css - Borders"
date:       2019-10-10 14:13:48 -0400
permalink:  css_-_borders
---


In this post we will be working with various border patterns created using CSS. With that in mind, let's jump right in.

## Continuous image borders

So in the past we have tackled problems using images or patterns as a background, but this time we are going to look at using an image or pattern as a border.

So one solution might  be using border-image property, but this property is not that flexible and only maybe works if you tailor it specifically for the image you are working with. This isn't going to cut for what we need. The easiest way is to use two HTML elements: one using background with the image, and one with a white background covering it for out content area. The results are shown below in the codepen. This works fine,  but it requires an extra HTML element. Thus, this is suboptimal.

Striving for DRYness, we will same effect with only one element. The goal is to use a second background of pure white, covering the image. We will also apply different values of background-clip to make the second image show through the border area. Additionally, we need to fake the white via a CSS gradient from white to white. First attempt at the code is as follows:

```
padding: 1em;
border: 1em solid transparent;
background: linear-gradient(white, white),
                           url(image.jpg);
background-size: cover;
background-clip: padding-box, border-box;
```

This will bring us closer to what we want, but there are some unexpected repitition. The reason is that the default background-origin is padding-box, and so, the image is sized based on the padding-box and placed on the 0,0 point on the padding box. The rest is just repititions of that first background tile. To fix this, we will set the background-origin to border-box as well. The final result is show below in the codepen. 

> Continuous Image Border -
> //codepen.io/monksandninjas/embed/VwwvWXw?height=265&theme-id=0&default-tab=css,result
> https://codepen.io/monksandninjas/pen/VwwvWXw

Now we will use the same technique, but this time with gradient-based patterns, like a vintage envelope. Unlike our image border example above, the envelope effect is doable with border-image too. However, this approach has several issues:

* We need to update border-image-slice every time we change the border-width and make them match.
* Because we cannot use ems in border-image-slice, we are restricted to only pixels for the border thickness.
* The stripe thickness needs to be encoded in the color stop positions, so we need to make four edits to change it.

Final result is show below in the codepen:

> Vintage Envelope -
> //codepen.io/monksandninjas/embed/LYYpjVp?height=265&theme-id=0&default-tab=css,result
> https://codepen.io/monksandninjas/pen/LYYpjVp

For our next exercise we will create marching ants box. To create this effect we will convert the stripes to just black and white, reduce the width of the border to 1px (notice how the stripes now turn to a dashed border?), and change the background-size to something appropriate. Then, we animate the background-position to 100% to make it scroll.

> Marching Ants -
> //codepen.io/monksandninjas/embed/gOOaxwx?height=265&theme-id=0&default-tab=css,result
> https://codepen.io/monksandninjas/pen/gOOaxwx

Finally, we end with mimicing traditional footnotes. It's pretty simple, result is show below.

> Footnotes -
> //codepen.io/monksandninjas/embed/oNNjeZL?height=265&theme-id=0&default-tab=css,result
> https://codepen.io/monksandninjas/pen/oNNjeZL

And that concludes our segment on continuous image borders, thanks for reading and don't miss our next post on shapes using CSS.

