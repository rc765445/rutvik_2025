---
layout: post
title: 🧠 Ai Chatbot Event Finder for Los Angeles & San Diego
permalink: /Event Helper/
---


<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Event Finder Chatbot</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      padding: 20px;
      max-width: 600px;
      margin: auto;
      background-color: #f4f4f4;
    }
#chat {
      background: white;
      padding: 20px;
      border-radius: 10px;
      height: 400px;
      overflow-y: auto;
      border: 1px solid #ccc;
      margin-bottom: 10px;
    }
.message {
      margin: 10px 0;
    }
.user {
      text-align: right;
      color: blue;
    }
.bot {
      text-align: left;
      color: green;
    }
input[type="text"] {
      width: 80%;
      padding: 10px;
      border-radius: 5px;
      border: 1px solid #ccc;
    }
button {
      padding: 10px 15px;
      border: none;
      border-radius: 5px;
      background-color: #008cba;
      color: white;
      cursor: pointer;
    }
a {
      color: #0066cc;
    }
  </style>
</head>
<body>
  <h2>🎉 Event Finder Chatbot</h2>
  <div id="chat"></div>
  <input type="text" id="userInput" placeholder="Type your city (e.g., Los Angeles)" />
  <button onclick="sendMessage()">Send</button>

  <script>
    const chat = document.getElementById("chat");

    const events = {
      "los angeles": [
        {
          name: "Hollywood Bowl Concert",
          date: "2025-06-10",
          location: "2301 N Highland Ave, Los Angeles, CA",
          map: "https://www.google.com/maps?q=2301+N+Highland+Ave,+Los+Angeles,+CA"
        },
        {
          name: "Downtown Art Walk",
          date: "2025-06-15",
          location: "634 S Spring St, Los Angeles, CA",
          map: "https://www.google.com/maps?q=634+S+Spring+St,+Los+Angeles,+CA"
        }
      ],
      "san diego": [
        {
          name: "Balboa Park Summer Festival",
          date: "2025-06-12",
          location: "1549 El Prado, San Diego, CA",
          map: "https://www.google.com/maps?q=1549+El+Prado,+San+Diego,+CA"
        },
        {
          name: "Gaslamp Quarter Night Market",
          date: "2025-06-18",
          location: "Fifth Ave, San Diego, CA",
          map: "https://www.google.com/maps?q=Fifth+Ave,+San+Diego,+CA"
        }
      ]
    };

    function addMessage(text, sender) {
      const msg = document.createElement("div");
      msg.className = "message " + sender;
      msg.innerHTML = text;
      chat.appendChild(msg);
      chat.scrollTop = chat.scrollHeight;
    }

    function sendMessage() {
      const input = document.getElementById("userInput");
      const city = input.value.trim().toLowerCase();
      addMessage("You: " + city, "user");

      if (events[city]) {
        let response = "<strong>Here are some events in " + city.charAt(0).toUpperCase() + city.slice(1) + ":</strong><br>";
        events[city].forEach(event => {
          response += `🎟️ <strong>${event.name}</strong> on ${event.date}<br>📍 ${event.location} - <a href="${event.map}" target="_blank">Map</a><br><br>`;
        });
        addMessage(response, "bot");
      } else {
        addMessage("Sorry! I don't have event info for that city. Try 'Los Angeles' or 'San Diego'.", "bot");
      }

      input.value = "";
    }
  </script>
</body>
</html>
```
