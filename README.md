# AGRI4401 Lectures Website

A Quarto-based website hosting lecture presentations for **AGRI4401: Precision Agriculture** at the University of Western Australia (UWA) School of Agriculture and Environment.

**Live Site:** https://00113844.github.io/AGRI4401_website/

---

## 📋 Project Structure

```
AGRI4401_website/
├── presentations/           # Source presentation files (Quarto format)
│   ├── lecture_01.qmd      # Lecture 1: Introduction to Precision Agriculture
│   ├── lecture_02.qmd
│   ├── ...
│   ├── uwa-theme.scss      # UWA brand theme (colors, fonts, styling)
│   ├── AGRI4401_PrecisionAg.css
│   └── assets/             # Images, logos, figures
│       └── uwa-logo-white.png
├── docs/                    # **Generated output folder** (deployed to GitHub Pages)
│   ├── presentations/       # Rendered HTML slides
│   │   └── lecture_01.html
│   └── index.html
├── _quarto.yml             # Quarto project configuration
├── index.qmd               # Homepage (listing of all lectures)
├── about.qmd               # About page
├── styles.css              # Global CSS styling
└── README.md               # This file
```

---

## 🔄 How the Pipeline Works

### 1. **Local Development (Your Machine)**

```
Edit .qmd files locally
        ↓
    [VS Code]
        ↓
quarto render (Build)
        ↓
docs/ folder updated with .html
```

When you edit a `.qmd` presentation file:
- **Quarto** processes the markdown + code blocks
- **RevealJS** transforms it into interactive HTML slides
- **SCSS theme** applies UWA branding (colors, fonts, styling)
- Output `.html` files go into `docs/` folder

### 2. **Version Control (Git)**

```
Make changes to .qmd files
        ↓
git add .
git commit -m "message"
git push origin main
        ↓
Changes pushed to GitHub
```

### 3. **Deployment (GitHub Pages)**

```
GitHub receives push
        ↓
GitHub Pages reads docs/ folder
        ↓
https://00113844.github.io/AGRI4401_website/ updated
        ↓
Live website reflects changes
```

**Note:** GitHub Pages automatically serves whatever is in the `docs/` folder. No additional build step happens on GitHub—it's already pre-rendered.

---

## 🚀 Workflow: Making Changes and Publishing

### Step 1: Edit a Presentation File

Edit a file like `presentations/lecture_01.qmd`:

```bash
cd presentations/
# Edit lecture_01.qmd in VS Code
```

### Step 2: Render Locally (Build)

Convert all `.qmd` files to `.html`:

```bash
quarto render
```

This command:
- Processes all `.qmd` files in the project
- Applies the `uwa-theme.scss` styling
- Generates `.html` files in `docs/presentations/`
- Updates the homepage index

### Step 3: Preview (Optional)

View the rendered output locally before committing:

```bash
quarto preview
```

Opens a local preview at `http://localhost:3000`

### Step 4: Commit and Push

```bash
git add docs/
git add presentations/
git commit -m "Beautify Lecture 01: Update UWA theme and structure"
git push origin main
```

### Step 5: Verify on GitHub Pages

1-2 minutes after pushing, visit: https://00113844.github.io/AGRI4401_website/

---

## 🎨 UWA Branding System

### Theme File: `presentations/uwa-theme.scss`

Contains all UWA brand styling:

```scss
// Colors
$uwa-blue:      #002147  // Primary blue
$uwa-gold:      #FFD100  // Accent gold
$uwa-grey:      #F5F5F5  // Background
$uwa-blue-tint: #b3c6d9  // Light blue for callouts

// Fonts
$font-family-sans-serif: "Roboto", Arial, sans-serif;
```

### Mermaid Diagrams

Flowcharts, timelines, and graphs automatically inherit UWA colors:

```{mermaid}
flowchart LR
    A[GPS/GNSS] --> B[IoT Sensors]
    B --> C[Cloud Platform]
```

---

## 📝 Editing Presentations

### YAML Front Matter (Header)

Each `.qmd` file starts with configuration:

```yaml
---
title: "Lecture Title"
subtitle: "AGRI4401 · Course · Lecture XX"
author:
  - name: "Gustavo Alckmin"
    affiliation: "School of Agriculture and Environment, UWA"
date: today
date-format: "D MMMM YYYY"
format:
  revealjs:
    theme: [default, uwa-theme.scss]
    slide-number: c/t
    transition: slide
---
```

### Slide Structure

```markdown
## Slide Title

- Bullet point 1
- Bullet point 2

::: {.notes}
Speaker notes (hidden from slides, visible in presenter view)
:::

---

## Next Slide
```

### Special Elements

**Learning Objectives Box:**
```markdown
::: learning-objectives
1. Define precision agriculture
2. Identify key technologies
:::
```

**Two-Column Layout:**
```markdown
:::: {.columns}
::: {.column width="50%"}
Left column content
:::
::: {.column width="50%"}
Right column content
:::
::::
```

**Section Divider (Dark Background):**
```markdown
## Section Title {background-color="#002147"}
```

---

## 🔧 Configuration Files

### `_quarto.yml` - Project Settings

Controls site-wide configuration:

```yaml
project:
  type: website
  output-dir: docs              # Output folder for GitHub Pages
website:
  title: "AGRI4401 Lectures"
  site-url: "https://..."
  navbar:
    left:
      - href: index.qmd
        text: "All Lectures"
```

### `index.qmd` - Homepage

Lists all presentations automatically:

```yaml
listing:
  contents: presentations/*.qmd  # Auto-discovers all .qmd files
  type: grid                     # Grid layout for cards
```

---

## ⚙️ Tech Stack

| Component | Purpose |
|-----------|---------|
| **Quarto** | Markdown-to-HTML converter with RevealJS integration |
| **RevealJS** | Interactive HTML slide framework |
| **SCSS** | Styling preprocessor for UWA theme |
| **GitHub** | Version control repository |
| **GitHub Pages** | Static website hosting (reads `docs/` folder) |
| **Git** | Version control system |

---

## 📋 Common Tasks

### Add a New Lecture

1. Create `presentations/lecture_XX.qmd`
2. Copy YAML header from existing lecture
3. Add slides with markdown
4. Run `quarto render`
5. Commit and push

### Update the Theme

1. Edit `presentations/uwa-theme.scss`
2. Run `quarto render` (re-renders all slides with new theme)
3. Commit both `.scss` and updated `docs/` files
4. Push to GitHub

### Fix a Typo

1. Edit the `.qmd` file
2. Run `quarto render`
3. Commit `presentations/` + `docs/`
4. Push

### Preview Before Publishing

```bash
quarto preview
# View at http://localhost:3000
# Make edits (auto-refreshes)
# When satisfied, stop preview and commit
```

---

## 🐛 Troubleshooting

### Changes Not Appearing on Website

**Problem:** You edited `.qmd` but the website shows old content

**Solution:** You need to render first!
```bash
quarto render
git add docs/
git commit -m "Render updates"
git push
```

### GitHub Actions Shows Success but Content Unchanged

**Reason:** GitHub Pages just deploys the `docs/` folder. If Quarto hasn't rendered, the old HTML is deployed.

**Fix:** Render locally before pushing (see above)

### Slides Look Wrong (Styling Issues)

**Check:**
1. Is `uwa-theme.scss` being referenced in YAML?
   ```yaml
   theme: [default, uwa-theme.scss]
   ```
2. Run `quarto render` to apply theme changes
3. Clear browser cache (Ctrl+Shift+R)

### Asset Images Not Loading

**Check paths are correct:**
- Relative to `.qmd` file: `![](assets/logo.png)`
- Not absolute paths starting with `/`

---

## 📚 Learning Resources

- **Quarto Docs:** https://quarto.org/docs/presentations/revealjs/
- **RevealJS:** https://revealjs.com/
- **GitHub Pages:** https://pages.github.com/

---

## 👤 Author

**Gustavo Alckmin**  
School of Agriculture and Environment  
University of Western Australia

---

## 📄 License

University of Western Australia - AGRI4401 Course Materials
