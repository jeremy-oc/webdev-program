# Part 1: HTML Fundamentals

## Introduction to HTML

### What is HTML and How It Works

HTML (HyperText Markup Language) is the standard markup language used to create web pages. It provides the structure and content of websites using a system of elements and tags.

#### Key Concepts:
- HTML uses tags to define elements
- Elements can contain text, other elements, or both
- Browsers interpret HTML and display it as a web page
- HTML works alongside CSS (styling) and JavaScript (functionality)


#### Getting Started:
This section provides all the content necessary to learn about the most relevant HTML features that will be used in many occasions.

For the introduction to HTML & CSS we will be learning with the [The Odin Project](https://www.theodinproject.com) course created by Erik Trautman and the [Responsive Web Design] course by FreeCodeCamp.

### Task 1
1. Work through the [HTML Foundations](https://www.theodinproject.com/paths/foundations/courses/foundations#html-foundations) section of the "The Odin Project" Foundations course.
2. Interactivly work through the [Learn HTML by building a Cat Photo App](https://www.freecodecamp.org/learn/2022/responsive-web-design/learn-html-by-building-a-cat-photo-app/) course.
3. If you prefer a all in one tutorial there is a good overview available on YouTube by FreeCodeCamp: [Extensive HTML Tutorial](https://www.youtube.com/watch?v=kUMe1FH4CHE)


### Recap of the content

There are some concepts that you should be familiar with after going through these tutorials. There are some HTML elements that you might not be familiar with just by watching the tutorials, but you should be able to understand their structure and how to apply them to a website based on your other HTML knowledge. 

#### HTML Document Structure
Every HTML document follows a standard structure:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document Title</title>
</head>
<body>
    <!-- Page content goes here -->
</body>
</html>
```

**Document Components:**
- `<!DOCTYPE html>`: Declares HTML5 document type
- `<html>`: Root element containing all content
- `<head>`: Contains metadata and document information
- `<body>`: Contains visible page content

**Additional Resources:**
- **MDN HTML Document Structure**: [Document and website structure](https://developer.mozilla.org/en-US/docs/Learn/HTML/Introduction_to_HTML/Document_and_website_structure)
- **W3Schools HTML Elements**: [HTML Elements](https://www.w3schools.com/html/html_elements.asp)

---

#### Basic HTML Elements Syntax

HTML uses tags to define elements. Tags are enclosed in angle brackets and usually come in pairs (opening and closing tags).

**Basic Syntax:**
```html
<tagname>Content goes here</tagname>

<tagname attribute="value">Content with attributes</tagname>

<voidelement />
```

**Essential HTML Tags to structure your Websites:**
- `<h1>` to `<h6>`: Headings
- `<p>`: Paragraphs
- `<div>`: Generic container
- `<span>`: Inline container
- `<br>`: Line break
- `<hr>`: Horizontal rule
- `<img>`: Image
- `<a>`: Anchor (Link)

**Resources:**
- **W3Schools HTML Tags**: [HTML Tag Reference](https://www.w3schools.com/tags/)
- **MDN HTML Elements**: [HTML elements reference](https://developer.mozilla.org/en-US/docs/Web/HTML/Element)

#### Nesting Elements

HTML elements can contain other elements, creating a hierarchical structure. Proper nesting is crucial for valid HTML.

**Correct Nesting:**
```html
<div>
    <h2>Section Title</h2>
    <p>This paragraph is properly nested inside the div.</p>
    <ul>
        <li>List item 1</li>
        <li>List item 2</li>
    </ul>
</div>
```

**Important Rules:**
- Always close tags in the reverse order they were opened
- Block elements can contain inline elements
- Inline elements cannot contain block elements
- Some elements are self-closing (`<img>`, `<br>`, `<hr>`)

#### Attributes

Attributes provide additional information about HTML elements and are specified in the opening tag.

**Common Attributes:**
- `lang`: Language of the HTML document (in `<html>` tag)
- `id`: Unique identifier for an element
- `class`: CSS class name(s) for styling
- `href`: URL for links
- `src`: Source URL for images, scripts, etc.
- `alt`: Alternative text for images

**Example:**
```html
<img src="image.jpg" alt="Description" id="main-image" class="responsive">

<a href="https://example.com">Link text</a>
```

**Resources:**
- **MDN HTML Attributes**: [HTML attribute reference](https://developer.mozilla.org/en-US/docs/Web/HTML/Attributes)
- **W3Schools HTML Attributes**: [HTML Attributes](https://www.w3schools.com/html/html_attributes.asp)

---

#### List Elements (Ordered and Unordered Lists)

**Unordered Lists:**
```html
<ul>
    <li>First item</li>
    <li>Second item</li>
    <li>Third item</li>
</ul>
```

**Ordered Lists:**
```html
<ol>
    <li>Step one</li>
    <li>Step two</li>
    <li>Step three</li>
</ol>
```

---

#### Links and Navigation

**External Links:**
```html
<a href="https://www.example.com">Visit Example Website</a>

<a href="https://www.example.com" target="_blank">Open in New Tab</a>
```

**Internal Links:**
```html
<a href="about.html">About Page</a>
<a href="./pages/contact.html">Contact Page</a>
<a href="../index.html">Back to Home</a>
```

**Email and Phone Links:**
```html
<a href="mailto:someone@example.com">Send Email</a>
<a href="tel:+1234567890">Call Us</a>
```

### Anchor Links and Navigation

**Anchor Links (Same Page):**
```html
<a href="#section1">Go to Section 1</a>
<a href="#top">Back to Top</a>

<!-- Target elements -->
<h2 id="section1">Section 1</h2>
<div id="top">Top of page</div>
```

**Navigation Menu:**
```html
<nav>
    <ul>
        <li><a href="index.html">Home</a></li>
        <li><a href="about.html">About</a></li>
        <li><a href="services.html">Services</a></li>
        <li><a href="contact.html">Contact</a></li>
    </ul>
</nav>
```

**Resources:**
- **The Odin Project**: [Links and Images](https://www.theodinproject.com/lessons/foundations-links-and-images)
- **MDN Creating Hyperlinks**: [Creating hyperlinks](https://developer.mozilla.org/en-US/docs/Learn/HTML/Introduction_to_HTML/Creating_hyperlinks)

---

#### Images and Media

**Basic Image Syntax:**
```html
<img src="path/to/image.jpg" alt="Description of image">
```

**Image with Additional Attributes:**
```html
<img src="profile.jpg" 
     alt="John Doe's profile photo" 
     width="300" 
     height="200">
```

#### Alternative Text and Accessibility

**Alt Text Guidelines:**
- Describe the image content and purpose
- Keep it concise but descriptive
- Use empty alt (`alt=""`) for decorative images
- Don't use "image of" or "picture of"

**Examples:**
```html
<!-- Informative image -->
<img src="chart.png" alt="Sales increased 25% from 2023 to 2024">

<!-- Decorative image -->
<img src="decoration.png" alt="">

<!-- Functional image (button) -->
<img src="search-icon.png" alt="Search icon">
```

#### Audio and Video Elements

**Video Element:**
```html
<video controls width="640" height="480">
    <source src="video.mp4" type="video/mp4">
    <source src="video.webm" type="video/webm">
    Your browser does not support the video element.
</video>
```

**Audio Element:**
```html
<audio controls>
    <source src="audio.mp3" type="audio/mpeg">
    <source src="audio.ogg" type="audio/ogg">
    Your browser does not support the audio element.
</audio>
```

**Resources:**
- **MDN Images in HTML**: [Images in HTML](https://developer.mozilla.org/en-US/docs/Learn/HTML/Multimedia_and_embedding/Images_in_HTML)
- **W3Schools HTML Media**: [HTML Audio and Video](https://www.w3schools.com/html/html_media.asp)

---

#### Tables and Forms

**Basic Table Structure:**
```html
<table>
    <thead>
        <tr>
            <th>Name</th>
            <th>Age</th>
            <th>City</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>John Doe</td>
            <td>30</td>
            <td>New York</td>
        </tr>
        <tr>
            <td>Jane Smith</td>
            <td>25</td>
            <td>Los Angeles</td>
        </tr>
    </tbody>
</table>
```

**Table with Caption and Scope:**
```html
<table>
    <caption>Employee Information</caption>
    <thead>
        <tr>
            <th scope="col">Name</th>
            <th scope="col">Department</th>
            <th scope="col">Salary</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <th scope="row">John Doe</th>
            <td>Engineering</td>
            <td>$75,000</td>
        </tr>
    </tbody>
</table>
```

#### Form Elements and Input Types

**Basic Form Structure:**
```html
<form action="/submit" method="post">
    <label for="name">Name:</label>
    <input type="text" id="name" name="name" required>
    
    <label for="email">Email:</label>
    <input type="email" id="email" name="email" required>
    
    <label for="message">Message:</label>
    <textarea id="message" name="message" rows="4" cols="50"></textarea>
    
    <button type="submit">Submit</button>
</form>
```

**Input Types:**
```html
<input type="text" placeholder="Enter text">

<input type="email" placeholder="Enter email">

<input type="password" placeholder="Enter password">

<input type="number" min="1" max="100">

<input type="date">

<input type="checkbox" id="agree">

<input type="radio" name="gender" value="female">

<input type="file" accept=".pdf,.doc,.docx">

```

**Select and Option Elements:**
```html
<label for="country">Country:</label>
<select id="country" name="country">
    <option value="">Choose a country</option>
    <option value="us">United States</option>
    <option value="ca">Canada</option>
    <option value="uk">United Kingdom</option>
</select>
```

### Form Validation and Accessibility

**HTML5 Validation:**
```html
<form>
    <label for="username">Username (required):</label>
    <input type="text" id="username" name="username" required minlength="3" maxlength="20">
    
    <label for="age">Age (18-100):</label>
    <input type="number" id="age" name="age" min="18" max="100">
    
    <label for="website">Website:</label>
    <input type="url" id="website" name="website">
    
    <button type="submit">Submit</button>
</form>
```

**Accessibility Best Practices:**
- Always use `<label>` elements with form inputs
- Use `for` attribute to associate labels with inputs
- Group related form elements with `<fieldset>` and `<legend>`
- Provide clear error messages and instructions

**Resources:**
- **FreeCodeCamp Interactive**: [Learn HTML Forms by Building a Registration Form](https://www.freecodecamp.org/learn/2022/responsive-web-design/learn-html-forms-by-building-a-registration-form/)
- **MDN Web Forms**: [Your first web form](https://developer.mozilla.org/en-US/docs/Learn/Forms/Your_first_form)

---

#### Semantic HTML

Semantic HTML uses elements that have meaning and describe the content structure, making websites more accessible and SEO-friendly.

**Semantic vs Non-Semantic:**
```html
<!-- Non-semantic -->
<div class="header">
    <div class="nav">...</div>
</div>
<div class="main">
    <div class="article">...</div>
</div>

<!-- Semantic -->
<header>
    <nav>...</nav>
</header>
<main>
    <article>...</article>
</main>
```

#### Page Structure with Semantic Elements

**Complete Page Structure:**
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Semantic HTML Example</title>
</head>
<body>
    <header>
        <h1>Website Title</h1>
        <nav>
            <ul>
                <li><a href="#home">Home</a></li>
                <li><a href="#about">About</a></li>
                <li><a href="#contact">Contact</a></li>
            </ul>
        </nav>
    </header>

    <main>
        <section>
            <h2>About Us</h2>
            <article>
                <h3>Our Story</h3>
                <p>Content about the company...</p>
            </article>
        </section>
        
        <aside>
            <h3>Related Links</h3>
            <ul>
                <li><a href="#">Link 1</a></li>
                <li><a href="#">Link 2</a></li>
            </ul>
        </aside>
    </main>

    <footer>
        <p>&copy; 2024 Company Name. All rights reserved.</p>
    </footer>
</body>
</html>
```

**Semantic Elements:**
- `<header>`: Page or section header
- `<nav>`: Navigation links
- `<main>`: Main content area
- `<section>`: Thematic grouping of content
- `<article>`: Self-contained content
- `<aside>`: Sidebar or complementary content
- `<footer>`: Page or section footer
- `<figure>` and `<figcaption>`: Images with captions
- `<time>`: Dates and times
- `<address>`: Contact information

---

### Task 2 (Project)
1. Create HTML files with base structure for the individual sections of the portfolio as described [here](project_personal-portfolio.md)
2. Create a basic HTML structure with all the elements that are part of the individual sections in their respective HTML file (as best as you currently can).
3. Apply what you learned about semantic HTML and accessibility (`alt` attributes for images, `label` elements in forms).
---

## Assessment Checklist

Before moving to Part 2, ensure you can:
- [ ] Create valid HTML5 documents with proper structure
- [ ] Use semantic HTML elements appropriately
- [ ] Implement navigation with proper link structure
- [ ] Add images with appropriate alt text
- [ ] Understand the relationship between HTML elements
- [ ] Write clean, well-organized HTML code

---

## Next Steps

Once you've mastered HTML fundamentals, you'll move on to [Part 2: CSS Fundamentals](2_css-fundamentals.md) where you'll learn to style your HTML content and create visually appealing web pages.