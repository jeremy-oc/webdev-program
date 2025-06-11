# Part 1: Code Editor Setup

## Installing Visual Studio Code

### What is Visual Studio Code?

Visual Studio Code (VS Code) is a free, open-source code editor developed by Microsoft. It's become the most popular choice for web developers due to its powerful features, extensive customization options, and robust ecosystem of extensions.

### Downloading VS Code

1. **Visit the official website**: Go to [https://code.visualstudio.com](https://code.visualstudio.com)
2. **Choose your platform**: The website automatically detects your operating system and suggests the appropriate download
3. **Download options**:
   - **Windows**: Download the `.exe` installer or the portable version
   - **macOS**: Download the `.dmg` file
   - **Linux**: Choose from `.deb`, `.rpm`, or `.tar.gz` packages

### Installation Process

#### Windows Installation
1. Run the downloaded `.exe` file
2. Accept the license agreement
3. Choose installation location (default is recommended)
4. Select additional tasks:
   - ✅ Add "Open with Code" action to Windows Explorer file context menu
   - ✅ Add "Open with Code" action to Windows Explorer directory context menu
   - ✅ Register Code as an editor for supported file types
   - ✅ Add to PATH (important for command line usage)
5. Click "Install" and wait for completion

#### macOS Installation
1. Open the downloaded `.dmg` file
2. Drag Visual Studio Code to the Applications folder
3. Launch VS Code from Applications or Spotlight search
4. If prompted about opening an app from the internet, click "Open"

#### Linux Installation
For Ubuntu/Debian:
```bash
sudo dpkg -i code_*.deb
sudo apt-get install -f
```

For Red Hat/Fedora:
```bash
sudo rpm -i code-*.rpm
```

### Initial Setup and Configuration

You don't have to understand all the explanations right away. Some points will become clearer as you use the tools to create websites and webapps.

#### First Launch
When you first open VS Code, you'll see:
- **Welcome tab**: Contains helpful getting-started information
- **Activity Bar**: On the left side with icons for different views
- **Editor area**: The main space where you'll write code
- **Status bar**: At the bottom showing file information

#### (Optional) Initial Settings

You can use VS Code out of the box, but if you want to make some customizations here are some suggestions:

1. **Theme Selection**: Go to File > Preferences > Color Theme (or Ctrl+K Ctrl+T)
   - Popular choices: Dark+ (default dark), Light+ (default light), Monokai
2. **Font Size**: File > Preferences > Settings, search "font size"
   - Recommended: 14-16px for better readability
3. **Auto Save**: File > Auto Save (or search "auto save" in settings)
   - Recommended: Enable for convenience

## Essential VS Code Features

### Emmet Abbreviations

Emmet is built into VS Code and dramatically speeds up HTML and CSS writing through abbreviations that expand into full code.

You can for example fill your HTML documents with a base structure:
- `!` + Tab → Creates basic HTML5 document structure

More on that in the Introduction to HTML part of this program.

### Prettier for Code Formatting

Prettier automatically formats your code to maintain consistent style across your projects.

Prettier should come pre-installed with your Visual Studio Code installation and can be used by the keyboard shortcut `Ctrl + Shift + p` followed by selecting "Format Document".

### Syntax Highlighting

VS Code provides excellent syntax highlighting out of the box for HTML, CSS, and JavaScript (and many other languages). The editor automatically detects file types and applies appropriate highlighting.

#### Language Modes
- VS Code automatically detects file types by extension
- You can manually change language mode in the bottom-right corner
- Common web file associations:
  - `.html` → HTML
  - `.css` → CSS
  - `.js` → JavaScript
  - `.json` → JSON

### Git Integration

VS Code has built-in Git support that provides visual indicators and easy-to-use Git operations.

#### Git Features in VS Code
- **Source Control view**: Shows changes, staged files, and commit history
- **Gutter indicators**: Show modified, added, and deleted lines
- **Diff viewer**: Compare file versions side by side
- **Branch management**: Switch branches from the status bar

#### Using Git in VS Code
1. **Initialize repository**: View > Command Palette > "Git: Initialize Repository"
2. **Stage changes**: Click the "+" next to files in Source Control view
3. **Commit changes**: Enter message and click checkmark
4. **View changes**: Click on modified files to see diff

### VS Code Extensions

Extensions enhance VS Code functionality for web development.

### Keyboard Shortcuts

Learning essential keyboard shortcuts dramatically improves coding efficiency.

Here are the most important for the beginning:

#### File Operations
- `Ctrl+S` → Save file
- `Ctrl+Shift+S` → Save as

#### Editing
- `Ctrl+Z` → Undo
- `Ctrl+Y` → Redo
- `Ctrl+C` → Copy
- `Ctrl+V` → Paste
- `Ctrl+X` → Cut
- `Ctrl+A` → Select all

This completes Part 1 of setting up your development environment. With VS Code properly installed and configured with essential features and extensions, you're ready to move on to setting up your browsers for testing and development.

[Part 2: Browser Installation and Setup](2_browser-installation-and-setup.md)