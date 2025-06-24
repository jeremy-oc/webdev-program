# Part 1: Accessibility Fundamentals

## Understanding Web Accessibility

### What is Web Accessibility and Why It Matters

Web accessibility means that people with disabilities can use the web. More specifically, web accessibility means that people with disabilities can perceive, understand, navigate, and interact with the web, and that they can contribute to the web.

#### Key Concepts:
- Accessibility is about removing barriers for people with disabilities
- It benefits everyone, not just people with disabilities
- It's a legal requirement in many jurisdictions
- It improves overall user experience and usability
- It's an ongoing process, not a one-time fix

#### Getting Started:
This section provides all the content necessary to learn about web accessibility fundamentals that will form the foundation for creating inclusive web experiences.

For learning web accessibility, we will be using resources from the [Web Accessibility Initiative (WAI)](https://www.w3.org/WAI/), [WebAIM](https://webaim.org/), and interactive courses from various accessibility experts.

### Task 1
1. Read through the [Web Accessibility Introduction](https://www.w3.org/WAI/fundamentals/accessibility-intro/) by W3C WAI
2. Complete the [WebAIM Screen Reader Testing](https://webaim.org/articles/screenreader_testing/) introduction
3. Watch [Web Accessibility Fundamentals](https://www.youtube.com/watch?v=z8xUCzToff8) by Google Chrome Developers
4. Install a screen reader on your system (NVDA for Windows, VoiceOver for Mac, or Orca for Linux)

### Recap of the Content

There are some concepts that you should be familiar with after going through these tutorials. Understanding these fundamentals is crucial for building accessible web experiences.

#### Types of Disabilities and How They Affect Web Usage

**Visual Disabilities:**
- Blindness: Complete or nearly complete vision loss
- Low vision: Significant visual impairment not correctable by glasses
- Color blindness: Difficulty distinguishing certain colors

**Hearing Disabilities:**
- Deafness: Complete or nearly complete hearing loss
- Hard of hearing: Mild to moderate hearing loss

**Motor/Physical Disabilities:**
- Limited fine motor control
- Paralysis or limb deficiencies
- Tremors or muscle weakness

**Cognitive Disabilities:**
- Learning disabilities (dyslexia, ADHD)
- Memory impairments
- Autism spectrum disorders
- Intellectual disabilities

**How These Affect Web Usage:**
- Screen readers for visual disabilities
- Keyboard-only navigation for motor disabilities
- Captions and transcripts for hearing disabilities
- Simple language and clear navigation for cognitive disabilities

**Additional Resources:**
- **WebAIM Disability Types**: [Types of Disabilities](https://webaim.org/articles/visual/)
- **W3C Diverse Abilities**: [How People with Disabilities Use the Web](https://www.w3.org/WAI/people-use-web/)

---

#### The Business Case for Accessibility

Accessibility provides significant business benefits beyond legal compliance:

**Market Reach:**
- 15% of the world's population has some form of disability
- $13 trillion in annual disposable income globally
- Aging population with increasing accessibility needs

**SEO and Technical Benefits:**
- Semantic HTML improves search engine rankings
- Better site structure and navigation
- Improved performance and mobile usability
- Reduced maintenance costs

**Brand Value:**
- Enhanced reputation and corporate responsibility
- Increased customer loyalty
- Positive media attention
- Competitive advantage

**Example Business Impact:**
```html
<!-- Accessible form increases completion rates -->
<form>
    <label for="email">Email Address (required)</label>
    <input type="email" id="email" name="email" required 
           aria-describedby="email-help">
    <div id="email-help">We'll never share your email</div>
    
    <button type="submit">Subscribe to Newsletter</button>
</form>
```

#### Legal Requirements and Compliance Standards

**Key Legislation:**
- **ADA (Americans with Disabilities Act)**: US federal law
- **Section 508**: US federal agency requirements
- **AODA (Accessibility for Ontarians with Disabilities Act)**: Ontario, Canada
- **EN 301 549**: European accessibility standard
- **JIS X 8341**: Japanese accessibility guidelines

**Compliance Levels:**
- **Level A**: Minimum level of accessibility
- **Level AA**: Standard level (most commonly required)
- **Level AAA**: Highest level (rarely required for entire sites)

**Legal Considerations:**
```html
<!-- Legal compliance example: Proper heading structure -->
<h1>Main Page Title</h1>
    <h2>Section Title</h2>
        <h3>Subsection Title</h3>
        <h3>Another Subsection</h3>
    <h2>Another Section</h2>
```

**Resources:**
- **WebAIM Legal Requirements**: [Legal Requirements](https://webaim.org/articles/laws/)
- **W3C Policy Resources**: [Web Accessibility Laws & Policies](https://www.w3.org/WAI/policies/)

---

## Introduction to WCAG

### Web Content Accessibility Guidelines Overview

WCAG 2.1 is organized around four main principles that provide the foundation for web accessibility.

#### The Four Principles: POUR

**1. Perceivable**
Information and UI components must be presentable to users in ways they can perceive.

```html
<!-- Example: Alt text for images -->
<img src="chart.jpg" alt="Sales increased 25% from Q1 to Q2 2024">

<!-- Example: Captions for video -->
<video controls>
    <source src="presentation.mp4" type="video/mp4">
    <track kind="captions" src="captions.vtt" srclang="en" label="English">
</video>
```

**2. Operable**
UI components and navigation must be operable by all users.

```html
<!-- Example: Keyboard accessible button -->
<button onclick="toggleMenu()" onkeydown="handleKeyPress(event)">
    Menu
</button>

<!-- Example: Skip navigation link -->
<a href="#main-content" class="skip-link">Skip to main content</a>
```

**3. Understandable**
Information and the operation of UI must be understandable.

```html
<!-- Example: Clear form labels and instructions -->
<label for="password">Password (minimum 8 characters)</label>
<input type="password" id="password" name="password" 
       minlength="8" aria-describedby="pwd-help">
<div id="pwd-help">Include letters, numbers, and symbols</div>
```

**4. Robust**
Content must be robust enough to be interpreted reliably by assistive technologies.

```html
<!-- Example: Semantic HTML -->
<main>
    <article>
        <h2>Article Title</h2>
        <p>Article content...</p>
    </article>
</main>
```

#### Understanding Conformance Levels

**Level A (Minimum):**
- Basic accessibility features
- Essential for any public website
- Examples: Alt text, keyboard navigation, proper headings

**Level AA (Standard):**
- Recommended for most websites
- Legal requirement in many jurisdictions
- Examples: Color contrast ratios, captions for videos

**Level AAA (Enhanced):**
- Highest level of accessibility
- Not required for entire websites
- Examples: Sign language interpretation, extended audio descriptions

### Key Success Criteria and Practical Applications

**Success Criterion 1.1.1 - Non-text Content (Level A):**
```html
<!-- Informative image -->
<img src="graph.png" alt="Website traffic increased 40% after redesign">

<!-- Decorative image -->
<img src="border-decoration.png" alt="" role="presentation">

<!-- Functional image -->
<button>
    <img src="search-icon.png" alt="Search">
</button>
```

**Success Criterion 1.4.3 - Contrast (Level AA):**
```css
/* Minimum contrast ratio 4.5:1 for normal text */
.text {
    color: #333333; /* Dark gray */
    background-color: #ffffff; /* White */
}

/* Minimum contrast ratio 3:1 for large text */
.large-text {
    font-size: 18px;
    font-weight: bold;
    color: #666666;
    background-color: #ffffff;
}
```

**Success Criterion 2.1.1 - Keyboard (Level A):**
```html
<!-- All interactive elements must be keyboard accessible -->
<button>Click Me</button> <!-- Native button is keyboard accessible -->

<!-- For custom interactive elements, use native elements when possible -->
<a href="#section1" role="button">Go to Section 1</a>

<!-- If custom styling is needed, start with semantic HTML -->
<button class="custom-styled-button">Custom Button</button>
```

**Success Criterion 3.3.1 - Error Identification (Level A):**
```html
<form>
    <label for="email">Email Address</label>
    <input type="email" id="email" name="email" required 
           aria-describedby="email-error">
    <!-- Error message will be shown by browser validation or server-side -->
    <div id="email-error">
        Please enter a valid email address
    </div>
</form>
```

**Resources:**
- **WCAG 2.1 Guidelines**: [Web Content Accessibility Guidelines](https://www.w3.org/WAI/WCAG21/quickref/)
- **WebAIM WCAG Checklist**: [WCAG 2 Checklist](https://webaim.org/standards/wcag/checklist)

---

## Accessibility and Universal Design

### Universal Design Principles in Web Development

Universal Design creates products usable by all people, to the greatest extent possible, without the need for adaptation.

**The Seven Principles:**

1. **Equitable Use**: Useful to people with diverse abilities
2. **Flexibility in Use**: Accommodates preferences and abilities
3. **Simple and Intuitive Use**: Easy to understand
4. **Perceptible Information**: Communicates effectively
5. **Tolerance for Error**: Minimizes hazards of accidental actions
6. **Low Physical Effort**: Efficient and comfortable to use
7. **Size and Space**: Appropriate for approach and use

**Web Implementation Examples:**
```html
<!-- Principle 1: Equitable Use - Multiple ways to access content -->
<video controls>
    <source src="video.mp4" type="video/mp4">
    <track kind="captions" src="captions.vtt" srclang="en">
    <track kind="descriptions" src="descriptions.vtt" srclang="en">
</video>
<p><a href="transcript.html">View full transcript</a></p>

<!-- Principle 3: Simple and Intuitive Use -->
<nav aria-label="Main navigation">
    <ul>
        <li><a href="/" aria-current="page">Home</a></li>
        <li><a href="/about">About</a></li>
        <li><a href="/contact">Contact</a></li>
    </ul>
</nav>
```

#### Inclusive Design Methodologies

**Design Process:**
1. **Include diverse users** in design and testing
2. **Consider accessibility from the start** (not as an afterthought)
3. **Test with real users** including people with disabilities
4. **Iterate based on feedback** from diverse user groups

**Inclusive Design Examples:**
```html
<!-- Multiple input methods -->
<div class="search-container">
    <label for="search">Search</label>
    <input type="search" id="search" name="search">
    <button type="submit">
        <span class="visually-hidden">Submit search</span>
        <svg aria-hidden="true"><!-- Search icon --></svg>
    </button>
</div>

<!-- Flexible content presentation -->
<article>
    <h2>Article Title</h2>
    <div class="meta">
        <time datetime="2024-01-15">January 15, 2024</time>
        <span class="reading-time">5 min read</span>
    </div>
    <p>Article content with clear structure...</p>
</article>
```

#### Accessibility as a Quality Indicator

**Quality Metrics:**
- **Code Quality**: Semantic HTML, valid markup
- **User Experience**: Clear navigation, consistent interface
- **Performance**: Fast loading, efficient interaction
- **Maintainability**: Clean, organized code structure

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

#### Debunking Common Accessibility Myths

**Myth 1: "Accessibility is expensive and time-consuming"**
- **Reality**: Costs more to retrofit than build in from start
- **Solution**: Include accessibility in initial requirements

**Myth 2: "Accessibility makes websites look boring"**
- **Reality**: Accessibility improves design for everyone
- **Example**: Good color contrast benefits all users

**Myth 3: "Only a small percentage of users need accessibility"**
- **Reality**: 15% of population + temporary disabilities + aging users
- **Benefits**: Improved SEO, better mobile experience

**Myth 4: "Automated tools catch all accessibility issues"**
- **Reality**: Automated tools catch only 20-30% of issues
- **Solution**: Combine automated testing with manual testing

---

### Task 2
1. Choose a popular website and identify potential accessibility barriers using the WCAG principles
2. Create a simple HTML page that demonstrates each of the four WCAG principles
3. Test your page with a screen reader and document your findings
4. Research accessibility laws in your country/region and create a summary

### Task 3 (Project Setup)
1. Set up your development environment for accessibility testing:
   - Install a screen reader (NVDA, VoiceOver, or Orca)
   - Install browser extensions (axe DevTools, WAVE)
   - Set up color contrast testing tools
2. Create a basic HTML page structure for your accessibility audit project
3. Document your testing setup and create a checklist for future accessibility reviews

---

## Assessment Checklist

Before moving to Part 2, ensure you can:
- [ ] Explain the four principles of WCAG (POUR)
- [ ] Identify different types of disabilities and their web usage needs
- [ ] Understand the business and legal case for accessibility
- [ ] Use basic accessibility testing tools
- [ ] Apply universal design principles to web development
- [ ] Distinguish between accessibility myths and facts

---

## Next Steps

Once you've mastered accessibility fundamentals, you'll move on to [Part 2: Semantic HTML and ARIA](2_semantic-html-and-aria.md) where you'll learn to implement semantic markup and ARIA attributes for enhanced accessibility.