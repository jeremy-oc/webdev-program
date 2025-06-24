# Part 2: Semantic HTML and ARIA

## Semantic HTML for Accessibility

### The Importance of Semantic Markup

Semantic HTML uses elements that convey meaning about the content's structure and purpose, not just its appearance. This is crucial for accessibility because screen readers and other assistive technologies rely on semantic information to help users navigate and understand web content.

#### Key Concepts:
- Semantic elements describe the content's meaning and structure
- Screen readers use semantic information for navigation
- Proper semantics improve SEO and code maintainability
- Semantic markup provides context for all users
- It creates a logical document outline

#### Getting Started:
This section covers semantic HTML implementation and ARIA (Accessible Rich Internet Applications) attributes for enhanced accessibility.

For learning semantic HTML and ARIA, we will use resources from [WebAIM](https://webaim.org/), [MDN Web Docs](https://developer.mozilla.org/), and the [W3C WAI-ARIA Authoring Practices](https://www.w3.org/WAI/ARIA/apg/).

### Task 1
1. Read through [WebAIM's Semantic Structure](https://webaim.org/techniques/semanticstructure/) guide
2. Complete the [MDN HTML Semantics](https://developer.mozilla.org/en-US/docs/Glossary/Semantics#semantics_in_html) tutorial
3. Study the [WAI-ARIA Authoring Practices Guide](https://www.w3.org/WAI/ARIA/apg/)
4. Test semantic markup with a screen reader to understand the user experience

### Recap of the Content

Understanding semantic HTML and ARIA is essential for creating accessible web experiences. These technologies work together to provide meaning and context to assistive technologies.

#### Proper Heading Structure and Navigation

**Logical Heading Hierarchy:**
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <title>Company Blog - Accessibility Best Practices</title>
</head>
<body>
    <header>
        <h1>Company Blog</h1> <!-- Page title -->
        <nav aria-label="Main navigation">
            <ul>
                <li><a href="/">Home</a></li>
                <li><a href="/articles">Articles</a></li>
                <li><a href="/about">About</a></li>
            </ul>
        </nav>
    </header>
    
    <main>
        <article>
            <h2>Accessibility Best Practices</h2> <!-- Article title -->
            
            <section>
                <h3>Getting Started</h3> <!-- Section heading -->
                <p>Content about getting started...</p>
                
                <h4>Installation</h4> <!-- Subsection heading -->
                <p>Installation instructions...</p>
                
                <h4>Configuration</h4> <!-- Another subsection -->
                <p>Configuration details...</p>
            </section>
            
            <section>
                <h3>Advanced Topics</h3> <!-- Another main section -->
                <p>Advanced content...</p>
            </section>
        </article>
    </main>
</body>
</html>
```

**Heading Best Practices:**
- Use only one `<h1>` per page (the main page title)
- Don't skip heading levels (h1 → h2 → h3, not h1 → h3)
- Use headings for structure, not for styling
- Make headings descriptive and meaningful

**Screen Reader Navigation:**
```html
<!-- Screen readers can jump between headings -->
<h2 id="overview">Overview</h2>
<h2 id="features">Key Features</h2>
<h2 id="installation">Installation Guide</h2>

<!-- Users can also navigate by landmarks -->
<nav aria-label="Article sections">
    <ul>
        <li><a href="#overview">Overview</a></li>
        <li><a href="#features">Key Features</a></li>
        <li><a href="#installation">Installation Guide</a></li>
    </ul>
</nav>
```

#### Form Labels and Fieldsets

**Proper Form Labeling:**
```html
<form>
    <fieldset>
        <legend>Personal Information</legend>
        
        <div class="form-group">
            <label for="first-name">First Name (required)</label>
            <input type="text" id="first-name" name="firstName" required>
        </div>
        
        <div class="form-group">
            <label for="last-name">Last Name (required)</label>
            <input type="text" id="last-name" name="lastName" required>
        </div>
        
        <div class="form-group">
            <label for="email">Email Address</label>
            <input type="email" id="email" name="email" 
                   aria-describedby="email-help">
            <div id="email-help">We'll never share your email</div>
        </div>
    </fieldset>
    
    <fieldset>
        <legend>Preferences</legend>
        
        <div class="checkbox-group">
            <input type="checkbox" id="newsletter" name="newsletter">
            <label for="newsletter">Subscribe to newsletter</label>
        </div>
        
        <div class="radio-group">
            <fieldset>
                <legend>Communication preference</legend>
                <input type="radio" id="email-pref" name="communication" value="email">
                <label for="email-pref">Email</label>
                
                <input type="radio" id="phone-pref" name="communication" value="phone">
                <label for="phone-pref">Phone</label>
                
                <input type="radio" id="none-pref" name="communication" value="none">
                <label for="none-pref">No contact</label>
            </fieldset>
        </div>
    </fieldset>
    
    <button type="submit">Submit Form</button>
</form>
```

**Form Accessibility Features:**
- Every input has an associated label
- Related inputs are grouped with fieldset/legend
- Additional instructions use aria-describedby
- Required fields are clearly marked

#### Table Headers and Captions

**Accessible Data Tables:**
```html
<table>
    <caption>
        Quarterly Sales Report 2024
        <details>
            <summary>Table Description</summary>
            <p>This table shows sales figures for each quarter of 2024, 
               broken down by product category.</p>
        </details>
    </caption>
    
    <thead>
        <tr>
            <th scope="col">Product</th>
            <th scope="col">Q1 Sales</th>
            <th scope="col">Q2 Sales</th>
            <th scope="col">Q3 Sales</th>
            <th scope="col">Q4 Sales</th>
            <th scope="col">Total</th>
        </tr>
    </thead>
    
    <tbody>
        <tr>
            <th scope="row">Laptops</th>
            <td>$125,000</td>
            <td>$150,000</td>
            <td>$175,000</td>
            <td>$200,000</td>
            <td>$650,000</td>
        </tr>
        <tr>
            <th scope="row">Desktops</th>
            <td>$75,000</td>
            <td>$80,000</td>
            <td>$85,000</td>
            <td>$90,000</td>
            <td>$330,000</td>
        </tr>
        <tr>
            <th scope="row">Tablets</th>
            <td>$50,000</td>
            <td>$60,000</td>
            <td>$70,000</td>
            <td>$80,000</td>
            <td>$260,000</td>
        </tr>
    </tbody>
    
    <tfoot>
        <tr>
            <th scope="row">Total</th>
            <td>$250,000</td>
            <td>$290,000</td>
            <td>$330,000</td>
            <td>$370,000</td>
            <td>$1,240,000</td>
        </tr>
    </tfoot>
</table>
```

**Complex Table with Headers:**
```html
<table>
    <caption>Employee Schedule - Week of January 15, 2024</caption>
    <thead>
        <tr>
            <th scope="col">Employee</th>
            <th scope="col">Monday</th>
            <th scope="col">Tuesday</th>
            <th scope="col">Wednesday</th>
            <th scope="col">Thursday</th>
            <th scope="col">Friday</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <th scope="row">John Smith</th>
            <td headers="john monday">9:00 AM - 5:00 PM</td>
            <td headers="john tuesday">9:00 AM - 5:00 PM</td>
            <td headers="john wednesday">Off</td>
            <td headers="john thursday">9:00 AM - 5:00 PM</td>
            <td headers="john friday">9:00 AM - 3:00 PM</td>
        </tr>
    </tbody>
</table>
```

#### Landmark Elements and Page Structure

**Complete Landmark Structure:**
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <title>Accessible Website Example</title>
</head>
<body>
    <!-- Skip to main content link -->
    <a href="#main-content" class="skip-link">Skip to main content</a>
    
    <!-- Banner landmark -->
    <header role="banner">
        <div class="logo">
            <img src="logo.png" alt="Company Name">
        </div>
        
        <!-- Navigation landmark -->
        <nav role="navigation" aria-label="Main navigation">
            <ul>
                <li><a href="/" aria-current="page">Home</a></li>
                <li><a href="/about">About</a></li>
                <li><a href="/services">Services</a></li>
                <li><a href="/contact">Contact</a></li>
            </ul>
        </nav>
        
        <!-- Search landmark -->
        <search role="search">
            <form>
                <label for="site-search">Search this site</label>
                <input type="search" id="site-search" name="search">
                <button type="submit">Search</button>
            </form>
        </search>
    </header>
    
    <!-- Main landmark -->
    <main id="main-content" role="main">
        <h1>Page Title</h1>
        
        <section aria-labelledby="intro-heading">
            <h2 id="intro-heading">Introduction</h2>
            <p>Main content goes here...</p>
        </section>
        
        <section aria-labelledby="details-heading">
            <h2 id="details-heading">Details</h2>
            <article>
                <h3>Article Title</h3>
                <p>Article content...</p>
            </article>
        </section>
    </main>
    
    <!-- Complementary landmark -->
    <aside role="complementary" aria-labelledby="sidebar-heading">
        <h2 id="sidebar-heading">Related Information</h2>
        <nav aria-label="Related links">
            <ul>
                <li><a href="/related-page-1">Related Page 1</a></li>
                <li><a href="/related-page-2">Related Page 2</a></li>
            </ul>
        </nav>
    </aside>
    
    <!-- Content info landmark -->
    <footer role="contentinfo">
        <p>&copy; 2024 Company Name. All rights reserved.</p>
        
        <nav aria-label="Footer navigation">
            <ul>
                <li><a href="/privacy">Privacy Policy</a></li>
                <li><a href="/terms">Terms of Service</a></li>
                <li><a href="/accessibility">Accessibility Statement</a></li>
            </ul>
        </nav>
    </footer>
</body>
</html>
```

**Landmark Elements:**
- `<header>` or `role="banner"`: Site header
- `<nav>` or `role="navigation"`: Navigation sections
- `<main>` or `role="main"`: Main content area
- `<aside>` or `role="complementary"`: Sidebar content
- `<footer>` or `role="contentinfo"`: Site footer
- `<search>` or `role="search"`: Search functionality

**Resources:**
- **WebAIM Page Structure**: [Semantic Structure](https://webaim.org/techniques/semanticstructure/)
- **MDN HTML Sections**: [Using HTML sections and outlines](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/Heading_Elements)

---

## Introduction to ARIA

### What is ARIA and When to Use It

ARIA (Accessible Rich Internet Applications) provides semantic information about elements to assistive technologies when HTML semantics are insufficient.

**ARIA Rules:**
1. **First Rule**: Don't use ARIA if semantic HTML can do the job
2. **Don't change semantics** unless absolutely necessary
3. **All interactive elements must be keyboard accessible**
4. **Don't hide visible focus indicators**
5. **All interactive elements must have accessible names**

**When to Use ARIA:**
```html
<!-- Good: Use semantic HTML when possible -->
<button onclick="saveDocument()">Save</button>

<!-- Sometimes necessary: Custom components -->
<div role="button" tabindex="0" onclick="saveDocument()" 
     onkeydown="handleKeyPress(event)">
    Save Document
</div>

<!-- Bad: Unnecessary ARIA -->
<button role="button">Save</button> <!-- Button already has button role -->
```

#### ARIA Roles, Properties, and States

**ARIA Roles:**
```html
<!-- Widget roles -->
<div role="button" tabindex="0">Custom Button</div>
<div role="checkbox" aria-checked="false" tabindex="0">Custom Checkbox</div>
<div role="slider" aria-valuemin="0" aria-valuemax="100" aria-valuenow="50" tabindex="0">Volume</div>

<!-- Document structure roles -->
<div role="article">
    <div role="heading" aria-level="2">Article Title</div>
    <p>Article content...</p>
</div>

<!-- Landmark roles (use semantic HTML instead when possible) -->
<div role="navigation" aria-label="Breadcrumb">
    <ol>
        <li><a href="/">Home</a></li>
        <li><a href="/products">Products</a></li>
        <li aria-current="page">Laptops</li>
    </ol>
</div>
```

**ARIA Properties (describe relationships):**
```html
<!-- aria-labelledby: References other elements that label this element -->
<fieldset>
    <legend id="payment-methods">Payment Methods</legend>
    <div role="radiogroup" aria-labelledby="payment-methods">
        <input type="radio" id="credit-card" name="payment" value="credit">
        <label for="credit-card">Credit Card</label>
        
        <input type="radio" id="paypal" name="payment" value="paypal">
        <label for="paypal">PayPal</label>
    </div>
</fieldset>

<!-- aria-describedby: References elements that provide additional description -->
<label for="password">Password</label>
<input type="password" id="password" aria-describedby="pwd-help pwd-strength">
<div id="pwd-help">Must be at least 8 characters</div>
<div id="pwd-strength">Password strength: Medium</div>

<!-- aria-label: Provides accessible name when visible text isn't sufficient -->
<button aria-label="Close dialog">×</button>

<!-- aria-controls: Identifies elements controlled by this element -->
<button aria-expanded="false" aria-controls="menu-panel">Menu</button>
<div id="menu-panel" hidden>
    <ul>
        <li><a href="/home">Home</a></li>
        <li><a href="/about">About</a></li>
    </ul>
</div>
```

**ARIA States (describe current conditions):**
```html
<!-- aria-expanded: Whether a collapsible element is expanded -->
<button aria-expanded="false" aria-controls="submenu">
    Products
</button>
<ul id="submenu" hidden>
    <li><a href="/laptops">Laptops</a></li>
    <li><a href="/desktops">Desktops</a></li>
</ul>

<!-- aria-checked: State of checkboxes and radio buttons -->
<div role="checkbox" aria-checked="true" tabindex="0">
    Accept terms and conditions
</div>

<!-- aria-selected: Whether an option is selected -->
<ul role="listbox">
    <li role="option" aria-selected="true">Option 1</li>
    <li role="option" aria-selected="false">Option 2</li>
    <li role="option" aria-selected="false">Option 3</li>
</ul>

<!-- aria-invalid: Whether input value is invalid -->
<label for="email">Email Address</label>
<input type="email" id="email" aria-invalid="true" aria-describedby="email-error">
<div id="email-error" role="alert">Please enter a valid email address</div>
```

#### The First Rule of ARIA Usage

**Use Semantic HTML First:**
```html
<!-- GOOD: Semantic HTML -->
<button onclick="submit()">Submit Form</button>
<input type="checkbox" id="agree">
<label for="agree">I agree to the terms</label>

<!-- AVOID: Unnecessary ARIA -->
<div role="button" onclick="submit()" tabindex="0">Submit Form</div>
<div role="checkbox" aria-checked="false" onclick="toggle()" tabindex="0">I agree</div>
```

**When ARIA is Necessary:**
```html
<!-- Custom dropdown menu structure (without JavaScript functionality) -->
<div class="dropdown">
    <button aria-haspopup="true" aria-expanded="false" aria-controls="dropdown-menu">
        Select Option
    </button>
    <ul id="dropdown-menu" role="menu" hidden>
        <li role="menuitem"><a href="/option1">Option 1</a></li>
        <li role="menuitem"><a href="/option2">Option 2</a></li>
        <li role="menuitem"><a href="/option3">Option 3</a></li>
    </ul>
</div>

<!-- Progress indicator -->
<div role="progressbar" aria-valuemin="0" aria-valuemax="100" aria-valuenow="65" aria-label="Upload progress">
    <div class="progress-bar" style="width: 65%"></div>
</div>
```

#### ARIA Landmarks and Navigation

**ARIA Landmark Roles:**
```html
<!-- Main landmarks -->
<div role="banner">Site header content</div>
<div role="navigation" aria-label="Main menu">Navigation content</div>
<div role="main">Primary page content</div>
<div role="complementary" aria-label="Sidebar">Related content</div>
<div role="contentinfo">Footer content</div>

<!-- Multiple landmarks of same type need labels -->
<nav role="navigation" aria-label="Main navigation">
    <ul>
        <li><a href="/">Home</a></li>
        <li><a href="/about">About</a></li>
    </ul>
</nav>

<nav role="navigation" aria-label="Breadcrumb">
    <ol>
        <li><a href="/">Home</a></li>
        <li aria-current="page">Current Page</li>
    </ol>
</nav>

<nav role="navigation" aria-label="Footer links">
    <ul>
        <li><a href="/privacy">Privacy</a></li>
        <li><a href="/terms">Terms</a></li>
    </ul>
</nav>
```

**Search Landmark:**
```html
<!-- Dedicated search -->
<div role="search">
    <label for="site-search">Search this site</label>
    <input type="search" id="site-search">
    <button type="submit">Search</button>
</div>

<!-- Search within navigation -->
<nav aria-label="Site search and navigation">
    <div role="search">
        <label for="nav-search">Search</label>
        <input type="search" id="nav-search">
        <button type="submit">Go</button>
    </div>
    
    <ul>
        <li><a href="/">Home</a></li>
        <li><a href="/products">Products</a></li>
    </ul>
</nav>
```

**Resources:**
- **WAI-ARIA Authoring Practices**: [ARIA Authoring Practices Guide](https://www.w3.org/WAI/ARIA/apg/)
- **WebAIM ARIA**: [Introduction to ARIA](https://webaim.org/techniques/aria/)

---

## ARIA Implementation Techniques

### Labeling and Describing Elements

**Accessible Names and Descriptions:**
```html
<!-- Method 1: aria-label -->
<button aria-label="Close dialog">×</button>
<input type="search" aria-label="Search products">

<!-- Method 2: aria-labelledby (references other elements) -->
<h2 id="billing-title">Billing Address</h2>
<fieldset aria-labelledby="billing-title">
    <input type="text" placeholder="Street Address">
    <input type="text" placeholder="City">
</fieldset>

<!-- Method 3: aria-describedby (additional information) -->
<label for="username">Username</label>
<input type="text" id="username" aria-describedby="username-help username-format">
<div id="username-help">Your username will be visible to other users</div>
<div id="username-format">3-20 characters, letters and numbers only</div>

<!-- Complex example: Multiple labeling techniques -->
<section aria-labelledby="checkout-heading" aria-describedby="checkout-description">
    <h2 id="checkout-heading">Checkout</h2>
    <p id="checkout-description">Complete your purchase by providing payment information</p>
    
    <form>
        <fieldset aria-labelledby="payment-heading">
            <legend id="payment-heading">Payment Information</legend>
            
            <label for="card-number">Card Number</label>
            <input type="text" id="card-number" 
                   aria-describedby="card-help" 
                   aria-invalid="false">
            <div id="card-help">16-digit number on front of card</div>
        </fieldset>
    </form>
</section>
```

### Managing Focus and Keyboard Navigation

**HTML-Based Focus Management:**
```html
<!-- Modal dialog structure (without JavaScript focus management) -->
<div role="dialog" aria-labelledby="dialog-title" aria-modal="true">
    <h2 id="dialog-title">Confirm Delete</h2>
    <p>Are you sure you want to delete this item?</p>
    
    <div class="dialog-buttons">
        <button>Delete</button>
        <button autofocus>Cancel</button>
    </div>
</div>

<!-- Natural tab order in forms -->
<form>
    <label for="name">Name:</label>
    <input type="text" id="name" name="name" tabindex="1">
    
    <label for="email">Email:</label>
    <input type="email" id="email" name="email" tabindex="2">
    
    <label for="message">Message:</label>
    <textarea id="message" name="message" tabindex="3"></textarea>
    
    <button type="submit" tabindex="4">Send</button>
</form>
```

**Keyboard Navigation Best Practices:**
```html
<!-- Tab panel structure (requires CSS for visual states) -->
<div class="tablist" role="tablist" aria-label="Content sections">
    <!-- Use links for tab navigation instead of JavaScript -->
    <a href="#panel1" role="tab" aria-selected="true" aria-controls="panel1" id="tab1">
        Section 1
    </a>
    <a href="#panel2" role="tab" aria-selected="false" aria-controls="panel2" id="tab2">
        Section 2
    </a>
    <a href="#panel3" role="tab" aria-selected="false" aria-controls="panel3" id="tab3">
        Section 3
    </a>
</div>

<div role="tabpanel" id="panel1" aria-labelledby="tab1">
    <h3>Section 1 Content</h3>
    <p>Content for the first section...</p>
</div>

<div role="tabpanel" id="panel2" aria-labelledby="tab2" hidden>
    <h3>Section 2 Content</h3>
    <p>Content for the second section...</p>
</div>

<!-- Use CSS :target selector to show/hide panels -->
<style>
.tabpanel {
    display: none;
}
.tabpanel:target {
    display: block;
}
</style>
```

### Live Regions for Dynamic Content

**ARIA Live Regions (Static Examples):**
```html
<!-- Status messages for form feedback -->
<form>
    <label for="username">Username</label>
    <input type="text" id="username" name="username" aria-describedby="username-status">
    <div id="username-status" aria-live="polite">
        Enter your username (3-20 characters)
    </div>
    
    <label for="password">Password</label>
    <input type="password" id="password" name="password" aria-describedby="password-status">
    <div id="password-status" aria-live="polite">
        Password must be at least 8 characters
    </div>
    
    <button type="submit">Create Account</button>
</form>

<!-- Shopping cart status -->
<div class="cart-status">
    <div aria-live="polite" id="cart-message">
        Your cart is empty
    </div>
</div>

<!-- Error announcements -->
<div role="alert" class="error-message" hidden>
    Please correct the following errors before submitting
</div>

<!-- Success confirmations -->
<div role="status" class="success-message" hidden>
    Your changes have been saved
</div>
```

**Live Region Properties:**
```html
<!-- Different types of live regions -->
<div aria-live="polite" aria-atomic="true" id="search-results">
    <p>5 results found for "laptop"</p>
</div>

<div aria-live="polite" aria-relevant="additions removals" id="chat-log">
    <p>User1: Hello everyone!</p>
    <p>User2: Hi there!</p>
</div>

<!-- Built-in live region roles -->
<div role="status" id="form-status">
    Form saved successfully
</div>

<div role="alert" id="error-alert">
    Error: Please fix the following issues
</div>

<!-- Timer or countdown (updates would require JavaScript) -->
<div role="timer" aria-live="off" id="countdown">
    Time remaining: 5:00
</div>
```

### Complex UI Patterns and ARIA

**Accordion Component (HTML/CSS Only):**
```html
<div class="accordion">
    <div class="accordion-item">
        <h3>
            <a href="#panel1" aria-expanded="false" aria-controls="panel1" id="accordion1" class="accordion-trigger">
                Section 1: Getting Started
            </a>
        </h3>
        <div id="panel1" role="region" aria-labelledby="accordion1" class="accordion-panel">
            <p>Content for section 1...</p>
        </div>
    </div>
    
    <div class="accordion-item">
        <h3>
            <a href="#panel2" aria-expanded="true" aria-controls="panel2" id="accordion2" class="accordion-trigger">
                Section 2: Advanced Features
            </a>
        </h3>
        <div id="panel2" role="region" aria-labelledby="accordion2" class="accordion-panel" style="display: block;">
            <p>Content for section 2...</p>
        </div>
    </div>
</div>

<style>
.accordion-panel {
    display: none;
}

.accordion-panel:target {
    display: block;
}

/* Alternative approach using checkboxes */
.accordion-checkbox {
    display: none;
}

.accordion-checkbox:checked + .accordion-panel {
    display: block;
}
</style>
```

**Combobox (Select-based Autocomplete):**
```html
<div class="combobox-container">
    <label for="country-select">Country</label>
    <select id="country-select" 
            name="country"
            aria-describedby="country-help">
        <option value="">Choose a country</option>
        <option value="us">United States</option>
        <option value="uk">United Kingdom</option>
        <option value="ca">Canada</option>
        <option value="de">Germany</option>
        <option value="fr">France</option>
    </select>
    <div id="country-help">Select your country from the dropdown</div>
</div>

<!-- Alternative with datalist for input autocomplete -->
<div class="combobox-container">
    <label for="country-input">Country</label>
    <input type="text" 
           id="country-input"
           list="countries"
           aria-describedby="country-help">
    <datalist id="countries">
        <option value="United States">
        <option value="United Kingdom">
        <option value="Canada">
        <option value="Germany">
        <option value="France">
    </datalist>
    <div id="country-help">Type to search for a country</div>
</div>
```

**Data Grid (Table-based):**
```html
<table role="grid" aria-label="Product inventory">
    <caption>Product Inventory - Use arrow keys to navigate</caption>
    <thead>
        <tr role="row">
            <th role="columnheader" aria-sort="ascending">
                <a href="?sort=name&dir=desc">Product Name</a>
            </th>
            <th role="columnheader" aria-sort="none">
                <a href="?sort=price&dir=asc">Price</a>
            </th>
            <th role="columnheader" aria-sort="none">
                <a href="?sort=stock&dir=asc">Stock</a>
            </th>
            <th role="columnheader">Actions</th>
        </tr>
    </thead>
    <tbody>
        <tr role="row">
            <td role="gridcell">Laptop</td>
            <td role="gridcell">$999</td>
            <td role="gridcell">15</td>
            <td role="gridcell">
                <a href="/edit/laptop" aria-label="Edit Laptop">Edit</a>
                <a href="/delete/laptop" aria-label="Delete Laptop">Delete</a>
            </td>
        </tr>
        <tr role="row">
            <td role="gridcell">Mouse</td>
            <td role="gridcell">$25</td>
            <td role="gridcell">50</td>
            <td role="gridcell">
                <a href="/edit/mouse" aria-label="Edit Mouse">Edit</a>
                <a href="/delete/mouse" aria-label="Delete Mouse">Delete</a>
            </td>
        </tr>
    </tbody>
</table>
```

**Resources:**
- **W3C ARIA Patterns**: [WAI-ARIA Authoring Practices](https://www.w3.org/WAI/ARIA/apg/patterns/)
- **WebAIM ARIA Examples**: [ARIA Examples](https://webaim.org/techniques/aria/)

---

### Task 2
1. Create an accessible form with proper labels, fieldsets, and error handling using ARIA
2. Build a simple accordion component with proper ARIA states and keyboard navigation
3. Implement a custom dropdown menu with ARIA roles and keyboard support
4. Test your components with a screen reader and document the experience

### Task 3 (Project Implementation)
1. Review your existing HTML structure and identify areas where semantic markup can be improved
2. Add appropriate ARIA labels and descriptions to complex interactive elements
3. Implement proper focus management for any modal dialogs or dynamic content
4. Create a comprehensive accessibility testing checklist for your components

---

## Assessment Checklist

Before moving to Part 3, ensure you can:
- [ ] Write semantic HTML with proper heading hierarchy
- [ ] Create accessible forms with labels and fieldsets
- [ ] Implement ARIA roles, properties, and states correctly
- [ ] Understand when to use ARIA vs semantic HTML
- [ ] Manage focus and keyboard navigation in interactive components
- [ ] Use live regions for dynamic content announcements
- [ ] Test components with screen readers

---

## Next Steps

Once you've mastered semantic HTML and ARIA, you'll move on to [Part 3: Assistive Technologies and Testing](3_assistive-technologies-and-testing.md) where you'll learn to test your accessible implementations with real assistive technologies and automated tools.