# Part 2: Variables and Basic Input/Output

## Pre-Learning Video Tutorial (Continued)

**🎥 Continue with: Net Ninja - Modern JavaScript Tutorial**
**Topic: "Syntax Basics & Types"**

Video: [https://www.youtube.com/watch?v=FhguwBJeqWs](https://www.youtube.com/watch?v=FhguwBJeqWs)

If you haven't already completed the Net Ninja tutorial from Part 1, make sure to watch it now. This section builds directly on the syntax and type concepts covered in that video, particularly focusing on:

**Advanced concepts from the video that apply to this section:**
- Variable declaration best practices
- Data type handling and conversion
- Modern JavaScript syntax patterns
- String manipulation techniques
- Number operations and methods

**Video Integration Note:** As you work through this section, refer back to the specific examples and patterns demonstrated in the tutorial, especially regarding variable declarations and data type operations.

---

## Modern Variable Declarations

### Understanding `let` vs `const`

**🎯 Video Connection:** The Net Ninja tutorial covers these modern declaration keywords. Apply those concepts here!

Modern JavaScript uses two primary ways to declare variables: `let` and `const`. Understanding when to use each is crucial for writing clean, maintainable code.

#### `const` - For Values That Don't Change
```javascript
const userName = "Alice";
const maxAge = 100;
const pi = 3.14159;

// This would cause an error:
// userName = "Bob"; // TypeError: Assignment to constant variable
```

**When to use `const`:**
- Values that won't be reassigned
- Mathematical constants
- Configuration values
- Function references

#### `let` - For Values That Change
```javascript
let currentAge = 25;
let score = 0;
let isLoggedIn = false;

// These are all valid:
currentAge = 26;
score = score + 10;
isLoggedIn = true;
```

**When to use `let`:**
- Counters and accumulators
- User input values
- Conditional assignments
- Loop variables

### Variable Naming Conventions

**Good naming practices (following video tutorial standards):**
```javascript
// Use camelCase for variables
const firstName = "John";
const userEmail = "john@example.com";
let totalPrice = 99.99;

// Use descriptive names
const maxRetries = 3;
const isFormValid = true;
let currentUserIndex = 0;
```

**Avoid these naming patterns:**
```javascript
// Too short or unclear
let x = "John";
let data = 25;

// Using reserved words
// let class = "beginner"; // Error!
// let function = "test"; // Error!
```

### Understanding Scope Basics

**Block Scope with `let` and `const`:**
```javascript
{
    let blockVariable = "I'm only available in this block";
    const blockConstant = 42;
}
// console.log(blockVariable); // Error: not defined
```

**Function Scope:**
```javascript
function calculateArea() {
    let length = 10;
    let width = 5;
    return length * width;
}
// console.log(length); // Error: not defined outside function
```

---

## Working with Data Types

**🎯 Video Reference:** This section directly applies the data type concepts from the Net Ninja tutorial. Review those examples as you work through these exercises.

### Strings and String Methods

#### Creating Strings
```javascript
const singleQuotes = 'Hello, World!';
const doubleQuotes = "Hello, World!";
const templateLiteral = `Hello, World!`;

// Strings with quotes inside
const message = "She said, 'Hello there!'";
const quote = 'He replied, "Nice to meet you!"';
```

#### Essential String Methods
```javascript
const text = "JavaScript is awesome";

// Length
console.log(text.length); // 20

// Case conversion
console.log(text.toUpperCase()); // "JAVASCRIPT IS AWESOME"
console.log(text.toLowerCase()); // "javascript is awesome"

// Finding text
console.log(text.includes("Script")); // true
console.log(text.indexOf("Script")); // 4

// Extracting parts
console.log(text.slice(0, 10)); // "JavaScript"
console.log(text.split(" ")); // ["JavaScript", "is", "awesome"]
```

#### String Concatenation
```javascript
// Traditional concatenation
const firstName = "John";
const lastName = "Doe";
const fullName = firstName + " " + lastName;

// Better approach with template literals (modern syntax from video)
const greeting = `Hello, ${firstName} ${lastName}!`;
const calculation = `The result is ${5 + 3}`;
```

### Numbers and Basic Math Operations

#### Working with Numbers
```javascript
const age = 25;
const price = 19.99;
const score = -5;

// Basic arithmetic
let total = 100;
total = total + 50;  // Addition: 150
total = total - 20;  // Subtraction: 130
total = total * 2;   // Multiplication: 260
total = total / 4;   // Division: 65
total = total % 10;  // Modulus (remainder): 5
```

#### Useful Math Methods
```javascript
// Rounding
console.log(Math.round(4.7));    // 5
console.log(Math.ceil(4.1));     // 5 (round up)
console.log(Math.floor(4.9));    // 4 (round down)

// Random numbers
console.log(Math.random());      // Random number 0-1
console.log(Math.random() * 10); // Random number 0-10

// Min/Max
console.log(Math.max(5, 10, 3)); // 10
console.log(Math.min(5, 10, 3)); // 3
```

### Template Literals for String Interpolation

**🎯 Video Application:** This modern syntax feature should align with the patterns shown in the Net Ninja tutorial.

Template literals (backticks) make string creation much more powerful:

```javascript
const name = "Alice";
const age = 30;
const city = "New York";

// Multi-line strings
const bio = `
Name: ${name}
Age: ${age}
City: ${city}
Status: Active
`;

// Expressions inside template literals
const shoppingCart = {
    items: 3,
    total: 45.99
};

const receipt = `
Thank you for your purchase!
Items: ${shoppingCart.items}
Total: $${shoppingCart.total.toFixed(2)}
Tax: $${(shoppingCart.total * 0.08).toFixed(2)}
`;
```

---

## Mini Project: Age Calculator

**🎯 Post-Video Application:** This project integrates the syntax patterns and data type handling techniques from the Net Ninja tutorial.

Build a simple age calculator that tells users interesting facts about their age.

### Project Goal:
Create an app that calculates how many days, hours, and minutes someone has been alive, applying proper variable declarations and data type handling from the video tutorial.

### Starter Code:
```html
<!DOCTYPE html>
<html>
<head>
    <title>Age Calculator</title>
</head>
<body>
    <h1>Age Calculator</h1>
    <button onclick="calculateAge()">Calculate My Age</button>

    <script>
        function calculateAge() {
            // Your code here
            // Apply video concepts: proper variable declarations,
            // data type handling, and modern syntax patterns
        }
    </script>
</body>
</html>
```

### Your Task:
1. **Apply video concepts**: Use `const` and `let` appropriately as demonstrated in the tutorial
2. Ask the user for their name and age using `prompt()`
3. **Data type handling**: Properly convert string inputs to numbers (video concept)
4. Calculate their birth year
5. Calculate how many days they've been alive (roughly)
6. **Modern syntax**: Use template literals for formatted output (video feature)
7. Display all results using `alert()` with template literals
8. Log the calculations to the console

### Expected Output:
```
Hello Sarah!
You are 25 years old.
You were born in 1999.
You have been alive for approximately 9,125 days!
```

### Key Concepts to Practice (Video Integration):
- Using `const` and `let` appropriately (video best practices)
- Converting strings to numbers with `parseInt()` (data type handling from video)
- Template literals for formatted output (modern syntax from video)
- Basic math operations (number types from video)
- Getting current year with `new Date().getFullYear()`

### Video Integration Checklist:
- [ ] Used proper variable declaration patterns from the tutorial
- [ ] Applied data type conversion techniques shown in the video
- [ ] Implemented modern string interpolation methods
- [ ] Followed coding style and syntax conventions from the tutorial

---

## Common Variable Mistakes and Solutions

**🎯 Video Reference:** These common mistakes align with the best practices covered in the Net Ninja tutorial.

### 1. Trying to Reassign `const` Variables
```javascript
// Wrong
const score = 0;
score = 10; // TypeError!

// Correct
let score = 0;
score = 10; // Works fine
```

### 2. Forgetting to Convert Strings to Numbers (Video Concept)
```javascript
// Wrong - this concatenates strings
const userInput = prompt("Enter a number:");
const result = userInput + 5; // "105" if user enters "10"

// Correct - convert to number first (data type handling from video)
const userInput = prompt("Enter a number:");
const result = parseInt(userInput) + 5; // 15 if user enters "10"
```

### 3. Template Literal Syntax Errors (Modern Syntax from Video)
```javascript
// Wrong - using regular quotes
const message = "Hello, ${name}!"; // Literal string, not interpolated

// Correct - using backticks (modern syntax from video)
const message = `Hello, ${name}!`; // Properly interpolated
```

---

## Assessment Checklist

Before moving to Part 3, ensure you can:
- [ ] **Applied concepts from the Net Ninja video tutorial**
- [ ] Choose between `let` and `const` appropriately
- [ ] Create and manipulate strings using various methods
- [ ] Work with numbers and perform basic calculations
- [ ] Use template literals for string interpolation
- [ ] Understand variable scope basics
- [ ] Collect and validate user input
- [ ] Create dynamic content based on user data
- [ ] **Handle data type conversions properly (video concept)**
- [ ] **Use modern JavaScript syntax patterns (video standards)**

---

## Additional Resources

**Essential Learning:**
- **MDN**: [Variables and Data Types](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/First_steps/Variables)
- **MDN**: [Strings in JavaScript](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/First_steps/Strings)
- **MDN**: [Template Literals](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals)

**Practice Platforms:**
- **Codecademy**: [Variables and Data Types](https://www.codecademy.com/learn/introduction-to-javascript)

**Tools:**
- **MDN**: [String Methods Reference](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)
- **MDN**: [Math Object Reference](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Math)

---

## Next Steps

Once you've completed the Net Ninja video tutorial concepts, mastered variables and basic input/output, and finished your Age Calculator project with proper modern JavaScript syntax, you're ready to move on to [Part 3: Making Decisions with Conditionals](3_conditionals.md) where you'll learn to make your programs respond intelligently to different situations.