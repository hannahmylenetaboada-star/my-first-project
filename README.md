# my-first-project
calculator 


html:

<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Advanced MDAS Calculator</title>
  <link rel="stylesheet" href="csscalc.css">
</head>
<body>

<div id="calculator">
  <div id="memory-indicator">M</div>
 
  <input id="display" readonly value="0">

  <div id="keys">
    <button onclick="memorySubtract()">M-</button> 
    <button onclick="memoryAdd()">M+</button>
    <button onclick="memoryClear()">MC</button>
    <button onclick="memoryRecall()">MR</button>
    <button onclick="resetCalculator()">AC</button> 

    <button onclick="appendtodisplay('7')">7</button>
    <button onclick="appendtodisplay('8')">8</button>
    <button onclick="appendtodisplay('9')">9</button>
    <button onclick="appendtodisplay('%')">%</button>
    <button onclick="cleardisplay()">C</button> 

    <button onclick="appendtodisplay('4')">4</button>
    <button onclick="appendtodisplay('5')">5</button>
    <button onclick="appendtodisplay('6')">6</button>
    <button onclick="appendtodisplay('*')">x</button>
    <button onclick="appendtodisplay('/')">÷</button>

    <button onclick="appendtodisplay('1')">1</button>
    <button onclick="appendtodisplay('2')">2</button>
    <button onclick="appendtodisplay('3')">3</button>
    <button onclick="appendtodisplay('+')" class="tall-plus">+</button>
    <button onclick="appendtodisplay('-')">-</button>

    <button onclick="appendtodisplay('0')">0</button>
    <button onclick="appendtodisplay('00')">00</button>
    <button onclick="appendtodisplay('.')">.</button>
    <button onclick="calculate()">=</button>
  </div>
</div>

<script src="CalculatorScript.js"></script>
</body>
</html>




css:





    body {
      margin: 0;
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
      background: #111;
    }

    #calculator {
      font-family: Arial, sans-serif;
      background-color: #292929;
      border-radius: 15px;
      width: 380px; 
      padding: 20px;
      box-shadow: 0 10px 25px rgba(0,0,0,0.5);
    }

 
    #memory-indicator {
      color: #0f0;
      font-size: 0.8rem;
      height: 20px;
      margin-left: 10px;
      visibility: hidden;
    }

    #display {
      width: 100%;
      padding: 20px;
      font-size: 2.5rem;
      color: white;
      text-align: right;
      border: none;
      background-color: #4d4c4c;
      box-sizing: border-box;
      border-radius: 10px;
      margin-bottom: 20px;
    }

    #keys {
      display: grid;
      grid-template-columns: repeat(5, 1fr); 
      gap: 10px;
    }

    button {
      height: 60px;
      border-radius: 10px;
      border: none;
      background-color: #545454;
      color: white;
      font-size: 1.1rem;
      font-weight: bold;
      cursor: pointer;
      transition: 0.2s;
    }

    button:hover { background-color: #6a6a6a; }
    button:active { transform: scale(0.95); }

    .tall-plus {
      grid-row: span 2;
      height: 100%;
    }



java script:


const display = document.getElementById("display");
const indicator = document.getElementById("memory-indicator"); 
let memorySlot = 0; 


function resetCalculator() {
    display.value = "0"; 
}

function cleardisplay() {
    display.value = "";
}

function appendtodisplay(input) {
    let currentVal = display.value;
    const lastChar = currentVal.slice(-1);
    const operators = ['+', '-', '*', '/', '%'];

 
    if (input === '.' && lastChar === '.') {
        display.value = currentVal.slice(0, -1);
        return; 
    }
 
 
    if (input === '.') {
        const parts = currentVal.split(/[\+\-\*\/\%]/);
        const lastOperand = parts[parts.length - 1];
        if (lastOperand.includes('.')) return; 
    }

  
    if (operators.includes(input) && operators.includes(lastChar)) {
        display.value = currentVal.slice(0, -1) + input;
        return;
    }


    if (operators.includes(input) && currentVal !== "0" && !operators.includes(lastChar)) {
        try {

            display.value = eval(currentVal).toString() + input;
        } catch (e) {
            display.value = "Error";
        }
    } else {
        if (display.value === "0" && input !== '.') {
            display.value = input;
        } else {
            display.value += input;
        }
    }

