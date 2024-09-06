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


--- <!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Animated Mario</title>
  <style>
    body {
      margin: 0;
      overflow: hidden;
      background-color: #87CEEB; /* Sky blue background */
    }
    canvas {
      display: block;
    }
  </style>
</head>
<body>
  <canvas id="gameCanvas"></canvas>

  <script src="mario.js"></script>
</body>
</html>

const canvas = document.getElementById('gameCanvas');
const ctx = canvas.getContext('2d');

canvas.width = window.innerWidth;
canvas.height = window.innerHeight;

const sprite = new Image();
sprite.src = 'mario-sprite.png'; // Replace with the path to your Mario sprite sheet

const spriteWidth = 48;  // Width of one frame of Mario sprite
const spriteHeight = 64; // Height of one frame of Mario sprite
let currentFrame = 0;
const totalFrames = 4;   // Total frames in the sprite sheet (e.g., 4 for walking animation)
const fps = 10;          // Frames per second for the animation
let x = 0;               // X position for Mario's initial location
let y = canvas.height - spriteHeight;  // Y position to place Mario on the ground

function updateFrame() {
  currentFrame = (currentFrame + 1) % totalFrames;
}

function drawMario() {
  ctx.clearRect(0, 0, canvas.width, canvas.height);  // Clear canvas
  ctx.drawImage(sprite, currentFrame * spriteWidth, 0, spriteWidth, spriteHeight, x, y, spriteWidth, spriteHeight);
  x += 2;  // Move Mario to the right
  if (x > canvas.width) x = -spriteWidth;  // Loop Mario to the left once he moves off the screen
}

function gameLoop() {
  updateFrame();
  drawMario();
  setTimeout(gameLoop, 1000 / fps);  // Run the game loop at the desired frame rate
}

sprite.onload = () => {
  gameLoop();  // Start animation once the sprite is loaded
};

window.addEventListener('resize', () => {
  canvas.width = window.innerWidth;
  canvas.height = window.innerHeight;
  y = canvas.height - spriteHeight;
});


