---
layout: post
title:  "A splash of jQuery"
date:   2017-05-19 08:26:51 -0400
---


Just as every recipe needs that one super-secret, special ingredient to take it over the top, a splash of jQuery can go a long way when it comes to a basic Rails application. Single page applications are the "It" thing nowadays, and rightfully they should be. For speedy interactability and improved user experience, it becoming more and more expected that web applications should be FAST. The HTML process is inherently SLOW, so it makes sense that we avoid that ish all together.

*1) Bind click handlers*
* Require jQuery-rails in your Gemfile to access this library in your application.
* Lots and lots of $$$

When you are integrating jQuery and AJAX into your application, you start with the broadest of perspectives: $(document). This jQuery selector refers to the entire browser window and encapsulates everything that might happen on the page. As such, any click events need to be bound to $(document). 

P.S. Try adding a little malt vinegar to your grits. You won't be sorry.
