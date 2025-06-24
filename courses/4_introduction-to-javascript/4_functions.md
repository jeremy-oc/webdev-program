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

## Mini Project: Tip Calculator

Build a simple but complete tip calculator that demonstrates various function concepts.

### Project Requirements:

1. **Basic Calculation Functions:**
   - Calculate tip amount based on bill and percentage
   - Calculate total amount including tip
   - Split total among multiple people

2. **Validation Functions:**
   - Validate bill amount (positive number)
   - Validate tip percentage (reasonable range)
   - Validate number of people (positive integer)

3. **User Interface:**
   - Input fields for bill amount, tip percentage, and number of people
   - Preset buttons for common tip percentages
   - Real-time calculation display
   - Clear formatting for currency amounts

### Starter Code:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Tip Calculator</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            max-width: 500px;
            margin: 50px auto;
            padding: 20px;
            background: #f5f5f5;
        }
        
        .calculator {
            background: white;
            padding: 30px;
            border-radius: 10px;
            box-shadow: 0 5px 15px rgba(0,0,0,0.1);
        }
        
        .input-group {
            margin: 20px 0;
        }
        
        label {
            display: block;
            margin-bottom: 5px;
            font-weight: bold;
        }
        
        input {
            width: 100%;
            padding: 10px;
            border: 2px solid #ddd;
            border-radius: 5px;
            font-size: 16px;
            box-sizing: border-box;
        }
        
        .tip-buttons {
            display: grid;
            grid-template-columns: repeat(4, 1fr);
            gap: 10px;
            margin: 15px 0;
        }
        
        .tip-btn {
            padding: 10px;
            border: 2px solid #ddd;
            background: white;
            border-radius: 5px;
            cursor: pointer;
            text-align: center;
            transition: all 0.3s;
        }
        
        .tip-btn:hover {
            background: #f0f0f0;
        }
        
        .tip-btn.active {
            background: #007bff;
            color: white;
            border-color: #007bff;
        }
        
        .results {
            background: #f8f9fa;
            padding: 20px;
            border-radius: 5px;
            margin-top: 20px;
        }
        
        .result-row {
            display: flex;
            justify-content: space-between;
            margin: 10px 0;
            font-size: 18px;
        }
        
        .total {
            font-weight: bold;
            color: #007bff;
            border-top: 2px solid #ddd;
            padding-top: 10px;
        }
    </style>
</head>
<body>
    <div class="calculator">
        <h1>💰 Tip Calculator</h1>
        
        <div class="input-group">
            <label for="billAmount">Bill Amount ($)</label>
            <input type="number" id="billAmount" placeholder="Enter bill amount" step="0.01">
        </div>
        
        <div class="input-group">
            <label>Select Tip Percentage</label>
            <div class="tip-buttons">
                <div class="tip-btn" data-tip="15">15%</div>
                <div class="tip-btn" data-tip="18">18%</div>
                <div class="tip-btn active" data-tip="20">20%</div>
                <div class="tip-btn" data-tip="25">25%</div>
            </div>
            <input type="number" id="customTip" placeholder="Custom tip %" min="0" max="100">
        </div>
        
        <div class="input-group">
            <label for="peopleCount">Number of People</label>
            <input type="number" id="peopleCount" value="1" min="1">
        </div>
        
        <div class="results">
            <div class="result-row">
                <span>Bill Amount:</span>
                <span id="displayBill">$0.00</span>
            </div>
            <div class="result-row">
                <span>Tip (<span id="tipPercent">20</span>%):</span>
                <span id="tipAmount">$0.00</span>
            </div>
            <div class="result-row">
                <span>Total:</span>
                <span id="totalAmount">$0.00</span>
            </div>
            <div class="result-row total">
                <span>Per Person:</span>
                <span id="perPersonAmount">$0.00</span>
            </div>
        </div>
    </div>

    <script>
        // Global variable to track current tip percentage
        let currentTipPercent = 20;
        
        // Core calculation functions
        function calculateTipAmount(billAmount, tipPercent) {
            // TODO: Calculate tip amount
            // Hint: tip = bill * (percentage / 100)
        }
        
        function calculateTotal(billAmount, tipAmount) {
            // TODO: Calculate total amount
            // Hint: total = bill + tip
        }
        
        function calculatePerPerson(totalAmount, peopleCount) {
            // TODO: Calculate amount per person
            // Hint: per person = total / number of people
        }
        
        // Validation functions
        function isValidBillAmount(amount) {
            // TODO: Check if bill amount is valid
            // Hint: should be a positive number
        }
        
        function isValidTipPercent(percent) {
            // TODO: Check if tip percentage is valid
            // Hint: should be between 0 and 100
        }
        
        function isValidPeopleCount(count) {
            // TODO: Check if people count is valid
            // Hint: should be a positive integer
        }
        
        // Utility functions
        function formatCurrency(amount) {
            // TODO: Format number as currency
            // Hint: use toFixed(2) and add $ sign
        }
        
        function updateDisplay() {
            // TODO: Update all display elements with calculated values
            // Get input values, validate them, calculate results, and update display
        }
        
        // Event handling functions
        function handleTipButtonClick(event) {
            // TODO: Handle tip percentage button clicks
            // Update active button, set current tip percent, and recalculate
        }
        
        function handleCustomTipInput() {
            // TODO: Handle custom tip percentage input
            // Validate input, update current tip percent, and recalculate
        }
        
        // Initialize event listeners
        document.addEventListener('DOMContentLoaded', function() {
            // TODO: Add event listeners for all inputs and buttons
            // Listen for: bill amount changes, people count changes, tip button clicks, custom tip input
        });
        
        // Initial display update
        updateDisplay();
    </script>
</body>
</html>
```

### Implementation Steps:

1. **Start with calculation functions:**
   - Implement `calculateTipAmount()`, `calculateTotal()`, and `calculatePerPerson()`
   - Test these functions with sample data in the console

2. **Add validation functions:**
   - Implement validation for bill amount, tip percentage, and people count
   - Consider edge cases (negative numbers, zero, etc.)

3. **Create utility functions:**
   - Implement `formatCurrency()` to display money properly
   - Make sure to handle rounding appropriately

4. **Build the update system:**
   - Implement `updateDisplay()` to get inputs, validate, calculate, and show results
   - This is the main function that ties everything together

5. **Add interactivity:**
   - Implement event handlers for tip buttons and custom input
   - Make sure the interface responds to all user interactions

6. **Test and refine:**
   - Test with various inputs including edge cases
   - Add error handling and user feedback

### Key Learning Points:

- **Function organization**: Each calculation is a separate, testable function
- **Validation**: Functions to check input validity before processing
- **Event handling**: Functions to respond to user interactions
- **DOM manipulation**: Functions to update the display
- **Error handling**: Graceful handling of invalid inputs

### Extension Ideas:

Once you complete the basic calculator, try adding:
- **Rounding options**: Round up, down, or to nearest dollar
- **Service quality feedback**: Suggest tip based on service rating
- **Save calculations**: Store and recall previous calculations
- **Different currencies**: Support for multiple currency formats

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

Once you've mastered functions and completed the tip calculator project, you're ready to move on to [Part 5: Loops - Repeating Tasks](5_loops.md) where you'll learn to automate repetitive tasks and work with collections of data.