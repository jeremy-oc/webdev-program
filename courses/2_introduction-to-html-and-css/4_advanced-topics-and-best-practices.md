# Part 4: Advanced Topics and Best Practices

## Modern CSS Features

WIP! Tasks and tutorials will follow!

### CSS Custom Properties (Variables)

CSS custom properties allow you to store values in variables that can be reused throughout your stylesheet, making maintenance easier and enabling dynamic theming.

**Basic Syntax:**
```css
:root {
    /* Define global variables */
    --primary-color: #3498db;
    --secondary-color: #2ecc71;
    --text-color: #333;
    --background-color: #ffffff;
    --font-family: 'Roboto', sans-serif;
    --border-radius: 8px;
    --spacing-unit: 1rem;
}

/* Use variables */
.button {
    background-color: var(--primary-color);
    color: var(--text-color);
    font-family: var(--font-family);
    border-radius: var(--border-radius);
    padding: var(--spacing-unit);
}
```

**Variable Fallbacks:**
```css
.element {
    /* Provide fallback value if variable is not defined */
    color: var(--text-color, #333);
    background: var(--background-color, white);
    
    /* Chain fallbacks */
    font-size: var(--large-text, var(--medium-text, 16px));
}
```

**Scoped Variables:**
```css
.card {
    /* Local variables scoped to .card and its children */
    --card-background: #f8f9fa;
    --card-padding: 1.5rem;
    
    background-color: var(--card-background);
    padding: var(--card-padding);
}

.card.dark-theme {
    /* Override variables for dark theme */
    --card-background: #2c3e50;
    --text-color: #ecf0f1;
}
```

**Dynamic Variables with JavaScript:**
```css
:root {
    --dynamic-color: #3498db;
    --user-preference: 16px;
}
```

```javascript
// Change variables dynamically
document.documentElement.style.setProperty('--dynamic-color', '#e74c3c');
document.documentElement.style.setProperty('--user-preference', '18px');
```

**Practical Variable System:**
```css
:root {
    /* Color palette */
    --color-primary: #2563eb;
    --color-primary-dark: #1d4ed8;
    --color-primary-light: #60a5fa;
    
    --color-secondary: #10b981;
    --color-secondary-dark: #059669;
    --color-secondary-light: #6ee7b7;
    
    --color-neutral-100: #f5f5f5;
    --color-neutral-200: #e5e5e5;
    --color-neutral-500: #737373;
    --color-neutral-900: #171717;
    
    /* Typography */
    --font-family-sans: 'Inter', -apple-system, sans-serif;
    --font-family-mono: 'Fira Code', monospace;
    
    --font-size-xs: 0.75rem;
    --font-size-sm: 0.875rem;
    --font-size-base: 1rem;
    --font-size-lg: 1.125rem;
    --font-size-xl: 1.25rem;
    --font-size-2xl: 1.5rem;
    
    --font-weight-normal: 400;
    --font-weight-medium: 500;
    --font-weight-bold: 700;
    
    /* Spacing */
    --space-1: 0.25rem;
    --space-2: 0.5rem;
    --space-3: 0.75rem;
    --space-4: 1rem;
    --space-6: 1.5rem;
    --space-8: 2rem;
    --space-12: 3rem;
    
    /* Layout */
    --container-max-width: 1200px;
    --border-radius-sm: 4px;
    --border-radius-md: 8px;
    --border-radius-lg: 12px;
    
    /* Shadows */
    --shadow-sm: 0 1px 2px rgba(0, 0, 0, 0.05);
    --shadow-md: 0 4px 6px rgba(0, 0, 0, 0.1);
    --shadow-lg: 0 10px 15px rgba(0, 0, 0, 0.1);
    
    /* Transitions */
    --transition-fast: 150ms ease-in-out;
    --transition-normal: 250ms ease-in-out;
    --transition-slow: 350ms ease-in-out;
}
```

### CSS Functions (calc, clamp, min, max)

**calc() Function:**
```css
.responsive-layout {
    /* Mathematical calculations */
    width: calc(100% - 2rem);
    height: calc(100vh - 60px);
    margin: calc(var(--space-4) * 2);
    
    /* Mix units */
    font-size: calc(1rem + 0.5vw);
    padding: calc(var(--space-2) + 5px);
    
    /* Complex calculations */
    width: calc((100% - 3 * var(--gap)) / 4);
}
```

**min() and max() Functions:**
```css
.flexible-sizing {
    /* Use smaller of the two values */
    width: min(90%, 1200px);        /* 90% width, max 1200px */
    font-size: min(4vw, 2rem);      /* 4vw, but not larger than 2rem */
    
    /* Use larger of the two values */
    height: max(200px, 50vh);       /* At least 200px, preferably 50vh */
    padding: max(1rem, 3vw);        /* At least 1rem, preferably 3vw */
}
```

**clamp() Function:**
```css
.fluid-typography {
    /* clamp(minimum, preferred, maximum) */
    font-size: clamp(1rem, 2.5vw, 2rem);
    /* Font size scales with viewport but stays between 1rem and 2rem */
    
    width: clamp(300px, 50%, 800px);
    /* Width scales but never smaller than 300px or larger than 800px */
    
    padding: clamp(1rem, 5vw, 3rem);
    /* Responsive padding with limits */
}
```

**Practical Examples:**
```css
/* Responsive container */
.container {
    width: min(90%, var(--container-max-width));
    margin: 0 auto;
    padding: clamp(1rem, 4vw, 2rem);
}

/* Fluid grid */
.grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(min(300px, 100%), 1fr));
    gap: clamp(1rem, 3vw, 2rem);
}

/* Responsive typography scale */
.heading-1 { font-size: clamp(2rem, 5vw, 4rem); }
.heading-2 { font-size: clamp(1.5rem, 4vw, 3rem); }
.heading-3 { font-size: clamp(1.25rem, 3vw, 2rem); }
```

### Container Queries Introduction

Container queries allow you to apply styles based on the size of a containing element rather than the viewport.

**Basic Container Query:**
```css
.card-container {
    container-type: inline-size;
    /* or container: card / inline-size; for named container */
}

/* Apply styles based on container width */
@container (min-width: 300px) {
    .card {
        display: flex;
        flex-direction: row;
    }
    
    .card-image {
        width: 150px;
    }
}

@container (min-width: 500px) {
    .card {
        padding: 2rem;
    }
    
    .card-title {
        font-size: 1.5rem;
    }
}
```

**Named Containers:**
```css
.sidebar {
    container-name: sidebar;
    container-type: inline-size;
}

.main-content {
    container-name: main;
    container-type: inline-size;
}

/* Query specific containers */
@container sidebar (min-width: 250px) {
    .nav-link {
        padding: 1rem;
        font-size: 1.1rem;
    }
}

@container main (min-width: 600px) {
    .article {
        columns: 2;
        column-gap: 2rem;
    }
}
```

**Note:** Container queries are a newer feature and may require browser support checks. Always provide fallbacks for older browsers.

**Resources:**
- **MDN CSS Custom Properties**: [Using CSS custom properties](https://developer.mozilla.org/en-US/docs/Web/CSS/Using_CSS_custom_properties)
- **MDN CSS Functions**: [CSS functional notation](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Functions)
- **Container Queries**: [CSS Container Queries](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Container_Queries)

---

## Debugging and Developer Tools

### Using Browser Developer Tools

**Opening Developer Tools:**
- **Chrome/Edge**: F12 or Ctrl+Shift+I (Windows), Cmd+Option+I (Mac)
- **Firefox**: F12 or Ctrl+Shift+I (Windows), Cmd+Option+I (Mac)
- **Safari**: Cmd+Option+I (Mac) - requires enabling in preferences

**Elements Panel:**
```css
/* Tips for effective debugging */
.debug-element {
    /* Add temporary borders to see boundaries */
    border: 1px solid red !important;
    
    /* Highlight with background colors */
    background-color: rgba(255, 0, 0, 0.1) !important;
    
    /* Force visibility for hidden elements */
    display: block !important;
    opacity: 1 !important;
}
```

**Key Developer Tools Features:**

**1. Element Inspection:**
- Right-click → "Inspect Element"
- Navigate HTML structure
- View computed styles
- See box model visualization
- Edit CSS in real-time

**2. Console for CSS Debugging:**
```javascript
// Check if element exists
console.log(document.querySelector('.my-element'));

// Get computed styles
const element = document.querySelector('.my-element');
const styles = window.getComputedStyle(element);
console.log(styles.getPropertyValue('display'));

// Check CSS custom property values
console.log(styles.getPropertyValue('--primary-color'));
```

**3. Responsive Design Mode:**
- Test different device sizes
- Simulate touch interactions
- Check responsive breakpoints
- View device-specific features

### Common CSS Issues and Solutions

**1. Box Model Problems:**
```css
/* Problem: Unexpected element sizes */
.problematic {
    width: 300px;
    padding: 20px;
    border: 2px solid black;
    /* Total width = 344px, not 300px! */
}

/* Solution: Use border-box */
.fixed {
    box-sizing: border-box;
    width: 300px;
    padding: 20px;
    border: 2px solid black;
    /* Total width = 300px */
}
```

**2. Margin Collapse:**
```css
/* Problem: Vertical margins collapse */
.top-element {
    margin-bottom: 20px;
}

.bottom-element {
    margin-top: 30px;
    /* Only 30px gap, not 50px! */
}

/* Solutions */
.solution-1 {
    /* Use padding instead */
    padding-bottom: 20px;
}

.solution-2 {
    /* Add border or padding to prevent collapse */
    border-top: 1px solid transparent;
}

.solution-3 {
    /* Use flexbox container */
    display: flex;
    flex-direction: column;
    gap: 20px; /* Consistent spacing */
}
```

**3. Specificity Issues:**
```css
/* Problem: Styles not applying due to specificity */
.button {
    background-color: blue; /* Specificity: 10 */
}

#header .button {
    background-color: red; /* Specificity: 110 - wins */
}

/* Solutions */
.button.primary {
    background-color: blue !important; /* Use !important sparingly */
}

/* Better: Increase specificity naturally */
.navigation .button.primary {
    background-color: blue; /* Specificity: 30 */
}
```

**4. Float Clearing Issues:**
```css
/* Problem: Parent doesn't contain floated children */
.parent {
    /* Empty height when children are floated */
}

.child {
    float: left;
}

/* Solution: Clearfix */
.clearfix::after {
    content: "";
    display: table;
    clear: both;
}

/* Modern solution: Use flexbox or grid instead */
.modern-parent {
    display: flex;
    flex-wrap: wrap;
}
```

**5. Z-index Issues:**
```css
/* Problem: Z-index not working */
.element {
    z-index: 999;
    /* Won't work without position! */
}

/* Solution: Add positioning */
.positioned-element {
    position: relative; /* or absolute, fixed, sticky */
    z-index: 999;
}

/* Understand stacking context */
.stacking-context {
    position: relative;
    z-index: 1;
    /* Creates new stacking context */
}

.child-element {
    position: absolute;
    z-index: 999;
    /* Z-index is relative to parent stacking context */
}
```

### Validation Tools and Techniques

**HTML Validation:**
- [W3C Markup Validator](https://validator.w3.org/)
- Check for semantic correctness
- Ensure proper nesting and attributes

**CSS Validation:**
- [W3C CSS Validator](https://jigsaw.w3.org/css-validator/)
- Check for syntax errors
- Verify property support

**Accessibility Testing:**
- [WAVE Web Accessibility Evaluator](https://wave.webaim.org/)
- Check color contrast ratios
- Verify semantic markup
- Test with screen readers

**Performance Testing:**
```css
/* Optimize CSS for performance */
.optimized {
    /* Use efficient selectors */
    /* Avoid: div > ul > li > a */
    /* Better: .nav-link */
    
    /* Minimize expensive properties */
    transform: translateX(10px); /* Better than changing 'left' */
    opacity: 0.5; /* Better than visibility changes */
    
    /* Use hardware acceleration */
    will-change: transform; /* For animations */
    transform: translateZ(0); /* Force GPU layer */
}
```

**CSS Linting Tools:**
- **Stylelint**: Automated CSS linting
- **Prettier**: Code formatting
- **VS Code Extensions**: Real-time error checking

**Browser Compatibility:**
- [Can I Use](https://caniuse.com/): Check feature support
- **Autoprefixer**: Automatic vendor prefixes
- **Polyfills**: Fill gaps for older browsers

**Resources:**
- **Chrome DevTools Documentation**: [Chrome DevTools](https://developers.google.com/web/tools/chrome-devtools)
- **Firefox Developer Tools**: [Firefox DevTools](https://developer.mozilla.org/en-US/docs/Tools)
- **CSS Debugging Guide**: [Debugging CSS](https://developer.mozilla.org/en-US/docs/Learn/CSS/Building_blocks/Debugging_CSS