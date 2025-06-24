# Part 5: Loops - Repeating Tasks

## Loop Fundamentals

### What Are Loops?

Loops are control structures that allow you to execute code repeatedly based on a condition. They're essential for automating repetitive tasks, processing data collections, and creating dynamic behaviors in your applications.

#### Why Use Loops?
- **Efficiency**: Avoid writing repetitive code
- **Scalability**: Handle varying amounts of data
- **Automation**: Process collections and datasets
- **User Experience**: Create animations and dynamic content
- **Data Processing**: Iterate through arrays and objects

### For Loops

The most common loop type, ideal when you know how many times to repeat:

```javascript
// Basic for loop structure
for (initialization; condition; increment) {
    // Code to execute
}

// Example: Count from 1 to 5
for (let i = 1; i <= 5; i++) {
    console.log(`Count: ${i}`);
}

// Example: Generate multiplication table
function generateMultiplicationTable(number, max = 10) {
    const results = [];
    for (let i = 1; i <= max; i++) {
        const result = number * i;
        results.push(`${number} x ${i} = ${result}`);
    }
    return results;
}

console.log(generateMultiplicationTable(7));
```

#### Advanced For Loop Patterns
```javascript
// Counting backwards
for (let i = 10; i >= 1; i--) {
    console.log(`Countdown: ${i}`);
}

// Incrementing by different amounts
for (let i = 0; i <= 100; i += 5) {
    console.log(`Every 5th number: ${i}`);
}

// Using variables in loop conditions
const userInput = 15;
for (let i = 1; i <= userInput; i++) {
    if (i % 3 === 0) {
        console.log(`${i} is divisible by 3`);
    }
}
```

### While Loops

Best when the number of iterations is unknown:

```javascript
// Basic while loop
let count = 0;
while (count < 5) {
    console.log(`While count: ${count}`);
    count++; // Don't forget to increment!
}

// User input validation
function getValidAge() {
    let age = prompt("Enter your age:");
    while (isNaN(age) || age < 0 || age > 150) {
        alert("Please enter a valid age between 0 and 150");
        age = prompt("Enter your age:");
    }
    return parseInt(age);
}

// Processing data until a condition is met
function findFirstEven(numbers) {
    let index = 0;
    while (index < numbers.length) {
        if (numbers[index] % 2 === 0) {
            return numbers[index];
        }
        index++;
    }
    return null; // No even number found
}
```

### Do-While Loops

Executes at least once before checking the condition:

```javascript
// Menu system that runs at least once
function showMenu() {
    let choice;
    do {
        choice = prompt(`
        Choose an option:
        1. View Profile
        2. Edit Settings
        3. Log Out
        Enter your choice (1-3):
        `);
        
        switch (choice) {
            case '1':
                alert("Viewing profile...");
                break;
            case '2':
                alert("Opening settings...");
                break;
            case '3':
                alert("Logging out...");
                break;
            default:
                alert("Invalid choice. Please try again.");
        }
    } while (choice !== '3');
}

// Game loop example
function playNumberGuessingGame() {
    const secretNumber = Math.floor(Math.random() * 100) + 1;
    let attempts = 0;
    let guessed = false;
    
    do {
        const guess = parseInt(prompt("Guess a number between 1 and 100:"));
        attempts++;
        
        if (guess === secretNumber) {
            alert(`Congratulations! You guessed it in ${attempts} attempts!`);
            guessed = true;
        } else if (guess < secretNumber) {
            alert("Too low! Try again.");
        } else {
            alert("Too high! Try again.");
        }
    } while (!guessed && attempts < 10);
    
    if (!guessed) {
        alert(`Game over! The number was ${secretNumber}`);
    }
}
```

### Loop Control: Break and Continue

#### Break Statement
```javascript
// Exit loop early when condition is met
function findPrimeNumbers(max) {
    const primes = [];
    
    for (let num = 2; num <= max; num++) {
        let isPrime = true;
        
        // Check if number is prime
        for (let divisor = 2; divisor < num; divisor++) {
            if (num % divisor === 0) {
                isPrime = false;
                break; // Exit inner loop early
            }
        }
        
        if (isPrime) {
            primes.push(num);
        }
    }
    
    return primes;
}
```

#### Continue Statement
```javascript
// Skip certain iterations
function processNumbers(numbers) {
    const results = [];
    
    for (let i = 0; i < numbers.length; i++) {
        // Skip negative numbers
        if (numbers[i] < 0) {
            continue;
        }
        
        // Process positive numbers
        const processed = numbers[i] * 2;
        results.push(processed);
    }
    
    return results;
}

// Print only odd numbers
for (let i = 1; i <= 20; i++) {
    if (i % 2 === 0) {
        continue; // Skip even numbers
    }
    console.log(`Odd number: ${i}`);
}
```

### Nested Loops

Loops inside other loops for complex iterations:

```javascript
// Creating a multiplication table
function createMultiplicationTable(size) {
    let table = [];
    
    for (let row = 1; row <= size; row++) {
        let currentRow = [];
        for (let col = 1; col <= size; col++) {
            currentRow.push(row * col);
        }
        table.push(currentRow);
    }
    
    return table;
}

// Pattern generation
function createStarPattern(height) {
    let pattern = '';
    
    for (let row = 1; row <= height; row++) {
        // Add spaces for centering
        for (let space = 1; space <= height - row; space++) {
            pattern += ' ';
        }
        
        // Add stars
        for (let star = 1; star <= row * 2 - 1; star++) {
            pattern += '*';
        }
        
        pattern += '\n';
    }
    
    return pattern;
}

console.log(createStarPattern(5));
/*
    *
   ***
  *****
 *******
*********
*/
```

---

## Mini Project: Interactive Number Pattern Generator

Build a web application that generates various number patterns using different types of loops. This project will help you practice all loop types and understand when to use each one.

### Project Requirements:

1. **Pattern Generation:**
   - Multiplication tables (for loops)
   - Prime number sequences (nested loops with break)
   - Fibonacci sequence (while loops)
   - Number pyramids (nested loops)

2. **Interactive Features:**
   - User input for pattern size/range
   - Real-time pattern updates
   - Multiple pattern display modes
   - Pattern explanations

3. **Loop Practice:**
   - Use different loop types appropriately
   - Implement break and continue statements
   - Handle edge cases and validation
   - Optimize for performance

### Minimal Starter Code:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Number Pattern Generator</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            max-width: 800px;
            margin: 0 auto;
            padding: 20px;
            background: #f5f5f5;
        }
        
        .container {
            background: white;
            padding: 30px;
            border-radius: 10px;
            box-shadow: 0 2px 10px rgba(0,0,0,0.1);
        }
        
        .controls {
            margin-bottom: 20px;
            padding: 15px;
            background: #f8f9fa;
            border-radius: 8px;
        }
        
        .controls label {
            display: inline-block;
            width: 120px;
            font-weight: bold;
        }
        
        .controls input, .controls select {
            padding: 8px;
            margin: 5px;
            border: 1px solid #ddd;
            border-radius: 4px;
        }
        
        .controls button {
            background: #007bff;
            color: white;
            border: none;
            padding: 10px 20px;
            border-radius: 4px;
            cursor: pointer;
            margin: 5px;
        }
        
        .controls button:hover {
            background: #0056b3;
        }
        
        .output {
            background: #f8f9fa;
            border: 1px solid #dee2e6;
            border-radius: 8px;
            padding: 20px;
            margin: 20px 0;
            font-family: monospace;
            white-space: pre-wrap;
            min-height: 200px;
        }
        
        .tabs {
            display: flex;
            margin-bottom: 20px;
        }
        
        .tab {
            background: #e9ecef;
            border: none;
            padding: 10px 20px;
            cursor: pointer;
            border-radius: 4px 4px 0 0;
            margin-right: 2px;
        }
        
        .tab.active {
            background: #007bff;
            color: white;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>🔢 Number Pattern Generator</h1>
        <p>Practice loops by generating different number patterns!</p>
        
        <div class="tabs">
            <button class="tab active" onclick="switchTab('multiplication')">Multiplication</button>
            <button class="tab" onclick="switchTab('fibonacci')">Fibonacci</button>
            <button class="tab" onclick="switchTab('primes')">Prime Numbers</button>
            <button class="tab" onclick="switchTab('patterns')">Visual Patterns</button>
        </div>
        
        <!-- Multiplication Table Tab -->
        <div id="multiplication" class="tab-content">
            <div class="controls">
                <label>Table for:</label>
                <input type="number" id="multNumber" value="7" min="1" max="20">
                <label>Up to:</label>
                <input type="number" id="multRange" value="12" min="1" max="20">
                <button onclick="generateMultiplication()">Generate</button>
            </div>
        </div>
        
        <!-- Fibonacci Tab -->
        <div id="fibonacci" class="tab-content hidden">
            <div class="controls">
                <label>Count:</label>
                <input type="number" id="fibCount" value="10" min="1" max="30">
                <button onclick="generateFibonacci()">Generate</button>
            </div>
        </div>
        
        <!-- Prime Numbers Tab -->
        <div id="primes" class="tab-content hidden">
            <div class="controls">
                <label>Up to:</label>
                <input type="number" id="primeMax" value="50" min="2" max="200">
                <button onclick="generatePrimes()">Generate</button>
            </div>
        </div>
        
        <!-- Visual Patterns Tab -->
        <div id="patterns" class="tab-content hidden">
            <div class="controls">
                <label>Pattern:</label>
                <select id="patternType">
                    <option value="triangle">Number Triangle</option>
                    <option value="pyramid">Star Pyramid</option>
                    <option value="diamond">Diamond</option>
                </select>
                <label>Size:</label>
                <input type="number" id="patternSize" value="5" min="3" max="10">
                <button onclick="generatePattern()">Generate</button>
            </div>
        </div>
        
        <div class="output" id="output">Click a Generate button to see patterns!</div>
    </div>

    <script>
        // Tab switching functionality
        function switchTab(tabName) {
            // Hide all tab contents
            document.querySelectorAll('.tab-content').forEach(tab => {
                tab.classList.add('hidden');
            });
            
            // Remove active class from all tabs
            document.querySelectorAll('.tab').forEach(tab => {
                tab.classList.remove('active');
            });
            
            // Show selected tab and mark as active
            document.getElementById(tabName).classList.remove('hidden');
            event.target.classList.add('active');
            
            // Clear output
            document.getElementById('output').textContent = 'Click Generate to see the pattern!';
        }
        
        // TODO: Implement these functions using different loop types
        
        function generateMultiplication() {
            // TODO: Use a for loop to generate multiplication table
            // Get values from multNumber and multRange inputs
            // Display results in output div
        }
        
        function generateFibonacci() {
            // TODO: Use a while loop to generate Fibonacci sequence
            // Get count from fibCount input
            // Display results in output div
        }
        
        function generatePrimes() {
            // TODO: Use nested loops with break to find prime numbers
            // Get max value from primeMax input
            // Display results in output div
        }
        
        function generatePattern() {
            // TODO: Use nested loops to create visual patterns
            // Get pattern type and size from inputs
            // Use continue statements where appropriate
            // Display results in output div
        }
        
        // Add CSS for hidden class
        const style = document.createElement('style');
        style.textContent = '.hidden { display: none; }';
        document.head.appendChild(style);
    </script>
</body>
</html>
```

### Your Tasks:

1. **Complete the `generateMultiplication()` function:**
   - Use a **for loop** to create a multiplication table
   - Format the output nicely (e.g., "7 x 1 = 7")

2. **Complete the `generateFibonacci()` function:**
   - Use a **while loop** to generate the Fibonacci sequence
   - Start with 0, 1 and calculate subsequent numbers

3. **Complete the `generatePrimes()` function:**
   - Use **nested loops** to find prime numbers
   - Use **break** statements to optimize prime checking
   - Display each prime number found

4. **Complete the `generatePattern()` function:**
   - Implement different visual patterns using **nested loops**
   - Use **continue** statements where appropriate
   - Handle the three pattern types: triangle, pyramid, diamond

### Learning Objectives:
- Practice all three loop types (for, while, do-while)
- Understand when to use break and continue
- Work with nested loops effectively
- Handle user input and validation
- Create interactive web applications

### Hints:
- Use `document.getElementById('output').textContent = result;` to display output
- Format multi-line output with `\n` for line breaks
- Test with small values first, then increase complexity
- Remember to validate user input (positive numbers, reasonable ranges)

---

## Advanced Loop Concepts

### Loop Performance and Optimization

```javascript
// Efficient loop practices
function optimizedArrayProcessing(largeArray) {
    const length = largeArray.length; // Cache length
    const results = [];
    
    for (let i = 0; i < length; i++) {
        results[i] = largeArray[i] * 2;
    }
    
    return results;
}
```

### Common Loop Mistakes and Solutions

#### 1. Off-by-One Errors
```javascript
// Wrong - misses last element
for (let i = 0; i < array.length - 1; i++) {
    console.log(array[i]);
}

// Correct
for (let i = 0; i < array.length; i++) {
    console.log(array[i]);
}
```

#### 2. Infinite Loop Prevention
```javascript
function safeWhileLoop(data) {
    let index = 0;
    const maxIterations = 1000; // Safety limit
    let iterations = 0;
    
    while (index < data.length && iterations < maxIterations) {
        // Process data[index]
        index++;
        iterations++;
    }
}
```

---

## Assessment Checklist

Before moving to Part 6, ensure you can:
- [ ] Write and understand for, while, and do-while loops
- [ ] Use break and continue statements appropriately
- [ ] Create nested loops for complex iterations
- [ ] Avoid common loop pitfalls and infinite loops
- [ ] Complete the number pattern generator project
- [ ] Handle user input validation in loops
- [ ] Debug loop-related issues effectively

---

## Next Steps

Once you've completed the number pattern generator project and mastered all loop types, you're ready to move on to [Part 6: Arrays and Array Methods](6_arrays.md) where you'll learn to work with collections of data and powerful array manipulation techniques.