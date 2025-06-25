# Part 1: Getting Started with the Basics

## Pre-Learning Video Tutorial

**🎥 Reccommended Viewing: Net Ninja - Modern JavaScript Tutorial**
**Topic: "Syntax Basics & Types"**

Video: [https://www.youtube.com/watch?v=FhguwBJeqWs](https://www.youtube.com/watch?v=FhguwBJeqWs)

Before diving into the text content and hands-on exercises below, watch this essential tutorial that covers the foundational concepts of JavaScript syntax and data types. This video will provide you with the visual and auditory learning foundation that complements the written materials.

**What you'll learn in the video:**
- JavaScript syntax fundamentals
- Basic data types and their usage
- Proper code structure and conventions
- Common syntax patterns in modern JavaScript

**Note:** Take notes while watching and refer back to them as you work through the exercises below.

---

## What is JavaScript?

### JavaScript's Role in Web Development

JavaScript is the programming language that makes websites interactive and dynamic. While HTML provides structure and CSS handles styling, JavaScript brings functionality and behavior to web pages.

#### Key Concepts:
- JavaScript runs in web browsers (client-side) and on servers (Node.js)
- It can manipulate HTML content, respond to user actions, and communicate with servers
- JavaScript works alongside HTML and CSS to create complete web experiences
- Modern web development relies heavily on JavaScript for user interactions

#### The Web Development Trinity:
- **HTML**: Structure and content ("What is on the page?")
- **CSS**: Styling and layout ("How does it look?")
- **JavaScript**: Behavior and interactivity ("What does it do?")

### Where JavaScript Runs

**In the Browser:**
- Directly embedded in HTML pages
- Responds to user interactions (clicks, form submissions, etc.)
- Manipulates page content in real-time
- Communicates with web servers

**Beyond the Browser:**
- Node.js for server-side applications
- Mobile app development (React Native, Cordova)
- Desktop applications (Electron)
- Game development and automation scripts

---

## Your First JavaScript Code

### Embedding JavaScript in HTML

There are three main ways to include JavaScript in your HTML:

#### 1. Inline JavaScript (Not Recommended)
```html
<button onclick="alert('Hello!')">Click me</button>
```

#### 2. Internal JavaScript
```html
<!DOCTYPE html>
<html>
<head>
    <title>My First JavaScript</title>
</head>
<body>
    <h1>Welcome to JavaScript</h1>
    
    <script>
        console.log("Hello, JavaScript!");
        alert("Welcome to my website!");
    </script>
</body>
</html>
```

#### 3. External JavaScript (Best Practice)
```html
<!DOCTYPE html>
<html>
<head>
    <title>My Website</title>
</head>
<body>
    <h1>Welcome</h1>
    <script src="script.js"></script>
</body>
</html>
```

**script.js:**
```javascript
console.log("Hello from external file!");
```

### Using the Browser Developer Tools Console

The browser console is your best friend for learning JavaScript!

#### How to Open Developer Tools:
- **Chrome/Edge**: Press `F12` or `Ctrl+Shift+I` (Windows) / `Cmd+Option+I` (Mac)
- **Firefox**: Press `F12` or `Ctrl+Shift+I` (Windows) / `Cmd+Option+I` (Mac)
- **Safari**: Press `Cmd+Option+I` (enable Developer menu first)

#### Your First `console.log()` Statement:
```javascript
console.log("Hello, World!");
console.log("My name is", "Alex");
console.log("I am", 25, "years old");
```

**Why use `console.log()`?**
- Displays messages in the developer console
- Essential for debugging and testing code
- Shows variable values and program flow
- Invisible to website visitors

---

## Basic Interaction

### Using `alert()` for Simple Messages

The `alert()` function displays a popup message to the user:

```javascript
alert("Welcome to my website!");
alert("This is important information!");
```

**When to use alerts:**
- Important notifications
- Simple user feedback
- Learning and testing (not for production websites)

### Getting User Input with `prompt()`

The `prompt()` function asks the user to enter information:

```javascript
let userName = prompt("What is your name?");
console.log("Hello, " + userName + "!");

let userAge = prompt("How old are you?");
alert("You are " + userAge + " years old!");
```

**Key Points:**
- `prompt()` always returns a string (even for numbers)
- Users can click "Cancel" (returns `null`)
- Not commonly used in modern web development, but great for learning

### Combining Input and Output

```javascript
let firstName = prompt("Enter your first name:");
let lastName = prompt("Enter your last name:");
let fullName = firstName + " " + lastName;

alert("Nice to meet you, " + fullName + "!");
console.log("User's full name:", fullName);
```

---

## Mini Project: Simple Greeting App

**🎯 Post-Video Application:** Now that you've watched the Net Ninja tutorial and read through the concepts above, it's time to apply what you've learned!

Create a webpage that asks for the user's name and displays a personalized greeting.

### Project Goal:
Build a simple interactive webpage that collects a user's name and shows them a welcome message, applying the syntax and type concepts from the video tutorial.

### Starter Code:
```html
<!DOCTYPE html>
<html>
<head>
    <title>My Greeting App</title>
</head>
<body>
    <h1>Welcome!</h1>
    <button onclick="greetUser()">Say Hello</button>

    <script>
        function greetUser() {
            // Your code here
            // Remember the syntax patterns from the video!
        }
    </script>
</body>
</html>
```

### Your Task:
1. **Apply video concepts**: Use proper JavaScript syntax as demonstrated in the tutorial
2. Ask the user for their name using `prompt()`
3. Display a personalized greeting using `alert()`  
4. Log the greeting to the console using `console.log()`
5. **Bonus**: Implement proper data type handling as shown in the video

### Expected Behavior:
1. User clicks the "Say Hello" button
2. Browser asks "What is your name?"
3. User enters their name and clicks OK
4. Browser shows alert: "Hello, [Name]! Welcome to my website!"
5. Console shows: "Greeting displayed for: [Name]"

### Video Integration Checklist:
- [ ] Applied proper JavaScript syntax from the tutorial
- [ ] Used appropriate data types as demonstrated
- [ ] Followed coding conventions shown in the video
- [ ] Implemented clean, readable code structure

---

## Common Beginner Mistakes and Solutions

### 1. Forgetting Semicolons
```javascript
// Inconsistent (works but not recommended)
alert("Hello")
console.log("World")

// Better (consistent style)
alert("Hello");
console.log("World");
```

### 2. Case Sensitivity Issues
```javascript
// Wrong - JavaScript is case-sensitive
Alert("Hello"); // Error: Alert is not defined

// Correct
alert("Hello");
```

### 3. Forgetting Quotes for Strings
```javascript
// Wrong
let name = John; // Error: John is not defined

// Correct
let name = "John";
let name = 'John'; // Both single and double quotes work
```

### 4. Mixing Up Console and Alert
```javascript
// For user-visible messages
alert("This shows to the user");

// For debugging/development
console.log("This shows in the developer console");
```

---

## Assessment Checklist

Before moving to Part 2, ensure you can:
- [ ] **Completed the Net Ninja video tutorial and took notes**
- [ ] Explain what JavaScript is and its role in web development
- [ ] Embed JavaScript in HTML using `<script>` tags
- [ ] Use `console.log()` to output messages
- [ ] Open and use browser developer tools
- [ ] Create user interactions with `alert()` and `prompt()`
- [ ] Combine user input with output messages
- [ ] Debug basic JavaScript issues
- [ ] **Apply syntax patterns learned from the video tutorial**

---

## Additional Resources

**Essential Learning:**
- **MDN Web Docs**: [JavaScript First Steps](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/First_steps)

**Practice Platforms:**
- **Codecademy**: [Introduction to JavaScript (Introduction)](https://www.codecademy.com/learn/introduction-to-javascript)

**Developer Tools:**
- **Chrome DevTools**: [Console Overview](https://developer.chrome.com/docs/devtools/console/)
- **Firefox Developer Tools**: [Web Console](https://developer.mozilla.org/en-US/docs/Tools/Web_Console)

---

## Next Steps

Once you've completed the Net Ninja video tutorial, worked through the Simple Greeting App, and feel comfortable with basic JavaScript concepts, you're ready to move on to [Part 2: Variables and Basic Input/Output](2_variables-and-io.md) where you'll learn about modern variable declarations and working with different data types.