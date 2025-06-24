# Part 8: Objects - Organizing Related Data

## Object Fundamentals

### What Are Objects?

Objects are collections of related data and functionality stored as key-value pairs. They allow you to group related information and behaviors together, making your code more organized and easier to understand.

#### Why Use Objects?
- **Organization**: Group related data and functions together
- **Real-world modeling**: Represent entities like users, products, etc.
- **Code reusability**: Create templates for similar entities
- **Data structure**: Efficient storage and access of complex data
- **Encapsulation**: Keep related functionality together

### Creating Objects

#### Object Literal Syntax
```javascript
// Basic object creation
const person = {
    name: 'Alice Johnson',
    age: 28,
    email: 'alice@example.com',
    isActive: true
};

// Accessing properties
console.log(person.name);        // 'Alice Johnson'
console.log(person['email']);    // 'alice@example.com'

// Complex object with nested data
const product = {
    id: 'PRD-001',
    name: 'Wireless Headphones',
    price: 129.99,
    category: 'Electronics',
    specifications: {
        brand: 'TechSound',
        model: 'WH-1000',
        color: 'Black',
        wireless: true,
        batteryLife: '30 hours'
    },
    reviews: [
        { rating: 5, comment: 'Excellent sound quality!' },
        { rating: 4, comment: 'Great battery life.' }
    ],
    inStock: true,
    tags: ['wireless', 'noise-canceling', 'premium']
};
```

#### Dynamic Property Names
```javascript
// Using variables as property names
const propertyName = 'dynamicProperty';
const obj = {
    [propertyName]: 'This is dynamic',
    ['computed_' + Date.now()]: 'Timestamp property'
};

// Dynamic property assignment
const user = {};
const field = 'username';
user[field] = 'johndoe';
user['profile_' + user.username] = { theme: 'dark' };
```

### Object Properties and Methods

#### Property Access and Modification
```javascript
const student = {
    firstName: 'John',
    lastName: 'Doe',
    grade: 85,
    subjects: ['Math', 'Science', 'English']
};

// Dot notation (preferred when property name is known)
student.grade = 90;
student.graduationYear = 2024;

// Bracket notation (use when property name is dynamic)
const prop = 'firstName';
console.log(student[prop]); // 'John'

// Property existence checking
console.log('grade' in student);              // true
console.log(student.hasOwnProperty('grade')); // true
console.log(student.teacher !== undefined);   // false

// Delete properties
delete student.subjects;
console.log(student.subjects); // undefined
```

#### Object Methods
```javascript
const calculator = {
    // Properties
    brand: 'MathPro',
    model: 'X-2000',
    
    // Methods - functions as object properties
    add: function(a, b) {
        return a + b;
    },
    
    // Shorthand method syntax (ES6)
    subtract(a, b) {
        return a - b;
    },
    
    // Arrow function method (be careful with 'this')
    multiply: (a, b) => a * b,
    
    // Method that uses 'this' to access object properties
    getInfo() {
        return `${this.brand} ${this.model} Calculator`;
    },
    
    // Method with complex logic
    calculate(operation, a, b) {
        switch (operation) {
            case 'add':
                return this.add(a, b);
            case 'subtract':
                return this.subtract(a, b);
            case 'multiply':
                return this.multiply(a, b);
            case 'divide':
                return b !== 0 ? a / b : 'Error: Division by zero';
            default:
                return 'Error: Unknown operation';
        }
    }
};

// Using object methods
console.log(calculator.add(5, 3));           // 8
console.log(calculator.getInfo());           // 'MathPro X-2000 Calculator'
console.log(calculator.calculate('add', 10, 5)); // 15
```

### The 'this' Keyword

#### Understanding 'this' Context
```javascript
const user = {
    name: 'Sarah',
    email: 'sarah@example.com',
    
    // 'this' refers to the user object
    greet() {
        return `Hello, I'm ${this.name}`;
    },
    
    // 'this' in nested methods
    profile: {
        age: 25,
        getAge() {
            return this.age; // 'this' refers to the profile object, not user
        }
    },
    
    // Method that demonstrates 'this' behavior
    introduce: function() {
        console.log(`Name: ${this.name}, Email: ${this.email}`);
    },
    
    // Arrow function doesn't have its own 'this'
    arrowGreet: () => {
        // 'this' here refers to the global object (window/global)
        return `Hello from ${this.name}`; // Will not work as expected
    }
};

// Different ways to call methods affect 'this'
user.introduce();                    // Works correctly
const introduce = user.introduce;
introduce();                         // 'this' is undefined or global object

// Binding 'this' explicitly
const boundIntroduce = user.introduce.bind(user);
boundIntroduce();                    // Works correctly
```

#### Practical 'this' Examples
```javascript
const shoppingCart = {
    items: [],
    total: 0,
    
    addItem(item) {
        this.items.push(item);
        this.total += item.price;
        this.updateDisplay();
        return this; // Enable method chaining
    },
    
    removeItem(itemId) {
        const index = this.items.findIndex(item => item.id === itemId);
        if (index !== -1) {
            const removedItem = this.items.splice(index, 1)[0];
            this.total -= removedItem.price;
            this.updateDisplay();
        }
        return this;
    },
    
    clearCart() {
        this.items = [];
        this.total = 0;
        this.updateDisplay();
        return this;
    },
    
    updateDisplay() {
        console.log(`Cart: ${this.items.length} items, Total: $${this.total.toFixed(2)}`);
    },
    
    // Method chaining example
    applyCoupon(discount) {
        this.total *= (1 - discount);
        console.log(`Coupon applied! New total: $${this.total.toFixed(2)}`);
        return this;
    }
};

// Method chaining
shoppingCart
    .addItem({ id: 1, name: 'Book', price: 15.99 })
    .addItem({ id: 2, name: 'Pen', price: 2.50 })
    .applyCoupon(0.1)
    .removeItem(1);
```

### Object Construction Patterns

#### Factory Functions
```javascript
// Factory function to create user objects
function createUser(name, email, role = 'user') {
    return {
        name: name,
        email: email,
        role: role,
        isActive: true,
        loginCount: 0,
        
        login() {
            this.loginCount++;
            console.log(`${this.name} logged in. Total logins: ${this.loginCount}`);
        },
        
        updateProfile(newName, newEmail) {
            this.name = newName || this.name;
            this.email = newEmail || this.email;
            console.log('Profile updated successfully');
        },
        
        deactivate() {
            this.isActive = false;
            console.log(`${this.name} account deactivated`);
        }
    };
}

// Create users using factory function
const admin = createUser('Admin User', 'admin@company.com', 'admin');
const regular = createUser('John Doe', 'john@example.com');

admin.login();
regular.updateProfile('John Smith', 'johnsmith@example.com');
```

#### Constructor Functions
```javascript
// Constructor function (traditional approach)
function Product(name, price, category) {
    this.name = name;
    this.price = price;
    this.category = category;
    this.id = Math.random().toString(36).substr(2, 9);
    this.createdAt = new Date();
}

// Add methods to prototype for memory efficiency
Product.prototype.updatePrice = function(newPrice) {
    if (newPrice > 0) {
        this.price = newPrice;
        console.log(`Price updated to $${this.price}`);
    } else {
        console.log('Invalid price');
    }
};

Product.prototype.applyDiscount = function(percentage) {
    this.price *= (1 - percentage / 100);
    console.log(`Discount applied. New price: $${this.price.toFixed(2)}`);
};

// Create instances using 'new' keyword
const laptop = new Product('Gaming Laptop', 1299.99, 'Electronics');
const book = new Product('JavaScript Guide', 39.95, 'Books');

laptop.updatePrice(1199.99);
book.applyDiscount(15);
```

#### ES6 Classes (Modern Approach)
```javascript
class Vehicle {
    constructor(make, model, year) {
        this.make = make;
        this.model = model;
        this.year = year;
        this.mileage = 0;
        this.isRunning = false;
    }
    
    // Instance methods
    start() {
        this.isRunning = true;
        console.log(`${this.getDisplayName()} started`);
    }
    
    stop() {
        this.isRunning = false;
        console.log(`${this.getDisplayName()} stopped`);
    }
    
    drive(miles) {
        if (this.isRunning) {
            this.mileage += miles;
            console.log(`Drove ${miles} miles. Total mileage: ${this.mileage}`);
        } else {
            console.log('Start the vehicle first!');
        }
    }
    
    getDisplayName() {
        return `${this.year} ${this.make} ${this.model}`;
    }
    
    // Static method (belongs to class, not instances)
    static compareByYear(vehicle1, vehicle2) {
        return vehicle1.year - vehicle2.year;
    }
}

// Inheritance
class Car extends Vehicle {
    constructor(make, model, year, doors) {
        super(make, model, year); // Call parent constructor
        this.doors = doors;
        this.fuelLevel = 100;
    }
    
    // Override parent method
    drive(miles) {
        if (this.fuelLevel > 0) {
            super.drive(miles); // Call parent method
            this.fuelLevel -= miles * 0.1;
            console.log(`Fuel level: ${this.fuelLevel.toFixed(1)}%`);
        } else {
            console.log('Out of fuel!');
        }
    }
    
    refuel() {
        this.fuelLevel = 100;
        console.log('Tank refueled');
    }
}

// Create and use instances
const car = new Car('Toyota', 'Camry', 2023, 4);
car.start();
car.drive(50);
car.refuel();
```

### Advanced Object Techniques

#### Object Destructuring
```javascript
const user = {
    id: 123,
    name: 'Alice Johnson',
    email: 'alice@example.com',
    address: {
        street: '123 Main St',
        city: 'Boston',
        state: 'MA',
        zip: '02101'
    },
    preferences: {
        theme: 'dark',
        notifications: true
    }
};

// Basic destructuring
const { name, email } = user;
console.log(name, email); // 'Alice Johnson', 'alice@example.com'

// Destructuring with renaming
const { name: userName, id: userId } = user;
console.log(userName, userId); // 'Alice Johnson', 123

// Nested destructuring
const { address: { city, state } } = user;
console.log(city, state); // 'Boston', 'MA'

// Default values
const { phone = 'Not provided', age = 'Unknown' } = user;
console.log(phone, age); // 'Not provided', 'Unknown'

// Function parameter destructuring
function displayUser({ name, email, address: { city } }) {
    console.log(`${name} (${email}) from ${city}`);
}

displayUser(user); // 'Alice Johnson (alice@example.com) from Boston'
```

#### Object Spread and Rest
```javascript
const baseConfig = {
    theme: 'light',
    language: 'en',
    notifications: true
};

const userConfig = {
    theme: 'dark',
    fontSize: 14,
    sidebar: 'collapsed'
};

// Spread operator - merge objects
const finalConfig = {
    ...baseConfig,
    ...userConfig,
    version: '2.0'
};
// Result: { theme: 'dark', language: 'en', notifications: true, fontSize: 14, sidebar: 'collapsed', version: '2.0' }

// Rest in destructuring
const { theme, ...otherSettings } = finalConfig;
console.log(theme);         // 'dark'
console.log(otherSettings); // { language: 'en', notifications: true, fontSize: 14, sidebar: 'collapsed', version: '2.0' }

// Creating modified copies
const updatedConfig = {
    ...finalConfig,
    theme: 'auto',
    newFeature: true
};
```

#### Object Methods and Utilities
```javascript
const inventory = {
    items: {
        'item1': { name: 'Laptop', quantity: 5, price: 999 },
        'item2': { name: 'Mouse', quantity: 20, price: 25 },
        'item3': { name: 'Keyboard', quantity: 0, price: 75 }
    }
};

// Object.keys() - get property names
const itemIds = Object.keys(inventory.items);
console.log(itemIds); // ['item1', 'item2', 'item3']

// Object.values() - get property values
const itemObjects = Object.values(inventory.items);
console.log(itemObjects); // Array of item objects

// Object.entries() - get key-value pairs
const itemEntries = Object.entries(inventory.items);
itemEntries.forEach(([id, item]) => {
    console.log(`${id}: ${item.name} - $${item.price}`);
});

// Object.assign() - copy/merge objects
const newItem = Object.assign({}, inventory.items.item1, { quantity: 10 });

// Object.freeze() - make object immutable
const frozenConfig = Object.freeze({ setting: 'value' });
// frozenConfig.setting = 'new value'; // This will fail

// Object.seal() - prevent adding/removing properties
const sealedObject = Object.seal({ existing: 'property' });
sealedObject.existing = 'modified'; // This works
// sealedObject.newProp = 'value'; // This fails
```

---

## Mini Project: Student Grade Tracker

Build a simple grade tracking system to practice object concepts.

### Project Overview:
Create a student management system that tracks multiple students and their grades across different subjects.

### Requirements:
1. Create student objects with properties for name, ID, and grades
2. Add methods to calculate averages and letter grades
3. Implement a class-based approach for managing multiple students
4. Practice object destructuring and manipulation

### Basic Implementation:

```javascript
// Student constructor function
function Student(name, id) {
    this.name = name;
    this.id = id;
    this.grades = {};
}

// Add methods to Student prototype
Student.prototype.addGrade = function(subject, grade) {
    if (!this.grades[subject]) {
        this.grades[subject] = [];
    }
    this.grades[subject].push(grade);
};

Student.prototype.getAverage = function(subject) {
    if (!this.grades[subject] || this.grades[subject].length === 0) {
        return 0;
    }
    const sum = this.grades[subject].reduce((acc, grade) => acc + grade, 0);
    return sum / this.grades[subject].length;
};

Student.prototype.getOverallAverage = function() {
    const subjects = Object.keys(this.grades);
    if (subjects.length === 0) return 0;
    
    const totalAverage = subjects.reduce((sum, subject) => {
        return sum + this.getAverage(subject);
    }, 0);
    
    return totalAverage / subjects.length;
};

Student.prototype.getLetterGrade = function(average) {
    if (average >= 90) return 'A';
    if (average >= 80) return 'B';
    if (average >= 70) return 'C';
    if (average >= 60) return 'D';
    return 'F';
};

// Usage example
const student1 = new Student('Alice Johnson', 'STU001');
student1.addGrade('Math', 85);
student1.addGrade('Math', 92);
student1.addGrade('Science', 88);
student1.addGrade('English', 76);

console.log(`Math Average: ${student1.getAverage('Math')}`);
console.log(`Overall Average: ${student1.getOverallAverage()}`);
console.log(`Grade: ${student1.getLetterGrade(student1.getOverallAverage())}`);
```

### Practice Exercises:

1. **Object Literals**: Create a simple student object using object literal syntax
2. **Method Practice**: Add a method to display all grades in a formatted way
3. **Object Destructuring**: Extract student information using destructuring
4. **Class Conversion**: Convert the constructor function to an ES6 class
5. **Class Manager**: Create a `ClassRoom` class to manage multiple students

Try implementing these exercises to reinforce your understanding of JavaScript objects!

---

## Assessment Checklist

Before moving to Part 9, ensure you can:
- [ ] Create objects using literal syntax and understand property access
- [ ] Write and use object methods effectively
- [ ] Understand the 'this' keyword and its context
- [ ] Use constructor functions and ES6 classes to create object templates
- [ ] Apply object destructuring for cleaner code
- [ ] Manipulate objects using spread/rest operators
- [ ] Use Object methods (keys, values, entries) for object manipulation
- [ ] Implement inheritance with classes and prototypes
- [ ] Organize complex data using nested objects
- [ ] Build interactive applications with object-oriented design

---

## Additional Resources

**Essential Learning:**
- **MDN**: [Working with Objects](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Working_with_Objects)
- **MDN**: [Object-oriented JavaScript](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Objects)
- **JavaScript.info**: [Objects: the basics](https://javascript.info/object)

**Practice Platforms:**
- **freeCodeCamp**: [Object Oriented Programming](https://www.freecodecamp.org/learn/javascript-algorithms-and-data-structures/)
- **Codewars**: [JavaScript Object Kata](https://www.codewars.com/)

**Advanced Topics:**
- **MDN**: [Classes](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes)
- **JavaScript.info**: [Class inheritance](https://javascript.info/class-inheritance)
- **MDN**: [Prototype chain](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Inheritance_and_the_prototype_chain)

---

## Next Steps

Once you've mastered objects and completed the student grade tracker project, you're ready to move on to [Part 9: Events and Forms - Interactive Web Pages](9_events-and-forms.md) where you'll learn to handle user interactions, process form data, and create dynamic, responsive web applications.