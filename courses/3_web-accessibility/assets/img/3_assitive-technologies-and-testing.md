# Part 3: Assistive Technologies and Testing

## Understanding Assistive Technologies

### Screen Readers and How They Work

Screen readers are software applications that convert digital text and interface elements into speech or braille output. They are the primary assistive technology used by people who are blind or have severe visual impairments.

#### Key Concepts:
- Screen readers parse HTML markup and DOM structure
- They create a virtual representation of the page content
- Users navigate using keyboard shortcuts and commands
- Semantic markup provides crucial navigation context
- ARIA attributes enhance the screen reader experience

#### Getting Started:
This section covers assistive technologies with a focus on screen readers, along with comprehensive testing methodologies.

For learning about assistive technologies and testing, we will use resources from [WebAIM](https://webaim.org/) and hands-on experience with actual screen reading software.

### Task 1
1. Install a screen reader on your system (NVDA for Windows, VoiceOver for Mac, or Orca for Linux)
2. Complete the [WebAIM Screen Reader Testing Guide](https://webaim.org/articles/screenreader_testing/)
3. Practice navigating websites using only a screen reader for 30 minutes
4. Watch [Screen Reader Basics: VoiceOver](https://www.youtube.com/watch?v=5R-6WvAihms) or [NVDA Screen Reader Basics](https://www.youtube.com/watch?v=Jao3s_CwdRU)

### Recap of the Content

Understanding how assistive technologies work is essential for creating truly accessible web experiences. This knowledge helps developers test their implementations effectively and understand the user experience.

#### How Screen Readers Parse Content

**HTML Structure Interpretation:**
```html
<!-- Screen readers create navigation lists from this structure -->
<main>
    <h1>Website Title</h1> <!-- Level 1 heading - main page title -->
        <h2>Section One</h2> <!-- Level 2 heading - major section -->
            <h3>Subsection A</h3> <!-- Level 3 heading - subsection -->
            <h3>Subsection B</h3> <!-- Another level 3 heading -->
        <h2>Section Two</h2> <!-- Back to level 2 - new major section -->
            <h3>Another Subsection</h3>
</main>

<!-- Screen readers also create lists of links, form controls, and landmarks -->
<nav aria-label="Main navigation">
    <ul>
        <li><a href="/">Home</a></li>
        <li><a href="/about">About</a></li>
        <li><a href="/contact">Contact</a></li>
    </ul>
</nav>
```

**Virtual Buffer Navigation:**
```html
<!-- Screen readers provide multiple navigation modes -->
<article>
    <header>
        <h2>Article Title</h2> <!-- Users can jump by headings -->
        <time datetime="2024-01-15">January 15, 2024</time>
    </header>
    
    <p>First paragraph with a <a href="/link">link</a>.</p> <!-- Users can jump by links -->
    
    <img src="chart.jpg" alt="Sales increased 25% in Q4"> <!-- Users can jump by graphics -->
    
    <form> <!-- Users can jump by form controls -->
        <label for="email">Email:</label>
        <input type="email" id="email" name="email">
        <button type="submit">Subscribe</button>
    </form>
</article>
```

#### Voice Recognition Software

**Dragon NaturallySpeaking and Similar Tools:**
```html
<!-- Voice control works better with proper labels and structure -->
<nav aria-label="Main navigation">
    <button aria-label="Open main menu">
        Menu
    </button>
    
    <ul id="main-menu" hidden>
        <li><a href="/">Home</a></li>
        <li><a href="/products">Products</a></li>
        <li><a href="/support">Support</a></li>
    </ul>
</nav>

<!-- Voice users can say "Click Home" or "Click Products" -->
<!-- Clear, descriptive text makes voice control more effective -->
```

**Voice Control Best Practices:**
- Use descriptive link text and button labels
- Avoid generic text like "click here" or "read more"
- Ensure visible text matches accessible names
- Provide clear navigation structure

#### Switch Navigation and Alternative Input Devices

**Switch Access Considerations:**
```html
<!-- Linear navigation order is crucial for switch users -->
<form>
    <fieldset>
        <legend>Contact Information</legend>
        
        <!-- Logical tab order: name, email, phone, message, submit -->
        <label for="name">Name:</label>
        <input type="text" id="name" name="name">
        
        <label for="email">Email:</label>
        <input type="email" id="email" name="email">
        
        <label for="phone">Phone:</label>
        <input type="tel" id="phone" name="phone">
        
        <label for="message">Message:</label>
        <textarea id="message" name="message"></textarea>
        
        <button type="submit">Send Message</button>
    </fieldset>
</form>
```

**Keyboard Navigation Requirements:**
```html
<!-- All interactive elements must be keyboard accessible -->
<div class="custom-dropdown">
    <!-- Use native select instead of custom JavaScript -->
    <label for="options">Select an option:</label>
    <select id="options" name="options">
        <option value="">Choose an option</option>
        <option value="option1">Option 1</option>
        <option value="option2">Option 2</option>
        <option value="option3">Option 3</option>
    </select>
</div>

<!-- For complex navigation, use logical HTML structure -->
<nav aria-label="Main navigation">
    <ul>
        <li><a href="/">Home</a></li>
        <li>
            <a href="/products">Products</a>
            <ul>
                <li><a href="/laptops">Laptops</a></li>
                <li><a href="/desktops">Desktops</a></li>
            </ul>
        </li>
        <li><a href="/contact">Contact</a></li>
    </ul>
</nav>
```

#### Magnification and High Contrast Tools

**Zoom and Magnification Considerations:**
```css
/* Design for 200% zoom minimum */
.container {
    max-width: 1200px;
    margin: 0 auto;
    padding: 1rem;
}

/* Responsive design helps with magnification */
@media (max-width: 768px) {
    .navigation {
        flex-direction: column;
    }
}

/* Avoid fixed positioning that breaks with zoom */
.sticky-header {
    position: sticky; /* Better than fixed for zoom */
    top: 0;
    z-index: 100;
}
```

**High Contrast Support:**
```css
/* Support Windows High Contrast Mode */
@media (prefers-contrast: high) {
    .button {
        border: 2px solid ButtonText;
        background: ButtonFace;
        color: ButtonText;
    }
    
    .button:hover {
        background: Highlight;
        color: HighlightText;
    }
}

/* Support forced colors mode */
@media (forced-colors: active) {
    .custom-checkbox {
        forced-color-adjust: none;
        border: 1px solid ButtonText;
    }
}
```

**Resources:**
- **WebAIM Assistive Technologies**: [Introduction to Assistive Technologies](https://webaim.org/articles/motor/assistive)

---

## Screen Reader Testing

### Popular Screen Readers

**NVDA (NonVisual Desktop Access) - Windows:**
```html
<!-- NVDA-specific testing considerations -->
<!DOCTYPE html>
<html lang="en">
<head>
    <title>Page Title - NVDA will announce this</title>
</head>
<body>
    <!-- NVDA announces landmarks -->
    <main>
        <h1>Main Heading</h1>
        <p>NVDA reads this content with proper pronunciation when lang is set</p>
        
        <!-- NVDA has excellent table support -->
        <table>
            <caption>NVDA announces the caption first</caption>
            <thead>
                <tr>
                    <th scope="col">Column 1</th>
                    <th scope="col">Column 2</th>
                </tr>
            </thead>
            <tbody>
                <tr>
                    <th scope="row">Row header</th>
                    <td>NVDA announces "Column 1, Row header"</td>
                </tr>
            </tbody>
        </table>
    </main>
</body>
</html>
```

**VoiceOver - macOS:**
```html
<!-- VoiceOver-specific considerations -->
<form>
    <!-- VoiceOver groups form controls well -->
    <fieldset>
        <legend>Personal Information</legend>
        
        <!-- VoiceOver announces: "Personal Information group, Name, edit text" -->
        <label for="name">Name</label>
        <input type="text" id="name" name="name">
        
        <!-- VoiceOver handles aria-describedby excellently -->
        <label for="password">Password</label>
        <input type="password" id="password" aria-describedby="pwd-help">
        <div id="pwd-help">Minimum 8 characters</div>
    </fieldset>
</form>

<!-- VoiceOver rotor navigation -->
<nav aria-label="Site navigation">
    <ul>
        <li><a href="/">Home</a></li>
        <li><a href="/about">About</a></li>
        <li><a href="/contact">Contact</a></li>
    </ul>
</nav>
```

**JAWS (Job Access With Speech) - Windows:**
```html
<!-- JAWS-specific optimizations -->
<article>
    <!-- JAWS has sophisticated heading navigation -->
    <h1>Article Title</h1>
    <h2>Section One</h2>
    <h3>Subsection</h3>
    
    <!-- JAWS virtual cursor modes -->
    <p>
        JAWS users can navigate by character, word, line, or element.
        <a href="/link">Links are easily discoverable</a> using JAWS commands.
    </p>
    
    <!-- JAWS form mode -->
    <form>
        <label for="search">Search</label>
        <input type="search" id="search" name="search">
        <!-- JAWS automatically enters form mode here -->
        <button type="submit">Search</button>
    </form>
</article>
```

#### Installing and Configuring Screen Readers

**NVDA Installation and Setup:**
```html
<!-- Create test content for NVDA -->
<div>
    <h1>NVDA Testing Page</h1>
    
    <!-- Test heading navigation with NVDA -->
    <h2>Navigation Test</h2>
    <p>Use H and Shift+H to navigate headings</p>
    
    <h2>Link Test</h2>
    <p><a href="#test">Use K and Shift+K to navigate links</a></p>
    
    <h2>Form Test</h2>
    <form>
        <label for="test-input">Test Input</label>
        <input type="text" id="test-input">
        <!-- Use F and Shift+F to navigate form fields -->
        <button type="submit">Submit</button>
    </form>
    
    <h2>List Test</h2>
    <ul>
        <li>Use L and Shift+L to navigate lists</li>
        <li>Use I and Shift+I to navigate list items</li>
    </ul>
</div>
```

**VoiceOver Setup and Configuration:**
```html
<!-- VoiceOver testing structure -->
<main>
    <h1>VoiceOver Testing</h1>
    
    <!-- Test VoiceOver rotor -->
    <nav aria-label="Test navigation">
        <ul>
            <li><a href="#section1">Section 1</a></li>
            <li><a href="#section2">Section 2</a></li>
        </ul>
    </nav>
    
    <!-- Test VoiceOver landmark navigation -->
    <section id="section1" aria-labelledby="heading1">
        <h2 id="heading1">Section 1</h2>
        <p>Use Control+Option+U to open rotor</p>
    </section>
    
    <aside aria-label="Sidebar content">
        <h3>Related Information</h3>
        <p>VoiceOver announces this as complementary content</p>
    </aside>
</main>
```

#### Navigation Techniques and Keyboard Shortcuts

**NVDA Navigation Commands:**
```
Basic Navigation:
- Arrow keys: Read by character/word/line
- Ctrl: Stop speech
- NVDA+Space: Switch between browse and focus modes

Quick Navigation (Browse Mode):
- H/Shift+H: Headings
- K/Shift+K: Links  
- F/Shift+F: Form fields
- T/Shift+T: Tables
- L/Shift+L: Lists
- G/Shift+G: Graphics
- D/Shift+D: Landmarks

Table Navigation:
- Ctrl+Alt+Arrow keys: Navigate table cells
- Ctrl+Alt+Home: Go to first cell
- Ctrl+Alt+End: Go to last cell
```

**VoiceOver Navigation Commands:**
```
Basic Navigation:
- Control+Option+Arrow keys: Navigate elements
- Control+Option+Space: Activate element
- Control+Option+A: Start reading

Rotor Navigation:
- Control+Option+U: Open rotor
- Left/Right arrows: Change rotor category
- Up/Down arrows: Navigate within category

Quick Navigation:
- Control+Option+Command+H: Headings
- Control+Option+Command+L: Links
- Control+Option+Command+T: Tables
- Control+Option+Command+G: Graphics
```

**JAWS Navigation Commands:**
```
Basic Navigation:
- Arrow keys: Read by character/word/line
- Ctrl: Stop speech
- Insert+Z: Switch between PC Cursor and Virtual Cursor

Quick Navigation (Virtual Cursor):
- H/Shift+H: Headings
- K/Shift+K: Links
- F/Shift+F: Form fields
- T/Shift+T: Tables
- L/Shift+L: Lists
- G/Shift+G: Graphics

Forms Navigation:
- Enter/Exit forms mode automatically
- Tab: Move to next form field
- Shift+Tab: Move to previous form field
```

#### Testing Procedures and Best Practices

**Comprehensive Screen Reader Testing Checklist:**
```html
<!-- Test document structure -->
<!DOCTYPE html>
<html lang="en">
<head>
    <title>Accessibility Test Page</title>
</head>
<body>
    <!-- 1. Test page title announcement -->
    <header>
        <h1>Main Page Title</h1>
        
        <!-- 2. Test navigation structure -->
        <nav aria-label="Main navigation">
            <ul>
                <li><a href="/">Home</a></li>
                <li><a href="/about">About</a></li>
            </ul>
        </nav>
    </header>
    
    <!-- 3. Test landmark navigation -->
    <main>
        <!-- 4. Test heading hierarchy -->
        <h2>Content Section</h2>
        <h3>Subsection</h3>
        
        <!-- 5. Test link context -->
        <p>
            Learn more about <a href="/accessibility">web accessibility best practices</a> 
            in our comprehensive guide.
        </p>
        
        <!-- 6. Test image descriptions -->
        <img src="chart.jpg" alt="Website traffic increased 40% from January to December 2024">
        
        <!-- 7. Test form labels and instructions -->
        <form>
            <fieldset>
                <legend>Contact Information</legend>
                
                <label for="email">Email Address (required)</label>
                <input type="email" id="email" name="email" required 
                       aria-describedby="email-help">
                <div id="email-help">We'll never share your email</div>
                
                <!-- 8. Test error handling -->
                <div id="email-error" role="alert" hidden>
                    Please enter a valid email address
                </div>
            </fieldset>
            
            <button type="submit">Submit Form</button>
        </form>
        
        <!-- 9. Test table structure -->
        <table>
            <caption>Monthly Sales Data</caption>
            <thead>
                <tr>
                    <th scope="col">Month</th>
                    <th scope="col">Sales</th>
                </tr>
            </thead>
            <tbody>
                <tr>
                    <th scope="row">January</th>
                    <td>$10,000</td>
                </tr>
            </tbody>
        </table>
        
        <!-- 10. Test interactive elements -->
        <details>
            <summary>Additional Information</summary>
            <p>This content can be expanded or collapsed.</p>
        </details>
    </main>
    
    <!-- 11. Test footer navigation -->
    <footer>
        <nav aria-label="Footer navigation">
            <ul>
                <li><a href="/privacy">Privacy Policy</a></li>
                <li><a href="/terms">Terms of Service</a></li>
            </ul>
        </nav>
    </footer>
</body>
</html>
```

**Testing Methodology (Manual Testing Focus):**
```html
<!-- Create a testing checklist for manual validation -->
<div class="testing-checklist">
    <h2>Manual Accessibility Testing Checklist</h2>
    
    <section>
        <h3>Keyboard Navigation Tests</h3>
        <ul>
            <li>Can you reach all interactive elements using only Tab and Shift+Tab?</li>
            <li>Is the tab order logical and predictable?</li>
            <li>Are focus indicators clearly visible?</li>
            <li>Can you activate buttons and links using Enter or Space?</li>
            <li>Are there any keyboard traps?</li>
        </ul>
    </section>
    
    <section>
        <h3>Screen Reader Tests</h3>
        <ul>
            <li>Does the page title clearly describe the page content?</li>
            <li>Can you navigate by headings in a logical order?</li>
            <li>Are all images described appropriately?</li>
            <li>Are form fields properly labeled?</li>
            <li>Can you navigate by landmarks?</li>
        </ul>
    </section>
    
    <section>
        <h3>Visual Tests</h3>
        <ul>
            <li>Does text maintain readability at 200% zoom?</li>
            <li>Is information conveyed without relying on color alone?</li>
            <li>Do focus indicators meet visibility requirements?</li>
            <li>Is there sufficient color contrast?</li>
        </ul>
    </section>
</div>

<!-- Example of accessible content structure for testing -->
<article>
    <header>
        <h1>Accessibility Testing Best Practices</h1>
        <p class="meta">Published on <time datetime="2024-01-15">January 15, 2024</time></p>
    </header>
    
    <section>
        <h2>Introduction</h2>
        <p>Testing for accessibility requires both automated tools and manual verification...</p>
        
        <figure>
            <img src="testing-process.jpg" alt="Flowchart showing accessibility testing process: automated scan, manual review, user testing, and remediation">
            <figcaption>The complete accessibility testing workflow</figcaption>
        </figure>
    </section>
    
    <section>
        <h2>Testing Methods</h2>
        <h3>Automated Testing</h3>
        <p>Automated tools can identify many accessibility issues quickly...</p>
        
        <h3>Manual Testing</h3>
        <p>Manual testing is essential for evaluating user experience...</p>
    </section>
</article>
```

**Resources:**
- **WebAIM NVDA Guide**: [Using NVDA to Evaluate Web Accessibility](https://webaim.org/articles/nvda/)

---

## Accessibility Testing Tools

### Automated Testing Tools

**axe-core Integration (Basic HTML Setup):**
```html
<!-- Include axe-core for automated testing -->
<script src="https://cdnjs.cloudflare.com/ajax/libs/axe-core/4.7.2/axe.min.js"></script>

<!-- Basic page structure for axe testing -->
<main>
    <h1>axe Testing Page</h1>
    
    <!-- Good: Proper alt text -->
    <img src="example.jpg" alt="Example image demonstrating proper alt text">
    
    <!-- Bad: Missing alt text (axe will flag this) -->
    <!-- <img src="bad-example.jpg"> -->
    
    <!-- Good: Proper form labels -->
    <form>
        <label for="name">Name</label>
        <input type="text" id="name" name="name">
        
        <!-- Bad: Missing label (axe will flag this) -->
        <!-- <input type="email" placeholder="Email"> -->
        
        <button type="submit">Submit</button>
    </form>
    
    <!-- Good: Proper heading hierarchy -->
    <h2>Section Heading</h2>
    <h3>Subsection Heading</h3>
    
    <!-- Bad: Skipped heading level (axe will flag this) -->
    <!-- <h5>Improperly nested heading</h5> -->
</main>

<!-- Note: To run axe tests, use browser developer tools console:
     axe.run().then(results => console.log(results)); -->
```

**WAVE (Web Accessibility Evaluation Tool):**
```html
<!-- WAVE-friendly markup -->
<main>
    <h1>WAVE Testing Page</h1>
    
    <!-- WAVE will flag missing alt text -->
    <img src="example.jpg" alt="Example image with proper alt text">
    
    <!-- WAVE will flag empty links -->
    <a href="/valid-link">Descriptive link text</a>
    
    <!-- WAVE will verify form labels -->
    <form>
        <label for="name">Name</label>
        <input type="text" id="name" name="name">
        
        <!-- WAVE checks color contrast -->
        <button type="submit" style="background: #0066cc; color: white; border: none; padding: 8px 16px;">
            Submit Form
        </button>
    </form>
    
    <!-- WAVE identifies heading structure -->
    <h2>Section Heading</h2>
    <h3>Subsection Heading</h3>
</main>
```

**Lighthouse Accessibility Audit:**
```html
<!-- Lighthouse-optimized page structure -->
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Lighthouse Accessibility Test Page</title>
</head>
<body>
    <main>
        <h1>Page Title</h1>
        
        <!-- Lighthouse checks for proper contrast -->
        <p style="color: #333; background: #fff;">
            Text with sufficient contrast ratio
        </p>
        
        <!-- Lighthouse verifies form accessibility -->
        <form>
            <label for="email">Email Address</label>
            <input type="email" id="email" name="email" required>
            <button type="submit">Submit</button>
        </form>
        
        <!-- Lighthouse checks image alt text -->
        <img src="chart.jpg" alt="Sales data showing quarterly growth">
        
        <!-- Lighthouse verifies heading structure -->
        <h2>Section Title</h2>
        <h3>Subsection Title</h3>
    </main>
</body>
</html>

<!-- 
To run Lighthouse:
1. Open Chrome DevTools (F12)
2. Go to Lighthouse tab
3. Select "Accessibility" category
4. Click "Generate report"
-->
```

#### Browser Extensions and Bookmarklets

**Accessibility Insights Testing:**
```html
<!-- Test page optimized for Accessibility Insights -->
<html lang="en">
<head>
    <title>Accessibility Insights Test Page</title>
    <meta name="viewport" content="width=device-width, initial-scale=1">
</head>
<body>
    <!-- FastPass checks -->
    <main>
        <h1>Page Title</h1> <!-- Automated checks: heading order -->
        
        <a href="#main-content" class="skip-link">Skip to main content</a>
        
        <nav aria-label="Main navigation">
            <ul>
                <li><a href="/">Home</a></li>
                <li><a href="/about">About</a></li>
            </ul>
        </nav>
        
        <div id="main-content">
            <button>Open Dialog</button> <!-- Tab stops check -->
            
            <img src="chart.jpg" alt="Sales data showing 25% increase"> <!-- Alt text check -->
            
            <!-- Color contrast check -->
            <p style="color: #666666; background: white;">
                This text should have sufficient contrast (4.5:1 ratio for normal text)
            </p>
            
            <form>
                <label for="email">Email Address</label>
                <input type="email" id="email" name="email" required>
                <button type="submit">Submit</button>
            </form>
        </div>
    </main>
    
    <!-- Modal structure for manual assessment -->
    <div role="dialog" aria-labelledby="dialog-title" aria-modal="true" hidden>
        <h2 id="dialog-title">Confirmation Dialog</h2>
        <p>Are you sure you want to continue?</p>
        <button>Yes</button>
        <button>No</button>
    </div>
</body>
</html>
```

**Manual Testing with Browser Extensions:**
```html
<!-- Structure optimized for manual testing -->
<article>
    <header>
        <h1>Article Title</h1>
        <p class="byline">By Author Name</p>
        <time datetime="2024-01-15">January 15, 2024</time>
    </header>
    
    <section>
        <h2>Introduction</h2>
        <p>This content can be tested with various browser extensions...</p>
        
        <!-- Test color contrast -->
        <p style="color: #767676; background: #ffffff;">
            This text has a 4.54:1 contrast ratio (WCAG AA compliant)
        </p>
        
        <!-- Test heading structure -->
        <h3>Subsection</h3>
        <p>Content under the subsection...</p>
        
        <!-- Test link context -->
        <p>
            For more information, visit our 
            <a href="/accessibility-guide">complete accessibility guide</a>.
        </p>
        
        <!-- Test form accessibility -->
        <form>
            <fieldset>
                <legend>Newsletter Signup</legend>
                <label for="newsletter-email">Email Address</label>
                <input type="email" id="newsletter-email" name="email" required>
                <button type="submit">Subscribe</button>
            </fieldset>
        </form>
    </section>
</article>
```

#### Manual Testing Checklists

**Comprehensive Accessibility Testing Checklist:**
```markdown
## Keyboard Navigation Testing
- [ ] All interactive elements are keyboard accessible
- [ ] Tab order is logical and predictable
- [ ] Focus indicators are visible
- [ ] No keyboard traps exist
- [ ] Skip links work properly
- [ ] Custom interactive elements handle keyboard events

## Screen Reader Testing
- [ ] Page title is descriptive and unique
- [ ] Heading structure is logical (h1-h6)
- [ ] All images have appropriate alt text
- [ ] Form labels are properly associated
- [ ] Tables have headers and captions
- [ ] Landmarks are properly identified
- [ ] Error messages are announced
- [ ] Dynamic content updates are announced

## Visual Design Testing
- [ ] Color contrast meets WCAG AA standards (4.5:1 normal, 3:1 large)
- [ ] Information is not conveyed by color alone
- [ ] Text can be resized to 200% without horizontal scrolling
- [ ] Content is readable and functional at high zoom levels
- [ ] Focus indicators are visible and clear

## Content Testing
- [ ] Language is identified in HTML
- [ ] Page structure is logical without CSS
- [ ] Links have descriptive text
- [ ] Instructions are clear and complete
- [ ] Error messages are helpful and specific
```

#### Color Contrast Analyzers

**Manual Color Contrast Checking:**
```html
<!-- Examples of different contrast ratios for manual testing -->
<div class="contrast-examples">
    <h2>Color Contrast Examples</h2>
    
    <!-- WCAG AA Compliant (4.5:1) -->
    <p style="color: #333333; background: #ffffff;">
        This text has excellent contrast (12.63:1 ratio)
    </p>
    
    <!-- WCAG AA Compliant - Minimum (4.5:1) -->
    <p style="color: #767676; background: #ffffff;">
        This text meets WCAG AA standard (4.54:1 ratio)
    </p>
    
    <!-- WCAG AA Large Text (3:1) -->
    <p style="color: #949494; background: #ffffff; font-size: 18px; font-weight: bold;">
        Large text can have lower contrast (3.28:1 ratio)
    </p>
    
    <!-- Failing contrast - for testing purposes -->
    <!-- <p style="color: #cccccc; background: #ffffff;">
        This text fails WCAG standards (1.61:1 ratio)
    </p> -->
</div>

<!-- Test form with proper contrast -->
<form style="background: #f8f9fa; padding: 1rem; border: 1px solid #dee2e6;">
    <fieldset>
        <legend style="color: #212529;">Contact Form</legend>
        
        <label for="name" style="color: #495057; font-weight: 600;">
            Name (required)
        </label>
        <input type="text" id="name" name="name" required
               style="border: 2px solid #ced4da; color: #495057;">
        
        <label for="message" style="color: #495057; font-weight: 600;">
            Message
        </label>
        <textarea id="message" name="message" rows="4"
                  style="border: 2px solid #ced4da; color: #495057;"></textarea>
        
        <button type="submit" 
                style="background: #007bff; color: #ffffff; border: none; padding: 0.5rem 1rem;">
            Send Message (7.22:1 contrast ratio)
        </button>
    </fieldset>
</form>
```

**CSS for High Contrast Support:**
```css
/* Support for Windows High Contrast Mode */
@media (prefers-contrast: high) {
    .button {
        border: 2px solid ButtonText;
        background: ButtonFace;
        color: ButtonText;
    }
    
    .button:focus {
        outline: 3px solid Highlight;
        outline-offset: 2px;
    }
    
    .link {
        color: LinkText;
        text-decoration: underline;
    }
    
    .visited-link {
        color: VisitedText;
    }
}

/* Custom high contrast styles */
.high-contrast {
    --text-color: #000000;
    --background-color: #ffffff;
    --link-color: #0000ff;
    --border-color: #000000;
}

.high-contrast * {
    color: var(--text-color) !important;
    background-color: var(--background-color) !important;
    border-color: var(--border-color) !important;
}

.high-contrast a {
    color: var(--link-color) !important;
    text-decoration: underline !important;
}

/* Ensure focus indicators are visible */
button:focus,
a:focus,
input:focus,
select:focus,
textarea:focus {
    outline: 2px solid #005fcc;
    outline-offset: 2px;
}

/* High contrast focus indicators */
@media (prefers-contrast: high) {
    button:focus,
    a:focus,
    input:focus,
    select:focus,
    textarea:focus {
        outline: 3px solid Highlight;
        outline-offset: 2px;
    }
}
```

**Accessibility Testing Integration:**
```html
<!-- Example: Well-structured, testable component -->
<section aria-labelledby="newsletter-heading">
    <h2 id="newsletter-heading">Subscribe to Newsletter</h2>
    <form>
        <div class="field-group">
            <label for="subscriber-email">Email Address</label>
            <input type="email" id="subscriber-email" name="email" 
                   required aria-describedby="email-hint">
            <div id="email-hint">We respect your privacy</div>
        </div>
        <button type="submit">Subscribe</button>
    </form>
</section>
```

**Resources:**
- **WebAIM Contrast Checker**: [Color Contrast Checker](https://webaim.org/resources/contrastchecker/)

---

## Mobile Accessibility Testing

### Touch and Gesture Accessibility

**Touch Target Size Requirements:**
```html
<!-- Minimum 44x44 pixel touch targets -->
<style>
.touch-target {
    min-height: 44px;
    min-width: 44px;
    padding: 12px;
    margin: 4px;
    border: none;
    background: #0066cc;
    color: white;
    border-radius: 4px;
    cursor: pointer;
}

.touch-target:focus {
    outline: 2px solid #ffffff;
    outline-offset: 2px;
}

/* Ensure adequate spacing between touch targets */
.button-group {
    display: flex;
    gap: 8px;
    flex-wrap: wrap;
}

@media (max-width: 768px) {
    .button-group {
        flex-direction: column;
        align-items: stretch;
    }
    
    .touch-target {
        min-height: 48px; /* Larger on mobile */
    }
}
</style>

<div class="button-group">
    <button class="touch-target">Primary Action</button>
    <button class="touch-target">Secondary Action</button>
    <button class="touch-target">Cancel</button>
</div>

<!-- Form controls with adequate touch targets -->
<form>
    <div class="form-group">
        <label for="mobile-email">Email Address</label>
        <input type="email" id="mobile-email" name="email" 
               style="min-height: 44px; padding: 12px; font-size: 16px;">
    </div>
    
    <div class="checkbox-group">
        <input type="checkbox" id="newsletter" name="newsletter" 
               style="width: 20px; height: 20px; margin-right: 12px;">
        <label for="newsletter" style="display: inline-block; padding: 12px 0;">
            Subscribe to newsletter
        </label>
    </div>
</form>
```

### Mobile Screen Reader Testing

**iOS VoiceOver Testing:**
```html
<!-- Optimize for iOS VoiceOver -->
<main>
    <h1>Mobile Accessibility Test</h1>
    
    <!-- VoiceOver gesture navigation -->
    <nav aria-label="Main navigation">
        <ul>
            <li><a href="/">Home</a></li>
            <li><a href="/products">Products</a></li>
            <li><a href="/contact">Contact</a></li>
        </ul>
    </nav>
    
    <!-- Swipe gestures work with proper semantics -->
    <article>
        <h2>Article Title</h2>
        <p>Content that can be navigated with swipe gestures...</p>
        
        <!-- Custom controls need proper labels -->
        <div role="slider" 
             aria-label="Volume control" 
             aria-valuemin="0" 
             aria-valuemax="100" 
             aria-valuenow="50"
             tabindex="0">
            <div class="slider-track">
                <div class="slider-thumb" style="left: 50%"></div>
            </div>
        </div>
    </article>
    
    <!-- Form optimization for mobile -->
    <form>
        <fieldset>
            <legend>Mobile Contact Form</legend>
            
            <label for="phone">Phone Number</label>
            <input type="tel" id="phone" name="phone" 
                   autocomplete="tel"
                   inputmode="tel">
            
            <label for="mobile-message">Message</label>
            <textarea id="mobile-message" name="message" 
                      rows="4"
                      aria-describedby="char-count"></textarea>
            <div id="char-count">0/500 characters</div>
        </fieldset>
    </form>
</main>
```

**Android TalkBack Testing:**
```html
<!-- Android TalkBack optimizations -->
<div class="mobile-card">
    <h3>Product Card</h3>
    
    <!-- TalkBack reads content in reading order -->
    <img src="product.jpg" alt="Wireless headphones in black color">
    
    <div class="product-info">
        <h4>Wireless Headphones</h4>
        <p class="price" aria-label="Price: 99 dollars and 99 cents">$99.99</p>
        <p class="rating">
            <span aria-label="Rating: 4.5 out of 5 stars">★★★★☆</span>
            <span class="sr-only">4.5 out of 5 stars</span>
        </p>
    </div>
    
    <!-- Group related actions -->
    <div class="product-actions" role="group" aria-label="Product actions">
        <button>Add to Cart</button>
        <button>Add to Wishlist</button>
        <button aria-expanded="false" aria-controls="product-details">
            More Details
        </button>
    </div>
    
    <div id="product-details" hidden>
        <h5>Product Details</h5>
        <ul>
            <li>Wireless Bluetooth 5.0</li>
            <li>30-hour battery life</li>
            <li>Noise cancellation</li>
        </ul>
    </div>
</div>

<style>
.mobile-card {
    border: 1px solid #dee2e6;
    border-radius: 8px;
    padding: 1rem;
    margin: 1rem 0;
    max-width: 400px;
}

.product-actions {
    display: flex;
    gap: 0.5rem;
    margin-top: 1rem;
}

.product-actions button {
    flex: 1;
    min-height: 44px;
    padding: 0.75rem;
    border: 1px solid #0066cc;
    background: white;
    color: #0066cc;
    border-radius: 4px;
    cursor: pointer;
}

.product-actions button:focus {
    outline: 2px solid #0066cc;
    outline-offset: 2px;
}

.sr-only {
    position: absolute;
    width: 1px;
    height: 1px;
    padding: 0;
    margin: -1px;
    overflow: hidden;
    clip: rect(0, 0, 0, 0);
    white-space: nowrap;
    border: 0;
}

@media (max-width: 768px) {
    .product-actions {
        flex-direction: column;
    }
    
    .product-actions button {
        min-height: 48px;
    }
}
</style>
```

---

## Advanced Testing Scenarios

### Testing Complex Interactions

**Multi-Step Process Testing:**
```html
<!-- Test complex workflows -->
<div class="checkout-process">
    <nav aria-label="Checkout progress">
        <ol class="progress-steps">
            <li class="step completed">
                <span class="step-number">1</span>
                <span class="step-label">Cart Review</span>
            </li>
            <li class="step current">
                <span class="step-number">2</span>
                <span class="step-label">Shipping Info</span>
            </li>
            <li class="step">
                <span class="step-number">3</span>
                <span class="step-label">Payment</span>
            </li>
        </ol>
    </nav>
    
    <main>
        <h1>Shipping Information</h1>
        
        <form>
            <fieldset>
                <legend>Delivery Address</legend>
                
                <div class="form-row">
                    <div class="form-group">
                        <label for="first-name">First Name</label>
                        <input type="text" id="first-name" name="firstName" 
                               required autocomplete="given-name">
                    </div>
                    
                    <div class="form-group">
                        <label for="last-name">Last Name</label>
                        <input type="text" id="last-name" name="lastName" 
                               required autocomplete="family-name">
                    </div>
                </div>
                
                <div class="form-group">
                    <label for="address">Street Address</label>
                    <input type="text" id="address" name="address" 
                           required autocomplete="street-address">
                </div>
                
                <div class="form-row">
                    <div class="form-group">
                        <label for="city">City</label>
                        <input type="text" id="city" name="city" 
                               required autocomplete="address-level2">
                    </div>
                    
                    <div class="form-group">
                        <label for="state">State</label>
                        <select id="state" name="state" required autocomplete="address-level1">
                            <option value="">Select State</option>
                            <option value="CA">California</option>
                            <option value="NY">New York</option>
                            <option value="TX">Texas</option>
                        </select>
                    </div>
                    
                    <div class="form-group">
                        <label for="zip">ZIP Code</label>
                        <input type="text" id="zip" name="zip" 
                               required autocomplete="postal-code"
                               pattern="[0-9]{5}(-[0-9]{4})?">
                    </div>
                </div>
            </fieldset>
            
            <div class="form-actions">
                <a href="/checkout/cart" class="btn btn-secondary">Back to Cart</a>
                <button type="submit" class="btn btn-primary">Continue to Payment</button>
            </div>
        </form>
    </main>
</div>

<style>
.checkout-process {
    max-width: 800px;
    margin: 0 auto;
    padding: 2rem;
}

.progress-steps {
    display: flex;
    list-style: none;
    padding: 0;
    margin: 0 0 2rem 0;
    counter-reset: step;
}

.step {
    flex: 1;
    text-align: center;
    position: relative;
}

.step:not(:last-child)::after {
    content: '';
    position: absolute;
    top: 20px;
    right: -50%;
    width: 100%;
    height: 2px;
    background: #dee2e6;
    z-index: 1;
}

.step.completed::after {
    background: #28a745;
}

.step-number {
    display: inline-flex;
    align-items: center;
    justify-content: center;
    width: 40px;
    height: 40px;
    border-radius: 50%;
    background: #dee2e6;
    color: #6c757d;
    font-weight: bold;
    position: relative;
    z-index: 2;
}

.step.completed .step-number {
    background: #28a745;
    color: white;
}

.step.current .step-number {
    background: #0066cc;
    color: white;
}

.step-label {
    display: block;
    margin-top: 0.5rem;
    font-size: 0.875rem;
    color: #6c757d;
}

.step.current .step-label {
    color: #0066cc;
    font-weight: 600;
}

.form-row {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 1rem;
}

.form-row.three-col {
    grid-template-columns: 1fr 1fr 1fr;
}

@media (max-width: 768px) {
    .form-row {
        grid-template-columns: 1fr;
    }
    
    .progress-steps {
        flex-direction: column;
        gap: 1rem;
    }
    
    .step::after {
        display: none;
    }
}
</style>
```

### Error State Testing

**Comprehensive Error Handling:**
```html
<!-- Test error states and recovery -->
<form class="error-testing-form">
    <h2>Error State Testing Form</h2>
    
    <!-- Global form errors -->
    <div role="alert" class="alert alert-error" id="form-errors">
        <h3>Please correct the following errors:</h3>
        <ul>
            <li><a href="#email-field">Email address is required</a></li>
            <li><a href="#password-field">Password must be at least 8 characters</a></li>
        </ul>
    </div>
    
    <fieldset>
        <legend>Account Information</legend>
        
        <!-- Field with error -->
        <div class="form-group error">
            <label for="email-field">
                Email Address
                <span class="required">*</span>
            </label>
            <input type="email" 
                   id="email-field" 
                   name="email" 
                   aria-invalid="true"
                   aria-describedby="email-error"
                   class="error">
            <div id="email-error" class="error-message" role="alert">
                <strong>Error:</strong> Please enter a valid email address
            </div>
        </div>
        
        <!-- Field with warning -->
        <div class="form-group warning">
            <label for="username-field">
                Username
                <span class="required">*</span>
            </label>
            <input type="text" 
                   id="username-field" 
                   name="username" 
                   value="user123"
                   aria-describedby="username-warning">
            <div id="username-warning" class="warning-message" role="alert">
                <strong>Warning:</strong> This username is already taken. Try "user123_alt"
            </div>
        </div>
        
        <!-- Field with success state -->
        <div class="form-group success">
            <label for="password-field">
                Password
                <span class="required">*</span>
            </label>
            <input type="password" 
                   id="password-field" 
                   name="password" 
                   value="securepass123"
                   aria-describedby="password-success">
            <div id="password-success" class="success-message">
                <strong>Success:</strong> Password meets all requirements
            </div>
        </div>
    </fieldset>
    
    <div class="form-actions">
        <button type="submit" disabled>Create Account</button>
        <p class="form-note">Please correct all errors before submitting</p>
    </div>
</form>

<style>
.error-testing-form {
    max-width: 600px;
    margin: 2rem auto;
    padding: 2rem;
}

.alert {
    padding: 1rem;
    margin-bottom: 1.5rem;
    border-radius: 4px;
    border: 1px solid transparent;
}

.alert-error {
    background-color: #f8d7da;
    border-color: #f5c6cb;
    color: #721c24;
}

.alert h3 {
    margin: 0 0 0.5rem 0;
    font-size: 1rem;
}

.alert ul {
    margin: 0;
    padding-left: 1.5rem;
}

.alert a {
    color: #721c24;
    text-decoration: underline;
}

.form-group {
    margin-bottom: 1.5rem;
}

.form-group.error input {
    border-color: #dc3545;
    background-color: #fff5f5;
}

.form-group.warning input {
    border-color: #ffc107;
    background-color: #fffef5;
}

.form-group.success input {
    border-color: #28a745;
    background-color: #f8fff8;
}

.error-message {
    color: #dc3545;
    font-size: 0.875rem;
    margin-top: 0.25rem;
    padding: 0.5rem;
    background-color: #f8d7da;
    border-radius: 4px;
    border: 1px solid #f5c6cb;
}

.warning-message {
    color: #856404;
    font-size: 0.875rem;
    margin-top: 0.25rem;
    padding: 0.5rem;
    background-color: #fff3cd;
    border-radius: 4px;
    border: 1px solid #ffeaa7;
}

.success-message {
    color: #155724;
    font-size: 0.875rem;
    margin-top: 0.25rem;
    padding: 0.5rem;
    background-color: #d4edda;
    border-radius: 4px;
    border: 1px solid #c3e6cb;
}

.form-note {
    font-size: 0.875rem;
    color: #6c757d;
    margin: 0.5rem 0 0 0;
}

button:disabled {
    background-color: #6c757d;
    cursor: not-allowed;
    opacity: 0.6;
}
</style>
```

---

## Performance and Accessibility

### Testing with Slow Connections

**Progressive Enhancement Testing:**
```html
<!-- Test content loading states -->
<article class="progressive-content">
    <header>
        <h1>Article Title</h1>
        <p class="loading-state" aria-live="polite">Loading content...</p>
    </header>
    
    <!-- Core content loads first -->
    <section class="core-content">
        <h2>Essential Information</h2>
        <p>This critical content loads immediately and works without CSS or JavaScript.</p>
        
        <noscript>
            <div class="fallback-notice">
                <p>This site works best with JavaScript enabled, but all core functionality is available without it.</p>
            </div>
        </noscript>
    </section>
    
    <!-- Enhanced content loads progressively -->
    <section class="enhanced-content" hidden>
        <h2>Enhanced Features</h2>
        <p>This content enhances the experience but isn't essential.</p>
    </section>
    
    <!-- Fallback for slow/failed loading -->
    <div class="offline-message" role="alert" hidden>
        <h3>Connection Issue</h3>
        <p>Some content couldn't load. You can still access the core features.</p>
        <button onclick="location.reload()">Try Again</button>
    </div>
</article>

<style>
/* Critical CSS loaded inline */
.progressive-content {
    max-width: 800px;
    margin: 0 auto;
    padding: 1rem;
    font-family: system-ui, sans-serif;
    line-height: 1.6;
}

.loading-state {
    color: #6c757d;
    font-style: italic;
}

.fallback-notice {
    background: #fff3cd;
    border: 1px solid #ffeaa7;
    border-radius: 4px;
    padding: 1rem;
    margin: 1rem 0;
}

.offline-message {
    background: #f8d7da;
    border: 1px solid #f5c6cb;
    border-radius: 4px;
    padding: 1rem;
    margin: 1rem 0;
    text-align: center;
}

/* Non-critical CSS can be loaded asynchronously */
.enhanced-content {
    background: #e3f2fd;
    padding: 1.5rem;
    border-radius: 8px;
    margin: 1rem 0;
}

/* Ensure content is readable without custom fonts */
body {
    font-family: system-ui, -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
}
</style>
```

### Testing with Reduced Motion

**Motion-Sensitive Design:**
```html
<!-- Respect user motion preferences -->
<div class="motion-example">
    <h2>Animation Example</h2>
    
    <div class="animated-card">
        <h3>Hover to See Animation</h3>
        <p>This card has subtle animation that respects user preferences.</p>
    </div>
    
    <button class="animated-button">Click Me</button>
</div>

<style>
/* Animations with reduced motion support */
.animated-card {
    background: white;
    border: 1px solid #dee2e6;
    border-radius: 8px;
    padding: 1.5rem;
    margin: 1rem 0;
    transition: transform 0.3s ease, box-shadow 0.3s ease;
}

.animated-card:hover {
    transform: translateY(-4px);
    box-shadow: 0 8px 16px rgba(0,0,0,0.1);
}

.animated-button {
    background: #0066cc;
    color: white;
    border: none;
    padding: 1rem 2rem;
    border-radius: 4px;
    cursor: pointer;
    transition: background-color 0.3s ease;
}

.animated-button:hover {
    background: #0052a3;
}

.animated-button:focus {
    outline: 2px solid #0066cc;
    outline-offset: 2px;
}

/* Respect reduced motion preferences */
@media (prefers-reduced-motion: reduce) {
    .animated-card {
        transition: none;
    }
    
    .animated-card:hover {
        transform: none;
        /* Keep box-shadow for visual feedback */
        box-shadow: 0 0 0 2px #0066cc;
    }
    
    .animated-button {
        transition: none;
    }
    
    /* Provide alternative feedback for reduced motion */
    .animated-button:hover {
        outline: 2px solid #ffffff;
        outline-offset: -2px;
    }
}

/* Essential animations that convey important information */
@media (prefers-reduced-motion: reduce) {
    /* Keep focus transitions as they're important for accessibility */
    *:focus {
        transition: outline 0.1s ease;
    }
    
    /* Keep loading indicators */
    .loading-spinner {
        animation: spin 2s linear infinite;
    }
}

@keyframes spin {
    from { transform: rotate(0deg); }
    to { transform: rotate(360deg); }
}
</style>
```

---

### Task 2
1. Install and configure at least two different screen readers on your development system
2. Complete a full screen reader test of a complex website (e.g., an e-commerce site)
3. Use automated testing tools (axe, WAVE, Lighthouse) to audit the same website
4. Create a comprehensive test report comparing automated vs manual testing findings

### Task 3 (Advanced Testing)
1. Set up automated accessibility testing in a development workflow
2. Create custom accessibility testing scripts for your specific use cases
3. Test your website with high contrast mode and 200% zoom
4. Document testing procedures for your team

---

## Assessment Checklist

Before moving to the next module, ensure you can:
- [ ] Use multiple screen readers effectively for testing
- [ ] Navigate websites using only assistive technologies
- [ ] Set up and use automated accessibility testing tools
- [ ] Perform manual accessibility audits with checklists
- [ ] Understand the limitations of automated testing
- [ ] Create comprehensive accessibility test reports
- [ ] Identify and prioritize accessibility issues
- [ ] Test mobile accessibility with touch and gesture interfaces
- [ ] Evaluate complex user workflows for accessibility barriers
- [ ] Test performance and progressive enhancement scenarios

<!-- ---

## Next Steps

Once you've mastered assistive technologies and testing, you'll move on to [Part 4: Common Patterns and Advanced Topics](4_common-patterns-and-advanced-topics.md) where you'll learn to implement accessible solutions for complex UI patterns using HTML and CSS techniques. -->