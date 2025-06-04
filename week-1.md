# Week 1: Development Environment Setup & HTML/CSS Foundations

## Learning Objectives

By the end of this week, you will be able to:

- Set up a complete web development environment
- Structure a HTML document with semantic elements
- Apply CSS styling and layout techniques
- Build and deploy a simple personal portfolio website
- Use Git and GitHub for version control and hosting of your portfolio

## Step 1: Development Environment Setup

### Code Editor Setup

For this course, we'll be using Visual Studio Code (VS Code) as our primary code editor. VS Code is an excellent choice for web development because it's free, lightweight, and packed with features that will make your coding experience smoother. It offers excellent syntax highlighting, intelligent code completion, built-in terminal, and seamless Git integration. VS Code also has a vast ecosystem of extensions that we can explore later in the course to enhance our development workflow.

**Resources:**
- [Visual Studio Code](https://code.visualstudio.com/)

#### Task 1.1: Install VS Code

Download and install Visual Studio Code for your operating system (Windows, MacOS, Linux). Once installed, launch VS Code and familiarize yourself with the interface. For now, we'll use VS Code without any additional extensions to focus on the fundamentals.

### Web Browser Setup

As web developers, it's crucial to test our websites across different browsers to ensure compatibility and consistent user experience. Different browsers may render websites slightly differently, and some features might not work the same way across all browsers. Having multiple browsers installed allows us to catch potential issues early and deliver a better product to our users. We recommend installing at least Chrome and Firefox, as they are the most widely used browsers and offer excellent developer tools.

**Resources:**
- [Google Chrome](https://www.google.com/intl/de/chrome/)
- [Firefox](https://www.mozilla.org/de/firefox/new/)
- [Responsively App](https://responsively.app/) (Optional)

#### Task 1.2: Install different web browsers

Install Google Chrome and Firefox on your computer. These will be our primary testing browsers throughout the course. Optionally, you can also install Responsively App, which is a specialized browser for responsive web development.

### Git & GitHub Setup

Git is a version control system that tracks changes in your code, allowing you to collaborate with others and maintain a history of your project. GitHub is a cloud-based platform that hosts Git repositories, making it easy to share your code, collaborate with others, and showcase your work. Throughout this course, you'll use GitHub to store your projects and build an impressive portfolio of your web development journey.

**Resources:**
- [Git Download Page](https://git-scm.com/downloads)
- [GitHub](https://github.com/)

#### Task 1.3: Setup Git and GitHub

> **Note:** Getting the connection with GitHub running is a bit tricky as it requires setting up an SSH connection. The initial setup might take some guidance that we can handle during an input session. Here are guides to set it up for different operating systems:
> - [Generating a SSH key](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)
> - [Adding the SSH key to GitHub](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account)

**Step 1:** Download and install Git for your operating system from the link above.

**Step 2:** Create a free GitHub account at github.com if you don't already have one.

**Step 3:** Create a new repository on GitHub:
- Click the "+" icon in the top right corner of GitHub
- Select "New repository"
- Name your repository (e.g., "my-portfolio-website")
- Make sure it's set to "Public"
- Do NOT initialize with README, .gitignore, or license
- Click "Create repository"

**Step 4:** Set up your local project:
- Create a new folder on your computer for this project
- Open your terminal or command prompt
- Navigate to your project folder using the `cd` command

**Step 5:** Initialize your Git repository and push to GitHub by running these commands one by one:

```bash
echo "# My Portfolio Website" >> README.md
git init
git add README.md
git commit -m "Initial commit: Add README"
git branch -M main
git remote add origin https://github.com/username/repository-name.git
git push -u origin main
```

> **Note:** Replace "username" with your GitHub username and "repository-name" with the name of your repository.

After completing these steps, refresh your GitHub repository page. You should see your README.md file, confirming that your local repository is successfully connected to GitHub!

## Step 2: Introduction to HTML

HTML (HyperText Markup Language) is the foundation of every website. Think of it as the skeleton that gives structure to web pages. You'll learn HTML through a hands-on approach: first mastering the basics with a guided tutorial, then applying those skills to build your portfolio!

At first we will focus on building the "Hero" and "About me" section of the portfolio.

![Portfolio only with hero section and about me section and without CSS styling](assets/img/portfolio_example/portfolio_example_no_css_top.jpeg)

### Part 1: Learn HTML Fundamentals

Before building your portfolio, you'll learn HTML through FreeCodeCamp's interactive tutorial. This tutorial teaches you HTML by building a fun Cat Photo App, covering all the essential elements you'll need for your portfolio.

Beside the interactive Cat Photo App Tutorial there are some introductory HTML articles linked that might help you better understand the structure of HTML documents and elements.

**Resources:**
- [🐱 Cat Photo App Tutorial](https://www.freecodecamp.org/learn/2022/responsive-web-design/learn-html-by-building-a-cat-photo-app/step-1) (FreeCodeCamp)
- [MDN HTML Basics](https://developer.mozilla.org/en-US/docs/Learn/Getting_started_with_the_web/HTML_basics)
- [W3Schools HTML Introduction](https://www.w3schools.com/html/html_intro.asp)

#### Task 2.1: Complete the Cat Photo App Tutorial

> **Note:** For the tasks currently available the first half of the tutorial (the first 30-40 steps) might be enough. To build the whole portfolio the content of the later steps becomes relevant.

Work through FreeCodeCamp's "Learn HTML by Building a Cat Photo App" tutorial. This interactive tutorial will teach you:

- HTML document structure and basic elements
- Headings, paragraphs, and text formatting
- Images, links, and lists
- Forms and input elements
- HTML attributes and semantic elements

**Time estimate:** 1-2 hours. Take your time and make sure you understand each step before moving forward!

### Part 2: Build Your Portfolio HTML Structure

Now that you've learned HTML fundamentals through the Cat Photo App, it's time to apply those skills to create your own portfolio website! You'll use the same HTML elements and concepts, but arrange them to showcase your professional information.

#### 🏗️ From Cat Photos to Professional Portfolio

You'll use the same HTML elements from the tutorial (headings, paragraphs, images, lists, forms) but arrange them to create a professional portfolio structure.

### Portfolio HTML Structure

Your portfolio will have these main sections, each using HTML elements you learned in the Cat Photo App:

#### Task 2.2: Create your portfolio's HTML foundation

Create a new file called `index.html` in your project folder and build the basic structure:

**Step 1: HTML Document Structure**

```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>[Your Name] - Web Developer Portfolio</title>
</head>
<body>
<!-- Your portfolio content will go here -->
</body>
</html>
```

**Step 2: Build the Hero Section:**

- Add a `<header>` that contains a "logo" text and a `<nav>` with a list of links with empty `href` attribute for now
- Add a profile image (either AI generated or a real picture) using `<img>` with proper `src` and `alt` attributes
- Add your name as the main heading (`<h1>`)
- Add a subtitle describing what you do (e.g., "Aspiring Web Developer")
- Add a one sentence paragraph going a little bit more into detail

#### Task 2.3: Add content to your About Me section

Add an About Me section and fill it with real content:

- Add a greeting as a `<h3>` element
- Add an emoji that fits you inside of a `<div>`
- Write a paragraph about yourself (2-3 sentences)
- Give your sections proper `id` attributes (like `id="about"`)

### Test Your HTML

#### 🔍 View Your Work

Open your `index.html` file in your web browser to see your portfolio taking shape! It won't look pretty yet (no styling), but you should see all your content structured properly.

#### Task 2.4: Commit your HTML to GitHub

Save your progress to GitHub:

- Save your `index.html` file
- Open terminal/command prompt in your project folder
- Run: `git add .`
- Run: `git commit -m "Add portfolio HTML structure"`
- Run: `git push`

Your portfolio HTML is now saved on GitHub! 🎉

**Congratulations!** You've successfully learned HTML fundamentals through the Cat Photo App and applied those skills to create your portfolio's structure. Your website now has all the essential sections - it just needs some styling to make it beautiful, which we'll do in the next section with CSS!

## Step 3: Introduction to CSS

> **Coming Soon!** CSS content will be added here to teach you how to style your HTML with CSS, including layout, colors, fonts, and responsive design.

---

**Previous**: [Project Introduction](./project-introduction.md)  
**Next**: Week 2 (Coming Soon)