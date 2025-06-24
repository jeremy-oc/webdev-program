# Part 7: DOM Manipulation - Making Pages Interactive

## DOM Fundamentals

### What Is the DOM?

The Document Object Model (DOM) is a programming interface that represents the structure of HTML documents as a tree of objects. It allows JavaScript to interact with and modify web pages dynamically, creating interactive user experiences.

#### Why Learn DOM Manipulation?
- **Interactivity**: Create responsive user interfaces
- **Dynamic Content**: Update page content without reloading
- **User Experience**: Respond to user actions instantly
- **Modern Web Development**: Foundation for frameworks and libraries
- **Real-world Applications**: Form validation, animations, dynamic layouts

### Understanding the DOM Tree

```html
<!DOCTYPE html>
<html>
<head>
    <title>Page Title</title>
</head>
<body>
    <h1 id="heading">Welcome</h1>
    <p class="intro">This is a paragraph.</p>
    <ul>
        <li>Item 1</li>
        <li>Item 2</li>
    </ul>
</body>
</html>
```

```javascript
// The DOM represents this as a tree structure:
// document
//   └── html
//       ├── head
//       │   └── title
//       │       └── "Page Title"
//       └── body
//           ├── h1 (id="heading")
//           │   └── "Welcome"
//           ├── p (class="intro")
//           │   └── "This is a paragraph."
//           └── ul
//               ├── li → "Item 1"
//               └── li → "Item 2"
```

### Selecting DOM Elements

#### Basic Selection Methods
```javascript
// Select by ID (returns single element or null)
const heading = document.getElementById('heading');
console.log(heading.textContent); // "Welcome"

// Select by class name (returns HTMLCollection)
const introElements = document.getElementsByClassName('intro');
console.log(introElements[0].textContent); // "This is a paragraph."

// Select by tag name (returns HTMLCollection)
const paragraphs = document.getElementsByTagName('p');
console.log(paragraphs.length); // Number of <p> elements
```

#### Modern Query Selectors (Preferred)
```javascript
// querySelector - returns first matching element
const heading = document.querySelector('#heading');
const firstParagraph = document.querySelector('p');
const introElement = document.querySelector('.intro');

// querySelectorAll - returns NodeList of all matching elements
const allParagraphs = document.querySelectorAll('p');
const listItems = document.querySelectorAll('ul li');

// Advanced CSS selectors
const firstListItem = document.querySelector('ul li:first-child');
const lastParagraph = document.querySelector('p:last-of-type');
const evenListItems = document.querySelectorAll('li:nth-child(even)');

// Attribute selectors
const requiredInputs = document.querySelectorAll('input[required]');
const externalLinks = document.querySelectorAll('a[href^="http"]');
```

#### Practical Selection Examples
```javascript
// Select elements for form validation
function validateForm() {
    const form = document.querySelector('#userForm');
    const requiredFields = form.querySelectorAll('input[required]');
    const emailField = form.querySelector('input[type="email"]');
    const submitButton = form.querySelector('button[type="submit"]');
    
    // Process each required field
    requiredFields.forEach(field => {
        if (!field.value.trim()) {
            markFieldAsError(field);
        }
    });
}

// Select elements for dynamic content
function updateNavigation() {
    const currentPage = window.location.pathname;
    const navLinks = document.querySelectorAll('nav a');
    
    navLinks.forEach(link => {
        if (link.getAttribute('href') === currentPage) {
            link.classList.add('active');
        }
    });
}
```

### Modifying Element Content

#### Text Content vs Inner HTML
```javascript
const element = document.querySelector('#content');

// textContent - safe, treats content as plain text
element.textContent = 'Hello <strong>World</strong>';
// Result: "Hello <strong>World</strong>" (HTML tags shown as text)

// innerHTML - can inject HTML (be careful with user input!)
element.innerHTML = 'Hello <strong>World</strong>';
// Result: "Hello World" (with "World" bolded)

// innerText - similar to textContent but respects styling
element.innerText = 'Visible text only';

// Safe HTML injection using template strings
const userName = 'Alice';
const userAge = 25;
element.innerHTML = `
    <h3>User Profile</h3>
    <p>Name: ${escapeHtml(userName)}</p>
    <p>Age: ${userAge}</p>
`;

// Helper function to escape HTML
function escapeHtml(text) {
    const div = document.createElement('div');
    div.textContent = text;
    return div.innerHTML;
}
```

#### Creating and Inserting Elements
```javascript
// Create new elements
const newParagraph = document.createElement('p');
newParagraph.textContent = 'This is a new paragraph';
newParagraph.className = 'dynamic-content';

// Create complex elements
const userCard = document.createElement('div');
userCard.className = 'user-card';
userCard.innerHTML = `
    <img src="avatar.jpg" alt="User Avatar" class="avatar">
    <h3 class="user-name">John Doe</h3>
    <p class="user-email">john@example.com</p>
`;

// Insert elements into the DOM
const container = document.querySelector('#container');

// Append to end
container.appendChild(newParagraph);

// Insert at beginning
container.insertBefore(userCard, container.firstChild);

// Modern insertion methods
container.append(newParagraph); // Can append text or multiple elements
container.prepend(userCard);    // Add to beginning
container.before(newElement);   // Insert before the container
container.after(newElement);    // Insert after the container

// Insert HTML strings
container.insertAdjacentHTML('beforebegin', '<p>Before container</p>');
container.insertAdjacentHTML('afterbegin', '<p>Start of container</p>');
container.insertAdjacentHTML('beforeend', '<p>End of container</p>');
container.insertAdjacentHTML('afterend', '<p>After container</p>');
```

### Modifying Element Attributes and Styles

#### Working with Attributes
```javascript
const image = document.querySelector('#profileImage');

// Get attributes
const src = image.getAttribute('src');
const alt = image.getAttribute('alt');

// Set attributes
image.setAttribute('src', 'new-image.jpg');
image.setAttribute('alt', 'New profile image');

// Remove attributes
image.removeAttribute('title');

// Check if attribute exists
if (image.hasAttribute('data-id')) {
    const id = image.getAttribute('data-id');
}

// Work with data attributes
image.dataset.userId = '12345';
image.dataset.profileType = 'premium';
console.log(image.dataset.userId); // '12345'

// Boolean attributes
const checkbox = document.querySelector('#terms');
checkbox.checked = true;
checkbox.disabled = false;
checkbox.required = true;
```

#### Styling Elements
```javascript
const element = document.querySelector('#dynamicElement');

// Direct style modification
element.style.color = 'blue';
element.style.backgroundColor = 'yellow';
element.style.fontSize = '20px';
element.style.padding = '10px';

// Multiple styles at once
element.style.cssText = 'color: blue; background: yellow; font-size: 20px;';

// Get computed styles
const computedStyle = window.getComputedStyle(element);
const currentColor = computedStyle.color;
const currentWidth = computedStyle.width;

// CSS custom properties (CSS variables)
element.style.setProperty('--theme-color', '#3498db');
const themeColor = element.style.getPropertyValue('--theme-color');
```

#### CSS Class Management
```javascript
const element = document.querySelector('.button');

// Add classes
element.classList.add('active');
element.classList.add('primary', 'large'); // Multiple classes

// Remove classes
element.classList.remove('inactive');
element.classList.remove('small', 'secondary');

// Toggle classes
element.classList.toggle('expanded'); // Add if not present, remove if present
element.classList.toggle('visible', true); // Force add
element.classList.toggle('hidden', false); // Force remove

// Check for classes
if (element.classList.contains('active')) {
    console.log('Element is active');
}

// Replace classes
element.classList.replace('old-class', 'new-class');

// Get all classes as array
const allClasses = Array.from(element.classList);
```

### Event Handling

#### Adding Event Listeners
```javascript
// Basic event listener
const button = document.querySelector('#myButton');
button.addEventListener('click', function() {
    console.log('Button clicked!');
});

// Arrow function syntax
button.addEventListener('click', () => {
    console.log('Button clicked with arrow function!');
});

// Named function (can be removed later)
function handleButtonClick(event) {
    console.log('Button clicked:', event.target);
}
button.addEventListener('click', handleButtonClick);

// Remove event listener
button.removeEventListener('click', handleButtonClick);

// Event listener with options
button.addEventListener('click', handleClick, {
    once: true,      // Run only once
    passive: true,   // Never calls preventDefault
    capture: true    // Capture phase instead of bubble phase
});
```

#### Common Event Types
```javascript
// Mouse events
element.addEventListener('click', handleClick);
element.addEventListener('dblclick', handleDoubleClick);
element.addEventListener('mousedown', handleMouseDown);
element.addEventListener('mouseup', handleMouseUp);
element.addEventListener('mouseover', handleMouseOver);
element.addEventListener('mouseout', handleMouseOut);
element.addEventListener('mousemove', handleMouseMove);

// Keyboard events
element.addEventListener('keydown', handleKeyDown);
element.addEventListener('keyup', handleKeyUp);
element.addEventListener('keypress', handleKeyPress);

// Form events
form.addEventListener('submit', handleSubmit);
input.addEventListener('change', handleChange);
input.addEventListener('input', handleInput); // Fires on every keystroke
input.addEventListener('focus', handleFocus);
input.addEventListener('blur', handleBlur);

// Window events
window.addEventListener('load', handlePageLoad);
window.addEventListener('resize', handleResize);
window.addEventListener('scroll', handleScroll);
window.addEventListener('beforeunload', handleBeforeUnload);
```

#### Event Object and Properties
```javascript
function handleEvent(event) {
    // Common event properties
    console.log('Event type:', event.type);
    console.log('Target element:', event.target);
    console.log('Current target:', event.currentTarget);
    console.log('Timestamp:', event.timeStamp);
    
    // Mouse event properties
    if (event.type === 'click') {
        console.log('Mouse position:', event.clientX, event.clientY);
        console.log('Button pressed:', event.button);
        console.log('Shift key held:', event.shiftKey);
        console.log('Ctrl key held:', event.ctrlKey);
    }
    
    // Keyboard event properties
    if (event.type === 'keydown') {
        console.log('Key pressed:', event.key);
        console.log('Key code:', event.keyCode);
        console.log('Alt key held:', event.altKey);
    }
    
    // Prevent default behavior
    event.preventDefault();
    
    // Stop event from bubbling
    event.stopPropagation();
}
```

### Advanced DOM Manipulation

#### Element Traversal
```javascript
const element = document.querySelector('#middleItem');

// Parent navigation
const parent = element.parentElement;
const parentNode = element.parentNode;

// Sibling navigation
const nextSibling = element.nextElementSibling;
const prevSibling = element.previousElementSibling;
const nextNode = element.nextSibling; // Includes text nodes
const prevNode = element.previousSibling;

// Children navigation
const children = element.children; // HTMLCollection of element children
const childNodes = element.childNodes; // NodeList including text nodes
const firstChild = element.firstElementChild;
const lastChild = element.lastElementChild;

// Find closest ancestor matching selector
const closestSection = element.closest('section');
const closestWithClass = element.closest('.container');

// Check if element contains another
const container = document.querySelector('#container');
const isChild = container.contains(element);
```

#### Document Fragments for Performance
```javascript
// Efficient DOM manipulation with fragments
function addManyElements(container, items) {
    // Create document fragment
    const fragment = document.createDocumentFragment();
    
    // Add elements to fragment (no DOM reflow yet)
    items.forEach(item => {
        const element = document.createElement('div');
        element.textContent = item.name;
        element.className = 'item';
        fragment.appendChild(element);
    });
    
    // Single DOM operation
    container.appendChild(fragment);
}

// Template-based creation
function createElementFromTemplate(templateId, data) {
    const template = document.querySelector(templateId);
    const clone = template.content.cloneNode(true);
    
    // Populate template with data
    clone.querySelector('.name').textContent = data.name;
    clone.querySelector('.email').textContent = data.email;
    clone.querySelector('.avatar').src = data.avatar;
    
    return clone;
}
```

---

## Mini Project: Interactive To-Do List

Build a functional to-do list that demonstrates essential DOM manipulation concepts.

### Project Requirements:

1. **Core Functionality:**
   - Add new tasks to the list
   - Mark tasks as complete/incomplete
   - Delete individual tasks
   - Clear all completed tasks

2. **Interactive Features:**
   - Click to toggle task completion
   - Double-click to edit task text
   - Keyboard shortcuts (Enter to add, Escape to cancel)
   - Visual feedback for user actions

3. **Dynamic Styling:**
   - Different styles for completed vs pending tasks
   - Hover effects and transitions
   - Progress indicator showing completion percentage

### Starter Code:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Interactive To-Do List</title>
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
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 20px;
        }
        
        .todo-container {
            background: white;
            border-radius: 15px;
            padding: 30px;
            box-shadow: 0 15px 35px rgba(0,0,0,0.1);
            width: 100%;
            max-width: 500px;
        }
        
        .header {
            text-align: center;
            margin-bottom: 30px;
        }
        
        .header h1 {
            color: #333;
            margin-bottom: 10px;
        }
        
        .progress-bar {
            width: 100%;
            height: 8px;
            background: #e0e0e0;
            border-radius: 4px;
            overflow: hidden;
            margin-bottom: 20px;
        }
        
        .progress-fill {
            height: 100%;
            background: linear-gradient(90deg, #667eea, #764ba2);
            width: 0%;
            transition: width 0.3s ease;
        }
        
        .input-section {
            display: flex;
            gap: 10px;
            margin-bottom: 20px;
        }
        
        #taskInput {
            flex: 1;
            padding: 12px 15px;
            border: 2px solid #e0e0e0;
            border-radius: 8px;
            font-size: 16px;
            outline: none;
            transition: border-color 0.3s ease;
        }
        
        #taskInput:focus {
            border-color: #667eea;
        }
        
        #addButton {
            padding: 12px 20px;
            background: linear-gradient(45deg, #667eea, #764ba2);
            color: white;
            border: none;
            border-radius: 8px;
            cursor: pointer;
            font-weight: bold;
            transition: transform 0.2s ease;
        }
        
        #addButton:hover {
            transform: translateY(-2px);
        }
        
        .task-list {
            list-style: none;
            margin-bottom: 20px;
        }
        
        .task-item {
            display: flex;
            align-items: center;
            padding: 15px;
            margin: 8px 0;
            background: #f8f9fa;
            border-radius: 8px;
            border-left: 4px solid #667eea;
            transition: all 0.3s ease;
            cursor: pointer;
        }
        
        .task-item:hover {
            background: #e9ecef;
            transform: translateX(5px);
        }
        
        .task-item.completed {
            background: #d4edda;
            border-left-color: #28a745;
            opacity: 0.8;
        }
        
        .task-checkbox {
            width: 20px;
            height: 20px;
            border: 2px solid #ddd;
            border-radius: 4px;
            margin-right: 15px;
            display: flex;
            align-items: center;
            justify-content: center;
            cursor: pointer;
            transition: all 0.3s ease;
        }
        
        .task-checkbox.checked {
            background: #28a745;
            border-color: #28a745;
            color: white;
        }
        
        .task-text {
            flex: 1;
            font-size: 16px;
            transition: all 0.3s ease;
        }
        
        .task-item.completed .task-text {
            text-decoration: line-through;
            color: #6c757d;
        }
        
        .task-actions {
            display: flex;
            gap: 8px;
            opacity: 0;
            transition: opacity 0.3s ease;
        }
        
        .task-item:hover .task-actions {
            opacity: 1;
        }
        
        .action-btn {
            width: 30px;
            height: 30px;
            border: none;
            border-radius: 4px;
            cursor: pointer;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 14px;
            transition: all 0.2s ease;
        }
        
        .edit-btn {
            background: #ffc107;
            color: white;
        }
        
        .edit-btn:hover {
            background: #e0a800;
        }
        
        .delete-btn {
            background: #dc3545;
            color: white;
        }
        
        .delete-btn:hover {
            background: #c82333;
        }
        
        .footer-actions {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding-top: 20px;
            border-top: 2px solid #e0e0e0;
        }
        
        .task-counter {
            color: #6c757d;
            font-size: 14px;
        }
        
        #clearCompleted {
            padding: 8px 16px;
            background: #dc3545;
            color: white;
            border: none;
            border-radius: 6px;
            cursor: pointer;
            font-size: 14px;
            transition: all 0.2s ease;
        }
        
        #clearCompleted:hover {
            background: #c82333;
        }
        
        .empty-state {
            text-align: center;
            padding: 40px 20px;
            color: #6c757d;
        }
        
        .hidden {
            display: none;
        }
    </style>
</head>
<body>
    <div class="todo-container">
        <div class="header">
            <h1>📝 To-Do List</h1>
            <div class="progress-bar">
                <div class="progress-fill" id="progressFill"></div>
            </div>
        </div>
        
        <div class="input-section">
            <input type="text" id="taskInput" placeholder="Add a new task...">
            <button id="addButton">Add Task</button>
        </div>
        
        <ul class="task-list" id="taskList">
            <!-- Tasks will be added here dynamically -->
        </ul>
        
        <div class="empty-state" id="emptyState">
            <p>No tasks yet. Add one above to get started! ✨</p>
        </div>
        
        <div class="footer-actions">
            <div class="task-counter">
                <span id="taskCounter">0 tasks remaining</span>
            </div>
            <button id="clearCompleted" class="hidden">Clear Completed</button>
        </div>
    </div>

    <script>
        // Global variables to track tasks
        let tasks = [];
        let taskIdCounter = 1;
        
        // DOM element references
        const taskInput = document.getElementById('taskInput');
        const addButton = document.getElementById('addButton');
        const taskList = document.getElementById('taskList');
        const emptyState = document.getElementById('emptyState');
        const taskCounter = document.getElementById('taskCounter');
        const clearCompleted = document.getElementById('clearCompleted');
        const progressFill = document.getElementById('progressFill');
        
        // Initialize the application
        function initializeApp() {
            // TODO: Set up event listeners
            // TODO: Update display
        }
        
        // Create a new task object
        function createTask(text) {
            // TODO: Return task object with id, text, completed properties
        }
        
        // Add a new task
        function addTask() {
            // TODO: Get input value, validate, create task, add to array, update display
        }
        
        // Toggle task completion
        function toggleTask(taskId) {
            // TODO: Find task by id, toggle completed status, update display
        }
        
        // Delete a task
        function deleteTask(taskId) {
            // TODO: Remove task from array, update display
        }
        
        // Edit task text
        function editTask(taskId, newText) {
            // TODO: Find task by id, update text, update display
        }
        
        // Clear all completed tasks
        function clearCompletedTasks() {
            // TODO: Filter out completed tasks, update display
        }
        
        // Create HTML for a single task
        function createTaskElement(task) {
            // TODO: Create li element with task content and controls
            // Include checkbox, text, edit button, delete button
            // Add appropriate event listeners
        }
        
        // Update the task list display
        function updateTaskList() {
            // TODO: Clear current list, create elements for each task, handle empty state
        }
        
        // Update task counter
        function updateTaskCounter() {
            // TODO: Count remaining tasks, update counter text
        }
        
        // Update progress bar
        function updateProgressBar() {
            // TODO: Calculate completion percentage, update progress bar width
        }
        
        // Update clear completed button visibility
        function updateClearButton() {
            // TODO: Show/hide clear button based on completed tasks
        }
        
        // Handle keyboard events
        function handleKeydown(event) {
            // TODO: Handle Enter key for adding tasks, Escape for canceling edits
        }
        
        // Handle edit mode for tasks
        function enterEditMode(taskElement, taskId) {
            // TODO: Convert task text to input field, handle save/cancel
        }
        
        // Validate task input
        function isValidTaskText(text) {
            // TODO: Check if text is not empty and not just whitespace
        }
        
        // Update all displays
        function updateDisplay() {
            updateTaskList();
            updateTaskCounter();
            updateProgressBar();
            updateClearButton();
        }
        
        // Initialize the app when page loads
        document.addEventListener('DOMContentLoaded', initializeApp);
    </script>
</body>
</html>
```

### Implementation Steps:

1. **Start with basic functionality:**
   - Implement `createTask()`, `addTask()`, and `updateTaskList()`
   - Get the basic add/display cycle working

2. **Add task management:**
   - Implement `toggleTask()`, `deleteTask()`, and `clearCompletedTasks()`
   - Connect these to the UI controls

3. **Create dynamic elements:**
   - Implement `createTaskElement()` to generate task HTML
   - Add event listeners for task interactions

4. **Add visual feedback:**
   - Implement progress bar, task counter, and empty state
   - Update these displays when tasks change

5. **Enhance with editing:**
   - Implement `editTask()` and `enterEditMode()`
   - Add double-click to edit functionality

6. **Polish the experience:**
   - Add keyboard shortcuts and validation
   - Test all interactions and edge cases

### Key Learning Points:

- **Element Selection**: Using `getElementById()` and `querySelector()`
- **Event Handling**: Multiple event types and event delegation
- **DOM Manipulation**: Creating, modifying, and removing elements
- **CSS Class Management**: Using `classList` for visual states
- **Form Handling**: Input validation and keyboard events
- **Dynamic Content**: Updating displays based on data changes

### Extension Ideas:

Once you complete the basic to-do list, try adding:
- **Local Storage**: Persist tasks between browser sessions
- **Drag and Drop**: Reorder tasks by dragging
- **Categories**: Group tasks into different categories
- **Due Dates**: Add deadlines and sorting by date
- **Search/Filter**: Find specific tasks or filter by status

---

## Common DOM Mistakes and Solutions

### 1. Forgetting to Check if Elements Exist
```javascript
// Wrong - might cause errors
const element = document.getElementById('nonexistent');
element.style.color = 'red'; // Error if element is null

// Correct - check first
const element = document.getElementById('myElement');
if (element) {
    element.style.color = 'red';
}
```

### 2. Adding Event Listeners in Loops Incorrectly
```javascript
// Wrong - all buttons will show the last value
for (let i = 0; i < buttons.length; i++) {
    buttons[i].addEventListener('click', function() {
        alert(i); // Always shows buttons.length
    });
}

// Correct - use closure or dataset
for (let i = 0; i < buttons.length; i++) {
    buttons[i].addEventListener('click', function() {
        alert(i); // Shows correct index
    });
}
```

### 3. Not Preventing Default Form Behavior
```javascript
// Wrong - form will submit and page will reload
form.addEventListener('submit', function(event) {
    processForm();
});

// Correct - prevent default behavior
form.addEventListener('submit', function(event) {
    event.preventDefault();
    processForm();
});
```

### 4. Modifying the DOM During Iteration
```javascript
// Wrong - can skip elements or cause errors
const items = document.querySelectorAll('.item');
items.forEach(item => {
    if (item.classList.contains('remove')) {
        item.remove(); // Modifying DOM during iteration
    }
});

// Correct - iterate backwards or collect first
const itemsToRemove = [...document.querySelectorAll('.item.remove')];
itemsToRemove.forEach(item => item.remove());
```

### 5. Memory Leaks with Event Listeners
```javascript
// Wrong - event listeners not removed
function createButton() {
    const button = document.createElement('button');
    button.addEventListener('click', handleClick);
    document.body.appendChild(button);
    // If button is removed later, event listener still exists
}

// Correct - remove event listeners when elements are removed
function removeButton(button) {
    button.removeEventListener('click', handleClick);
    button.remove();
}
```

---

## Assessment Checklist

Before moving to the next section, ensure you can:
- [ ] Select elements using various DOM methods effectively
- [ ] Modify element content, attributes, and styles dynamically
- [ ] Create and insert new elements into the DOM
- [ ] Handle different types of events and understand event objects
- [ ] Manage CSS classes for interactive visual states
- [ ] Validate user input and handle errors gracefully
- [ ] Navigate the DOM tree using parent/child/sibling relationships
- [ ] Build complete interactive applications with multiple features
- [ ] Debug DOM-related issues using browser developer tools
- [ ] Optimize DOM manipulation for performance

---

## Additional Resources

**Essential Learning:**
- **MDN**: [DOM Introduction](https://developer.mozilla.org/en-US/docs/Web/API/Document_Object_Model/Introduction)
- **MDN**: [Document Object](https://developer.mozilla.org/en-US/docs/Web/API/Document)
- **JavaScript.info**: [Document](https://javascript.info/document)

**Practice Platforms:**
- **freeCodeCamp**: [DOM Manipulation](https://www.freecodecamp.org/learn/)
- **JavaScript30**: [30 Day Vanilla JS Coding Challenge](https://javascript30.com/)

**Advanced Topics:**
- **MDN**: [Event Handling](https://developer.mozilla.org/en-US/docs/Web/Guide/Events)
- **JavaScript.info**: [Browser Events](https://javascript.info/events)
- **MDN**: [Performance and DOM](https://developer.mozilla.org/en-US/docs/Web/Performance)

---

## Next Steps

Once you've mastered DOM manipulation and completed the to-do list project, you're ready to move on to [Part 8: Objects](8_objects.md) where you'll learn to organize data and behavior using object-oriented programming concepts.