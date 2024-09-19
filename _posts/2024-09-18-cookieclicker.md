---
layout: post
title: Snake
permalink: /cookieclicker
toc: true
---


<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Cookie Clicker Game</title>
    <style>
        body {
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            height: 100vh;
            background-color: #f5f5f5;
            font-family: Arial, sans-serif;
        }

        #cookie {
            width: 200px;
            height: 200px;
            background-image: url('https://via.placeholder.com/200.png?text=Cookie');
            background-size: cover;
            cursor: pointer;
            margin-bottom: 20px;
            border-radius: 50%;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.5);
        }

        #score {
            font-size: 24px;
            margin-bottom: 20px;
        }

        #upgrades {
            display: flex;
            flex-direction: column;
            align-items: center;
        }

        .upgrade {
            margin: 5px;
            padding: 10px 15px;
            background-color: #4caf50;
            color: white;
            border: none;
            cursor: pointer;
            border-radius: 5px;
            font-size: 18px;
        }

        .upgrade:disabled {
            background-color: #aaa;
        }
    </style>
</head>
<body>
    <div id="cookie"></div>
    <div id="score">Cookies: 0</div>
    <div id="upgrades">
        <button class="upgrade" id="upgrade1">Upgrade: +1 cookie per click (Cost: 10 cookies)</button>
        <button class="upgrade" id="upgrade2">Upgrade: +5 cookies per click (Cost: 50 cookies)</button>
    </div>
    <script>
        let cookies = 0;
        let cookiesPerClick = 1;

        const cookieElement = document.getElementById('cookie');
        const scoreElement = document.getElementById('score');
        const upgrade1Button = document.getElementById('upgrade1');
        const upgrade2Button = document.getElementById('upgrade2');

        cookieElement.addEventListener('click', () => {
            cookies += cookiesPerClick;
            updateScore();
            checkUpgrades();
        });

        function updateScore() {
            scoreElement.innerText = `Cookies: ${cookies}`;
        }

        function checkUpgrades() {
            upgrade1Button.disabled = cookies < 10;
            upgrade2Button.disabled = cookies < 50;
        }

        upgrade1Button.addEventListener('click', () => {
            if (cookies >= 10) {
                cookies -= 10;
                cookiesPerClick += 1;
                updateScore();
                checkUpgrades();
            }
        });

        upgrade2Button.addEventListener('click', () => {
            if (cookies >= 50) {
                cookies -= 50;
                cookiesPerClick += 5;
                updateScore();
                checkUpgrades();
            }
        });

        checkUpgrades();
    </script>
</body>
</html>
