---
layout: post
title: Calculator
permalink: /calculator
toc: true
---


<html>
<head>
  <style>
    /* Style for button when hovered */
    input[type="button"]:hover {
      background-color: #073d94;
    }
/* Style for different buttons /
    .add-button {
      background-color: #3498db;
      color: white;
    }

    .subtract-button {
      background-color: #e74c3c;
      color: white;
    }

    .multiply-button {
      background-color: #f39c12;
      color: white;
    }

    .divide-button {
      background-color: #9b59b6;
      color: white;
    }

    / Style for input boxes */
    input[type="text"] {
      padding: 5px;
      border: 1px solid #1778cd;
      border-radius: 5px;
    }

    h6 {
      font-size: 200%;
    }
  </style>
<title>Binary Operations</title>
</head>
<body>
  <form>
    <label for="binary1">Binary Number 1:</label>
    <input type="text" id="binary1" name="binary1"><br><br>
    <label for="binary2">Binary Number 2:</label>
    <input type="text" id="binary2" name="binary2"><br><br>
    <input class="add-button" type="button" value="Add Binary Numbers" onclick="binaryOperation('add')">
    <input class="subtract-button" type="button" value="Subtract Binary Numbers" onclick="binaryOperation('subtract')">
    <input class="multiply-button" type="button" value="Multiply Binary Numbers" onclick="binaryOperation('multiply')">
    <input class="divide-button" type="button" value="Divide Binary Numbers" onclick="binaryOperation('divide')">
  </form>
  <br>
  <p id="binary_result"></p>
  <p id="decimal_result"></p>
  <script>
    function binaryOperation(operation) {
      var binary1 = document.getElementById("binary1").value;
      var binary2 = document.getElementById("binary2").value;

      var decimalResult, binaryResult;

      if (operation === 'add') {
        decimalResult = parseInt(binary1, 2) + parseInt(binary2, 2);
      } else if (operation === 'subtract') {
        decimalResult = parseInt(binary1, 2) - parseInt(binary2, 2);
      } else if (operation === 'multiply') {
        decimalResult = parseInt(binary1, 2) * parseInt(binary2, 2);
      } else if (operation === 'divide') {
        decimalResult = parseInt(binary1, 2) / parseInt(binary2, 2);
      }

      binaryResult = decimalResult.toString(2);

      document.getElementById("binary_result").innerHTML = "Result in binary:  " + binaryResult;
      document.getElementById("decimal_result").innerHTML = "Result in base 10:  " + decimalResult;
    }
  </script>
</body>
</html>
