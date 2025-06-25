# Part 2: CSS Fundamentals

## Introduction to CSS

### What is CSS and How It Works with HTML

CSS (Cascading Style Sheets) is a styling language that controls the presentation and layout of HTML documents. While HTML provides structure and content, CSS handles the visual appearance.

#### Getting Started:
This section provides all the content necessary to learn about the most relevant CSS features that will be used in many occasions.

For the introduction to HTML & CSS we will be learning with the [The Odin Project](https://www.theodinproject.com) course created by Erik Trautman and the [Responsive Web Design] course by FreeCodeCamp.

### Task 1
1. Work through the [CSS Foundations](https://www.theodinproject.com/paths/foundations/courses/foundations#css-foundations) section of the "The Odin Project" Foundations course.
2. Interactivly work through the [Learn CSS by building a Cafe Menu](https://www.freecodecamp.org/learn/2022/responsive-web-design/learn-basic-css-by-building-a-cafe-menu/) course.
3. If you prefer a crash course like tutorial there is a good overview available on YouTube by Traversy Media: [CSS Crash Course for Absolute Beginners](https://www.youtube.com/watch?v=yfoY53QXEnI)


### Recap of the content

There are some concepts that you should be familiar with after going through these tutorials. Some properties might not have been part of the tutorials, but the same concepts apply. 

#### The Relationship:
```html
<!-- HTML provides structure -->
<h1>Welcome to My Website</h1>
<p>This is a paragraph of text.</p>
```

```css
/* CSS provides styling */
h1 {
    color: blue;
    font-size: 2em;
}

p {
    color: gray;
    line-height: 1.5;
}
```

**Resources:**
- **MDN CSS Basics**: [CSS Basics](https://developer.mozilla.org/en-US/docs/Learn/Getting_started_with_the_web/CSS_basics)
- **W3Schools CSS Tutorial**: [CSS Introduction](https://www.w3schools.com/css/css_intro.asp)

#### CSS Syntax and Structure

**Basic CSS Syntax:**
```css
selector {
    property: value;
    property: value;
}
```

**CSS Rule Components:**
- **Selector**: Targets HTML elements
- **Declaration Block**: Contains style declarations
- **Property**: The style attribute to change
- **Value**: The setting for the property

**Example:**
```css
h1 {
    color: #333333;
    font-size: 24px;
    font-weight: bold;
    margin-bottom: 20px;
}
```

#### Ways to Include CSS

**1. External CSS (Recommended):**
```html
<head>
    <link rel="stylesheet" href="styles.css">
</head>
```

**2. Internal CSS:**
```html
<head>
    <style>
        body {
            background-color: lightblue;
        }
    </style>
</head>
```

**3. Inline CSS:**
```html
<p style="color: red; font-size: 16px;">This text is styled inline.</p>
```

**Best Practices:**
- Use external stylesheets for maintainability
- Keep CSS organized and commented
- Use internal CSS sparingly for page-specific styles
- Avoid inline CSS except for dynamic styling

**Resources:**
- **FreeCodeCamp Interactive**: [Learn Basic CSS by Building a Cafe Menu](https://www.freecodecamp.org/learn/2022/responsive-web-design/learn-basic-css-by-building-a-cafe-menu/)
- **MDN How CSS Works**: [How CSS works](https://developer.mozilla.org/en-US/docs/Learn/CSS/First_steps/How_CSS_works)

---

#### CSS Selectors (Element, Class, and ID Selectors)

**Element Selectors:**
```css
/* Select all paragraphs */
p {
    color: black;
    font-size: 16px;
}

/* Select all headings level 1 */
h1 {
    color: blue;
    font-weight: bold;
}
```

**Class Selectors:**
```css
/* Select elements with class="highlight" */
.highlight {
    background-color: yellow;
    padding: 10px;
}

/* Multiple classes */
.highlight.important {
    border: 2px solid red;
}
```

```html
<p class="highlight">This paragraph is highlighted.</p>
<div class="highlight important">This div has multiple classes.</div>
```

**ID Selectors:**
```css
/* Select element with id="header" */
#header {
    background-color: navy;
    color: white;
    padding: 20px;
}
```

```html
<div id="header">This is the header</div>
```

#### Descendant and Child Selectors

**Descendant Selectors (space):**
```css
/* Select all <p> elements inside <div> elements */
div p {
    margin-left: 20px;
}

/* Select all <a> elements inside <nav> elements */
nav a {
    text-decoration: none;
    color: blue;
}
```

**Child Selectors (>):**
```css
/* Select only direct <li> children of <ul> */
ul > li {
    list-style-type: square;
}

/* Select direct <p> children of <article> */
article > p {
    font-size: 18px;
}
```

**Adjacent Sibling Selector (+):**
```css
/* Select <p> immediately following <h2> */
h2 + p {
    font-weight: bold;
    margin-top: 0;
}
```

**General Sibling Selector (~):**
```css
/* Select all <p> siblings after <h2> */
h2 ~ p {
    color: gray;
}
```

#### Pseudo-classes and Pseudo-elements

**Link Pseudo-classes:**
```css
a:link { color: blue; }          /* Unvisited links */
a:visited { color: purple; }     /* Visited links */
a:hover { color: red; }          /* Mouse over */
a:active { color: orange; }      /* Being clicked */
```

**Structural Pseudo-classes:**
```css
/* First and last children */
li:first-child { font-weight: bold; }
li:last-child { border-bottom: none; }

/* Nth child selections */
tr:nth-child(even) { background-color: #f2f2f2; }
tr:nth-child(odd) { background-color: white; }
p:nth-child(3) { color: red; }
```

**Form Pseudo-classes:**
```css
input:focus { border-color: blue; }
input:required { border-left: 3px solid red; }
input:valid { border-left: 3px solid green; }
input:invalid { border-left: 3px solid red; }
```

**Pseudo-elements:**
```css
/* Style first line and first letter */
p::first-line { font-weight: bold; }
p::first-letter { font-size: 2em; float: left; }

/* Add content before and after elements */
.quote::before { content: """; }
.quote::after { content: """; }
```

#### Understanding CSS Specificity

**Specificity Hierarchy (from highest to lowest):**
1. **Inline styles** (1000 points)
2. **IDs** (100 points each)
3. **Classes, attributes, pseudo-classes** (10 points each)
4. **Elements and pseudo-elements** (1 point each)

**Specificity Examples:**
```css
/* Specificity: 1 (one element) */
p { color: black; }

/* Specificity: 10 (one class) */
.highlight { color: yellow; }

/* Specificity: 100 (one ID) */
#main { color: blue; }

/* Specificity: 111 (ID + class + element) */
#main .highlight p { color: red; }

/* Specificity: 1000 (inline style) */
/* <p style="color: green;">Text</p> */
```

**Important Declaration:**
```css
/* !important overrides specificity (use sparingly) */
p { color: red !important; }
```

**Resources:**
- **MDN CSS Selectors**: [CSS selectors](https://developer.mozilla.org/en-US/docs/Learn/CSS/Building_blocks/Selectors)
- **W3Schools CSS Selectors**: [CSS Selectors](https://www.w3schools.com/css/css_selectors.asp)
- **CSS Specificity Calculator**: [Specificity Calculator](https://specificity.keegan.st/)

---

#### The Box Model (Content, Padding, Border, and Margin)

Every HTML element is a rectangular box consisting of four areas:

**Box Model Components:**
```css
.box {
    /* Content area */
    width: 200px;
    height: 100px;
    
    /* Padding (inside the border) */
    padding: 20px;
    
    /* Border */
    border: 2px solid black;
    
    /* Margin (outside the border) */
    margin: 10px;
}
```

**Visual Representation:**
```
┌─────────────────────────────────────┐ ← margin
│ ┌─────────────────────────────────┐ │ ← border
│ │ ┌─────────────────────────────┐ │ │ ← padding
│ │ │                             │ │ │ ← content
│ │ │         Content Area        │ │ │
│ │ │                             │ │ │
│ │ └─────────────────────────────┘ │ │
│ └─────────────────────────────────┘ │
└─────────────────────────────────────┘
```

**Individual Sides:**
```css
.element {
    /* Margin shorthand: top right bottom left */
    margin: 10px 15px 20px 25px;
    
    /* Individual margins */
    margin-top: 10px;
    margin-right: 15px;
    margin-bottom: 20px;
    margin-left: 25px;
    
    /* Same for padding and border */
    padding: 10px 20px; /* top/bottom left/right */
    border-width: 1px 2px 3px 4px;
}
```

#### Box-sizing Property

**Default Box Model (content-box):**
```css
.box {
    width: 200px;
    padding: 20px;
    border: 2px solid black;
    /* Total width = 200 + 40 + 4 = 244px */
}
```

#### Debugging with Developer Tools

**Using Browser Developer Tools:**
1. Right-click on element → "Inspect Element"
2. View the box model in the "Computed" tab
3. See visual representation of margins, padding, borders
4. Edit values in real-time for testing

**CSS for Debugging:**
```css
/* Temporary border to see element boundaries */
* {
    border: 1px solid red;
}

/* Background colors for layout debugging */
.container { background-color: lightblue; }
.content { background-color: lightgreen; }
```

**Resources:**
- **FreeCodeCamp Interactive**: [Learn the CSS Box Model by Building a Rothko Painting](https://www.freecodecamp.org/learn/2022/responsive-web-design/learn-the-css-box-model-by-building-a-rothko-painting/)
- **MDN Box Model**: [The box model](https://developer.mozilla.org/en-US/docs/Learn/CSS/Building_blocks/The_box_model)
- **The Odin Project**: [The Box Model](https://www.theodinproject.com/lessons/foundations-the-box-model)

---

#### Typography and Text Styling

**Basic Font Properties:**
```css
.text {
    font-family: Arial, Helvetica, sans-serif;
    font-size: 16px;
    font-weight: bold; /* or 100-900 */
    font-style: italic;
    line-height: 1.5;
}

/* Font shorthand */
.shorthand {
    font: italic bold 16px/1.5 Arial, sans-serif;
    /*    style weight size/line-height family */
}
```

**Font Stack Examples:**
```css
/* Serif fonts */
.serif {
    font-family: "Times New Roman", Times, serif;
}

/* Sans-serif fonts */
.sans-serif {
    font-family: Arial, Helvetica, sans-serif;
}

/* Monospace fonts */
.monospace {
    font-family: "Courier New", Courier, monospace;
}
```

### Text Alignment, Spacing, and Decoration

**Text Alignment:**
```css
.text-alignment {
    text-align: left;    /* default */
    text-align: center;
    text-align: right;
    text-align: justify;
}
```

**Text Spacing:**
```css
.text-spacing {
    letter-spacing: 2px;     /* Space between letters */
    word-spacing: 5px;       /* Space between words */
    line-height: 1.6;        /* Space between lines */
    text-indent: 2em;        /* First line indentation */
}
```

**Text Decoration and Transform:**
```css
.text-decoration {
    text-decoration: none;           /* Remove underlines */
    text-decoration: underline;
    text-decoration: line-through;
    text-decoration: overline;
}

.text-transform {
    text-transform: uppercase;       /* ALL CAPS */
    text-transform: lowercase;       /* all lowercase */
    text-transform: capitalize;      /* Title Case */
}
```

#### Bonus: Working with Google Fonts

**1. Import in CSS:**
```css
@import url('https://fonts.googleapis.com/css2?family=Roboto:wght@300;400;700&display=swap');

body {
    font-family: 'Roboto', sans-serif;
}
```

**2. Link in HTML:**
```html
<head>
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Roboto:wght@300;400;700&display=swap" rel="stylesheet">
</head>
```

**Using Google Fonts:**
```css
h1 {
    font-family: 'Roboto', sans-serif;
    font-weight: 700; /* Bold */
}

p {
    font-family: 'Roboto', sans-serif;
    font-weight: 400; /* Regular */
}
```

**Typography Best Practices:**
- Limit to 2-3 font families per site
- Ensure good contrast between text and background
- Use relative units (em, rem) for scalability
- Consider loading performance with web fonts

**Resources:**
- **Google Fonts**: [Google Fonts](https://fonts.google.com/)
- **MDN Web Fonts**: [Web fonts](https://developer.mozilla.org/en-US/docs/Learn/CSS/Styling_text/Web_fonts)
- **Typography Guidelines**: [Typography Handbook](https://typographyhandbook.com/)

---

#### Color Values (Hex, RGB, HSL)

**Hexadecimal Colors:**
```css
.hex-colors {
    color: #ff0000;        /* Red */
    color: #00ff00;        /* Green */
    color: #0000ff;        /* Blue */
    color: #000000;        /* Black */
    color: #ffffff;        /* White */
    color: #f00;           /* Short hex for #ff0000 */
}
```

**RGB and RGBA:**
```css
.rgb-colors {
    color: rgb(255, 0, 0);           /* Red */
    color: rgb(0, 255, 0);           /* Green */
    color: rgb(0, 0, 255);           /* Blue */
    
    /* RGBA with alpha (transparency) */
    background-color: rgba(255, 0, 0, 0.5);  /* 50% transparent red */
    background-color: rgba(0, 0, 0, 0.8);    /* 80% transparent black */
}
```

**HSL and HSLA:**
```css
.hsl-colors {
    color: hsl(0, 100%, 50%);        /* Red: hue, saturation, lightness */
    color: hsl(120, 100%, 50%);      /* Green */
    color: hsl(240, 100%, 50%);      /* Blue */
    
    /* HSLA with alpha */
    background-color: hsla(0, 100%, 50%, 0.3);  /* 30% transparent red */
}
```

**Named Colors:**
```css
.named-colors {
    color: red;
    color: blue;
    color: green;
    color: white;
    color: black;
    color: gray;
    color: transparent;
}
```

#### Background Properties and Images

**Background Colors:**
```css
.background-color {
    background-color: #f0f0f0;
    background-color: rgba(255, 255, 255, 0.9);
}
```

**Background Images:**
```css
.background-image {
    background-image: url('path/to/image.jpg');
    background-repeat: no-repeat;
    background-position: center center;
    background-size: cover;
}

/* Background shorthand */
.bg-shorthand {
    background: url('image.jpg') no-repeat center center/cover;
}
```

**Background Properties:**
```css
.background-properties {
    background-image: url('image.jpg');
    background-repeat: no-repeat;     /* repeat, repeat-x, repeat-y */
    background-position: top left;    /* center, bottom, right, etc. */
    background-size: cover;           /* contain, 100px 200px, 50% */
    background-attachment: fixed;     /* scroll, local */
}
```

**Multiple Backgrounds:**
```css
.multiple-backgrounds {
    background-image: 
        url('overlay.png'),
        url('background.jpg');
    background-position: 
        center center,
        top left;
    background-repeat: 
        no-repeat,
        repeat;
}
```

#### Gradients and Transparency

**Linear Gradients:**
```css
.linear-gradient {
    background: linear-gradient(to right, red, blue);
    background: linear-gradient(45deg, #ff0000, #0000ff);
    background: linear-gradient(to bottom, red 0%, yellow 50%, blue 100%);
}
```

**Radial Gradients:**
```css
.radial-gradient {
    background: radial-gradient(circle, red, blue);
    background: radial-gradient(ellipse at center, red 0%, blue 100%);
}
```

**Transparency Techniques:**
```css
.transparency {
    /* Using RGBA/HSLA */
    background-color: rgba(255, 0, 0, 0.5);
    
    /* Using opacity (affects entire element) */
    opacity: 0.8;
    
    /* Transparent keyword */
    border-color: transparent;
}
```

**Color Best Practices:**
- Ensure sufficient contrast for accessibility (4.5:1 ratio minimum)
- Use consistent color schemes throughout your site
- Test colors on different devices and screens
- Consider color blindness when choosing color combinations

**Resources:**
- **MDN CSS Colors**: [CSS Color](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Color)
- **Color Contrast Checker**: [WebAIM Contrast Checker](https://webaim.org/resources/contrastchecker/)
- **Coolors Color Palette Generator**: [Coolors.co](https://coolors.co/)

---
### Task 2 (Project)
1. Go through the individual section HTML files you created in [Part 1: HTML Fundamentals](1_html-fundamentals.md) and apply CSS styling as best as you can (you can already try to create multi-column layouts, but it will become much easier in the next section with CSS flexbox).
2. Create individual stylesheets as `.css` files and link them to the `.html` files they belong to.
---

## Assessment Checklist

Before moving to Part 3, ensure you can:
- [ ] Apply CSS using external, internal, and inline methods
- [ ] Use different types of selectors effectively
- [ ] Understand and calculate CSS specificity
- [ ] Implement the box model with proper sizing
- [ ] Style typography with web fonts and text properties
- [ ] Apply colors using different value formats
- [ ] Create background effects with images and gradients
- [ ] Debug CSS issues using developer tools
- [ ] Write clean, organized CSS code with proper commenting

---

## Next Steps

You're now ready for [Part 3: CSS Layout and Positioning](3_css-layout-and-positioning.md) where you'll learn advanced layout techniques including flexbox, grid, and responsive design principles.