---
layout: base
title: Student Home 
description: Home Page
image: /images/mario_animation.png
hide: true
---


---
<html>
<head>
<body>

<h1 style= "font-size: 250%; color: blue; font: bold 50x Arial;"> Rutvik Chavda's Github Page </h1>
<h2 style= "font-size: 175%; color: white; font: bold 50x Arial;"> Welcome to my Page </h2>


---
layout: base
title: Course Descriptions
description: An overview of Computer Science pathway at Del Norte High School
author: John Mortensen, Vivian Ni, Bria Gilliam
image: /images/mario_animation.png
hide: true
---

<!-- Liquid:  statements -->

<!-- Include submenu from _includes to top of pages -->
{% include nav/home.html %}
<!--- Concatenation of site URL to frontmatter image  --->
{% assign sprite_file = site.baseurl | append: page.image %}
<!--- Has is a list variable containing mario metadata for sprite --->
{% assign hash = site.data.mario_metadata %}  
<!--- Size width/height of Sprit images --->
{% assign pixels = 256 %}

<!--- HTML for page contains <p> tag named "Mario" and class properties for a "sprite"  -->

<p id="mario" class="sprite"></p>
  
<!--- Embedded Cascading Style Sheet (CSS) rules, 
        define how HTML elements look 
--->