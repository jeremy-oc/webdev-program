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

## Mini Project: Simple Quiz Game

Create an interactive quiz game that asks the user questions and provides feedback based on their answers.

### Project Requirements:

1. **Game Structure:**
   - Ask 3-5 multiple choice questions
   - Track correct and incorrect answers
   - Provide immediate feedback after each question
   - Show final score and grade

2. **User Interface:**
   - Simple buttons for answer choices
   - Clear feedback messages
   - Score display
   - Play again option

3. **Conditional Logic:**
   - Use `if/else` statements to check answers
   - Provide different feedback based on score
   - Grade the final performance

### Minimal Starter Code:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Simple Quiz</title>
    <style>
        body { font-family: Arial, sans-serif; max-width: 600px; margin: 50px auto; padding: 20px; }
        .question { margin: 20px 0; padding: 15px; border: 1px solid #ddd; border-radius: 5px; }
        button { margin: 5px; padding: 10px 15px; cursor: pointer; }
        .correct { background-color: #d4edda; }
        .incorrect { background-color: #f8d7da; }
    </style>
</head>
<body>
    <h1>JavaScript Quiz</h1>
    <div id="quiz-container">
        <div id="question-1" class="question">
            <p><strong>Question 1:</strong> What does HTML stand for?</p>
            <button onclick="checkAnswer(1, 'correct')">HyperText Markup Language</button>
            <button onclick="checkAnswer(1, 'wrong')">Home Tool Markup Language</button>
            <button onclick="checkAnswer(1, 'wrong')">Hyperlinks and Text Markup Language</button>
        </div>
        
        <div id="question-2" class="question">
            <p><strong>Question 2:</strong> Which symbol is used for comments in JavaScript?</p>
            <button onclick="checkAnswer(2, 'wrong')">#</button>
            <button onclick="checkAnswer(2, 'correct')">//</button>
            <button onclick="checkAnswer(2, 'wrong')">/* */</button>
        </div>
        
        <!-- Add more questions here -->
    </div>
    
    <div id="results" style="display: none;">
        <h2>Quiz Complete!</h2>
        <p id="score-display"></p>
        <p id="grade-message"></p>
        <button onclick="resetQuiz()">Take Quiz Again</button>
    </div>

    <script>
        let score = 0;
        let questionsAnswered = 0;
        const totalQuestions = 2; // Update this as you add questions

        function checkAnswer(questionNum, answerType) {
            // Your conditional logic goes here
            // Check if answer is correct
            // Update score
            // Provide feedback
            // Check if quiz is complete
        }

        function showResults() {
            // Calculate final grade
            // Display results with conditional messages
        }

        function resetQuiz() {
            // Reset game state
        }
    </script>
</body>
</html>
```

### Implementation Guidelines:

1. **Start Simple**: Begin with just 2-3 questions to focus on the conditional logic
2. **Use Clear Conditionals**: Practice `if/else` statements for checking answers
3. **Add Feedback**: Use conditionals to show different messages based on performance
4. **Expand Gradually**: Add more questions and features as you master the basics

### Key Learning Objectives:

- Practice writing conditional statements
- Understand how to validate user input
- Learn to provide dynamic feedback based on conditions
- Use logical operators to create complex conditions
- Implement game state management with conditionals

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

Once you've mastered conditional logic and completed the Simple Quiz Game project, you're ready to move on to [Part 4: Functions - Organizing Your Code](4_functions.md) where you'll learn to organize your code into reusable, modular functions.