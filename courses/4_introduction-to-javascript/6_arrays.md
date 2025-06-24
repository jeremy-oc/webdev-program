# Part 6: Arrays and Array Methods

## Array Fundamentals

### What Are Arrays?

Arrays are ordered collections of data that allow you to store multiple values in a single variable. They're one of the most important data structures in JavaScript, essential for managing lists, collections, and sequences of information.

#### Why Use Arrays?
- **Organization**: Store related data together
- **Efficiency**: Process multiple items with loops
- **Flexibility**: Dynamic sizing and diverse data types
- **Functionality**: Rich set of built-in methods
- **Real-world applications**: Shopping lists, user data, game scores, etc.

### Creating and Accessing Arrays

#### Array Creation Methods
```javascript
// Array literal syntax (preferred)
const fruits = ['apple', 'banana', 'orange'];
const numbers = [1, 2, 3, 4, 5];
const mixed = ['hello', 42, true, null];

// Array constructor
const emptyArray = new Array();
const sizedArray = new Array(5); // Creates array with 5 empty slots
const constructorArray = new Array('a', 'b', 'c');

// Creating arrays with different data types
const shoppingList = [
    'milk',
    'bread', 
    'eggs',
    'cheese'
];

const userScores = [95, 87, 92, 78, 88];
const booleanFlags = [true, false, true, true];
```

#### Accessing Array Elements
```javascript
const colors = ['red', 'green', 'blue', 'yellow'];

// Access by index (zero-based)
console.log(colors[0]);    // 'red'
console.log(colors[1]);    // 'green'
console.log(colors[3]);    // 'yellow'

// Access last element
console.log(colors[colors.length - 1]); // 'yellow'

// Check if index exists
if (colors[10] !== undefined) {
    console.log(colors[10]);
} else {
    console.log('Index 10 does not exist');
}

// Safe access with optional chaining (modern approach)
console.log(colors[10] ?? 'Default value');
```

### Array Properties and Basic Operations

#### Length Property
```javascript
const items = ['a', 'b', 'c', 'd'];

console.log(items.length); // 4

// Dynamically change array size
items.length = 2;
console.log(items); // ['a', 'b']

items.length = 5;
console.log(items); // ['a', 'b', undefined, undefined, undefined]

// Check if array is empty
if (items.length === 0) {
    console.log('Array is empty');
}
```

#### Adding and Removing Elements
```javascript
const animals = ['cat', 'dog'];

// Add to end
animals.push('bird');           // ['cat', 'dog', 'bird']
animals.push('fish', 'rabbit'); // ['cat', 'dog', 'bird', 'fish', 'rabbit']

// Add to beginning
animals.unshift('hamster');     // ['hamster', 'cat', 'dog', 'bird', 'fish', 'rabbit']

// Remove from end
const lastAnimal = animals.pop(); // 'rabbit'
console.log(animals); // ['hamster', 'cat', 'dog', 'bird', 'fish']

// Remove from beginning
const firstAnimal = animals.shift(); // 'hamster'
console.log(animals); // ['cat', 'dog', 'bird', 'fish']

// Remove/add at specific index
animals.splice(1, 1, 'elephant'); // Remove 1 element at index 1, add 'elephant'
console.log(animals); // ['cat', 'elephant', 'bird', 'fish']
```

### Essential Array Methods

#### Finding Elements
```javascript
const students = ['Alice', 'Bob', 'Charlie', 'Diana', 'Bob'];

// Check if element exists
console.log(students.includes('Alice'));  // true
console.log(students.includes('Eve'));    // false

// Find index of element
console.log(students.indexOf('Bob'));     // 1 (first occurrence)
console.log(students.lastIndexOf('Bob')); // 4 (last occurrence)
console.log(students.indexOf('Eve'));     // -1 (not found)

// Find element by condition
const grades = [85, 92, 78, 96, 89];
const firstHighGrade = grades.find(grade => grade > 90);
console.log(firstHighGrade); // 92

const highGradeIndex = grades.findIndex(grade => grade > 90);
console.log(highGradeIndex); // 1
```

#### Transforming Arrays
```javascript
const numbers = [1, 2, 3, 4, 5];

// Create new array with transformed elements
const doubled = numbers.map(num => num * 2);
console.log(doubled); // [2, 4, 6, 8, 10]

// Filter elements by condition
const evenNumbers = numbers.filter(num => num % 2 === 0);
console.log(evenNumbers); // [2, 4]

// Combine multiple operations
const processedNumbers = numbers
    .filter(num => num > 2)       // [3, 4, 5]
    .map(num => num * 10)         // [30, 40, 50]
    .filter(num => num < 45);     // [30, 40]

console.log(processedNumbers); // [30, 40]
```

#### Array Iteration
```javascript
const fruits = ['apple', 'banana', 'orange'];

// forEach - execute function for each element
fruits.forEach((fruit, index) => {
    console.log(`${index}: ${fruit}`);
});

// for...of loop (modern approach)
for (const fruit of fruits) {
    console.log(fruit);
}

// for...in loop (gets indices)
for (const index in fruits) {
    console.log(`${index}: ${fruits[index]}`);
}

// Traditional for loop
for (let i = 0; i < fruits.length; i++) {
    console.log(`${i}: ${fruits[i]}`);
}
```

#### Reducing Arrays
```javascript
const prices = [10.99, 5.50, 23.75, 8.25];

// Sum all prices
const total = prices.reduce((sum, price) => sum + price, 0);
console.log(total); // 48.49

// Find maximum value
const maxPrice = prices.reduce((max, price) => price > max ? price : max);
console.log(maxPrice); // 23.75

// Count occurrences
const letters = ['a', 'b', 'a', 'c', 'b', 'a'];
const letterCount = letters.reduce((count, letter) => {
    count[letter] = (count[letter] || 0) + 1;
    return count;
}, {});
console.log(letterCount); // {a: 3, b: 2, c: 1}
```

### Advanced Array Operations

#### Combining Arrays
```javascript
const arr1 = [1, 2, 3];
const arr2 = [4, 5, 6];
const arr3 = [7, 8, 9];

// Concatenate arrays
const combined = arr1.concat(arr2, arr3);
console.log(combined); // [1, 2, 3, 4, 5, 6, 7, 8, 9]

// Spread operator (modern approach)
const spreadCombined = [...arr1, ...arr2, ...arr3];
console.log(spreadCombined); // [1, 2, 3, 4, 5, 6, 7, 8, 9]

// Join array elements into string
const words = ['Hello', 'world', 'from', 'JavaScript'];
const sentence = words.join(' ');
console.log(sentence); // 'Hello world from JavaScript'
```

#### Sorting and Reversing
```javascript
const names = ['Charlie', 'Alice', 'Bob', 'Diana'];
const scores = [85, 92, 78, 96, 89];

// Sort alphabetically (modifies original array)
names.sort();
console.log(names); // ['Alice', 'Bob', 'Charlie', 'Diana']

// Sort numbers (need custom compare function)
scores.sort((a, b) => a - b); // Ascending
console.log(scores); // [78, 85, 89, 92, 96]

scores.sort((a, b) => b - a); // Descending
console.log(scores); // [96, 92, 89, 85, 78]

// Reverse array
names.reverse();
console.log(names); // ['Diana', 'Charlie', 'Bob', 'Alice']

// Non-destructive sorting
const originalNumbers = [3, 1, 4, 1, 5, 9];
const sortedNumbers = [...originalNumbers].sort((a, b) => a - b);
console.log(originalNumbers); // [3, 1, 4, 1, 5, 9] (unchanged)
console.log(sortedNumbers);   // [1, 1, 3, 4, 5, 9]
```

#### Array Slicing and Splicing
```javascript
const alphabet = ['a', 'b', 'c', 'd', 'e', 'f', 'g'];

// slice() - extract portion without modifying original
const portion = alphabet.slice(2, 5); // From index 2 to 5 (exclusive)
console.log(portion); // ['c', 'd', 'e']
console.log(alphabet); // ['a', 'b', 'c', 'd', 'e', 'f', 'g'] (unchanged)

// splice() - modify original array
const removed = alphabet.splice(2, 3, 'X', 'Y'); // Remove 3 elements at index 2, add 'X', 'Y'
console.log(removed); // ['c', 'd', 'e']
console.log(alphabet); // ['a', 'b', 'X', 'Y', 'f', 'g']
```

---

## Mini Project: Simple Task Manager

Build a task management application that demonstrates essential array methods and operations.

### Project Goals:
- Practice array creation, manipulation, and iteration
- Use array methods like `push()`, `splice()`, `filter()`, `map()`, and `find()`
- Implement search and filtering functionality
- Apply sorting and data transformation techniques

### Features to Implement:
1. **Add Tasks**: Create new tasks with descriptions and priorities
2. **Complete Tasks**: Mark tasks as completed/incomplete
3. **Delete Tasks**: Remove tasks from the list
4. **Filter Tasks**: Show all, active, or completed tasks
5. **Search Tasks**: Find tasks by description
6. **Sort Tasks**: Order by priority or completion status
7. **Statistics**: Display task counts and completion percentage

### Starter Code:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Simple Task Manager</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            padding: 20px;
        }
        
        .container {
            max-width: 800px;
            margin: 0 auto;
            background: white;
            border-radius: 15px;
            padding: 30px;
            box-shadow: 0 10px 30px rgba(0,0,0,0.2);
        }
        
        h1 {
            text-align: center;
            color: #333;
            margin-bottom: 30px;
        }
        
        .add-task {
            display: flex;
            gap: 10px;
            margin-bottom: 30px;
        }
        
        .add-task input, .add-task select, .add-task button {
            padding: 12px 15px;
            border: 2px solid #e0e0e0;
            border-radius: 8px;
            font-size: 14px;
        }
        
        .add-task input {
            flex: 1;
        }
        
        .add-task button {
            background: linear-gradient(45deg, #667eea, #764ba2);
            color: white;
            border: none;
            cursor: pointer;
            font-weight: bold;
        }
        
        .add-task button:hover {
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(0,0,0,0.2);
        }
        
        .controls {
            display: flex;
            gap: 15px;
            margin-bottom: 20px;
            flex-wrap: wrap;
            align-items: center;
        }
        
        .filter-btn {
            padding: 8px 16px;
            border: 1px solid #ddd;
            background: #f8f9fa;
            border-radius: 20px;
            cursor: pointer;
            transition: all 0.3s;
        }
        
        .filter-btn.active {
            background: linear-gradient(45deg, #667eea, #764ba2);
            color: white;
            border-color: transparent;
        }
        
        .search-box {
            flex: 1;
            min-width: 200px;
            padding: 8px 15px;
            border: 1px solid #ddd;
            border-radius: 20px;
        }
        
        .task-list {
            background: #f8f9fa;
            border-radius: 10px;
            padding: 20px;
            min-height: 200px;
        }
        
        .task-item {
            background: white;
            border-radius: 8px;
            padding: 15px;
            margin-bottom: 10px;
            display: flex;
            align-items: center;
            gap: 15px;
            box-shadow: 0 2px 5px rgba(0,0,0,0.1);
            transition: all 0.3s;
        }
        
        .task-item:hover {
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(0,0,0,0.15);
        }
        
        .task-item.completed {
            opacity: 0.7;
            background: #e8f5e8;
        }
        
        .task-checkbox {
            width: 20px;
            height: 20px;
            cursor: pointer;
        }
        
        .task-content {
            flex: 1;
        }
        
        .task-text {
            font-size: 16px;
            margin-bottom: 5px;
        }
        
        .task-item.completed .task-text {
            text-decoration: line-through;
            color: #666;
        }
        
        .task-priority {
            display: inline-block;
            padding: 2px 8px;
            border-radius: 12px;
            font-size: 12px;
            font-weight: bold;
        }
        
        .priority-high {
            background: #ffebee;
            color: #c62828;
        }
        
        .priority-medium {
            background: #fff3e0;
            color: #ef6c00;
        }
        
        .priority-low {
            background: #e8f5e8;
            color: #2e7d32;
        }
        
        .task-actions {
            display: flex;
            gap: 5px;
        }
        
        .delete-btn {
            background: #dc3545;
            color: white;
            border: none;
            padding: 5px 10px;
            border-radius: 4px;
            cursor: pointer;
            font-size: 12px;
        }
        
        .delete-btn:hover {
            background: #c82333;
        }
        
        .stats {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
            gap: 15px;
            margin-top: 30px;
        }
        
        .stat-card {
            background: linear-gradient(45deg, #28a745, #20c997);
            color: white;
            padding: 20px;
            border-radius: 10px;
            text-align: center;
        }
        
        .stat-number {
            font-size: 2rem;
            font-weight: bold;
            display: block;
        }
        
        .stat-label {
            font-size: 0.9rem;
            opacity: 0.9;
        }
        
        .empty-state {
            text-align: center;
            padding: 40px;
            color: #666;
        }
        
        .empty-state h3 {
            margin-bottom: 10px;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>📝 Simple Task Manager</h1>
        
        <div class="add-task">
            <input type="text" id="taskInput" placeholder="Enter a new task..." maxlength="100">
            <select id="prioritySelect">
                <option value="low">Low Priority</option>
                <option value="medium" selected>Medium Priority</option>
                <option value="high">High Priority</option>
            </select>
            <button onclick="addTask()">Add Task</button>
        </div>
        
        <div class="controls">
            <button class="filter-btn active" onclick="filterTasks('all')">All</button>
            <button class="filter-btn" onclick="filterTasks('active')">Active</button>
            <button class="filter-btn" onclick="filterTasks('completed')">Completed</button>
            <input type="text" class="search-box" id="searchInput" placeholder="Search tasks..." oninput="searchTasks()">
            <select id="sortSelect" onchange="sortTasks()">
                <option value="date">Sort by Date</option>
                <option value="priority">Sort by Priority</option>
                <option value="alphabetical">Sort A-Z</option>
            </select>
        </div>
        
        <div class="task-list" id="taskList">
            <div class="empty-state">
                <h3>No tasks yet!</h3>
                <p>Add your first task above to get started.</p>
            </div>
        </div>
        
        <div class="stats">
            <div class="stat-card">
                <span class="stat-number" id="totalTasks">0</span>
                <span class="stat-label">Total Tasks</span>
            </div>
            <div class="stat-card">
                <span class="stat-number" id="completedTasks">0</span>
                <span class="stat-label">Completed</span>
            </div>
            <div class="stat-card">
                <span class="stat-number" id="activeTasks">0</span>
                <span class="stat-label">Active</span>
            </div>
            <div class="stat-card">
                <span class="stat-number" id="completionRate">0%</span>
                <span class="stat-label">Completion Rate</span>
            </div>
        </div>
    </div>

    <script>
        // Task array to store all tasks
        let tasks = [];
        let currentFilter = 'all';
        let taskIdCounter = 1;

        // Function to add a new task
        function addTask() {
            const taskInput = document.getElementById('taskInput');
            const prioritySelect = document.getElementById('prioritySelect');
            
            const taskText = taskInput.value.trim();
            if (!taskText) {
                alert('Please enter a task description');
                return;
            }
            
            // Create new task object
            const newTask = {
                id: taskIdCounter++,
                text: taskText,
                priority: prioritySelect.value,
                completed: false,
                dateAdded: new Date()
            };
            
            // Add to tasks array using push()
            tasks.push(newTask);
            
            // Clear input
            taskInput.value = '';
            
            // Update display
            renderTasks();
            updateStats();
        }

        // Function to toggle task completion
        function toggleTask(taskId) {
            // Find task using find() method
            const task = tasks.find(task => task.id === taskId);
            if (task) {
                task.completed = !task.completed;
                renderTasks();
                updateStats();
            }
        }

        // Function to delete a task
        function deleteTask(taskId) {
            // Remove task using filter() method
            tasks = tasks.filter(task => task.id !== taskId);
            renderTasks();
            updateStats();
        }

        // Function to filter tasks
        function filterTasks(filter) {
            currentFilter = filter;
            
            // Update active filter button
            document.querySelectorAll('.filter-btn').forEach(btn => {
                btn.classList.remove('active');
            });
            event.target.classList.add('active');
            
            renderTasks();
        }

        // Function to search tasks
        function searchTasks() {
            renderTasks();
        }

        // Function to sort tasks
        function sortTasks() {
            renderTasks();
        }

        // Function to render tasks on screen
        function renderTasks() {
            const taskList = document.getElementById('taskList');
            const searchTerm = document.getElementById('searchInput').value.toLowerCase();
            const sortBy = document.getElementById('sortSelect').value;
            
            // Filter tasks based on current filter and search
            let filteredTasks = tasks.filter(task => {
                // Apply filter
                const matchesFilter = currentFilter === 'all' || 
                                    (currentFilter === 'active' && !task.completed) || 
                                    (currentFilter === 'completed' && task.completed);
                
                // Apply search
                const matchesSearch = task.text.toLowerCase().includes(searchTerm);
                
                return matchesFilter && matchesSearch;
            });
            
            // Sort tasks
            filteredTasks.sort((a, b) => {
                switch(sortBy) {
                    case 'priority':
                        const priorityOrder = { high: 3, medium: 2, low: 1 };
                        return priorityOrder[b.priority] - priorityOrder[a.priority];
                    case 'alphabetical':
                        return a.text.localeCompare(b.text);
                    case 'date':
                    default:
                        return new Date(b.dateAdded) - new Date(a.dateAdded);
                }
            });
            
            // Render tasks
            if (filteredTasks.length === 0) {
                taskList.innerHTML = `
                    <div class="empty-state">
                        <h3>No tasks found</h3>
                        <p>Try adjusting your filters or add a new task.</p>
                    </div>
                `;
            } else {
                taskList.innerHTML = filteredTasks.map(task => `
                    <div class="task-item ${task.completed ? 'completed' : ''}">
                        <input type="checkbox" class="task-checkbox" 
                               ${task.completed ? 'checked' : ''} 
                               onchange="toggleTask(${task.id})">
                        <div class="task-content">
                            <div class="task-text">${task.text}</div>
                            <span class="task-priority priority-${task.priority}">
                                ${task.priority.toUpperCase()}
                            </span>
                        </div>
                        <div class="task-actions">
                            <button class="delete-btn" onclick="deleteTask(${task.id})">
                                Delete
                            </button>
                        </div>
                    </div>
                `).join('');
            }
        }

        // Function to update statistics
        function updateStats() {
            const totalTasks = tasks.length;
            const completedTasks = tasks.filter(task => task.completed).length;
            const activeTasks = totalTasks - completedTasks;
            const completionRate = totalTasks > 0 ? Math.round((completedTasks / totalTasks) * 100) : 0;
            
            document.getElementById('totalTasks').textContent = totalTasks;
            document.getElementById('completedTasks').textContent = completedTasks;
            document.getElementById('activeTasks').textContent = activeTasks;
            document.getElementById('completionRate').textContent = completionRate + '%';
        }

        // Allow Enter key to add tasks
        document.getElementById('taskInput').addEventListener('keypress', function(e) {
            if (e.key === 'Enter') {
                addTask();
            }
        });

        // Initial render
        renderTasks();
        updateStats();
    </script>
</body>
</html>
```

### Your Tasks:

1. **Complete the Core Functionality**: The starter code provides the basic structure. Make sure all features work correctly.

2. **Add Priority Sorting Enhancement**: Modify the sorting to also consider completion status within priority levels.

3. **Implement Data Persistence**: Use `localStorage` to save and load tasks between browser sessions.

4. **Add Bulk Operations**: 
   - "Complete All" button
   - "Delete Completed" button
   - "Clear All" button

5. **Create Task Categories**: Allow users to assign categories to tasks and filter by category.

6. **Add Due Dates**: Extend tasks to include optional due dates and sort by urgency.

### Array Methods Practice:

As you work on this project, focus on using these array methods:
- `push()` - Add new tasks
- `filter()` - Filter and search tasks
- `find()` - Locate specific tasks
- `map()` - Transform task data for display
- `sort()` - Order tasks by different criteria
- `reduce()` - Calculate statistics
- `splice()` - Remove tasks at specific positions
- `includes()` - Search functionality
- `forEach()` - Iterate through tasks

This project will give you hands-on experience with all the essential array operations while building something practical and useful!