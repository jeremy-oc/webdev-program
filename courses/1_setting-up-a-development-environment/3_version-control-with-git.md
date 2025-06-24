# Part 3: Version Control with Git

## Introduction to Version Control

### What is Version Control and Why It's Essential

Version control is a system that records changes to files over time, allowing you to recall specific versions later. Think of it as a detailed history of your project that lets you:

- **Track changes**: See exactly what changed, when, and who made the change
- **Collaborate safely**: Multiple people can work on the same project without conflicts
- **Backup and recovery**: Never lose work due to accidental deletion or corruption
- **Experimentation**: Try new features without fear of breaking existing code
- **Release management**: Maintain multiple versions of your software

#### Real-World Analogies
- **Document versioning**: Like having multiple drafts of an essay with tracked changes
- **Save game checkpoints**: Return to previous states when things go wrong
- **Photography contact sheets**: Multiple versions of the same shot to choose from

### Understanding Git vs GitHub

This distinction is crucial for beginners:

#### Git
- **What it is**: Version control software that runs on your computer
- **Function**: Tracks changes in your local files and folders
- **Location**: Works entirely offline on your machine
- **Analogy**: Like a sophisticated "undo" system for your entire project

#### GitHub
- **What it is**: Online service that hosts Git repositories
- **Function**: Stores your code online and enables collaboration
- **Location**: Cloud-based platform accessible via web browser
- **Analogy**: Like Dropbox or Google Drive, but specifically designed for code with Git integration

#### The Relationship
- Git manages version control locally
- GitHub stores your Git repositories online
- You use Git commands to sync between local and GitHub
- GitHub adds collaboration features on top of Git

### Benefits of Version Control in Web Development

#### For Individual Developers
- **Experiment fearlessly**: Try new approaches knowing you can revert
- **Bug tracking**: Identify exactly when and where bugs were introduced
- **Feature development**: Work on multiple features simultaneously
- **Backup security**: Never lose work due to hardware failure

#### For Team Collaboration
- **Conflict resolution**: Merge changes from multiple developers safely
- **Code review**: Review and discuss changes before they're implemented
- **Accountability**: Track who made what changes and when
- **Release coordination**: Manage different versions and deployments

#### For Client Work
- **Change requests**: Easily revert or modify previous work
- **Project history**: Show client the evolution of their project
- **Backup assurance**: Professional backup and recovery capabilities
- **Quality control**: Maintain stable versions while developing new features

## Installing Git

### System Requirements and Preparation

Before installing Git, ensure your system meets basic requirements:
- **Operating system**: Windows, macOS or any modern Linux distribution
- **Administrator access**: Required for installation

### Installing Git on Windows

#### Download and Installation
1. **Visit**: [https://git-scm.com/download/win](https://git-scm.com/download/win)
2. **Download**: The installer automatically detects your system (32-bit or 64-bit)
3. **Run installer**: Execute the downloaded `.exe` file

#### Installation Options (Recommended Settings)
- **Text editor**: Choose your preferred editor (VS Code recommended)
- **PATH environment**: "Git from the command line and 3rd-party software"
- **HTTPS transport**: "Use the OpenSSL library"
- **Line ending conversions**: "Checkout Windows-style, commit Unix-style"
- **Terminal emulator**: "Use Windows' default console window"
- **Git Credential Manager**: Enable for easier GitHub authentication

#### Verification
Open Command Prompt or PowerShell and type:
```bash
git --version
```
You should see output like: `git version 2.x.x`

### Installing Git on macOS

#### Homebrew (Recommended)
If you have Homebrew installed:
```bash
brew install git
```

You can find the instructions to install Homebrew [here](https://brew.sh/).

#### Verification
Open Terminal and type:
```bash
git --version
```

### Installing Git on Linux

#### Ubuntu/Debian
```bash
sudo apt update
sudo apt install git
```

#### CentOS/RHEL/Fedora
```bash
# CentOS/RHEL
sudo yum install git

# Fedora
sudo dnf install git
```

#### Arch Linux
```bash
sudo pacman -S git
```

#### Verification
```bash
git --version
```

### Configuring Git with Your Name and Email

After installation, configure Git with your identity:

#### Essential Configuration
```bash
git config --global user.name "Your Full Name"
git config --global user.email "your.email@example.com"
```

#### Verify Configuration
```bash
git config --list
```

### Understanding Git Terminology

Learning Git terminology is essential for effective use:

#### Repository (Repo)
- **Definition**: A folder containing your project files and Git history
- **Types**: Local (on your computer) and remote (on GitHub)
- **Analogy**: Like a project folder with a complete timeline

#### Commit
- **Definition**: A snapshot of your project at a specific point in time
- **Content**: Changes made + descriptive message
- **Analogy**: Like saving a checkpoint in a video game

#### Branch
- **Definition**: An independent line of development
- **Purpose**: Work on features without affecting main code
- **Default**: Usually "main" or "master"

#### Working Directory
- **Definition**: Your current project folder where you edit files
- **Status**: Files can be modified, staged, or committed
- **Visibility**: What you see in your file explorer

#### Staging Area (Index)
- **Definition**: A prep area for your next commit
- **Purpose**: Choose exactly which changes to include
- **Analogy**: Like a shopping cart before checkout

#### HEAD
- **Definition**: Pointer to your current location in Git history
- **Typically**: Points to the latest commit on current branch
- **Movement**: Changes when you switch branches or commits

## Git Fundamentals

### Initializing a Git Repository

#### Creating a New Repository
Navigate to your project folder and run:
```bash
git init
```

This creates a hidden `.git` folder containing all Git data.

#### What Happens During Initialization
- Creates `.git` directory with Git metadata
- Sets up initial branch (usually "main")
- Prepares tracking for all files in the folder
- Repository is now ready for commits

#### Verifying Initialization
```bash
git status
```
You should see: "On branch main" and "No commits yet"

### Adding and Committing Files

#### The Git Workflow
1. **Modify files** in your working directory
2. **Stage changes** you want to commit
3. **Commit staged changes** with a message

#### Staging Files
```bash
# Stage a specific file
git add filename.html

# Stage multiple files
git add file1.css file2.js

# Stage all files
git add .

# Stage all HTML files
git add *.html
```

#### Committing Changes
```bash
# Commit with inline message
git commit -m "Add homepage HTML structure"

# Commit with detailed message (opens editor)
git commit
```

#### Best Practices for Commit Messages
- **Use imperative mood**: "Add feature" not "Added feature"
- **Be specific**: "Fix navigation menu alignment" not "Fix bug"
- **Keep first line under 50 characters**
- **Use detailed description for complex changes**

#### Examples of Good Commit Messages
```bash
git commit -m "Add responsive navigation menu"

git commit -m "Fix CSS grid layout on mobile devices"

git commit -m "Update contact form validation"

git commit -m "Remove unused JavaScript functions"
```

### Understanding the Git Workflow

#### The Three States of Files
1. **Modified**: Changed but not staged
2. **Staged**: Marked for next commit
3. **Committed**: Stored in Git history

#### Checking File Status
```bash
git status
```

Output explanation:
- **Red files**: Modified but not staged
- **Green files**: Staged and ready to commit
- **"Clean working tree"**: No changes to commit

#### Viewing Changes
```bash
# See unstaged changes
git diff

# See staged changes
git diff --staged

# See changes in specific file
git diff filename.html
```

### Basic Git Commands

#### Essential Commands for Daily Use

**Checking Status**
```bash
git status          # Show current status
```

**Adding Files**
```bash
git add filename    # Stage specific file
git add .          # Stage all changes
git add -A         # Stage all changes (including deletions)
```

**Committing**
```bash
git commit -m "message"     # Commit with message
```

**Viewing History**
```bash
git log                 # Show commit history
```



### Ignoring Files
Create a `.gitignore` file to exclude files from version control:
```
# Operating system files
.DS_Store
Thumbs.db

# Editor files
.vscode/
*.swp
*.swo

# Dependencies
node_modules/
bower_components/

# Build outputs
dist/
build/
*.min.js
*.min.css

# Logs
*.log
logs/

# Environment files
.env
.env.local
```

### Practical Examples

#### Example 1: Starting a New Web Project
```bash
# Create project directory
mkdir my-website
cd my-website

# Initialize Git repository
git init

# Create initial files
touch index.html style.css script.js

# Add initial content to index.html
echo "<!DOCTYPE html><html><head><title>My Website</title></head><body><h1>Hello World</h1></body></html>" > index.html

# Stage and commit initial files
git add .
git commit -m "Initial project setup with basic HTML structure"
```

#### Example 2: Making Changes and Committing
```bash
# Edit CSS file (imagine adding styles)
# Check what changed
git status
git diff style.css

# Stage and commit changes
git add style.css
git commit -m "Add basic styling for header and navigation"

# View commit history
git log --oneline
```

#### Example 3: Working with Multiple Files
```bash
# Modify multiple files
# Check status
git status

# Stage specific files
git add index.html style.css

# Commit staged files
git commit -m "Update HTML structure and corresponding styles"

# Stage remaining files
git add script.js
git commit -m "Add interactive functionality with JavaScript"
```

### Common Git Workflows

#### Daily Development Workflow
1. **Start work**: `git status` to check current state
2. **Make changes**: Edit files in your editor
3. **Review changes**: `git diff` to see what changed
4. **Stage changes**: `git add` specific files or `git add .`
5. **Commit changes**: `git commit -m "descriptive message"`
6. **Repeat**: Continue this cycle for ongoing development

#### Feature Development Workflow
1. **Plan feature**: Understand what you're building
2. **Make small commits**: Break work into logical chunks
3. **Test frequently**: Ensure code works at each step
4. **Commit milestones**: Save progress at working points
5. **Review before finishing**: Check all changes make sense

#### Problem-Solving Workflow
1. **Identify issue**: Understand what needs fixing
2. **Use Git history**: `git log` to see when problem was introduced
3. **Make targeted fix**: Address specific issue
4. **Test fix**: Ensure problem is resolved
5. **Commit fix**: Clear message describing solution

### Git Best Practices

#### Commit Frequency
- **Commit often**: Small, frequent commits are better than large ones
- **Logical chunks**: Each commit should represent a complete thought
- **Working state**: Only commit code that works (compiles/runs)
- **One feature per commit**: Don't mix unrelated changes

#### Commit Message Guidelines
- **First line summary**: Clear, concise description under 50 characters
- **Imperative mood**: "Add", "Fix", "Update", not "Added", "Fixed"
- **Detailed explanation**: Use body for complex changes
- **Reference issues**: Include ticket numbers when applicable (becomes relevant when working in a professional setting)

#### File Organization
- **Use .gitignore**: Exclude files that shouldn't be tracked
- **Track source files**: Include original HTML, CSS, JS files
- **Exclude generated files**: Don't track minified or compiled files
- **Keep secrets out**: Never commit passwords or API keys

### Troubleshooting Common Issues

#### "Nothing to commit, working tree clean"
This means all changes are already committed. It's actually good news!

#### "Changes not staged for commit"
You've modified files but haven't staged them yet:
```bash
git add filename.xyz    # Stage specific file
git add .          # Stage all changes
```

#### "Your branch is ahead of 'origin/main'"
You have local commits that aren't pushed to remote yet. This is normal during development.

#### Accidentally staged wrong file
```bash
git restore --staged filename    # Unstage specific file
git restore --staged .          # Unstage all files
```

#### Want to undo last commit
```bash
git reset HEAD~1               # Undo commit, keep changes
git reset --hard HEAD~1        # Undo commit, discard changes (careful!)
```

#### Forgot to add file to last commit
```bash
git add forgotten-file.html
git commit --amend --no-edit    # Add to previous commit
```

### Viewing and Understanding Git Status

#### Interpreting `git status` Output

**Clean working directory:**
```
On branch main
nothing to commit, working tree clean
```

**With untracked files:**
```
On branch main
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        new-file.html

nothing added to commit but untracked files present
```

**With modified files:**
```
On branch main
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
        modified:   index.html
        modified:   style.css
```

**With staged changes:**
```
On branch main
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        modified:   index.html
        new file:   about.html
```

This foundation in Git basics prepares you for the next step: connecting your local Git repository to GitHub for backup, sharing, and collaboration.

[Part 4: Version Control with Git](4_github-integration.md)