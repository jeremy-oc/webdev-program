# Part 3: Making Decisions with Conditionals

## Conditional Logic

### Understanding `if`, `else if`, and `else` Statements

Conditional statements allow your programs to make decisions and execute different code based on different situations.

#### Basic `if` Statement
```javascript
const age = 18;

if (age >= 18) {
    console.log("You are an adult!");
}
```

#### `if...else` Statement
```javascript
const weather = "sunny";

if (weather === "sunny") {
    console.log("Perfect day for a picnic!");
} else {
    console.log("Maybe stay inside today.");
}
```

#### `if...else if...else` Statement
```javascript
const score = 85;

if (score >= 90) {
    console.log("Grade: A");
} else if (score >= 80) {
    console.log("Grade: B");
} else if (score >= 70) {
    console.log("Grade: C");
} else if (score >= 60) {
    console.log("Grade: D");
} else {
    console.log("Grade: F");
}
```

### Comparison Operators

#### Equality and Inequality
```javascript
// Strict equality (recommended)
console.log(5 === 5);        // true
console.log(5 === "5");      // false (different types)
console.log(5 !== "5");      // true

// Loose equality (avoid in modern JavaScript)
console.log(5 == "5");       // true (converts types)
```

#### Comparison Operators
```javascript
const a = 10;
const b = 20;

console.log(a > b);    // false
console.log(a < b);    // true
console.log(a >= 10);  // true
console.log(b <= 20);  // true
```

#### Comparing Strings
```javascript
const name1 = "Alice";
const name2 = "Bob";

console.log(name1 === name2);           // false
console.log(name1.toLowerCase() === "alice"); // true
```

### Boolean Logic and Logical Operators

#### Logical AND (`&&`)
```javascript
const age = 25;
const hasLicense = true;

if (age >= 18 && hasLicense) {
    console.log("You can drive!");
}
```

#### Logical OR (`||`)
```javascript
const day = "Saturday";

if (day === "Saturday" || day === "Sunday") {
    console.log("It's the weekend!");
}
```

#### Logical NOT (`!`)
```javascript
const isLoggedIn = false;

if (!isLoggedIn) {
    console.log("Please log in first.");
}
```

#### Complex Logical Expressions
```javascript
const age = 22;
const isStudent = true;
const hasJob = false;

if ((age >= 18 && age <= 25) && (isStudent || hasJob)) {
    console.log("Eligible for young adult discount!");
}
```

### Truthy and Falsy Values

Understanding what JavaScript considers "true" or "false" in conditions:

#### Falsy Values
```javascript
// These are all falsy:
if (false) { } // false
if (0) { }     // zero
if ("") { }    // empty string
if (null) { }  // null
if (undefined) { } // undefined
if (NaN) { }   // Not a Number
```

#### Truthy Values
```javascript
// These are all truthy:
if (true) { }      // true
if (1) { }         // any non-zero number
if ("hello") { }   // any non-empty string
if ([]) { }        // arrays (even empty)
if ({}) { }        // objects (even empty)
```

---

## Mini Project: Number Guessing Game

Create an interactive number guessing game where the computer picks a random number and the user tries to guess it with helpful feedback.

### Project Requirements:

1. **Game Setup:**
   - Computer generates a random number between 1 and 100
   - User has unlimited attempts to guess
   - Provide hints after each guess ("too high", "too low")

2. **User Interface:**
   - Welcome message explaining the rules
   - Input method for guesses (prompt or HTML form)
   - Clear feedback after each attempt
   - Victory message when correct

3. **Game Logic:**
   - Track number of attempts
   - Validate user input (must be a number 1-100)
   - Provide different messages based on how close the guess is
   - Option to play again

4. **Enhanced Features:**
   - Difficulty levels (different number ranges)
   - Scoring system based on number of attempts
   - Best score tracking
   - Visual feedback with colors

### Starter Code Structure:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Number Guessing Game</title>
    <style>
        body {
            font-family: 'Arial', sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            margin: 0;
            padding: 20px;
            min-height: 100vh;
            color: white;
        }
        
        .game-container {
            max-width: 600px;
            margin: 0 auto;
            background: rgba(255, 255, 255, 0.1);
            padding: 30px;
            border-radius: 15px;
            backdrop-filter: blur(10px);
            text-align: center;
        }
        
        .input-section {
            margin: 20px 0;
        }
        
        input {
            padding: 10px 15px;
            font-size: 18px;
            border: none;
            border-radius: 5px;
            margin: 0 10px;
            text-align: center;
        }
        
        button {
            background: #ff6b6b;
            color: white;
            border: none;
            padding: 12px 24px;
            border-radius: 5px;
            cursor: pointer;
            font-size: 16px;
            margin: 10px;
        }
        
        button:hover {
            background: #ff5252;
        }
        
        .feedback {
            margin: 20px 0;
            padding: 15px;
            border-radius: 10px;
            font-size: 18px;
            font-weight: bold;
        }
        
        .too-high { background: rgba(255, 193, 7, 0.3); }
        .too-low { background: rgba(33, 150, 243, 0.3); }
        .close { background: rgba(255, 152, 0, 0.3); }
        .correct { background: rgba(76, 175, 80, 0.3); }
        
        .stats {
            display: flex;
            justify-content: space-around;
            margin: 20px 0;
        }
        
        .stat {
            text-align: center;
        }
        
        .stat-number {
            font-size: 24px;
            font-weight: bold;
            color: #ffd700;
        }
    </style>
</head>
<body>
    <div class="game-container">
        <h1>🎯 Number Guessing Game</h1>
        <p>I'm thinking of a number between 1 and 100. Can you guess it?</p>
        
        <div class="stats">
            <div class="stat">
                <div class="stat-number" id="attempts">0</div>
                <div>Attempts</div>
            </div>
            <div class="stat">
                <div class="stat-number" id="bestScore">-</div>
                <div>Best Score</div>
            </div>
        </div>
        
        <div class="input-section">
            <input type="number" id="guessInput" min="1" max="100" placeholder="Enter your guess">
            <button onclick="makeGuess()">Guess!</button>
        </div>
        
        <div id="feedback" class="feedback" style="display: none;">
            Your feedback will appear here
        </div>
        
        <button onclick="newGame()" style="display: none;" id="newGameBtn">Play Again</button>
    </div>

    <script>
        let secretNumber;
        let attempts;
        let gameActive;
        
        function startGame() {
            // Initialize new game
        }
        
        function makeGuess() {
            // Handle user guess
        }
        
        function provideFeedback(guess) {
            // Provide feedback based on guess
        }
        
        function endGame() {
            // Handle game completion
        }
        
        function newGame() {
            // Reset for new game
        }
        
        // Start the game when page loads
        startGame();
    </script>
</body>
</html>
```

### Implementation Guide:

#### Core Game Logic:
```javascript
function startGame() {
    secretNumber = Math.floor(Math.random() * 100) + 1;
    attempts = 0;
    gameActive = true;
    
    // Reset UI
    document.getElementById('feedback').style.display = 'none';
    document.getElementById('newGameBtn').style.display = 'none';
    document.getElementById('guessInput').disabled = false;
    updateAttempts();
}

function makeGuess() {
    if (!gameActive) return;
    
    const guessInput = document.getElementById('guessInput');
    const guess = parseInt(guessInput.value);
    
    // Validate input
    if (isNaN(guess) || guess < 1 || guess > 100) {
        showFeedback("Please enter a number between 1 and 100!", "");
        return;
    }
    
    attempts++;
    updateAttempts();
    
    if (guess === secretNumber) {
        endGame();
    } else {
        provideFeedback(guess);
    }
    
    guessInput.value = '';
}
```

### Helpful Concepts to Explore:

**JavaScript Concepts:**
- `Math.random()` and `Math.floor()` for random number generation
- Input validation with `isNaN()` and range checking
- Conditional statements with multiple conditions
- DOM manipulation for dynamic feedback
- Event handling for user interactions

**HTML Concepts:**
- Form inputs with validation attributes
- Button interactions and state management
- Dynamic content updates
- Semantic structure for game interface

**CSS Concepts:**
- Visual feedback with different background colors
- Hover effects and transitions
- Flexbox for statistics layout
- Responsive design for different screen sizes

### Extension Ideas:

Once you complete the basic game, try adding:
- **Difficulty modes**: Easy (1-50), Medium (1-100), Hard (1-500)
- **Hint system**: "Very close!" when within 5 numbers
- **Time limit**: Add a countdown timer
- **High score system**: Track best scores for each difficulty
- **Sound effects**: Audio feedback for different outcomes
- **Multiplayer mode**: Two players take turns guessing
- **Statistics**: Track win rate, average attempts, etc.

---

## Mini Project: Grade Calculator

Build a comprehensive grade calculator that takes multiple test scores and calculates letter grades with visual feedback and helpful statistics.

### Project Requirements:

1. **Score Input:**
   - Accept multiple test scores (3-5 tests)
   - Validate that scores are between 0-100
   - Allow different point values for different tests

2. **Grade Calculation:**
   - Calculate average score
   - Determine letter grade (A, B, C, D, F)
   - Show grade point average (4.0 scale)
   - Display grade with appropriate styling

3. **Visual Feedback:**
   - Color-coded grades (A=green, F=red, etc.)
   - Progress bars showing performance
   - Different messages based on performance level

4. **Advanced Features:**
   - Weighted grades (tests, homework, participation)
   - Grade improvement suggestions
   - Class rank simulation
   - Export grade report

### Starter Code Structure:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Grade Calculator</title>
    <style>
        body {
            font-family: 'Arial', sans-serif;
            background: linear-gradient(135deg, #2196F3 0%, #21CBF3 100%);
            margin: 0;
            padding: 20px;
            min-height: 100vh;
        }
        
        .calculator-container {
            max-width: 700px;
            margin: 0 auto;
            background: white;
            padding: 30px;
            border-radius: 15px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.2);
        }
        
        .grade-display {
            text-align: center;
            padding: 20px;
            border-radius: 10px;
            margin: 20px 0;
            font-size: 24px;
            font-weight: bold;
        }
        
        .grade-a { background: linear-gradient(45deg, #4CAF50, #8BC34A); color: white; }
        .grade-b { background: linear-gradient(45deg, #2196F3, #03DAC6); color: white; }
        .grade-c { background: linear-gradient(45deg, #FF9800, #FFC107); color: white; }
        .grade-d { background: linear-gradient(45deg, #FF5722, #FF9800); color: white; }
        .grade-f { background: linear-gradient(45deg, #F44336, #E91E63); color: white; }
        
        .input-group {
            margin: 15px 0;
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
        }
        
        input:focus {
            border-color: #2196F3;
            outline: none;
        }
        
        button {
            background: #2196F3;
            color: white;
            border: none;
            padding: 12px 24px;
            border-radius: 5px;
            cursor: pointer;
            font-size: 16px;
            width: 100%;
            margin: 10px 0;
        }
        
        button:hover {
            background: #1976D2;
        }
        
        .progress-bar {
            width: 100%;
            height: 20px;
            background: #e0e0e0;
            border-radius: 10px;
            overflow: hidden;
            margin: 10px 0;
        }
        
        .progress-fill {
            height: 100%;
            border-radius: 10px;
            transition: width 0.5s ease;
        }
        
        .statistics {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
            gap: 15px;
            margin: 20px 0;
        }
        
        .stat-card {
            background: #f5f5f5;
            padding: 15px;
            border-radius: 8px;
            text-align: center;
        }
        
        .stat-value {
            font-size: 24px;
            font-weight: bold;
            color: #2196F3;
        }
    </style>
</head>
<body>
    <div class="calculator-container">
        <h1>📊 Grade Calculator</h1>
        <p>Enter your test scores to calculate your overall grade</p>
        
        <div class="input-group">
            <label for="test1">Test 1 Score (0-100):</label>
            <input type="number" id="test1" min="0" max="100" placeholder="Enter score">
        </div>
        
        <div class="input-group">
            <label for="test2">Test 2 Score (0-100):</label>
            <input type="number" id="test2" min="0" max="100" placeholder="Enter score">
        </div>
        
        <div class="input-group">
            <label for="test3">Test 3 Score (0-100):</label>
            <input type="number" id="test3" min="0" max="100" placeholder="Enter score">
        </div>
        
        <div class="input-group">
            <label for="test4">Test 4 Score (0-100) [Optional]:</label>
            <input type="number" id="test4" min="0" max="100" placeholder="Enter score">
        </div>
        
        <button onclick="calculateGrade()">Calculate My Grade</button>
        
        <div id="results" style="display: none;">
            <div id="gradeDisplay" class="grade-display">
                Your grade will appear here
            </div>
            
            <div class="progress-bar">
                <div id="progressFill" class="progress-fill"></div>
            </div>
            
            <div class="statistics">
                <div class="stat-card">
                    <div class="stat-value" id="average">0</div>
                    <div>Average Score</div>
                </div>
                <div class="stat-card">
                    <div class="stat-value" id="letterGrade">-</div>
                    <div>Letter Grade</div>
                </div>
                <div class="stat-card">
                    <div class="stat-value" id="gpa">0.0</div>
                    <div>GPA (4.0 Scale)</div>
                </div>
                <div class="stat-card">
                    <div class="stat-value" id="testsCount">0</div>
                    <div>Tests Counted</div>
                </div>
            </div>
            
            <div id="feedback" style="margin: 20px 0; padding: 15px; border-radius: 8px;">
                Performance feedback will appear here
            </div>
        </div>
        
        <button onclick="reset()" style="display: none;" id="resetBtn">Calculate New Grades</button>
    </div>

    <script>
        function calculateGrade() {
            // Collect all scores
            const scores = [];
            const inputs = ['test1', 'test2', 'test3', 'test4'];
            
            inputs.forEach(inputId => {
                const value = document.getElementById(inputId).value;
                if (value !== '' && !isNaN(value)) {
                    const score = parseFloat(value);
                    if (score >= 0 && score <= 100) {
                        scores.push(score);
                    }
                }
            });
            
            // Validate minimum scores
            if (scores.length < 2) {
                alert('Please enter at least 2 valid test scores.');
                return;
            }
            
            // Calculate average
            const average = scores.reduce((sum, score) => sum + score, 0) / scores.length;
            
            // Determine letter grade and GPA
            const letterGrade = getLetterGrade(average);
            const gpa = getGPA(letterGrade);
            const gradeClass = getGradeClass(letterGrade);
            
            // Display results
            displayResults(average, letterGrade, gpa, scores.length, gradeClass);
            
            // Show feedback
            showFeedback(average, letterGrade);
        }
        
        function getLetterGrade(average) {
            if (average >= 90) return 'A';
            else if (average >= 80) return 'B';
            else if (average >= 70) return 'C';
            else if (average >= 60) return 'D';
            else return 'F';
        }
        
        function getGPA(letterGrade) {
            const gpaScale = { 'A': 4.0, 'B': 3.0, 'C': 2.0, 'D': 1.0, 'F': 0.0 };
            return gpaScale[letterGrade];
        }
        
        function getGradeClass(letterGrade) {
            return `grade-${letterGrade.toLowerCase()}`;
        }
        
        function displayResults(average, letterGrade, gpa, testCount, gradeClass) {
            // Show results section
            document.getElementById('results').style.display = 'block';
            document.getElementById('resetBtn').style.display = 'block';
            
            // Update grade display
            const gradeDisplay = document.getElementById('gradeDisplay');
            gradeDisplay.className = `grade-display ${gradeClass}`;
            gradeDisplay.textContent = `Grade: ${letterGrade} (${average.toFixed(1)}%)`;
            
            // Update progress bar
            const progressFill = document.getElementById('progressFill');
            progressFill.style.width = `${average}%`;
            progressFill.className = `progress-fill ${gradeClass}`;
            
            // Update statistics
            document.getElementById('average').textContent = average.toFixed(1) + '%';
            document.getElementById('letterGrade').textContent = letterGrade;
            document.getElementById('gpa').textContent = gpa.toFixed(1);
            document.getElementById('testsCount').textContent = testCount;
        }
        
        function showFeedback(average, letterGrade) {
            const feedbackElement = document.getElementById('feedback');
            let message = '';
            let bgColor = '';
            
            if (letterGrade === 'A') {
                message = '🎉 Excellent work! You\'re performing at the highest level. Keep up the outstanding effort!';
                bgColor = '#e8f5e8';
            } else if (letterGrade === 'B') {
                message = '👍 Great job! You\'re doing well. A little more effort could get you to an A!';
                bgColor = '#e3f2fd';
            } else if (letterGrade === 'C') {
                message = '📚 You\'re passing, but there\'s room for improvement. Consider studying more or getting help.';
                bgColor = '#fff3e0';
            } else if (letterGrade === 'D') {
                message = '⚠️ You\'re barely passing. It\'s time to seek help and develop better study habits.';
                bgColor = '#fce4ec';
            } else {
                message = '🚨 You\'re currently failing. Please speak with your teacher immediately for help and support.';
                bgColor = '#ffebee';
            }
            
            feedbackElement.textContent = message;
            feedbackElement.style.backgroundColor = bgColor;
            feedbackElement.style.border = `2px solid ${bgColor}`;
        }
        
        function reset() {
            // Clear all inputs
            document.getElementById('test1').value = '';
            document.getElementById('test2').value = '';
            document.getElementById('test3').value = '';
            document.getElementById('test4').value = '';
            
            // Hide results
            document.getElementById('results').style.display = 'none';
            document.getElementById('resetBtn').style.display = 'none';
        }
    </script>
</body>
</html>
```

### Helpful Concepts to Explore:

**JavaScript Concepts:**
- Array methods (`.forEach()`, `.reduce()`, `.filter()`)
- Input validation and data sanitization
- Object literal notation for lookup tables
- Complex conditional logic with multiple criteria
- DOM manipulation for dynamic styling
- Mathematical calculations and rounding

**HTML Concepts:**
- Form design and user experience
- Input attributes for validation
- Progressive disclosure (showing/hiding content)
- Accessibility considerations for form labels

**CSS Concepts:**
- CSS Grid for responsive statistics layout
- CSS custom properties for theme colors
- Transition animations for smooth interactions
- Gradient backgrounds for visual appeal

### Extension Ideas:

Once you complete the basic calculator, try adding:
- **Weighted categories**: Tests (60%), Homework (25%), Participation (15%)
- **Grade trends**: Show improvement or decline over time
- **What-if calculator**: "What do I need on the final to get an A?"
- **Class comparison**: Compare your grades to class average
- **Export functionality**: Generate a PDF grade report
- **Multiple subjects**: Track grades across different classes
- **Goal setting**: Set target grades and track progress

---

## Advanced Conditional Patterns

### Ternary Operator (Conditional Operator)

The ternary operator provides a concise way to write simple conditional statements:

```javascript
// Basic syntax: condition ? valueIfTrue : valueIfFalse
const age = 20;
const status = age >= 18 ? "adult" : "minor";

// Multiple ternary operators
const grade = score >= 90 ? "A" : 
              score >= 80 ? "B" : 
              score >= 70 ? "C" : 
              score >= 60 ? "D" : "F";

// With function calls
const message = isLoggedIn ? getWelcomeMessage() : getLoginPrompt();
```

### Switch Statements

For multiple conditions based on the same variable:

```javascript
const day = "Monday";

switch (day) {
    case "Monday":
        console.log("Start of the work week!");
        break;
    case "Tuesday":
    case "Wednesday":
    case "Thursday":
        console.log("Midweek grind!");
        break;
    case "Friday":
        console.log("TGIF!");
        break;
    case "Saturday":
    case "Sunday":
        console.log("Weekend time!");
        break;
    default:
        console.log("Not a valid day");
}
```

### Short-Circuit Evaluation

Using logical operators for concise conditional execution:

```javascript
// Logical AND for conditional execution
isLoggedIn && displayDashboard();

// Logical OR for default values
const username = userInput || "Guest";

// Nullish coalescing for null/undefined checks
const config = userConfig ?? defaultConfig;
```

---

## Common Conditional Mistakes and Solutions

### 1. Assignment vs Comparison
```javascript
// Wrong - assignment instead of comparison
if (score = 100) { } // Always true, assigns 100 to score

// Correct - comparison
if (score === 100) { } // Checks if score equals 100
```

### 2. Floating Point Comparison
```javascript
// Wrong - direct comparison of floating point numbers
if (0.1 + 0.2 === 0.3) { } // false due to precision

// Correct - use a tolerance
if (Math.abs((0.1 + 0.2) - 0.3) < 0.0001) { } // true
```

### 3. Truthy/Falsy Confusion
```javascript
// Potentially confusing
if (value) { } // true for any truthy value

// More explicit
if (value !== null && value !== undefined) { }
if (value.length > 0) { } // for strings/arrays
```

---

## Assessment Checklist

Before moving to Part 4, ensure you can:
- [ ] Write `if`, `else if`, and `else` statements correctly
- [ ] Use comparison operators appropriately (`===`, `!==`, `>`, `<`, etc.)
- [ ] Combine conditions with logical operators (`&&`, `||`, `!`)
- [ ] Understand truthy and falsy values
- [ ] Validate user input with conditional logic
- [ ] Create interactive programs that respond to different inputs
- [ ] Use ternary operators for simple conditional assignments
- [ ] Debug conditional logic issues

---

## Additional Resources

**Essential Learning:**
- **MDN**: [Making Decisions in Your Code - Conditionals](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Building_blocks/conditionals)
- **MDN**: [Logical Operators](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Logical_Operators)
- **freeCodeCamp**: [Basic JavaScript - Conditional Logic](https://www.freecodecamp.org/learn/javascript-algorithms-and-data-structures/)

**Practice Platforms:**
- **Codecademy**: [Conditional Statements](https://www.codecademy.com/learn/introduction-to-javascript)
- **JavaScript.info**: [Conditional Operators](https://javascript.info/logical-operators)

**Interactive Challenges:**
- **Codewars**: [Beginner JavaScript Kata](https://www.codewars.com/)
- **HackerRank**: [JavaScript Domain](https://www.hackerrank.com/domains/javascript)

---

## Next Steps

Once you've mastered conditional logic and completed both the Number Guessing Game and Grade Calculator projects, you're ready to move on to [Part 4: Functions - Organizing Your Code](4_functions.md) where you'll learn to organize your code into reusable, modular functions.