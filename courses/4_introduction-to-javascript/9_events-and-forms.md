# Part 9: Events and Forms - Real-World Interactions

## Event Handling Fundamentals

### Understanding Events

Events are actions that happen in the browser - user clicks, keyboard input, page loading, form submissions, and many others. Event handling is the foundation of interactive web applications, allowing your JavaScript code to respond to user actions and system changes.

#### Why Master Event Handling?
- **User Interaction**: Respond to clicks, touches, and keyboard input
- **Real-time Updates**: Create dynamic, responsive interfaces
- **Form Processing**: Handle user input and validation
- **Performance**: Optimize user experience with smooth interactions
- **Accessibility**: Support keyboard navigation and screen readers

### Event Types and Categories

#### Mouse Events
```javascript
const button = document.querySelector('#myButton');

// Basic mouse events
button.addEventListener('click', function(event) {
    console.log('Button clicked!');
});

button.addEventListener('dblclick', function(event) {
    console.log('Button double-clicked!');
});

button.addEventListener('mouseover', function(event) {
    console.log('Mouse entered element');
    event.target.style.backgroundColor = '#e0e0e0';
});

button.addEventListener('mouseout', function(event) {
    console.log('Mouse left element');
    event.target.style.backgroundColor = '';
});
```

#### Keyboard Events
```javascript
const input = document.querySelector('#textInput');

input.addEventListener('keydown', function(event) {
    console.log(`Key pressed: ${event.key}`);
    
    // Prevent default behavior for specific keys
    if (event.key === 'Enter' && event.ctrlKey) {
        event.preventDefault();
        console.log('Ctrl+Enter blocked');
    }
});

// Real-time input processing
input.addEventListener('input', function(event) {
    console.log(`Current value: ${event.target.value}`);
    
    // Example: Real-time validation
    if (event.target.value.length > 100) {
        event.target.style.borderColor = 'red';
    } else {
        event.target.style.borderColor = '';
    }
});
```

#### Form Events
```javascript
const form = document.querySelector('#myForm');

// Form submission
form.addEventListener('submit', function(event) {
    event.preventDefault(); // Prevent default form submission
    
    // Process form data
    const formData = new FormData(form);
    console.log('Form submitted:', Object.fromEntries(formData));
});

// Input focus and blur events
const nameInput = document.querySelector('#name');

nameInput.addEventListener('focus', function(event) {
    event.target.classList.add('focused');
});

nameInput.addEventListener('blur', function(event) {
    event.target.classList.remove('focused');
    validateField(event.target);
});

function validateField(field) {
    if (field.required && !field.value.trim()) {
        field.classList.add('error');
        return false;
    }
    field.classList.remove('error');
    return true;
}
```

### Event Object Properties
```javascript
function handleEvent(event) {
    console.log('Event details:');
    console.log('Type:', event.type);
    console.log('Target:', event.target);
    console.log('Timestamp:', event.timeStamp);
    
    // Mouse-specific properties
    if (event.type.startsWith('mouse')) {
        console.log('Click position:', event.clientX, event.clientY);
    }
    
    // Keyboard-specific properties
    if (event.type.startsWith('key')) {
        console.log('Key pressed:', event.key);
        console.log('Ctrl key:', event.ctrlKey);
    }
}
```

### Event Delegation
```javascript
// Efficient event handling for dynamic content
const todoList = document.querySelector('#todoList');

// Single event listener handles all todo items
todoList.addEventListener('click', function(event) {
    const target = event.target;
    const todoItem = target.closest('.todo-item');
    
    if (!todoItem) return;
    
    const todoId = todoItem.dataset.id;
    
    if (target.classList.contains('complete-btn')) {
        toggleTodoComplete(todoId);
    } else if (target.classList.contains('delete-btn')) {
        deleteTodo(todoId);
    }
});

function toggleTodoComplete(id) {
    const todoItem = document.querySelector(`[data-id="${id}"]`);
    todoItem.classList.toggle('completed');
}

function deleteTodo(id) {
    const todoItem = document.querySelector(`[data-id="${id}"]`);
    todoItem.remove();
}
```

---

## Form Validation Essentials

### Basic Validation Techniques
```javascript
function validateEmail(email) {
    const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
    return emailRegex.test(email);
}

function validatePassword(password) {
    return password.length >= 8 &&
           /[A-Z]/.test(password) &&
           /[a-z]/.test(password) &&
           /\d/.test(password);
}

function showError(field, message) {
    field.classList.add('error');
    
    // Remove existing error message
    const existingError = field.parentElement.querySelector('.error-message');
    if (existingError) {
        existingError.remove();
    }
    
    // Add new error message
    const errorElement = document.createElement('div');
    errorElement.className = 'error-message';
    errorElement.textContent = message;
    field.parentElement.appendChild(errorElement);
}

function clearError(field) {
    field.classList.remove('error');
    const errorMessage = field.parentElement.querySelector('.error-message');
    if (errorMessage) {
        errorMessage.remove();
    }
}
```

---

## Mini Project: Interactive Contact Form

Build a contact form with real-time validation and dynamic user feedback.

### Project Requirements:

1. **Form Fields:**
   - Name (required, minimum 2 characters)
   - Email (required, valid email format)
   - Message (required, maximum 500 characters)

2. **Interactive Features:**
   - Real-time validation as user types
   - Character counter for message field
   - Visual feedback (green for valid, red for invalid)
   - Form submission with success message

3. **User Experience:**
   - Clear error messages
   - Smooth visual transitions
   - Prevent submission of invalid forms

### Starter Code:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Interactive Contact Form</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        
        body {
            font-family: 'Arial', sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            padding: 20px;
            display: flex;
            align-items: center;
            justify-content: center;
        }
        
        .form-container {
            background: white;
            border-radius: 15px;
            padding: 40px;
            box-shadow: 0 20px 40px rgba(0,0,0,0.1);
            width: 100%;
            max-width: 500px;
        }
        
        h1 {
            text-align: center;
            color: #333;
            margin-bottom: 30px;
            font-size: 28px;
        }
        
        .form-group {
            margin-bottom: 25px;
            position: relative;
        }
        
        label {
            display: block;
            margin-bottom: 8px;
            font-weight: bold;
            color: #555;
        }
        
        input, textarea {
            width: 100%;
            padding: 12px 15px;
            border: 2px solid #ddd;
            border-radius: 8px;
            font-size: 16px;
            transition: border-color 0.3s, box-shadow 0.3s;
        }
        
        input:focus, textarea:focus {
            outline: none;
            border-color: #667eea;
            box-shadow: 0 0 0 3px rgba(102, 126, 234, 0.1);
        }
        
        .error {
            border-color: #e74c3c !important;
            box-shadow: 0 0 0 3px rgba(231, 76, 60, 0.1) !important;
        }
        
        .valid {
            border-color: #27ae60 !important;
            box-shadow: 0 0 0 3px rgba(39, 174, 96, 0.1) !important;
        }
        
        .error-message {
            color: #e74c3c;
            font-size: 14px;
            margin-top: 5px;
            display: block;
        }
        
        .char-counter {
            text-align: right;
            font-size: 14px;
            color: #666;
            margin-top: 5px;
        }
        
        .char-counter.warning {
            color: #f39c12;
        }
        
        .char-counter.danger {
            color: #e74c3c;
        }
        
        .submit-btn {
            width: 100%;
            padding: 15px;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            color: white;
            border: none;
            border-radius: 8px;
            font-size: 18px;
            font-weight: bold;
            cursor: pointer;
            transition: all 0.3s;
        }
        
        .submit-btn:hover:not(:disabled) {
            transform: translateY(-2px);
            box-shadow: 0 10px 20px rgba(0,0,0,0.2);
        }
        
        .submit-btn:disabled {
            background: #ccc;
            cursor: not-allowed;
            transform: none;
            box-shadow: none;
        }
        
        .success-message {
            background: #d4edda;
            color: #155724;
            padding: 15px;
            border-radius: 8px;
            text-align: center;
            margin-top: 20px;
            border: 1px solid #c3e6cb;
        }
        
        .hidden {
            display: none;
        }
    </style>
</head>
<body>
    <div class="form-container">
        <h1>📧 Contact Us</h1>
        
        <form id="contactForm">
            <div class="form-group">
                <label for="name">Full Name *</label>
                <input type="text" id="name" name="name" required>
            </div>
            
            <div class="form-group">
                <label for="email">Email Address *</label>
                <input type="email" id="email" name="email" required>
            </div>
            
            <div class="form-group">
                <label for="message">Message *</label>
                <textarea id="message" name="message" rows="6" maxlength="500" required></textarea>
                <div class="char-counter" id="charCounter">0/500 characters</div>
            </div>
            
            <button type="submit" class="submit-btn" id="submitBtn" disabled>Send Message</button>
        </form>
        
        <div class="success-message hidden" id="successMessage">
            Thank you! Your message has been sent successfully. ✅
        </div>
    </div>

    <script>
        // Get form elements
        const form = document.getElementById('contactForm');
        const nameInput = document.getElementById('name');
        const emailInput = document.getElementById('email');
        const messageInput = document.getElementById('message');
        const charCounter = document.getElementById('charCounter');
        const submitBtn = document.getElementById('submitBtn');
        const successMessage = document.getElementById('successMessage');
        
        // Validation functions
        function validateName(name) {
            // TODO: Check if name is at least 2 characters long
            // Return true if valid, false if invalid
        }
        
        function validateEmail(email) {
            // TODO: Check if email has valid format
            // Hint: use regular expression or simple check for @ and .
            const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
            // Return emailRegex.test(email);
        }
        
        function validateMessage(message) {
            // TODO: Check if message is not empty and within character limit
            // Return true if valid, false if invalid
        }
        
        // UI update functions
        function showError(field, message) {
            // TODO: Add error class to field and show error message
            // 1. Add 'error' class to field
            // 2. Remove any existing error message
            // 3. Create and append new error message element
        }
        
        function clearError(field) {
            // TODO: Remove error class and error message
            // 1. Remove 'error' class from field
            // 2. Remove error message element if it exists
        }
        
        function markValid(field) {
            // TODO: Add valid class to field (green border)
            // Remove error class and add 'valid' class
        }
        
        function updateCharCounter() {
            // TODO: Update character counter for message field
            // 1. Get current message length
            // 2. Update counter text (e.g., "150/500 characters")
            // 3. Add warning class if > 400 characters
            // 4. Add danger class if > 450 characters
        }
        
        function updateSubmitButton() {
            // TODO: Enable/disable submit button based on form validity
            // Check if all fields are valid, then enable/disable button
        }
        
        // Field validation functions
        function validateNameField() {
            const name = nameInput.value.trim();
            
            if (!name) {
                showError(nameInput, 'Name is required');
                return false;
            } else if (!validateName(name)) {
                showError(nameInput, 'Name must be at least 2 characters long');
                return false;
            } else {
                clearError(nameInput);
                markValid(nameInput);
                return true;
            }
        }
        
        function validateEmailField() {
            // TODO: Implement email field validation
            // Similar to validateNameField but for email
            // Check if empty, then check if valid email format
        }
        
        function validateMessageField() {
            // TODO: Implement message field validation
            // Check if empty and within character limit
        }
        
        // Event listeners
        function setupEventListeners() {
            // TODO: Add event listeners for all inputs
            // Add 'input' event listeners to all fields for real-time validation
            // Add 'blur' event listeners for validation when user leaves field
            // Add 'submit' event listener to form
            
            // Example for name field:
            // nameInput.addEventListener('input', function() {
            //     validateNameField();
            //     updateSubmitButton();
            // });
        }
        
        function handleFormSubmit(event) {
            // TODO: Handle form submission
            // 1. Prevent default form submission
            // 2. Validate all fields
            // 3. If valid, simulate sending (show success message)
            // 4. If invalid, focus first error field
        }
        
        // Initialize the form
        function init() {
            setupEventListeners();
            updateCharCounter();
            updateSubmitButton();
        }
        
        // Start the application
        init();
    </script>
</body>
</html>
```

### Implementation Steps:

1. **Start with validation functions:**
   - Implement `validateName()`, `validateEmail()`, and `validateMessage()`
   - Test these functions in the console with sample data

2. **Add UI feedback functions:**
   - Implement `showError()`, `clearError()`, and `markValid()`
   - Implement `updateCharCounter()` and `updateSubmitButton()`

3. **Create field validation functions:**
   - Complete `validateEmailField()` and `validateMessageField()`
   - These combine validation logic with UI updates

4. **Set up event handling:**
   - Implement `setupEventListeners()` to add all event handlers
   - Implement `handleFormSubmit()` for form submission

5. **Test and refine:**
   - Test with various inputs including edge cases
   - Ensure smooth user experience with real-time feedback

### Key Learning Points:

- **Event handling**: Responding to user input in real-time
- **Form validation**: Client-side validation for better UX
- **DOM manipulation**: Dynamically updating classes and content
- **User feedback**: Providing clear visual and textual feedback
- **Progressive enhancement**: Form works even without JavaScript

### Extension Ideas:

Once you complete the basic form, try adding:
- **Loading animation**: Show spinner during form submission
- **Field icons**: Add checkmarks for valid fields
- **Advanced validation**: Phone number formatting, password strength
- **Auto-save**: Save form data to localStorage as user types

---

## Common Event Handling Mistakes

### 1. Forgetting to Prevent Default
```javascript
// Wrong - form will submit and page will reload
form.addEventListener('submit', function(event) {
    validateForm();
});

// Correct - prevent default browser behavior
form.addEventListener('submit', function(event) {
    event.preventDefault();
    validateForm();
});
```

### 2. Not Using Event Delegation
```javascript
// Inefficient - adds listener to each button
document.querySelectorAll('.btn').forEach(btn => {
    btn.addEventListener('click', handleClick);
});

// Better - single listener handles all buttons
document.addEventListener('click', function(event) {
    if (event.target.classList.contains('btn')) {
        handleClick(event);
    }
});
```

### 3. Memory Leaks from Event Listeners
```javascript
// Problem - listeners not removed
function createWidget() {
    const widget = document.createElement('div');
    widget.addEventListener('click', expensiveFunction);
    document.body.appendChild(widget);
}

// Solution - remove listeners when done
function createWidget() {
    const widget = document.createElement('div');
    const clickHandler = () => expensiveFunction();
    widget.addEventListener('click', clickHandler);
    
    // Later, when removing widget
    widget.removeEventListener('click', clickHandler);
    widget.remove();
}
```

---

## Assessment Checklist

Before moving to the next part, ensure you can:
- [ ] Add event listeners to DOM elements
- [ ] Handle different types of events (click, input, submit, etc.)
- [ ] Access and use event object properties
- [ ] Prevent default browser behaviors when needed
- [ ] Validate form inputs with JavaScript
- [ ] Provide real-time user feedback
- [ ] Use event delegation for dynamic content
- [ ] Create smooth, interactive user experiences

---

## Additional Resources

**Essential Learning:**
- **MDN**: [Introduction to Events](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Building_blocks/Events)
- **MDN**: [Event Reference](https://developer.mozilla.org/en-US/docs/Web/Events)
- **JavaScript.info**: [Introduction to Browser Events](https://javascript.info/introduction-browser-events)

**Form Validation:**
- **MDN**: [Client-side Form Validation](https://developer.mozilla.org/en-US/docs/Learn/Forms/Form_validation)
- **MDN**: [HTML5 Constraint Validation](https://developer.mozilla.org/en-US/docs/Web/Guide/HTML/Constraint_validation)

**Advanced Topics:**
- **MDN**: [Event Delegation](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Building_blocks/Events#event_delegation)
- **JavaScript.info**: [Event Delegation](https://javascript.info/event-delegation)

---

## Next Steps

Once you've mastered events and forms and completed the contact form project, you're ready to move on to the next part where you'll learn about asynchronous JavaScript and working with APIs to create truly dynamic web applications.