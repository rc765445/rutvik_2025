---
layout: base
title: Homepage
description: Rutvik Chavda's GitHub Page!
author: Rutvik Chavda
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
<style>

  /*CSS style rules for the id and class of the sprite...
  */
  .sprite {
    height: {{pixels}}px;
    width: {{pixels}}px;
    background-image: url('{{sprite_file}}');
    background-repeat: no-repeat;
  }

  /*background position of sprite element
  */
  #mario {
    background-position: calc({{animations[0].col}} * {{pixels}} * -1px) calc({{animations[0].row}} * {{pixels}}* -1px);
  }
</style>

<!--- Embedded executable code--->
<script>
  ////////// convert YML hash to javascript key:value objects /////////

  var mario_metadata = {}; //key, value object
  {% for key in hash %}  
  
  var key = "{{key | first}}"  //key
  var values = {} //values object
  values["row"] = {{key.row}}
  values["col"] = {{key.col}}
  values["frames"] = {{key.frames}}
  mario_metadata[key] = values; //key with values added

  {% endfor %}

  ////////// game object for player /////////

  class Mario {
    constructor(meta_data) {
      this.tID = null;  //capture setInterval() task ID
      this.positionX = 0;  // current position of sprite in X direction
      this.currentSpeed = 0;
      this.marioElement = document.getElementById("mario"); //HTML element of sprite
      this.pixels = {{pixels}}; //pixel offset of images in the sprite, set by liquid constant
      this.interval = 100; //animation time interval
      this.obj = meta_data;
      this.marioElement.style.position = "absolute";
    }

    animate(obj, speed) {
      let frame = 0;
      const row = obj.row * this.pixels;
      this.currentSpeed = speed;

      this.tID = setInterval(() => {
        const col = (frame + obj.col) * this.pixels;
        this.marioElement.style.backgroundPosition = `-${col}px -${row}px`;
        this.marioElement.style.left = `${this.positionX}px`;

        this.positionX += speed;
        frame = (frame + 1) % obj.frames;

        const viewportWidth = window.innerWidth;
        if (this.positionX > viewportWidth - this.pixels) {
          document.documentElement.scrollLeft = this.positionX - viewportWidth + this.pixels;
        }
      }, this.interval);
    }

    startWalking() {
      this.stopAnimate();
      this.animate(this.obj["Walk"], 3);
    }

    startRunning() {
      this.stopAnimate();
      this.animate(this.obj["Run1"], 6);
    }

    startPuffing() {
      this.stopAnimate();
      this.animate(this.obj["Puff"], 0);
    }

    startCheering() {
      this.stopAnimate();
      this.animate(this.obj["Cheer"], 0);
    }

    startFlipping() {
      this.stopAnimate();
      this.animate(this.obj["Flip"], 0);
    }

    startResting() {
      this.stopAnimate();
      this.animate(this.obj["Rest"], 0);
    }

    stopAnimate() {
      clearInterval(this.tID);
    }
  }

  const mario = new Mario(mario_metadata);

  ////////// event control /////////

  window.addEventListener("keydown", (event) => {
    if (event.key === "ArrowRight") {
      event.preventDefault();
      if (event.repeat) {
        mario.startCheering();
      } else {
        if (mario.currentSpeed === 0) {
          mario.startWalking();
        } else if (mario.currentSpeed === 3) {
          mario.startRunning();
        }
      }
    } else if (event.key === "ArrowLeft") {
      event.preventDefault();
      if (event.repeat) {
        mario.stopAnimate();
      } else {
        mario.startPuffing();
      }
    }
  });

  //touch events that enable animations
  window.addEventListener("touchstart", (event) => {
    event.preventDefault(); // prevent default browser action
    if (event.touches[0].clientX > window.innerWidth / 2) {
      // move right
      if (currentSpeed === 0) { // if at rest, go to walking
        mario.startWalking();
      } else if (currentSpeed === 3) { // if walking, go to running
        mario.startRunning();
      }
    } else {
      // move left
      mario.startPuffing();
    }
  });

  //stop animation on window blur
  window.addEventListener("blur", () => {
    mario.stopAnimate();
  });

  //start animation on window focus
  window.addEventListener("focus", () => {
     mario.startFlipping();
  });

  //start animation on page load or page refresh
  document.addEventListener("DOMContentLoaded", () => {
    // adjust sprite size for high pixel density devices
    const scale = window.devicePixelRatio;
    const sprite = document.querySelector(".sprite");
    sprite.style.transform = `scale(${0.2 * scale})`;
    mario.startResting();
  });

</script>

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Rutvik Chavda</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            text-align: center;
            background-color: #f4f4f4;
            margin: 0;
            padding: 0;
        }
        h1 {
            color: #333;
            font-size: 3rem;
            margin-top: 50px;
            animation: colorChange 4s infinite alternate;
        }
        @keyframes colorChange {
            0% { color: #333; }
            50% { color: #ff5722; }
            100% { color: #4caf50; }
        }
        p {
            font-size: 1.5rem;
            color: #555;
        }
        button {
            padding: 10px 20px;
            font-size: 1.2rem;
            background-color: #4caf50;
            border: none;
            color: white;
            cursor: pointer;
            margin-top: 20px;
            transition: background-color 0.3s ease;
        }
        button:hover {
            background-color: #45a049;
        }
        #dynamicText {
            margin-top: 30px;
            font-size: 1.8rem;
            color: #007BFF;
            display: none;
        }
    </style>
</head>
<body>

    <h1>Rutvik Chavda</h1>
    <p>Welcome to my personal web page!</p>
    
    <button onclick="displayMessage()">Click Me</button>
    
    <div id="dynamicText">Welcome to My Page!😀</div>

    <script>
        function displayMessage() {
            var textElement = document.getElementById('dynamicText');
            textElement.style.display = 'block';
        }
    </script>
 

<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Customizable Button in Paragraph</title>
    <style>
        /* Style for the button-link class */
        .button-link {
            display: inline-block;
            padding: 10px 20px;
            font-size: 16px;
            text-align: center;
            text-decoration: none; /* Remove underline from links */
            color: white; /* Text color */
            background-color: #4CAF50; /* Green background */
            border-radius: 5px; /* Rounded corners */
            border: 1px solid #4CAF50; /* Border color same as background */
            transition: background-color 0.3s, border-color 0.3s; /* Smooth transition */
        }

        /* Hover effect for the button */
        .button-link:hover {
            background-color: #45a049; /* Darker green */
            border-color: #45a049; /* Darker border */
        }
        
        /* Additional styles for paragraphs and divisions */
        .container {
            padding: 20px;
            margin: 10px 0;
        }
    </style>

    
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>MyPlan</title>
    <style>
        /* Style for the button-link class */
        .button-link {
            display: inline-block;
            padding: 10px 20px;
            font-size: 16px;
            text-align: center;
            text-decoration: none; /* Remove underline from links */
            color: white; /* Text color */
            background-color: #4CAF50; /* Green background */
            border-radius: 5px; /* Rounded corners */
            border: 1px solid #4CAF50; /* Border color same as background */
            transition: background-color 0.3s, border-color 0.3s; /* Smooth transition */
        }

        /* Hover effect for the button */
        .button-link:hover {
            background-color: #45a049; /* Darker green */
            border-color: #45a049; /* Darker border */
        }
        
        /* Additional styles for paragraphs and divisions */
        .container {
            padding: 20px;
            margin: 10px 0;
        }
    </style>
</head>
<body>

    <p> Click Here to go to MyPlan:</p>

    <!-- Division with button -->
    <div class="container">
        <a href="https://myapps.classlink.com/home" class="button-link">MyPlan</a>
    </div>

</body>
</html>

</head>
<body>
    
    <p> Click Here to go to Canvas:</p>


    <!-- Division with button -->
    <div class="container">
        <a href="https://poway.instructure.com/" class="button-link">Canvas</a>
    </div>

</body>
</html>


</body>
</html>






![image](images/IMG_3654.jpg)
 <!-- Button with Text and Additional Attributes -->

 <td><a href="{{site.baseurl}}/python/">Python</a></td>
    
