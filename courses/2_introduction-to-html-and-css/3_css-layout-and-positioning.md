# Part 3: CSS Layout and Positioning

## CSS Layout Basics

WIP! Tasks and tutorials will follow!

### Display Property (Block, Inline, Inline-block)

The `display` property determines how an element behaves in the document flow and how it interacts with other elements.

**Block Elements:**
```css
.block-element {
    display: block;
    /* Characteristics:
     - Takes full width available
     - Starts on new line
     - Can have width, height, margin, padding
     - Examples: div, h1-h6, p, ul, li
    */
    width: 300px;
    height: 100px;
    margin: 20px 0;
    padding: 15px;
}
```

**Inline Elements:**
```css
.inline-element {
    display: inline;
    /* Characteristics:
     - Takes only necessary width
     - Stays on same line
     - Cannot have width/height set
     - Only horizontal margin/padding
     - Examples: span, a, strong, em
    */
    margin: 0 10px; /* only horizontal margins work */
    padding: 5px 10px; /* vertical padding doesn't affect layout */
}
```

**Inline-block Elements:**
```css
.inline-block-element {
    display: inline-block;
    /* Characteristics:
     - Stays on same line like inline
     - Can have width, height, full margin/padding like block
     - Great for navigation items, buttons
    */
    width: 150px;
    height: 40px;
    margin: 10px;
    padding: 10px;
    vertical-align: top; /* Control alignment with siblings */
}
```

**Other Display Values:**
```css
.display-examples {
    display: none;        /* Element is completely hidden */
    display: flex;        /* Flexbox container */
    display: grid;        /* Grid container */
    display: table;       /* Behaves like table element */
    display: table-cell;  /* Behaves like td element */
}
```

### Normal Document Flow

Elements in normal flow are laid out according to their source order and display type:

```html
<div class="container">
    <h1>Block Element (Full Width)</h1>
    <p>Another block element on new line</p>
    <span>Inline element</span>
    <span>stays on same line</span>
    <div class="inline-block-item">Inline-block</div>
    <div class="inline-block-item">can sit side by side</div>
</div>
```

```css
.container {
    width: 600px;
    margin: 0 auto;
}

.inline-block-item {
    display: inline-block;
    width: 150px;
    height: 50px;
    background-color: lightblue;
    margin: 5px;
}
```

### CSS Positioning (Static, Relative, Absolute, Fixed)

**Static Positioning (Default):**
```css
.static {
    position: static;
    /* Default behavior - follows normal document flow
     - top, right, bottom, left have no effect
    */
}
```

**Relative Positioning:**
```css
.relative {
    position: relative;
    top: 20px;    /* Move 20px down from original position */
    left: 30px;   /* Move 30px right from original position */
    /* Element maintains its space in document flow
     - Other elements are not affected
     - Creates new stacking context
    */
}
```

**Absolute Positioning:**
```css
.absolute {
    position: absolute;
    top: 50px;
    right: 20px;
    /* Removed from normal document flow
     - Positioned relative to nearest positioned ancestor
     - If no positioned ancestor, relative to initial containing block
     - Other elements flow as if this element doesn't exist
    */
}

.relative-parent {
    position: relative; /* Creates positioning context for absolute children */
}
```

**Fixed Positioning:**
```css
.fixed {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    /* Positioned relative to viewport
     - Stays in place when page is scrolled
     - Removed from normal document flow
     - Common for navigation bars, modals
    */
}
```

**Sticky Positioning:**
```css
.sticky {
    position: sticky;
    top: 10px;
    /* Hybrid of relative and fixed
     - Acts like relative until scroll threshold is met
     - Then acts like fixed
     - Great for sticky headers
    */
}
```

**Z-index for Layering:**
```css
.layered-elements {
    position: relative; /* or absolute, fixed, sticky */
    z-index: 10; /* Higher values appear on top */
}

.modal-overlay {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, 0.5);
    z-index: 1000;
}
```

**Resources:**
- **MDN CSS Layout**: [CSS layout](https://developer.mozilla.org/en-US/docs/Learn/CSS/CSS_layout)
- **The Odin Project**: [Block and Inline](https://www.theodinproject.com/lessons/foundations-block-and-inline)
- **W3Schools CSS Position**: [CSS Position](https://www.w3schools.com/css/css_positioning.asp)

---

## Flexbox Layout

### Flex Container and Flex Items

Flexbox is a one-dimensional layout method for arranging items in rows or columns.

**Creating a Flex Container:**
```css
.flex-container {
    display: flex;
    /* All direct children become flex items */
}

/* Alternative for inline flex container */
.inline-flex {
    display: inline-flex;
}
```

**Basic Flex Example:**
```html
<div class="flex-container">
    <div class="flex-item">Item 1</div>
    <div class="flex-item">Item 2</div>
    <div class="flex-item">Item 3</div>
</div>
```

```css
.flex-container {
    display: flex;
    background-color: lightgray;
    padding: 10px;
}

.flex-item {
    background-color: lightblue;
    margin: 5px;
    padding: 20px;
    text-align: center;
}
```

### Main Axis and Cross Axis

**Flex Direction:**
```css
.flex-container {
    display: flex;
    flex-direction: row;         /* default: left to right */
    flex-direction: row-reverse; /* right to left */
    flex-direction: column;      /* top to bottom */
    flex-direction: column-reverse; /* bottom to top */
}
```

**Flex Wrap:**
```css
.flex-container {
    display: flex;
    flex-wrap: nowrap;    /* default: items stay on one line */
    flex-wrap: wrap;      /* items wrap to new lines */
    flex-wrap: wrap-reverse; /* items wrap in reverse order */
    
    /* Shorthand */
    flex-flow: row wrap;  /* flex-direction flex-wrap */
}
```

### Flex Properties for Alignment and Distribution

**Justify Content (Main Axis):**
```css
.flex-container {
    display: flex;
    justify-content: flex-start;    /* default: items at start */
    justify-content: flex-end;      /* items at end */
    justify-content: center;        /* items centered */
    justify-content: space-between; /* equal space between items */
    justify-content: space-around;  /* equal space around items */
    justify-content: space-evenly;  /* equal space everywhere */
}
```

**Align Items (Cross Axis):**
```css
.flex-container {
    display: flex;
    height: 200px; /* Container needs height for cross-axis alignment */
    align-items: stretch;     /* default: items stretch to fill */
    align-items: flex-start;  /* items at cross-axis start */
    align-items: flex-end;    /* items at cross-axis end */
    align-items: center;      /* items centered on cross-axis */
    align-items: baseline;    /* items aligned to text baseline */
}
```

**Align Content (Multiple Lines):**
```css
.flex-container {
    display: flex;
    flex-wrap: wrap;
    height: 300px;
    align-content: stretch;      /* default: lines stretch */
    align-content: flex-start;   /* lines at start */
    align-content: flex-end;     /* lines at end */
    align-content: center;       /* lines centered */
    align-content: space-between; /* space between lines */
    align-content: space-around;  /* space around lines */
}
```

**Individual Flex Item Properties:**
```css
.flex-item {
    /* Flex grow: how much item should grow */
    flex-grow: 0;   /* default: don't grow */
    flex-grow: 1;   /* grow to fill available space */
    flex-grow: 2;   /* grow twice as much as items with flex-grow: 1 */
    
    /* Flex shrink: how much item should shrink */
    flex-shrink: 1; /* default: can shrink */
    flex-shrink: 0; /* don't shrink */
    
    /* Flex basis: initial size before growing/shrinking */
    flex-basis: auto;   /* default: based on content */
    flex-basis: 200px;  /* specific width */
    flex-basis: 20%;    /* percentage of container */
    
    /* Shorthand: grow shrink basis */
    flex: 1;           /* flex: 1 1 0% - equal distribution */
    flex: 0 0 200px;   /* flex: 0 0 200px - fixed 200px width */
    flex: 2;           /* flex: 2 1 0% - grows twice as much */
    
    /* Align individual item on cross axis */
    align-self: auto;      /* default: inherit from align-items */
    align-self: flex-start;
    align-self: flex-end;
    align-self: center;
    align-self: stretch;
}
```

**Practical Flexbox Examples:**

**1. Navigation Bar:**
```css
.navbar {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 1rem 2rem;
    background-color: #333;
}

.nav-brand {
    color: white;
    font-size: 1.5rem;
}

.nav-links {
    display: flex;
    list-style: none;
    gap: 2rem;
}
```

**2. Card Layout:**
```css
.card-container {
    display: flex;
    flex-wrap: wrap;
    gap: 20px;
    justify-content: center;
}

.card {
    flex: 0 0 300px; /* Don't grow/shrink, 300px base width */
    background: white;
    border-radius: 8px;
    box-shadow: 0 2px 10px rgba(0,0,0,0.1);
    padding: 20px;
}
```

**3. Centering Content:**
```css
.center-content {
    display: flex;
    justify-content: center;
    align-items: center;
    min-height: 100vh;
}
```

**Resources:**
- **FreeCodeCamp Interactive**: [Learn CSS Flexbox by Building a Photo Gallery](https://www.freecodecamp.org/learn/2022/responsive-web-design/learn-css-flexbox-by-building-a-photo-gallery/)
- **MDN Flexbox**: [Basic concepts of flexbox](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Flexible_Box_Layout/Basic_Concepts_of_Flexbox)
- **Flexbox Froggy Game**: [Flexbox Froggy](https://flexboxfroggy.com/)
- **The Odin Project**: [Flexbox](https://www.theodinproject.com/lessons/foundations-flexbox)

---

## CSS Grid Layout

### Grid Container and Grid Items

CSS Grid is a two-dimensional layout system for creating complex layouts with rows and columns.

**Creating a Grid Container:**
```css
.grid-container {
    display: grid;
    /* All direct children become grid items */
}

/* Inline grid */
.inline-grid {
    display: inline-grid;
}
```

**Basic Grid Example:**
```html
<div class="grid-container">
    <div class="grid-item">1</div>
    <div class="grid-item">2</div>
    <div class="grid-item">3</div>
    <div class="grid-item">4</div>
    <div class="grid-item">5</div>
    <div class="grid-item">6</div>
</div>
```

```css
.grid-container {
    display: grid;
    grid-template-columns: 1fr 1fr 1fr; /* 3 equal columns */
    grid-template-rows: 100px 100px;    /* 2 rows of 100px each */
    gap: 10px;
    background-color: lightgray;
    padding: 10px;
}

.grid-item {
    background-color: lightblue;
    padding: 20px;
    text-align: center;
}
```

### Creating Grid Templates

**Grid Template Columns and Rows:**
```css
.grid-examples {
    display: grid;
    
    /* Fixed sizes */
    grid-template-columns: 200px 300px 100px;
    
    /* Flexible units */
    grid-template-columns: 1fr 2fr 1fr; /* fractions of available space */
    
    /* Mixed units */
    grid-template-columns: 200px 1fr 100px;
    
    /* Repeat function */
    grid-template-columns: repeat(3, 1fr); /* repeat 1fr three times */
    grid-template-columns: repeat(auto-fit, minmax(200px, 1fr)); /* responsive columns */
    
    /* Auto-sizing */
    grid-template-columns: auto auto auto; /* size based on content */
}
```

**Grid Template Areas:**
```css
.layout-grid {
    display: grid;
    grid-template-areas: 
        "header header header"
        "sidebar main main"
        "footer footer footer";
    grid-template-columns: 200px 1fr 1fr;
    grid-template-rows: 80px 1fr 60px;
    min-height: 100vh;
    gap: 10px;
}

.header { grid-area: header; }
.sidebar { grid-area: sidebar; }
.main { grid-area: main; }
.footer { grid-area: footer; }
```

**Grid Lines and Positioning:**
```css
.positioned-item {
    /* Position by line numbers */
    grid-column-start: 2;
    grid-column-end: 4;
    grid-row-start: 1;
    grid-row-end: 3;
    
    /* Shorthand */
    grid-column: 2 / 4;  /* start / end */
    grid-row: 1 / 3;
    
    /* Span notation */
    grid-column: 2 / span 2;  /* start at line 2, span 2 columns */
    grid-row: span 2;         /* span 2 rows from auto-placement */
    
    /* Ultra shorthand */
    grid-area: 1 / 2 / 3 / 4; /* row-start / col-start / row-end / col-end */
}
```

### Grid Areas and Responsive Grids

**Named Grid Lines:**
```css
.named-lines {
    display: grid;
    grid-template-columns: 
        [sidebar-start] 250px 
        [sidebar-end main-start] 1fr 
        [main-end];
    grid-template-rows: 
        [header-start] 80px 
        [header-end content-start] 1fr 
        [content-end];
}

.main-content {
    grid-column: main-start / main-end;
    grid-row: content-start / content-end;
}
```

**Auto-placement and Dense Packing:**
```css
.auto-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
    grid-auto-rows: 150px;
    gap: 15px;
    grid-auto-flow: row;    /* default: fill rows first */
    grid-auto-flow: column; /* fill columns first */
    grid-auto-flow: dense;  /* pack items densely */
}
```

**Responsive Grid Examples:**

**1. Magazine Layout:**
```css
.magazine-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
    grid-auto-rows: 200px;
    gap: 20px;
}

.featured-article {
    grid-column: span 2;
    grid-row: span 2;
}
```

**2. Dashboard Layout:**
```css
.dashboard {
    display: grid;
    grid-template-areas:
        "header header header"
        "sidebar main main"
        "sidebar main main";
    grid-template-columns: 250px 1fr 1fr;
    grid-template-rows: 60px 1fr 1fr;
    min-height: 100vh;
    gap: 10px;
}

@media (max-width: 768px) {
    .dashboard {
        grid-template-areas:
            "header"
            "main"
            "sidebar";
        grid-template-columns: 1fr;
        grid-template-rows: 60px 1fr auto;
    }
}
```

**Grid Alignment:**
```css
.grid-alignment {
    display: grid;
    grid-template-columns: repeat(3, 200px);
    grid-template-rows: repeat(2, 100px);
    
    /* Align the entire grid within container */
    justify-content: center;    /* horizontal alignment */
    align-content: center;      /* vertical alignment */
    
    /* Align items within their grid cells */
    justify-items: center;      /* horizontal alignment of items */
    align-items: center;        /* vertical alignment of items */
    
    /* Individual item alignment */
    .special-item {
        justify-self: end;      /* align this item horizontally */
        align-self: start;      /* align this item vertically */
    }
}
```

**Resources:**
- **MDN CSS Grid**: [Basic concepts of grid layout](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Grid_Layout/Basic_Concepts_of_Grid_Layout)
- **Grid Garden Game**: [Grid Garden](https://cssgridgarden.com/)
- **The Odin Project**: [CSS Grid](https://www.theodinproject.com/lessons/intermediate-html-and-css-grid)
- **CSS Grid Complete Guide**: [CSS-Tricks Grid Guide](https://css-tricks.com/snippets/css/complete-guide-grid/)

---

## Responsive Design

### Mobile-first Approach

Mobile-first design starts with mobile devices and progressively enhances for larger screens.

**Mobile-first Philosophy:**
```css
/* Base styles for mobile (smallest screens) */
.container {
    width: 100%;
    padding: 15px;
    font-size: 16px;
}

.navigation {
    display: flex;
    flex-direction: column;
}

/* Enhance for tablets */
@media (min-width: 768px) {
    .container {
        padding: 30px;
        font-size: 18px;
    }
    
    .navigation {
        flex-direction: row;
    }
}

/* Enhance for desktop */
@media (min-width: 1024px) {
    .container {
        max-width: 1200px;
        margin: 0 auto;
        padding: 40px;
    }
}
```

### Media Queries and Breakpoints

**Basic Media Query Syntax:**
```css
/* Mobile First */
@media (min-width: 480px) {
    /* Styles for screens 480px and larger */
}

@media (min-width: 768px) {
    /* Styles for tablets and larger */
}

@media (min-width: 1024px) {
    /* Styles for desktop and larger */
}

/* Desktop First (less recommended) */
@media (max-width: 1023px) {
    /* Styles for screens smaller than desktop */
}
```

**Common Breakpoints:**
```css
/* Extra small devices (phones) */
@media (min-width: 320px) { }

/* Small devices (large phones) */
@media (min-width: 576px) { }

/* Medium devices (tablets) */
@media (min-width: 768px) { }

/* Large devices (desktops) */
@media (min-width: 992px) { }

/* Extra large devices (large desktops) */
@media (min-width: 1200px) { }
```

**Advanced Media Queries:**
```css
/* Orientation */
@media (orientation: portrait) {
    /* Styles for portrait orientation */
}

@media (orientation: landscape) {
    /* Styles for landscape orientation */
}

/* Resolution */
@media (min-resolution: 2dppx) {
    /* Styles for high-resolution displays */
}

/* Hover capability */
@media (hover: hover) {
    .button:hover {
        background-color: blue;
    }
}

/* Combining conditions */
@media (min-width: 768px) and (max-width: 1023px) {
    /* Styles for tablets only */
}

@media (min-width: 768px) and (orientation: landscape) {
    /* Styles for tablets in landscape mode */
}
```

### Flexible Units (em, rem, %, vw, vh)

**Absolute Units:**
```css
.absolute-units {
    width: 300px;        /* Pixels - fixed size */
    font-size: 16px;     /* Pixels - fixed size */
    border: 1pt solid;   /* Points - print media */
}
```

**Relative Units:**
```css
.relative-units {
    /* EM - relative to parent element's font size */
    font-size: 1.2em;    /* 1.2 times parent's font size */
    margin: 0.5em;       /* 0.5 times current element's font size */
    
    /* REM - relative to root element's font size */
    font-size: 1.5rem;   /* 1.5 times root font size (usually 16px) */
    padding: 2rem;       /* 32px if root is 16px */
    
    /* Percentages - relative to parent element */
    width: 80%;          /* 80% of parent's width */
    height: 50%;         /* 50% of parent's height */
    
    /* Viewport units */
    width: 50vw;         /* 50% of viewport width */
    height: 100vh;       /* 100% of viewport height */
    font-size: 4vw;      /* 4% of viewport width */
    
    /* Minimum and maximum of viewport dimensions */
    width: 50vmin;       /* 50% of smaller viewport dimension */
    font-size: 3vmax;    /* 3% of larger viewport dimension */
}
```

**Practical Unit Usage:**
```css
/* Typography with rem for consistency */
html {
    font-size: 16px; /* Base font size */
}

h1 { font-size: 2.5rem; }    /* 40px */
h2 { font-size: 2rem; }      /* 32px */
h3 { font-size: 1.5rem; }    /* 24px */
p { font-size: 1rem; }       /* 16px */

/* Layout with flexible units */
.container {
    max-width: 1200px;
    width: 90%;              /* Flexible width */
    margin: 0 auto;
    padding: 2rem;           /* Consistent spacing */
}

.hero-section {
    height: 100vh;           /* Full viewport height */
    min-height: 400px;       /* Minimum height fallback */
}

.card {
    width: calc(33.333% - 2rem); /* Calculated width */
    margin: 1rem;
}
```

**Responsive Typography:**
```css
/* Fluid typography using clamp() */
.responsive-text {
    font-size: clamp(1rem, 2.5vw, 2rem);
    /* minimum: 1rem, preferred: 2.5vw, maximum: 2rem */
}

/* Media query approach */
.heading {
    font-size: 1.5rem;
}

@media (min-width: 768px) {
    .heading {
        font-size: 2rem;
    }
}

@media (min-width: 1024px) {
    .heading {
        font-size: 2.5rem;
    }
}
```

**Responsive Images:**
```css
.responsive-image {
    max-width: 100%;
    height: auto;
}

/* CSS-only responsive images */
.image-container {
    width: 100%;
    height: 0;
    padding-bottom: 56.25%; /* 16:9 aspect ratio */
    position: relative;
    overflow: hidden;
}

.image-container img {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    object-fit: cover;
}
```

**Complete Responsive Layout Example:**
```css
/* Mobile-first responsive navigation */
.navbar {
    display: flex;
    flex-direction: column;
    padding: 1rem;
    background-color: #333;
}

.nav-brand {
    color: white;
    font-size: 1.5rem;
    margin-bottom: 1rem;
}

.nav-menu {
    display: flex;
    flex-direction: column;
    gap: 0.5rem;
}

.nav-link {
    color: white;
    text-decoration: none;
    padding: 0.5rem;
    border-radius: 4px;
    transition: background-color 0.3s;
}

.nav-link:hover {
    background-color: rgba(255, 255, 255, 0.1);
}

/* Tablet and up */
@media (min-width: 768px) {
    .navbar {
        flex-direction: row;
        justify-content: space-between;
        align-items: center;
        padding: 1rem 2rem;
    }
    
    .nav-brand {
        margin-bottom: 0;
    }
    
    .nav-menu {
        flex-direction: row;
        gap: 1rem;
    }
}

/* Desktop responsive grid */
.content-grid {
    display: grid;
    grid-template-columns: 1fr;
    gap: 1rem;
    padding: 1rem;
}

@media (min-width: 768px) {
    .content-grid {
        grid-template-columns: repeat(2, 1fr);
        gap: 2rem;
        padding: 2rem;
    }
}

@media (min-width: 1024px) {
    .content-grid {
        grid-template-columns: repeat(3, 1fr);
        max-width: 1200px;
        margin: 0 auto;
    }
}
```

**Resources:**
- **MDN Responsive Design**: [Responsive design](https://developer.mozilla.org/en-US/docs/Learn/CSS/CSS_layout/Responsive_Design)
- **The Odin Project**: [Responsive Design](https://www.theodinproject.com/lessons/intermediate-html-and-css-responsive-design)
- **W3Schools Responsive Web Design**: [RWD Introduction](https://www.w3schools.com/css/css_rwd_intro.asp)

---

## Practice Exercises

### Exercise 1: Flexbox Navigation Bar
Create a responsive navigation bar that:
- Stacks vertically on mobile
- Displays horizontally on desktop
- Includes a logo and menu items
- Has proper spacing and alignment

### Exercise 2: CSS Grid Magazine Layout
Build a magazine-style layout featuring:
- Header spanning full width
- Sidebar for navigation
- Main content area with article grid
- Featured articles that span multiple columns
- Footer spanning full width

### Exercise 3: Responsive Card Grid
Design a responsive card layout that:
- Shows 1 column on mobile
- Shows 2 columns on tablet
- Shows 3-4 columns on desktop
- Uses CSS Grid with auto-fit
- Maintains aspect ratios

### Exercise 4: Dashboard Layout
Create a dashboard interface with:
- Fixed header with navigation
- Collapsible sidebar
- Main content area with widget grid
- Responsive behavior for different screen sizes
- Proper use of CSS Grid and Flexbox

### Exercise 5: Landing Page Layout
Build a complete landing page featuring:
- Hero section with full viewport height
- Feature sections with flexible layouts
- Responsive image galleries
- Contact form with proper styling
- Mobile-first responsive design

---

## Assessment Checklist

Before moving to Part 4, ensure you can:
- [ ] Understand and apply different display values
- [ ] Use CSS positioning effectively
- [ ] Create layouts with Flexbox
- [ ] Build complex layouts with CSS Grid
- [ ] Implement responsive design with media queries
- [ ] Use flexible units appropriately
- [ ] Create mobile-first responsive designs
- [ ] Combine layout methods effectively
- [ ] Debug layout issues using developer tools
- [ ] Optimize layouts for different devices and screen sizes

---

## Portfolio Project Progress

At this stage, your portfolio should include:
- **Responsive layout** that works on all device sizes
- **Modern CSS Grid or Flexbox** for complex layouts
- **Mobile-first design** approach
- **Proper navigation** that adapts to screen size
- **Flexible typography** and spacing
- **Optimized images** and media

**Portfolio Layout Checklist:**
1. Header with responsive navigation
2. Hero section with compelling introduction
3. About section with flexible layout
4. Projects gallery using CSS Grid
5. Contact form with proper styling
6. Footer with social links and information
7. Consistent responsive behavior across all sections

---

## Common Layout Patterns

### Holy Grail Layout
```css
.holy-grail {
    display: grid;
    grid-template-areas:
        "header header header"
        "nav main aside"
        "footer footer footer";
    grid-template-columns: 200px 1fr 200px;
    grid-template-rows: auto 1fr auto;
    min-height: 100vh;
}
```

### Sidebar Layout
```css
.sidebar-layout {
    display: grid;
    grid-template-columns: 250px 1fr;
    min-height: 100vh;
}

@media (max-width: 768px) {
    .sidebar-layout {
        grid-template-columns: 1fr;
        grid-template-rows: auto 1fr;
    }
}
```

### Centered Content
```css
.centered-content {
    display: flex;
    justify-content: center;
    align-items: center;
    min-height: 100vh;
}

/* Alternative with Grid */
.grid-centered {
    display: grid;
    place-items: center;
    min-height: 100vh;
}
```

---

## Next Steps

You're now ready for **Part 4: Advanced Topics and Best Practices** where you'll learn modern CSS features, debugging techniques, and optimization strategies.

**Coming Up in Part 4:**
- CSS custom properties (variables)
- Modern CSS functions and features
- Debugging and development tools
- Performance optimization
- Final project completion