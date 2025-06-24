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

## Mini Project: Countdown Timer

Build an interactive countdown timer with multiple features and visual feedback.

### Project Requirements:

1. **Basic Timer Functionality:**
   - Set custom countdown time (minutes and seconds)
   - Start, pause, and reset controls
   - Real-time display updates
   - Sound notification when timer reaches zero

2. **Visual Features:**
   - Progress bar showing remaining time
   - Color changes as time runs out
   - Smooth animations and transitions
   - Full-screen mode option

3. **Preset Timers:**
   - Quick buttons for common times (5min, 10min, 25min)
   - Pomodoro technique support
   - Custom preset creation and saving

4. **Advanced Features:**
   - Multiple simultaneous timers
   - Lap/split time recording
   - Timer history and statistics
   - Keyboard shortcuts

### Starter Code Structure:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Advanced Countdown Timer</title>
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
            color: white;
        }
        
        .timer-container {
            background: rgba(255, 255, 255, 0.1);
            backdrop-filter: blur(20px);
            border-radius: 30px;
            padding: 40px;
            box-shadow: 0 20px 40px rgba(0,0,0,0.2);
            text-align: center;
            max-width: 500px;
            width: 90%;
        }
        
        .timer-display {
            font-size: 4rem;
            font-weight: bold;
            margin: 30px 0;
            text-shadow: 0 2px 10px rgba(0,0,0,0.3);
            transition: color 0.3s ease;
        }
        
        .timer-display.warning {
            color: #ffeb3b;
        }
        
        .timer-display.danger {
            color: #f44336;
            animation: pulse 1s infinite;
        }
        
        @keyframes pulse {
            0%, 50%, 100% { opacity: 1; }
            25%, 75% { opacity: 0.7; }
        }
        
        .progress-container {
            width: 100%;
            height: 20px;
            background: rgba(255, 255, 255, 0.2);
            border-radius: 10px;
            overflow: hidden;
            margin: 20px 0;
        }
        
        .progress-bar {
            height: 100%;
            background: linear-gradient(90deg, #4caf50, #8bc34a);
            border-radius: 10px;
            transition: width 0.1s linear, background 0.3s ease;
        }
        
        .progress-bar.warning {
            background: linear-gradient(90deg, #ff9800, #ffeb3b);
        }
        
        .progress-bar.danger {
            background: linear-gradient(90deg, #f44336, #ff5722);
        }
        
        .controls {
            display: flex;
            gap: 15px;
            justify-content: center;
            margin: 25px 0;
            flex-wrap: wrap;
        }
        
        button {
            padding: 12px 24px;
            border: none;
            border-radius: 25px;
            font-size: 16px;
            font-weight: bold;
            cursor: pointer;
            transition: all 0.3s ease;
            background: rgba(255, 255, 255, 0.2);
            color: white;
            backdrop-filter: blur(10px);
        }
        
        button:hover {
            transform: translateY(-2px);
            box-shadow: 0 5px 15px rgba(0,0,0,0.2);
        }
        
        .btn-primary {
            background: linear-gradient(45deg, #4caf50, #45a049);
        }
        
        .btn-secondary {
            background: linear-gradient(45deg, #ff9800, #f57c00);
        }
        
        .btn-danger {
            background: linear-gradient(45deg, #f44336, #d32f2f);
        }
        
        .input-section {
            margin: 20px 0;
            display: flex;
            gap: 10px;
            justify-content: center;
            align-items: center;
            flex-wrap: wrap;
        }
        
        input {
            padding: 10px 15px;
            border: none;
            border-radius: 15px;
            font-size: 16px;
            text-align: center;
            background: rgba(255, 255, 255, 0.9);
            color: #333;
            width: 80px;
        }
        
        .presets {
            display: flex;
            gap: 10px;
            justify-content: center;
            margin: 20px 0;
            flex-wrap: wrap;
        }
        
        .preset-btn {
            padding: 8px 16px;
            font-size: 14px;
            background: rgba(255, 255, 255, 0.15);
        }
        
        .status {
            margin: 15px 0;
            font-size: 18px;
            font-weight: bold;
        }
        
        .fullscreen-btn {
            position: fixed;
            top: 20px;
            right: 20px;
            width: 50px;
            height: 50px;
            border-radius: 50%;
            background: rgba(255, 255, 255, 0.2);
            border: none;
            color: white;
            font-size: 20px;
            cursor: pointer;
        }
        
        .timer-history {
            margin-top: 20px;
            background: rgba(255, 255, 255, 0.1);
            border-radius: 15px;
            padding: 15px;
            max-height: 200px;
            overflow-y: auto;
        }
        
        .history-item {
            padding: 5px 0;
            font-size: 14px;
            border-bottom: 1px solid rgba(255, 255, 255, 0.1);
        }
        
        .hidden {
            display: none;
        }
        
        /* Fullscreen styles */
        .fullscreen {
            position: fixed;
            top: 0;
            left: 0;
            width: 100vw;
            height: 100vh;
            z-index: 1000;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            display: flex;
            justify-content: center;
            align-items: center;
        }
        
        .fullscreen .timer-display {
            font-size: 8rem;
        }
    </style>
</head>
<body>
    <button class="fullscreen-btn" onclick="toggleFullscreen()" title="Toggle Fullscreen">⛶</button>
    
    <div class="timer-container" id="timerContainer">
        <h1>🕒 Advanced Timer</h1>
        
        <div class="status" id="timerStatus">Ready to start</div>
        
        <div class="timer-display" id="timerDisplay">00:00</div>
        
        <div class="progress-container">
            <div class="progress-bar" id="progressBar"></div>
        </div>
        
        <div class="input-section">
            <label>Minutes:</label>
            <input type="number" id="minutesInput" value="5" min="0" max="59">
            <label>Seconds:</label>
            <input type="number" id="secondsInput" value="0" min="0" max="59">
        </div>
        
        <div class="presets">
            <button class="preset-btn" onclick="setPreset(5, 0)">5 min</button>
            <button class="preset-btn" onclick="setPreset(10, 0)">10 min</button>
            <button class="preset-btn" onclick="setPreset(25, 0)">25 min (Pomodoro)</button>
            <button class="preset-btn" onclick="setPreset(0, 30)">30 sec</button>
        </div>
        
        <div class="controls">
            <button class="btn-primary" id="startBtn" onclick="startTimer()">Start</button>
            <button class="btn-secondary" id="pauseBtn" onclick="pauseTimer()" disabled>Pause</button>
            <button class="btn-danger" onclick="resetTimer()">Reset</button>
        </div>
        
        <div class="timer-history" id="timerHistory">
            <strong>Timer History:</strong>
            <div id="historyList"></div>
        </div>
    </div>

    <script>
        // Timer state variables
        let timerInterval = null;
        let totalSeconds = 0;
        let remainingSeconds = 0;
        let isRunning = false;
        let isPaused = false;
        let startTime = null;
        let history = [];
        
        // Audio for notifications
        const audioContext = new (window.AudioContext || window.webkitAudioContext)();
        
        // Core timer functions
        function setTimer(minutes, seconds) {
            const total = (minutes * 60) + seconds;
            if (total <= 0) {
                alert("Please enter a valid time greater than 0");
                return false;
            }
            
            totalSeconds = total;
            remainingSeconds = total;
            updateDisplay();
            updateProgressBar();
            return true;
        }
        
        function startTimer() {
            if (!isRunning && !isPaused) {
                const minutes = parseInt(document.getElementById('minutesInput').value) || 0;
                const seconds = parseInt(document.getElementById('secondsInput').value) || 0;
                
                if (!setTimer(minutes, seconds)) {
                    return;
                }
            }
            
            isRunning = true;
            isPaused = false;
            startTime = Date.now() - (totalSeconds - remainingSeconds) * 1000;
            
            // Start the countdown loop
            timerInterval = setInterval(updateTimer, 100);
            
            updateUI();
            updateStatus("Timer running...");
        }
        
        function updateTimer() {
            if (remainingSeconds <= 0) {
                completeTimer();
                return;
            }
            
            remainingSeconds--;
            updateDisplay();
            updateProgressBar();
            
            // Visual warnings
            if (remainingSeconds <= 10) {
                setTimerState('danger');
            } else if (remainingSeconds <= 30) {
                setTimerState('warning');
            } else {
                setTimerState('normal');
            }
        }
        
        function pauseTimer() {
            if (isRunning) {
                clearInterval(timerInterval);
                isRunning = false;
                isPaused = true;
                updateUI();
                updateStatus("Timer paused");
            }
        }
        
        function resetTimer() {
            clearInterval(timerInterval);
            isRunning = false;
            isPaused = false;
            
            const minutes = parseInt(document.getElementById('minutesInput').value) || 0;
            const seconds = parseInt(document.getElementById('secondsInput').value) || 0;
            setTimer(minutes, seconds);
            
            setTimerState('normal');
            updateUI();
            updateStatus("Timer reset");
        }
        
        function completeTimer() {
            clearInterval(timerInterval);
            isRunning = false;
            isPaused = false;
            remainingSeconds = 0;
            
            updateDisplay();
            updateProgressBar();
            setTimerState('danger');
            updateUI();
            updateStatus("Time's up! 🎉");
            
            // Add to history
            addToHistory(`${formatTime(totalSeconds)} - Completed`);
            
            // Play notification sound
            playNotificationSound();
            
            // Browser notification if supported
            if (Notification.permission === 'granted') {
                new Notification('Timer Complete!', {
                    body: 'Your countdown timer has finished.',
                    icon: '🕒'
                });
            }
        }
        
        // Display and UI functions
        function updateDisplay() {
            document.getElementById('timerDisplay').textContent = formatTime(remainingSeconds);
        }
        
        function formatTime(seconds) {
            const mins = Math.floor(seconds / 60);
            const secs = seconds % 60;
            return `${mins.toString().padStart(2, '0')}:${secs.toString().padStart(2, '0')}`;
        }
        
        function updateProgressBar() {
            const progress = totalSeconds > 0 ? (remainingSeconds / totalSeconds) * 100 : 0;
            const progressBar = document.getElementById('progressBar');
            progressBar.style.width = `${progress}%`;
        }
        
        function setTimerState(state) {
            const display = document.getElementById('timerDisplay');
            const progressBar = document.getElementById('progressBar');
            
            // Remove all state classes
            display.classList.remove('warning', 'danger');
            progressBar.classList.remove('warning', 'danger');
            
            // Add appropriate state class
            if (state !== 'normal') {
                display.classList.add(state);
                progressBar.classList.add(state);
            }
        }
        
        function updateUI() {
            const startBtn = document.getElementById('startBtn');
            const pauseBtn = document.getElementById('pauseBtn');
            
            if (isRunning) {
                startBtn.disabled = true;
                pauseBtn.disabled = false;
                startBtn.textContent = 'Running';
                pauseBtn.textContent = 'Pause';
            } else if (isPaused) {
                startBtn.disabled = false;
                pauseBtn.disabled = true;
                startBtn.textContent = 'Resume';
                pauseBtn.textContent = 'Paused';
            } else {
                startBtn.disabled = false;
                pauseBtn.disabled = true;
                startBtn.textContent = 'Start';
                pauseBtn.textContent = 'Pause';
            }
        }
        
        function updateStatus(message) {
            document.getElementById('timerStatus').textContent = message;
        }
        
        // Preset and input functions
        function setPreset(minutes, seconds) {
            document.getElementById('minutesInput').value = minutes;
            document.getElementById('secondsInput').value = seconds;
            
            if (!isRunning && !isPaused) {
                setTimer(minutes, seconds);
                updateStatus(`Preset: ${formatTime(totalSeconds)}`);
            }
        }
        
        // History functions
        function addToHistory(entry) {
            const timestamp = new Date().toLocaleTimeString();
            history.unshift(`${timestamp} - ${entry}`);
            
            // Keep only last 10 entries
            if (history.length > 10) {
                history = history.slice(0, 10);
            }
            
            updateHistoryDisplay();
        }
        
        function updateHistoryDisplay() {
            const historyList = document.getElementById('historyList');
            historyList.innerHTML = history.map(entry => 
                `<div class="history-item">${entry}</div>`
            ).join('');
        }
        
        // Fullscreen functionality
        function toggleFullscreen() {
            const container = document.getElementById('timerContainer');
            container.classList.toggle('fullscreen');
        }
        
        // Sound functions
        function playNotificationSound() {
            // Create a simple beep sound
            const oscillator = audioContext.createOscillator();
            const gainNode = audioContext.createGain();
            
            oscillator.connect(gainNode);
            gainNode.connect(audioContext.destination);
            
            oscillator.frequency.setValueAtTime(800, audioContext.currentTime);
            gainNode.gain.setValueAtTime(0.3, audioContext.currentTime);
            gainNode.gain.exponentialRampToValueAtTime(0.01, audioContext.currentTime + 0.5);
            
            oscillator.start(audioContext.currentTime);
            oscillator.stop(audioContext.currentTime + 0.5);
        }
        
        // Keyboard shortcuts
        document.addEventListener('keydown', function(event) {
            if (event.target.tagName === 'INPUT') return;
            
            switch (event.key.toLowerCase()) {
                case ' ':
                case 'enter':
                    event.preventDefault();
                    if (isRunning) {
                        pauseTimer();
                    } else {
                        startTimer();
                    }
                    break;
                case 'r':
                    resetTimer();
                    break;
                case 'f':
                    toggleFullscreen();
                    break;
                case '1':
                    setPreset(5, 0);
                    break;
                case '2':
                    setPreset(10, 0);
                    break;
                case '3':
                    setPreset(25, 0);
                    break;
            }
        });
        
        // Request notification permission
        if ('Notification' in window && Notification.permission === 'default') {
            Notification.requestPermission();
        }
        
        // Initialize timer
        setTimer(5, 0);
        updateUI();
    </script>
</body>
</html>
```

### Helpful Concepts to Explore:

**JavaScript Concepts:**
- `setInterval()` and `clearInterval()` for timed execution
- Date and time manipulation for accurate timing
- Event handling for user interactions
- State management for timer controls
- Local storage for saving presets and history
- Browser APIs for notifications and audio

**HTML Concepts:**
- Semantic structure for timer interface
- Form inputs with validation
- Accessibility considerations for timers
- Responsive design for different devices

**CSS Concepts:**
- CSS animations and transitions
- Flexbox for responsive layouts
- CSS variables for dynamic theming
- Media queries for fullscreen mode

### Extension Ideas:

Once you complete the basic timer, try adding:
- **Interval training**: Alternating work/rest periods
- **Multiple timers**: Run several timers simultaneously
- **Custom sounds**: Upload and use custom notification sounds
- **Theme customization**: Different color schemes and backgrounds
- **Timer templates**: Save and load timer configurations
- **Statistics tracking**: Track usage patterns and productivity
- **Integration**: Connect with calendar or task management apps