# Part 4: Functions - Organizing Your Code

## Function Fundamentals

### What Are Functions?

Functions are reusable blocks of code that perform specific tasks. They help organize your code, eliminate repetition, and make programs easier to understand and maintain.

#### Why Use Functions?
- **Reusability**: Write once, use multiple times
- **Organization**: Break complex problems into smaller parts
- **Maintainability**: Update code in one place
- **Testing**: Test individual pieces of functionality
- **Collaboration**: Different developers can work on different functions

### Function Declarations vs Expressions

#### Function Declarations
```javascript
// Function declaration - can be called before it's defined
function greetUser(name) {
    return `Hello, ${name}! Welcome to our website.`;
}

// Can be called anywhere in the file
const message = greetUser("Alice");
console.log(message); // "Hello, Alice! Welcome to our website."
```

#### Function Expressions
```javascript
// Function expression - must be defined before use
const calculateTax = function(amount, rate) {
    return amount * (rate / 100);
};

// Must be called after definition
const tax = calculateTax(100, 8.5);
console.log(tax); // 8.5
```

#### Arrow Functions (Modern Syntax)
```javascript
// Arrow function - concise syntax
const multiply = (a, b) => {
    return a * b;
};

// Even more concise for simple expressions
const square = x => x * x;
const add = (a, b) => a + b;

// No parameters
const getCurrentTime = () => new Date().toLocaleTimeString();
```

### Parameters and Arguments

#### Basic Parameters
```javascript
function createProfile(firstName, lastName, age) {
    return {
        name: `${firstName} ${lastName}`,
        age: age,
        id: Math.random().toString(36).substr(2, 9)
    };
}

// Arguments are passed in order
const profile = createProfile("John", "Doe", 30);
```

#### Default Parameters
```javascript
function calculateDiscount(price, discountRate = 10) {
    return price - (price * discountRate / 100);
}

console.log(calculateDiscount(100));     // Uses default 10%
console.log(calculateDiscount(100, 20)); // Uses provided 20%
```

#### Rest Parameters
```javascript
function calculateAverage(...scores) {
    if (scores.length === 0) return 0;
    const sum = scores.reduce((total, score) => total + score, 0);
    return sum / scores.length;
}

console.log(calculateAverage(85, 92, 78, 96)); // 87.75
console.log(calculateAverage(100, 95));        // 97.5
```

### Return Values and Scope

#### Return Values
```javascript
// Function with return value
function calculateCompoundInterest(principal, rate, time) {
    const amount = principal * Math.pow(1 + rate/100, time);
    return Math.round(amount * 100) / 100; // Round to 2 decimal places
}

// Function that doesn't return a value (returns undefined)
function logWelcomeMessage(name) {
    console.log(`Welcome, ${name}!`);
    // No return statement = returns undefined
}

// Early return for validation
function validateAge(age) {
    if (age < 0) {
        return "Age cannot be negative";
    }
    if (age > 150) {
        return "Age seems unrealistic";
    }
    return "Age is valid";
}
```

#### Function Scope
```javascript
let globalVariable = "I'm global";

function demonstrateScope() {
    let localVariable = "I'm local";
    
    function innerFunction() {
        let innerVariable = "I'm inner";
        console.log(globalVariable);  // Can access global
        console.log(localVariable);   // Can access parent scope
        console.log(innerVariable);   // Can access own scope
    }
    
    innerFunction();
    // console.log(innerVariable); // Error: not accessible
}
```

---

## Mini Project: Multi-Function Calculator

Build a comprehensive calculator that performs various operations, with each operation implemented as a separate function.

### Project Requirements:

1. **Basic Operations:**
   - Addition, subtraction, multiplication, division
   - Each operation as a separate function
   - Error handling for division by zero

2. **Advanced Operations:**
   - Percentage calculations
   - Power/exponent calculations
   - Square root and nth root
   - Factorial calculation

3. **User Interface:**
   - Clean, responsive calculator layout
   - Button interactions for all operations
   - Display showing current operation and result
   - Clear and reset functionality

4. **Enhanced Features:**
   - Memory functions (store, recall, clear)
   - History of calculations
   - Keyboard support
   - Scientific notation for large numbers

### Starter Code Structure:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Multi-Function Calculator</title>
    <style>
        body {
            font-family: 'Arial', sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            margin: 0;
            padding: 20px;
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
        }
        
        .calculator {
            background: rgba(255, 255, 255, 0.95);
            border-radius: 20px;
            padding: 20px;
            box-shadow: 0 15px 35px rgba(0,0,0,0.2);
            max-width: 400px;
            width: 100%;
        }
        
        .display {
            background: #1a1a1a;
            color: #fff;
            padding: 20px;
            border-radius: 10px;
            margin-bottom: 20px;
            text-align: right;
            min-height: 60px;
            display: flex;
            flex-direction: column;
            justify-content: center;
        }
        
        .display-operation {
            font-size: 14px;
            color: #888;
            margin-bottom: 5px;
        }
        
        .display-result {
            font-size: 24px;
            font-weight: bold;
        }
        
        .buttons {
            display: grid;
            grid-template-columns: repeat(4, 1fr);
            gap: 10px;
        }
        
        button {
            padding: 20px;
            border: none;
            border-radius: 10px;
            font-size: 18px;
            font-weight: bold;
            cursor: pointer;
            transition: all 0.2s;
        }
        
        button:hover {
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(0,0,0,0.2);
        }
        
        .btn-number {
            background: #f0f0f0;
            color: #333;
        }
        
        .btn-operator {
            background: #ff9500;
            color: white;
        }
        
        .btn-function {
            background: #a6a6a6;
            color: white;
        }
        
        .btn-equals {
            background: #ff9500;
            color: white;
            grid-column: span 2;
        }
        
        .btn-zero {
            grid-column: span 2;
        }
        
        .memory-functions {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 10px;
            margin-bottom: 15px;
        }
        
        .btn-memory {
            background: #34495e;
            color: white;
            padding: 10px;
            font-size: 14px;
        }
        
        .history {
            max-height: 150px;
            overflow-y: auto;
            background: #f8f9fa;
            border-radius: 8px;
            padding: 10px;
            margin-top: 15px;
            font-size: 12px;
        }
        
        .history-item {
            padding: 5px 0;
            border-bottom: 1px solid #dee2e6;
        }
    </style>
</head>
<body>
    <div class="calculator">
        <div class="display">
            <div id="displayOperation" class="display-operation"></div>
            <div id="displayResult" class="display-result">0</div>
        </div>
        
        <div class="memory-functions">
            <button class="btn-memory" onclick="memoryStore()">MS</button>
            <button class="btn-memory" onclick="memoryRecall()">MR</button>
            <button class="btn-memory" onclick="memoryClear()">MC</button>
        </div>
        
        <div class="buttons">
            <button class="btn-function" onclick="clearAll()">AC</button>
            <button class="btn-function" onclick="clearEntry()">CE</button>
            <button class="btn-function" onclick="percentage()">%</button>
            <button class="btn-operator" onclick="setOperation('/')">÷</button>
            
            <button class="btn-number" onclick="inputNumber('7')">7</button>
            <button class="btn-number" onclick="inputNumber('8')">8</button>
            <button class="btn-number" onclick="inputNumber('9')">9</button>
            <button class="btn-operator" onclick="setOperation('*')">×</button>
            
            <button class="btn-number" onclick="inputNumber('4')">4</button>
            <button class="btn-number" onclick="inputNumber('5')">5</button>
            <button class="btn-number" onclick="inputNumber('6')">6</button>
            <button class="btn-operator" onclick="setOperation('-')">−</button>
            
            <button class="btn-number" onclick="inputNumber('1')">1</button>
            <button class="btn-number" onclick="inputNumber('2')">2</button>
            <button class="btn-number" onclick="inputNumber('3')">3</button>
            <button class="btn-operator" onclick="setOperation('+')">+</button>
            
            <button class="btn-number btn-zero" onclick="inputNumber('0')">0</button>
            <button class="btn-number" onclick="inputDecimal()">.</button>
            <button class="btn-equals" onclick="calculate()">=</button>
        </div>
        
        <div class="buttons" style="margin-top: 15px;">
            <button class="btn-function" onclick="squareRoot()">√</button>
            <button class="btn-function" onclick="power()">x²</button>
            <button class="btn-function" onclick="factorial()">n!</button>
            <button class="btn-function" onclick="inverse()">1/x</button>
        </div>
        
        <div id="history" class="history" style="display: none;">
            <strong>History:</strong>
            <div id="historyList"></div>
        </div>
        
        <button onclick="toggleHistory()" style="width: 100%; margin-top: 10px; padding: 8px; background: #6c757d; color: white; border: none; border-radius: 5px;">
            Toggle History
        </button>
    </div>

    <script>
        // Global variables
        let currentNumber = '0';
        let previousNumber = null;
        let operation = null;
        let waitingForNewNumber = false;
        let memory = 0;
        let history = [];
        
        // Basic arithmetic functions
        function add(a, b) {
            return a + b;
        }
        
        function subtract(a, b) {
            return a - b;
        }
        
        function multiply(a, b) {
            return a * b;
        }
        
        function divide(a, b) {
            if (b === 0) {
                throw new Error("Cannot divide by zero");
            }
            return a / b;
        }
        
        // Advanced mathematical functions
        function calculatePercentage(number, percent) {
            return (number * percent) / 100;
        }
        
        function calculatePower(base, exponent) {
            return Math.pow(base, exponent);
        }
        
        function calculateSquareRoot(number) {
            if (number < 0) {
                throw new Error("Cannot calculate square root of negative number");
            }
            return Math.sqrt(number);
        }
        
        function calculateFactorial(n) {
            if (n < 0 || !Number.isInteger(n)) {
                throw new Error("Factorial is only defined for non-negative integers");
            }
            if (n === 0 || n === 1) return 1;
            let result = 1;
            for (let i = 2; i <= n; i++) {
                result *= i;
            }
            return result;
        }
        
        function calculateInverse(number) {
            if (number === 0) {
                throw new Error("Cannot calculate inverse of zero");
            }
            return 1 / number;
        }
        
        // Calculator interface functions
        function updateDisplay() {
            document.getElementById('displayResult').textContent = currentNumber;
            if (operation && previousNumber !== null) {
                document.getElementById('displayOperation').textContent = 
                    `${previousNumber} ${getOperationSymbol(operation)}`;
            } else {
                document.getElementById('displayOperation').textContent = '';
            }
        }
        
        function getOperationSymbol(op) {
            const symbols = { '+': '+', '-': '−', '*': '×', '/': '÷' };
            return symbols[op] || op;
        }
        
        function inputNumber(num) {
            if (waitingForNewNumber) {
                currentNumber = num;
                waitingForNewNumber = false;
            } else {
                currentNumber = currentNumber === '0' ? num : currentNumber + num;
            }
            updateDisplay();
        }
        
        function inputDecimal() {
            if (waitingForNewNumber) {
                currentNumber = '0.';
                waitingForNewNumber = false;
            } else if (!currentNumber.includes('.')) {
                currentNumber += '.';
            }
            updateDisplay();
        }
        
        function setOperation(op) {
            if (operation && !waitingForNewNumber) {
                calculate();
            }
            operation = op;
            previousNumber = parseFloat(currentNumber);
            waitingForNewNumber = true;
        }
        
        function calculate() {
            if (operation && previousNumber !== null && !waitingForNewNumber) {
                try {
                    const current = parseFloat(currentNumber);
                    let result;
                    
                    switch (operation) {
                        case '+':
                            result = add(previousNumber, current);
                            break;
                        case '-':
                            result = subtract(previousNumber, current);
                            break;
                        case '*':
                            result = multiply(previousNumber, current);
                            break;
                        case '/':
                            result = divide(previousNumber, current);
                            break;
                        default:
                            return;
                    }
                    
                    // Add to history
                    addToHistory(`${previousNumber} ${getOperationSymbol(operation)} ${current} = ${result}`);
                    
                    currentNumber = formatResult(result);
                    operation = null;
                    previousNumber = null;
                    waitingForNewNumber = true;
                    
                } catch (error) {
                    currentNumber = 'Error';
                    operation = null;
                    previousNumber = null;
                    alert(error.message);
                }
            }
            updateDisplay();
        }
        
        function formatResult(number) {
            // Handle very large or very small numbers
            if (Math.abs(number) > 1e10 || (Math.abs(number) < 1e-6 && number !== 0)) {
                return number.toExponential(6);
            }
            // Round to avoid floating point precision issues
            return (Math.round(number * 1e10) / 1e10).toString();
        }
        
        // Advanced operation functions
        function percentage() {
            const current = parseFloat(currentNumber);
            if (previousNumber !== null && operation) {
                currentNumber = formatResult(calculatePercentage(previousNumber, current));
            } else {
                currentNumber = formatResult(current / 100);
            }
            addToHistory(`${parseFloat(currentNumber)} %`);
            waitingForNewNumber = true;
            updateDisplay();
        }
        
        function squareRoot() {
            try {
                const current = parseFloat(currentNumber);
                const result = calculateSquareRoot(current);
                addToHistory(`√${current} = ${result}`);
                currentNumber = formatResult(result);
                waitingForNewNumber = true;
                updateDisplay();
            } catch (error) {
                alert(error.message);
            }
        }
        
        function power() {
            const current = parseFloat(currentNumber);
            const result = calculatePower(current, 2);
            addToHistory(`${current}² = ${result}`);
            currentNumber = formatResult(result);
            waitingForNewNumber = true;
            updateDisplay();
        }
        
        function factorial() {
            try {
                const current = parseFloat(currentNumber);
                const result = calculateFactorial(current);
                addToHistory(`${current}! = ${result}`);
                currentNumber = formatResult(result);
                waitingForNewNumber = true;
                updateDisplay();
            } catch (error) {
                alert(error.message);
            }
        }
        
        function inverse() {
            try {
                const current = parseFloat(currentNumber);
                const result = calculateInverse(current);
                addToHistory(`1/${current} = ${result}`);
                currentNumber = formatResult(result);
                waitingForNewNumber = true;
                updateDisplay();
            } catch (error) {
                alert(error.message);
            }
        }
        
        // Memory functions
        function memoryStore() {
            memory = parseFloat(currentNumber);
            addToHistory(`Memory stored: ${memory}`);
        }
        
        function memoryRecall() {
            currentNumber = formatResult(memory);
            waitingForNewNumber = true;
            updateDisplay();
        }
        
        function memoryClear() {
            memory = 0;
            addToHistory("Memory cleared");
        }
        
        // Clear functions
        function clearAll() {
            currentNumber = '0';
            previousNumber = null;
            operation = null;
            waitingForNewNumber = false;
            updateDisplay();
        }
        
        function clearEntry() {
            currentNumber = '0';
            updateDisplay();
        }
        
        // History functions
        function addToHistory(calculation) {
            history.unshift(calculation);
            if (history.length > 20) {
                history = history.slice(0, 20);
            }
            updateHistoryDisplay();
        }
        
        function updateHistoryDisplay() {
            const historyList = document.getElementById('historyList');
            historyList.innerHTML = history.map(item => 
                `<div class="history-item">${item}</div>`
            ).join('');
        }
        
        function toggleHistory() {
            const historyDiv = document.getElementById('history');
            historyDiv.style.display = historyDiv.style.display === 'none' ? 'block' : 'none';
        }
        
        // Keyboard support
        document.addEventListener('keydown', function(event) {
            const key = event.key;
            
            if (key >= '0' && key <= '9') {
                inputNumber(key);
            } else if (key === '.') {
                inputDecimal();
            } else if (key === '+' || key === '-' || key === '*' || key === '/') {
                setOperation(key);
            } else if (key === 'Enter' || key === '=') {
                calculate();
            } else if (key === 'Escape' || key === 'c' || key === 'C') {
                clearAll();
            } else if (key === 'Backspace') {
                clearEntry();
            }
        });
        
        // Initialize display
        updateDisplay();
    </script>
</body>
</html>
```

### Helpful Concepts to Explore:

**JavaScript Concepts:**
- Function declarations, expressions, and arrow functions
- Parameters, default values, and rest parameters
- Return values and error handling with try/catch
- Scope and variable accessibility
- Event handling and keyboard input
- Array methods for history management

**HTML Concepts:**
- CSS Grid for calculator button layout
- Event handling with onclick attributes
- Dynamic content updates
- Accessibility considerations for calculator interface

**CSS Concepts:**
- CSS Grid for responsive button layouts
- Hover effects and transitions
- Color theming and visual feedback
- Responsive design for different screen sizes

### Extension Ideas:

Once you complete the basic calculator, try adding:
- **Scientific functions**: Sin, cos, tan, logarithms
- **Unit converter**: Length, weight, temperature conversions
- **Currency calculator**: Real-time exchange rates
- **Graphing capability**: Simple function plotting
- **Custom themes**: Dark mode, color customization
- **Voice input**: Speech recognition for calculations
- **Export functionality**: Save calculations to file

---

## Mini Project: Tip Calculator

Build a sophisticated tip calculator that handles various scenarios and provides detailed breakdowns.

### Project Requirements:

1. **Basic Calculation:**
   - Bill amount input
   - Tip percentage selection
   - Number of people splitting the bill
   - Calculate tip amount and total per person

2. **Preset Options:**
   - Quick buttons for common tip percentages (15%, 18%, 20%, 25%)
   - Service quality descriptors
   - Custom tip percentage input

3. **Advanced Features:**
   - Tax handling (before or after tip calculation)
   - Rounding options (round up, down, or to nearest dollar)
   - Split bill unevenly (different amounts per person)
   - Currency formatting for different locales

4. **User Experience:**
   - Real-time calculation updates
   - Clear breakdown of all amounts
   - Save favorite settings
   - Share calculation results

### Starter Code Structure:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Smart Tip Calculator</title>
    <style>
        body {
            font-family: 'Arial', sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            margin: 0;
            padding: 20px;
            min-height: 100vh;
        }
        
        .container {
            max-width: 600px;
            margin: 0 auto;
            background: white;
            border-radius: 20px;
            padding: 30px;
            box-shadow: 0 15px 35px rgba(0,0,0,0.2);
        }
        
        .input-group {
            margin: 20px 0;
        }
        
        label {
            display: block;
            margin-bottom: 8px;
            font-weight: bold;
            color: #333;
        }
        
        input {
            width: 100%;
            padding: 12px 15px;
            border: 2px solid #e0e0e0;
            border-radius: 8px;
            font-size: 16px;
            transition: border-color 0.3s;
        }
        
        input:focus {
            outline: none;
            border-color: #667eea;
        }
        
        .tip-buttons {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(80px, 1fr));
            gap: 10px;
            margin: 15px 0;
        }
        
        .tip-btn {
            padding: 12px;
            border: 2px solid #e0e0e0;
            background: white;
            border-radius: 8px;
            cursor: pointer;
            text-align: center;
            font-weight: bold;
            transition: all 0.3s;
        }
        
        .tip-btn:hover {
            background: #f0f0f0;
        }
        
        .tip-btn.active {
            background: #667eea;
            color: white;
            border-color: #667eea;
        }
        
        .results {
            background: #f8f9fa;
            border-radius: 12px;
            padding: 25px;
            margin: 25px 0;
        }
        
        .result-row {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 8px 0;
            border-bottom: 1px solid #e0e0e0;
        }
        
        .result-row:last-child {
            border-bottom: none;
            font-weight: bold;
            font-size: 18px;
            color: #667eea;
        }
        
        .amount {
            font-weight: bold;
            color: #2c3e50;
        }
        
        .total-amount {
            font-size: 24px;
            color: #27ae60;
        }
        
        .options {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 15px;
            margin: 20px 0;
        }
        
        .option-group {
            background: #f8f9fa;
            padding: 15px;
            border-radius: 8px;
        }
        
        select {
            width: 100%;
            padding: 8px;
            border: 1px solid #ddd;
            border-radius: 4px;
            font-size: 14px;
        }
        
        .share-btn {
            background: #27ae60;
            color: white;
            border: none;
            padding: 12px 24px;
            border-radius: 8px;
            cursor: pointer;
            font-size: 16px;
            width: 100%;
            margin-top: 15px;
        }
        
        .share-btn:hover {
            background: #219a52;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>💰 Smart Tip Calculator</h1>
        <p>Calculate tips and split bills with ease</p>
        
        <div class="input-group">
            <label for="billAmount">Bill Amount ($)</label>
            <input type="number" id="billAmount" placeholder="Enter bill amount" step="0.01" oninput="calculateTip()">
        </div>
        
        <div class="input-group">
            <label>Tip Percentage</label>
            <div class="tip-buttons">
                <div class="tip-btn" data-tip="15" onclick="selectTip(15)">
                    15%<br><small>Fair</small>
                </div>
                <div class="tip-btn" data-tip="18" onclick="selectTip(18)">
                    18%<br><small>Good</small>
                </div>
                <div class="tip-btn active" data-tip="20" onclick="selectTip(20)">
                    20%<br><small>Great</small>
                </div>
                <div class="tip-btn" data-tip="25" onclick="selectTip(25)">
                    25%<br><small>Excellent</small>
                </div>
            </div>
            <input type="number" id="customTip" placeholder="Custom tip %" min="0" max="100" oninput="selectCustomTip()">
        </div>
        
        <div class="input-group">
            <label for="peopleCount">Number of People</label>
            <input type="number" id="peopleCount" value="1" min="1" oninput="calculateTip()">
        </div>
        
        <div class="options">
            <div class="option-group">
                <label for="taxOption">Tax Calculation</label>
                <select id="taxOption" onchange="calculateTip()">
                    <option value="none">No tax</option>
                    <option value="before">Calculate tip before tax</option>
                    <option value="after">Calculate tip after tax</option>
                </select>
                <input type="number" id="taxRate" placeholder="Tax rate %" step="0.01" style="margin-top: 5px;" oninput="calculateTip()">
            </div>
            
            <div class="option-group">
                <label for="roundingOption">Rounding</label>
                <select id="roundingOption" onchange="calculateTip()">
                    <option value="none">No rounding</option>
                    <option value="up">Round up</option>
                    <option value="down">Round down</option>
                    <option value="nearest">Round to nearest dollar</option>
                </select>
            </div>
        </div>
        
        <div id="results" class="results">
            <div class="result-row">
                <span>Subtotal:</span>
                <span id="subtotal" class="amount">$0.00</span>
            </div>
            <div class="result-row">
                <span>Tax:</span>
                <span id="taxAmount" class="amount">$0.00</span>
            </div>
            <div class="result-row">
                <span>Tip (<span id="tipPercent">20</span>%):</span>
                <span id="tipAmount" class="amount">$0.00</span>
            </div>
            <div class="result-row">
                <span>Total:</span>
                <span id="totalAmount" class="total-amount">$0.00</span>
            </div>
            <div class="result-row">
                <span>Per Person:</span>
                <span id="perPersonAmount" class="total-amount">$0.00</span>
            </div>
        </div>
        
        <button class="share-btn" onclick="shareCalculation()">📤 Share Calculation</button>
    </div>

    <script>
        let currentTipPercent = 20;
        
        // Core calculation functions
        function calculateSubtotal(billAmount, taxRate, taxOption) {
            if (taxOption === 'before') {
                return billAmount / (1 + taxRate / 100);
            }
            return billAmount;
        }
        
        function calculateTax(subtotal, taxRate) {
            return subtotal * (taxRate / 100);
        }
        
        function calculateTipAmount(baseAmount, tipPercent) {
            return baseAmount * (tipPercent / 100);
        }
        
        function calculateTotal(subtotal, tax, tip) {
            return subtotal + tax + tip;
        }
        
        function calculatePerPerson(total, peopleCount) {
            return total / peopleCount;
        }
        
        // Rounding functions
        function applyRounding(amount, roundingOption) {
            switch (roundingOption) {
                case 'up':
                    return Math.ceil(amount);
                case 'down':
                    return Math.floor(amount);
                case 'nearest':
                    return Math.round(amount);
                default:
                    return amount;
            }
        }
        
        // Formatting functions
        function formatCurrency(amount) {
            return new Intl.NumberFormat('en-US', {
                style: 'currency',
                currency: 'USD',
                minimumFractionDigits: 2
            }).format(amount);
        }
        
        function formatPercent(percent) {
            return percent.toFixed(1);
        }
        
        // UI interaction functions
        function selectTip(percent) {
            currentTipPercent = percent;
            
            // Update UI
            document.querySelectorAll('.tip-btn').forEach(btn => {
                btn.classList.remove('active');
            });
            document.querySelector(`[data-tip="${percent}"]`).classList.add('active');
            document.getElementById('customTip').value = '';
            
            calculateTip();
        }
        
        function selectCustomTip() {
            const customValue = parseFloat(document.getElementById('customTip').value);
            if (!isNaN(customValue) && customValue >= 0) {
                currentTipPercent = customValue;
                
                // Remove active class from preset buttons
                document.querySelectorAll('.tip-btn').forEach(btn => {
                    btn.classList.remove('active');
                });
                
                calculateTip();
            }
        }
        
        // Main calculation function
        function calculateTip() {
            const billAmount = parseFloat(document.getElementById('billAmount').value) || 0;
            const peopleCount = parseInt(document.getElementById('peopleCount').value) || 1;
            const taxOption = document.getElementById('taxOption').value;
            const taxRate = parseFloat(document.getElementById('taxRate').value) || 0;
            const roundingOption = document.getElementById('roundingOption').value;
            
            if (billAmount <= 0) {
                resetResults();
                return;
            }
            
            // Calculate amounts step by step
            let subtotal = calculateSubtotal(billAmount, taxRate, taxOption);
            let tax = 0;
            
            if (taxOption !== 'none' && taxRate > 0) {
                if (taxOption === 'before') {
                    tax = billAmount - subtotal;
                } else {
                    tax = calculateTax(subtotal, taxRate);
                }
            }
            
            // Determine base amount for tip calculation
            const tipBaseAmount = taxOption === 'after' ? subtotal + tax : subtotal;
            let tip = calculateTipAmount(tipBaseAmount, currentTipPercent);
            
            let total = calculateTotal(subtotal, tax, tip);
            
            // Apply rounding to appropriate amounts
            if (roundingOption !== 'none') {
                tip = applyRounding(tip, roundingOption);
                total = subtotal + tax + tip;
            }
            
            const perPerson = calculatePerPerson(total, peopleCount);
            
            // Update display
            updateResults(subtotal, tax, tip, total, perPerson);
        }
        
        function updateResults(subtotal, tax, tip, total, perPerson) {
            document.getElementById('subtotal').textContent = formatCurrency(subtotal);
            document.getElementById('taxAmount').textContent = formatCurrency(tax);
            document.getElementById('tipAmount').textContent = formatCurrency(tip);
            document.getElementById('totalAmount').textContent = formatCurrency(total);
            document.getElementById('perPersonAmount').textContent = formatCurrency(perPerson);
            document.getElementById('tipPercent').textContent = formatPercent(currentTipPercent);
        }
        
        function resetResults() {
            document.getElementById('subtotal').textContent = '$0.00';
            document.getElementById('taxAmount').textContent = '$0.00';
            document.getElementById('tipAmount').textContent = '$0.00';
            document.getElementById('totalAmount').textContent = '$0.00';
            document.getElementById('perPersonAmount').textContent = '$0.00';
        }
        
        // Sharing functionality
        function shareCalculation() {
            const billAmount = parseFloat(document.getElementById('billAmount').value) || 0;
            const peopleCount = parseInt(document.getElementById('peopleCount').value) || 1;
            const subtotal = document.getElementById('subtotal').textContent;
            const tip = document.getElementById('tipAmount').textContent;
            const total = document.getElementById('totalAmount').textContent;
            const perPerson = document.getElementById('perPersonAmount').textContent;
            
            const shareText = `💰 Tip Calculator Results:
Bill: ${formatCurrency(billAmount)}
Tip (${formatPercent(currentTipPercent)}%): ${tip}
Total: ${total}
Per Person (${peopleCount}): ${perPerson}`;
            
            if (navigator.share) {
                navigator.share({
                    title: 'Tip Calculator Results',
                    text: shareText
                }).catch(console.error);
            } else {
                // Fallback: copy to clipboard
                navigator.clipboard.writeText(shareText).then(() => {
                    alert('Calculation copied to clipboard!');
                }).catch(() => {
                    alert('Share text:\n\n' + shareText);
                });
            }
        }
        
        // Validation functions
        function validateBillAmount(amount) {
            return !isNaN(amount) && amount > 0;
        }
        
        function validateTipPercent(percent) {
            return !isNaN(percent) && percent >= 0 && percent <= 100;
        }
        
        function validatePeopleCount(count) {
            return Number.isInteger(count) && count > 0;
        }
        
        // Initialize calculator
        calculateTip();
    </script>
</body>
</html>
```

### Helpful Concepts to Explore:

**JavaScript Concepts:**
- Function organization and modular design
- Input validation and error handling
- Number formatting and internationalization
- DOM manipulation for dynamic updates
- Event handling for user interactions
- Conditional logic for different calculation modes

**HTML Concepts:**
- Form inputs with validation attributes
- Grid layouts for responsive button arrangements
- Semantic structure for accessibility
- Progressive enhancement for mobile devices

**CSS Concepts:**
- CSS Grid for flexible layouts
- Interactive button states and transitions
- Visual hierarchy with typography and spacing
- Responsive design for various screen sizes

### Extension Ideas:

Once you complete the basic tip calculator, try adding:
- **Service quality survey**: Rate service and suggest tip accordingly
- **Multiple currency support**: Different currencies and exchange rates
- **Bill item breakdown**: Individual items with different tip rates
- **Group expense tracking**: Multiple bills and shared expenses
- **Receipt scanning**: OCR to extract bill amounts from photos
- **Expense analytics**: Track spending patterns over time
- **Integration**: Connect with payment apps or expense trackers

---

## Advanced Function Concepts

### Higher-Order Functions

Functions that take other functions as parameters or return functions:

```javascript
// Function that takes another function as parameter
function operateOnNumbers(a, b, operation) {
    return operation(a, b);
}

const add = (x, y) => x + y;
const multiply = (x, y) => x * y;

console.log(operateOnNumbers(5, 3, add));      // 8
console.log(operateOnNumbers(5, 3, multiply)); // 15

// Function that returns another function
function createMultiplier(factor) {
    return function(number) {
        return number * factor;
    };
}

const double = createMultiplier(2);
const triple = createMultiplier(3);

console.log(double(5));  // 10
console.log(triple(5));  // 15
```

### Callback Functions

Functions passed as arguments to be called later:

```javascript
function processUserData(userData, successCallback, errorCallback) {
    if (userData && userData.name) {
        successCallback(`Welcome, ${userData.name}!`);
    } else {
        errorCallback("Invalid user data");
    }
}

function onSuccess(message) {
    console.log("Success:", message);
}

function onError(error) {
    console.error("Error:", error);
}

processUserData({ name: "Alice" }, onSuccess, onError);
```

### Immediately Invoked Function Expressions (IIFE)

Functions that execute immediately upon definition:

```javascript
// IIFE to avoid polluting global namespace
(function() {
    const privateVariable = "This won't be accessible outside";
    
    function privateFunction() {
        console.log("This function is private");
    }
    
    // Only expose what's needed
    window.myModule = {
        publicMethod: function() {
            return "This is public";
        }
    };
})();
```

---

## Common Function Mistakes and Solutions

### 1. Forgetting Return Values
```javascript
// Wrong - function doesn't return anything
function calculateArea(width, height) {
    width * height; // Missing return
}

// Correct
function calculateArea(width, height) {
    return width * height;
}
```

### 2. Modifying Parameters Directly
```javascript
// Problematic - modifies original object
function updateUser(user, newName) {
    user.name = newName; // Modifies original
    return user;
}

// Better - create new object
function updateUser(user, newName) {
    return { ...user, name: newName };
}
```

### 3. Scope Confusion
```javascript
// Wrong - variable not accessible
function createCounter() {
    let count = 0;
}
console.log(count); // Error: count not defined

// Correct - return value or function
function createCounter() {
    let count = 0;
    return function() {
        return ++count;
    };
}
```

---

## Assessment Checklist

Before moving to Part 5, ensure you can:
- [ ] Write function declarations, expressions, and arrow functions
- [ ] Use parameters and return values effectively
- [ ] Understand function scope and variable accessibility
- [ ] Create functions that accept other functions as parameters
- [ ] Organize code into logical, reusable functions
- [ ] Handle errors and edge cases in functions
- [ ] Create interactive applications using multiple functions
- [ ] Debug function-related issues

---

## Additional Resources

**Essential Learning:**
- **MDN**: [Functions](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Functions)
- **MDN**: [Arrow Functions](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions)
- **JavaScript.info**: [Functions](https://javascript.info/function-basics)

**Practice Platforms:**
- **freeCodeCamp**: [Basic Algorithm Scripting](https://www.freecodecamp.org/learn/javascript-algorithms-and-data-structures/)
- **Codewars**: [JavaScript Kata](https://www.codewars.com/)

**Advanced Topics:**
- **MDN**: [Closures](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Closures)
- **JavaScript.info**: [Advanced Functions](https://javascript.info/advanced-functions)

---

## Next Steps

Once you've mastered functions and completed both calculator projects, you're ready to move on to [Part 5: Loops - Repeating Tasks](5_loops.md) where you'll learn to automate repetitive tasks and work with collections of data.