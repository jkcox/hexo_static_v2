---
title: Making an HTML Element Full Screen Width Inside a Fixed Width Container
date: 2016-02-25 16:20:25
tags: 
    - Front-end
    - CSS
categories:
  - Web Development
  - Front-End
  - CSS
author: John Cox
---
We came across a design that we found to be difficult to solve, at least under the terms that the client had requested. On mobile, our content area stays at a fixed size. The design had a social share icon area that was inside our content area above the footer, but stretched full width beyond the content area. We ended up not using this solution and changing the design for the area to only be as wide as our content area, but that was only because we are required to support some older devices that are inconsistent in dealing with some of the newer CSS properties. 

If for some reason you cannot use `overflow: visible` because you are floating other elements within the container, this seems to be a good solution depending on the browsers that you need to support. Check out the jsfiddle to view the container CSS.

``` css Full view with Elements inside fixed width container https://jsfiddle.net/black_cat/0hezseLt/ jsfiddle
width: 100vw;
margin-left: -webkit-calc((100vw - 320px) / -2);
margin-left: calc((100vw - 320px) / -2);
```
Just replace 320px with the size of your fixed container and the functions with do all the calculations. 