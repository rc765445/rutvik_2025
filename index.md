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


<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Mario Animation</title>
  <style>
    body {
      margin: 0;
      background-color: #87CEEB;
      overflow: hidden;
    }

    .sprite {
      position: absolute;
      height: 256px;
      width: 256px;
      background-image: url('https://i.imgur.com/Tpi5Bcf.png'); /* Sample sprite sheet for Mario */
      background-repeat: no-repeat;
    }

    /* This will be used to set the background position for the sprite */
    #mario {
      background-position: 0px 0px; /* Initial Mario position */
    }
  </style>
</head>
<body>

  <div id="mario" class="sprite"></div>

  <script>
    // Define the sprite dimensions
    const spriteWidth = 256;   // Width of each frame
    const spriteHeight = 256;  // Height of each frame

    // Get the mario element
    const marioElement = document.getElementById("mario");

    // Define animation metadata
    const marioFrames = {
      "Walk": { row: 0, frames: 3 },
      "Run": { row: 1, frames: 3 },
      "Rest": { row: 2, frames: 1 }
    };

    // Setup the initial state for Mario
    let currentFrame = 0;
    let currentSpeed = 0;
    let positionX = 0;
    let frameCount = marioFrames["Walk"].frames;
    let tID = null;

    // Function to animate Mario
    function animateMario(row, frames, speed) {
      tID = setInterval(() => {
        // Calculate column position based on current frame
        const col = currentFrame * spriteWidth;
        marioElement.style.backgroundPosition = `-${col}px -${row * spriteHeight}px`;

        // Move Mario horizontally
        marioElement.style.left = `${positionX}px`;
        positionX += speed;  // Move Mario to the right

        // Loop frames and handle the screen edges
        currentFrame = (currentFrame + 1) % frames;
        if (positionX > window.innerWidth) {
          positionX = -spriteWidth;  // Reset position to start from left
        }
      }, 150);  // Run every 150ms
    }

    // Start animation based on key press
    window.addEventListener("keydown", (event) => {
      if (event.key === "ArrowRight") {
        event.preventDefault();
        if (tID) clearInterval(tID);  // Stop any running animation

        if (currentSpeed === 0) {
          animateMario(marioFrames["Walk"].row, marioFrames["Walk"].frames, 3);  // Walk
        } else {
          animateMario(marioFrames["Run"].row, marioFrames["Run"].frames, 6);   // Run
        }
        currentSpeed += 3;  // Increase speed with each key press
      } else if (event.key === "ArrowLeft") {
        clearInterval(tID);  // Stop animation
        marioElement.style.backgroundPosition = `0px -${marioFrames["Rest"].row * spriteHeight}px`;  // Rest frame
        currentSpeed = 0;  // Reset speed
      }
    });

    // Start resting animation on load
    document.addEventListener("DOMContentLoaded", () => {
      marioElement.style.backgroundPosition = `0px -${marioFrames["Rest"].row * spriteHeight}px`;
    });
  </script>

</body>
</html>
