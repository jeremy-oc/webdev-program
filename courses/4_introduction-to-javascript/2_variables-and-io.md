# Part 2: Variables and Basic Input/Output

## Modern Variable Declarations

### Understanding `let` vs `const`

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

**Good naming practices:**
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

// Better approach with template literals
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

## Mini Project: Personal Information Card

Build a comprehensive personal information card that collects user data and displays it in a beautifully formatted layout with dynamic styling.

### Project Requirements:

1. **Data Collection:**
   - Full name (first and last)
   - Age
   - City/Location
   - Favorite color
   - Occupation or hobby

2. **Dynamic Display:**
   - Create a card layout showing all information
   - Style the card based on the user's age group:
     - Under 18: Bright, playful colors
     - 18-65: Professional, clean design
     - Over 65: Classic, elegant styling
   - Use the user's favorite color as an accent

3. **Information Processing:**
   - Calculate and display birth year
   - Create a personalized greeting message
   - Generate a unique user ID from their information

4. **Advanced Features:**
   - Validate age input (must be positive number)
   - Capitalize names properly
   - Show different messages for different age groups

### Starter Code Structure:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Personal Information Card</title>
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
            padding: 30px;
            border-radius: 15px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.3);
        }
        
        .info-card {
            display: none;
            margin-top: 20px;
            padding: 20px;
            border-radius: 10px;
            text-align: center;
        }
        
        .young { background: linear-gradient(45deg, #ff6b6b, #4ecdc4); }
        .adult { background: linear-gradient(45deg, #667eea, #764ba2); }
        .senior { background: linear-gradient(45deg, #d4af37, #8b7355); }
        
        button {
            background: #667eea;
            color: white;
            border: none;
            padding: 12px 24px;
            border-radius: 5px;
            cursor: pointer;
            font-size: 16px;
        }
        
        button:hover {
            background: #764ba2;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Personal Information Card Generator</h1>
        <p>Create your personalized information card!</p>
        
        <button onclick="createCard()">Create My Card</button>
        
        <div id="infoCard" class="info-card">
            <!-- Card content will be generated here -->
        </div>
    </div>

    <script>
        function createCard() {
            // Your JavaScript code here!
        }
        
        function getAgeGroup(age) {
            // Helper function to determine age group
        }
        
        function formatName(name) {
            // Helper function to capitalize names
        }
    </script>
</body>
</html>
```

### Helpful Concepts to Explore:

**JavaScript Concepts:**
- Variable assignment with `let` and `const`
- String methods (`.toUpperCase()`, `.toLowerCase()`, `.slice()`)
- Template literals for complex strings
- Number conversion and validation
- Conditional logic for age groups
- DOM manipulation (`.innerHTML`, `.style`)

**HTML Concepts:**
- Form structure and input types
- Div containers and semantic elements
- ID and class attributes for styling
- Button interactions

**CSS Concepts:**
- CSS classes and dynamic class assignment
- Flexbox or grid for card layout
- Gradient backgrounds and transitions
- Responsive design principles
- Box shadows and border radius

### Sample Implementation Features:

```javascript
// Example of what your code might include:
function createCard() {
    // Collect information
    const firstName = prompt("Enter your first name:");
    const lastName = prompt("Enter your last name:");
    const age = parseInt(prompt("Enter your age:"));
    const city = prompt("Enter your city:");
    const favoriteColor = prompt("Enter your favorite color:");
    
    // Validate and process data
    if (isNaN(age) || age < 0) {
        alert("Please enter a valid age!");
        return;
    }
    
    // Calculate additional information
    const currentYear = new Date().getFullYear();
    const birthYear = currentYear - age;
    const ageGroup = getAgeGroup(age);
    
    // Generate unique ID
    const userId = (firstName.slice(0,2) + lastName.slice(0,2) + age).toUpperCase();
    
    // Create personalized message
    const greeting = generateGreeting(ageGroup, firstName);
    
    // Display the card
    displayCard(firstName, lastName, age, city, favoriteColor, birthYear, userId, greeting, ageGroup);
}
```

### Extension Ideas:

Once you complete the basic project, try adding:
- **Photo upload**: Allow users to add a profile picture
- **Social media links**: Include optional social media handles
- **Interests selection**: Multiple choice hobbies/interests
- **Export functionality**: Download the card as an image
- **Multiple cards**: Create and compare multiple profiles
- **Local storage**: Save and reload user information
- **Animation effects**: Smooth transitions and hover effects

### Testing Checklist:

- [ ] All prompts collect user information correctly
- [ ] Age validation works (handles invalid input)
- [ ] Names are properly capitalized
- [ ] Card styling changes based on age group
- [ ] Favorite color is incorporated into the design
- [ ] Birth year calculation is accurate
- [ ] All information displays correctly
- [ ] Card is visually appealing and responsive

---

## Common Variable Mistakes and Solutions

### 1. Trying to Reassign `const` Variables
```javascript
// Wrong
const score = 0;
score = 10; // TypeError!

// Correct
let score = 0;
score = 10; // Works fine
```

### 2. Forgetting to Convert Strings to Numbers
```javascript
// Wrong - this concatenates strings
const userInput = prompt("Enter a number:");
const result = userInput + 5; // "105" if user enters "10"

// Correct - convert to number first
const userInput = prompt("Enter a number:");
const result = parseInt(userInput) + 5; // 15 if user enters "10"
```

### 3. Template Literal Syntax Errors
```javascript
// Wrong - using regular quotes
const message = "Hello, ${name}!"; // Literal string, not interpolated

// Correct - using backticks
const message = `Hello, ${name}!`; // Properly interpolated
```

---

## Assessment Checklist

Before moving to Part 3, ensure you can:
- [ ] Choose between `let` and `const` appropriately
- [ ] Create and manipulate strings using various methods
- [ ] Work with numbers and perform basic calculations
- [ ] Use template literals for string interpolation
- [ ] Understand variable scope basics
- [ ] Collect and validate user input
- [ ] Create dynamic content based on user data

---

## Additional Resources

**Essential Learning:**
- **MDN**: [Variables and Data Types](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/First_steps/Variables)
- **MDN**: [Strings in JavaScript](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/First_steps/Strings)
- **MDN**: [Template Literals](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals)

**Practice Platforms:**
- **Codecademy**: [Variables and Data Types](https://www.codecademy.com/learn/introduction-to-javascript)
- **freeCodeCamp**: [Basic JavaScript](https://www.freecodecamp.org/learn/javascript-algorithms-and-data-structures/)

**Tools:**
- **MDN**: [String Methods Reference](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String)
- **MDN**: [Math Object Reference](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Math)

---

## Next Steps

Once you've mastered variables and basic input/output and completed your Personal Information Card project, you're ready to move on to [Part 3: Making Decisions with Conditionals](3_conditionals.md) where you'll learn to make your programs respond intelligently to different situations.