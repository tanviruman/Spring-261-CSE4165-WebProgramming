# CSE 4165 — Web Programming  
## 📚 Hyper-Detailed Crash Notes (with Examples)

> Based on the CSE 4165 10-Hour Survival Guide. All code examples are exam-ready.

---

## 🗂️ TABLE OF CONTENTS
1. [Exam Boilerplate (Start Here!)](#1-exam-boilerplate)
2. [HTML Tables](#2-html-tables)
3. [HTML Forms](#3-html-forms)
4. [Links & iFrames](#4-links--iframes)
5. [CSS Box Model](#5-css-box-model)
6. [Flexbox](#6-flexbox)
7. [CSS Grid](#7-css-grid)
8. [CSS Positioning](#8-css-positioning)
9. [Exam Patterns — Full Solutions](#9-exam-patterns--full-solutions)
10. [Quick Reference & Common Mistakes](#10-quick-reference--common-mistakes)

---

## 1. Exam Boilerplate

> ✅ **Write this FIRST in every exam. Memorize it. It saves 5 minutes and prevents silly mistakes.**

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Page Title</title>
  <style>
    /* ── RESET ── */
    * { margin: 0; padding: 0; box-sizing: border-box; }
    body { font-family: Arial, sans-serif; color: #333; }
    a { text-decoration: none; }
    ul { list-style: none; }
    img { max-width: 100%; }
    input, button, select, textarea { font-family: inherit; }

    /* ── REUSABLE UTILITIES ── */
    .btn {
      display: inline-block; padding: 10px 24px;
      background: #2563eb; color: #fff;
      border: none; border-radius: 6px;
      cursor: pointer; font-weight: 600;
    }
    .card {
      background: #fff; padding: 24px;
      border-radius: 8px;
      box-shadow: 0 4px 15px rgba(0,0,0,0.08);
    }

    /* ── YOUR QUESTION CSS BELOW ── */

  </style>
</head>
<body>

  <!-- YOUR HTML BELOW -->

</body>
</html>
```

**Pre-submit Checklist:**
- `<!DOCTYPE html>` written?
- All tags properly closed?
- `label for=""` matches `input id=""`?
- `display:flex` on navbar parent?
- `border-collapse:collapse` for tables?
- Exact hex colors copied from question?

---

## 2. HTML Tables

### Core Concept
Tables use strict nesting: `table > thead/tbody/tfoot > tr > th/td`

### All Table Tags

| Tag | Purpose |
|-----|---------|
| `<table>` | Outer wrapper for everything |
| `<caption>` | Title above/below the table |
| `<thead>` | Header section (top rows) |
| `<tbody>` | Main data rows |
| `<tfoot>` | Footer rows (totals, summaries) |
| `<tr>` | A single row |
| `<th>` | Header cell — bold + centered |
| `<td>` | Data cell — regular text |
| `<colgroup>/<col>` | Style entire columns |

### Key Attributes (Most Tested)

| Attribute | What it does |
|-----------|-------------|
| `colspan="2"` | Merge 2 columns **horizontally** |
| `rowspan="2"` | Merge 2 rows **vertically** |
| `scope="col"` | Header applies to whole column |
| `scope="row"` | Header applies to whole row |
| `border="1"` | Show table border (legacy, but works) |

> ⚠️ **Always use `border-collapse: collapse;` in CSS to remove double borders.**

### Example: Full Table with colspan + rowspan

```html
<table style="width:100%; border-collapse:collapse;" border="1">
  <caption>Student Results</caption>

  <thead>
    <tr>
      <th scope="col">Name</th>
      <th scope="col">Math</th>
      <th scope="col">Science</th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <th scope="row" rowspan="2">Alice</th>  <!-- Merges 2 rows DOWN -->
      <td>90</td>
      <td>85</td>
    </tr>
    <tr>
      <!-- Alice's td is GONE here because rowspan covers it -->
      <td>88</td>
      <td>92</td>
    </tr>
    <tr>
      <td>Bob</td>
      <td colspan="2" style="text-align:center">Absent</td>  <!-- Merges 2 cols -->
    </tr>
  </tbody>

  <tfoot>
    <tr>
      <th>Total</th>
      <td>178</td>
      <td>177</td>
    </tr>
  </tfoot>
</table>
```

### Exam Trap 🚨
- `colspan`/`rowspan` go on `<td>` or `<th>` — **NOT on `<tr>`**
- When you use `rowspan="2"` on a cell, the next row has **one fewer `<td>`** — don't add a blank one.

---

## 3. HTML Forms

### Core Concept
Forms appear in almost every exam. Know label+input pairing and input types.

### All Form Tags

| Tag | Purpose |
|-----|---------|
| `<form>` | Container. Use `action` + `method` |
| `<input>` | Most versatile — changes with `type=""` |
| `<label>` | Clickable text for input (`for=""` must match `id=""`) |
| `<textarea>` | Multi-line text box |
| `<select>` | Dropdown container |
| `<option>` | Each item in a dropdown |
| `<button>` | `type="submit"`, `"reset"`, or `"button"` |
| `<fieldset>` | Groups inputs with a border box |
| `<legend>` | Caption for a fieldset |

### Input Types

| `type=""` | Shows as |
|-----------|----------|
| `text` | Plain text box |
| `email` | Validates email format |
| `password` | Hides characters |
| `number` | Numbers only + arrows |
| `checkbox` | Tick box |
| `radio` | Round selection (one only per group) |
| `file` | File picker button |
| `date` | Calendar date picker |
| `range` | Slider |
| `color` | Color picker |
| `hidden` | Invisible (stores data) |
| `submit` | Submits the form |

### Example: Complete Registration Form

```html
<form action="/register" method="POST">

  <fieldset>
    <legend>Personal Information</legend>

    <!-- TEXT INPUT: label for="" must match input id="" -->
    <label for="fullname">Full Name:</label>
    <input type="text" id="fullname" name="fullname"
           placeholder="Enter full name" required>

    <!-- EMAIL INPUT -->
    <label for="email">Email:</label>
    <input type="email" id="email" name="email"
           placeholder="name@students.uiu.ac.bd" required>

    <!-- PASSWORD -->
    <label for="pwd">Password:</label>
    <input type="password" id="pwd" name="password"
           placeholder="Enter password" minlength="8">

    <!-- DROPDOWN -->
    <label for="dept">Department:</label>
    <select id="dept" name="dept">
      <option value="">-- Select --</option>
      <option value="cse">CSE</option>
      <option value="eee">EEE</option>
    </select>

    <!-- CHECKBOX -->
    <input type="checkbox" id="agree" name="agree" required>
    <label for="agree">I agree to the Terms of Service</label>
  </fieldset>

  <button type="reset">Clear</button>
  <button type="submit">Register</button>

</form>
```

### Exam Trap 🚨
**`label for=""` must EXACTLY match `input id=""`**  
If `<label for="email">` — the input MUST have `id="email"`. Mismatch = lost marks.  
This is the #1 mistake students make.

---

## 4. Links & iFrames

### Example

```html
<!-- Normal link -->
<a href="about.html">About Us</a>

<!-- Opens in NEW TAB (use rel for security) -->
<a href="https://google.com" target="_blank" rel="noopener noreferrer">Google</a>

<!-- Download a file -->
<a href="report.pdf" download="report.pdf">Download PDF</a>

<!-- Embedded iframe (e.g. YouTube video) -->
<iframe
  src="https://www.youtube.com/embed/VIDEO_ID"
  width="560" height="315"
  title="Video"
  allowfullscreen>
</iframe>
```

---

## 5. CSS Box Model

### Core Concept
Every element is a box. Margin / Padding / Border is mandatory knowledge.

### Properties

| Property | Controls |
|----------|----------|
| `margin` | Space **OUTSIDE** the element (between elements) |
| `padding` | Space **INSIDE** the element (between border & content) |
| `border` | Line around the element |
| `width / height` | Size of content area |
| `box-sizing: border-box` | Padding/border included in width — **ALWAYS use this** |

### Clockwise Shorthand (T R B L)

```css
padding: 10px;              /* All 4 sides equal */
padding: 10px 20px;         /* Top/Bottom | Left/Right */
padding: 10px 20px 30px;    /* Top | Left/Right | Bottom */
padding: 10px 20px 30px 40px; /* Top Right Bottom Left */
```

### Visual Styling Cheatsheet

| Property | Common Values |
|----------|--------------|
| `background-color` | `#ffffff`, `rgba(0,0,0,0.5)` |
| `border-radius` | `8px` (soft), `50%` (circle), `0` (sharp) |
| `border` | `1px solid #ccc` (width style color) |
| `box-shadow` | `0 4px 15px rgba(0,0,0,0.1)` |
| `font-weight` | `400` (normal), `700` (bold), `800` (extra bold) |
| `text-decoration` | `none` (removes link underline) |
| `cursor` | `pointer` (hand icon on hover) |

### Example: CSS Reset + Card + Button

```css
/* ── ALWAYS START WITH THIS ── */
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box; /* Critical: padding won't break widths */
}

body {
  font-family: Arial, sans-serif;
  color: #333;
  background-color: #fff;
}

/* ── CARD STYLE (used everywhere) ── */
.card {
  background: #fff;
  border-radius: 8px;
  padding: 24px;
  box-shadow: 0 4px 15px rgba(0,0,0,0.08);
  border: 1px solid #e2e6ea;
}

/* ── BUTTON STYLE ── */
.btn {
  display: inline-block;
  padding: 10px 24px;
  background-color: #2563eb;
  color: #fff;
  border: none;
  border-radius: 6px;
  cursor: pointer;
  text-decoration: none;
  font-weight: 600;
}
```

---

## 6. Flexbox

### Core Concept
Flexbox is **one-dimensional** (row OR column). Apply properties to the **PARENT** to control the **CHILDREN**.  
Use it for: navbars, split screens, card rows.

### Parent Properties

| Property | Values | Use Case |
|----------|--------|----------|
| `display: flex` | — | **Activates flexbox — ALWAYS first** |
| `flex-direction` | `row` (default), `column` | row = side-by-side, column = stacked |
| `justify-content` | `space-between`, `center`, `flex-start`, `flex-end` | Horizontal spacing |
| `align-items` | `center`, `stretch`, `flex-start` | Vertical alignment |
| `gap` | `20px`, `1rem` | Space between children |
| `flex-wrap` | `wrap`, `nowrap` | wrap = items wrap to next line if too wide |

### Child Properties

| Property | Values | Use Case |
|----------|--------|----------|
| `flex: 1` | 1, 2, 3… | Takes up remaining space. Two children with `flex:1` → equal halves (split screen!) |
| `flex: 0 0 200px` | grow shrink basis | Fixed-width sidebar that won't shrink |

### Example: 3 Key Flexbox Patterns

```css
/* ─── PATTERN 1: NAVBAR (Logo left, Links right) ─── */
.navbar {
  display: flex;
  justify-content: space-between;  /* Logo left, Links right */
  align-items: center;             /* Vertically centered */
  padding: 16px 40px;
  background-color: #1a1d23;
}
.nav-links {
  display: flex;
  gap: 24px;       /* Space between links */
  list-style: none;
}

/* ─── PATTERN 2: SPLIT SCREEN (50/50) ─── */
.split-container {
  display: flex;
  min-height: 100vh;
}
.left-panel  { flex: 1; background: #0976a7; padding: 60px; }
.right-panel { flex: 1; padding: 60px; }

/* ─── PATTERN 3: CENTER CONTENT IN A CONTAINER ─── */
.center-box {
  display: flex;
  justify-content: center;   /* Center horizontally */
  align-items: center;       /* Center vertically */
  min-height: 100vh;
}
```

```html
<!-- HTML STRUCTURE for Split Screen -->
<div class="split-container">
  <div class="left-panel"> Left content </div>
  <div class="right-panel"> Right content </div>
</div>
```

---

## 7. CSS Grid

### Core Concept
Grid is **two-dimensional** (rows AND columns). Use it for dashboards, card galleries, and any layout that needs both rows AND columns.

### Properties

| Property | Values | What it does |
|----------|--------|-------------|
| `display: grid` | — | Activates grid — always first |
| `grid-template-columns` | `repeat(3, 1fr)`, `200px 1fr` | Defines column widths |
| `grid-template-rows` | `auto`, `100px` | Defines row heights |
| `gap` | `20px`, `16px 24px` | Space between grid cells |
| `grid-column` | `span 2`, `1 / -1` | On child: span 2 = takes 2 cols; `1/-1` = full width |
| `grid-row` | `span 2` | On child: takes 2 rows tall |

### Example: 3 Key Grid Patterns

```css
/* ─── PATTERN 1: 3-COLUMN CARD GRID ─── */
.card-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);  /* 3 equal columns */
  gap: 20px;
  padding: 40px;
}

/* ─── PATTERN 2: SIDEBAR + MAIN (Dashboard layout) ─── */
.dashboard {
  display: grid;
  grid-template-columns: 220px 1fr;  /* Sidebar 220px, main gets rest */
  min-height: 100vh;
}
.sidebar  { background: #1e3a5f; padding: 24px; }
.main     { padding: 24px; background: #f8f9fa; }

/* ─── PATTERN 3: FULL-WIDTH ITEM inside a grid ─── */
.full-width-item {
  grid-column: 1 / -1;  /* Spans ALL columns */
}
```

```html
<!-- HTML STRUCTURE for 3-column cards -->
<div class="card-grid">
  <div class="card">Card 1</div>
  <div class="card">Card 2</div>
  <div class="card">Card 3</div>
</div>
```

---

## 8. CSS Positioning

### Position Values Summary

| Value | Behaviour |
|-------|-----------|
| `static` | Default, normal flow. No top/left/right/bottom. |
| `relative` | Normal flow BUT can be nudged, AND is a reference box for absolute children |
| `absolute` | Removed from flow, positioned relative to nearest `relative` parent |
| `fixed` | Removed from flow, stays in viewport when scrolling (sticky navbars) |
| `z-index` | Stack order — higher = on top. Only works on positioned elements. |

### The Golden Rule
> 🏆 **Parent = `position: relative` → Child = `position: absolute`**

### Example: Password Eye Icon (Common Exam Pattern)

```css
/* The RULE: parent = relative, moving child = absolute */
.input-group {
  position: relative;   /* Step 1: Parent is the reference box */
}
.eye-icon {
  position: absolute;   /* Step 2: Child moves freely inside parent */
  right: 12px;          /* Step 3: Position it */
  top: 50%;
  transform: translateY(-50%); /* Perfect vertical center trick */
  cursor: pointer;
}
```

```html
<div class="input-group">
  <input type="password" id="password" placeholder="Enter your password">
  <span class="eye-icon">Show</span>
</div>
```

---

## 9. Exam Patterns — Full Solutions

> Based on 4 past papers. Every exam question maps to one of these patterns.

---

### Pattern 1 — Universal Navbar (~5–8 Marks)
**Appears in ALL papers.** Use `justify-content: space-between`.

```html
<!-- HTML -->
<nav class="navbar">
  <div class="nav-logo">
    <img src="logo.png" alt="Logo" width="40">
    <span>UIU Housing Society</span>
  </div>

  <ul class="nav-links">
    <li><a href="#">HOME</a></li>
    <li><a href="#">ABOUT</a></li>
    <li><a href="#">CONTACT</a></li>
    <li><a href="#" class="btn-nav">Visit UCAM</a></li>
  </ul>
</nav>
```

```css
/* CSS */
.navbar {
  display: flex;
  justify-content: space-between; /* Logo left, links right */
  align-items: center;
  padding: 16px 40px;
  background-color: #fff;
  box-shadow: 0 2px 8px rgba(0,0,0,0.1);
}
.nav-logo {
  display: flex;
  align-items: center;
  gap: 10px;
  font-size: 20px;
  font-weight: 700;
}
.nav-links {
  display: flex;
  list-style: none;
  gap: 28px;
  align-items: center;
}
.nav-links a {
  text-decoration: none;
  color: #333;
  font-size: 14px;
  font-weight: 600;
}
.btn-nav {
  background: #20c997;
  color: #fff !important;
  padding: 8px 20px;
  border-radius: 6px;
}
```

---

### Pattern 2 — Split Screen Sign-in Page (15 Marks)
**From Spring 2025 Q2, Fall 2025 Q1.** Use `flex: 1` on BOTH panels.

```html
<!-- HTML -->
<div class="page-wrapper">

  <!-- LEFT PANEL: colored background, quote/info -->
  <div class="left-panel">
    <blockquote>
      <p>"Lorem ipsum dolor sit amet, consectetur adipiscing elit..."</p>
      <footer>
        <strong>Niassoh Dihan</strong>
        <span>Assistant Professor, CSE</span>
      </footer>
    </blockquote>
  </div>

  <!-- RIGHT PANEL: sign-in form -->
  <div class="right-panel">
    <h2>Sign in to your WEB PROGRAMMING account.</h2>
    <p>Don't have an account? <a href="#" class="link-red">Create one</a></p>

    <form action="#" method="POST">
      <label for="email">Email</label>
      <input type="email" id="email" name="email"
             placeholder="Enter your email address">

      <label for="password">Password</label>
      <div class="input-group">
        <input type="password" id="password" name="password"
               placeholder="Enter your password">
        <span class="eye-icon">Show</span>
      </div>

      <button type="submit" class="btn-signin">SIGN IN</button>
    </form>
  </div>
</div>
```

```css
/* CSS */
.page-wrapper {
  display: flex;
  min-height: 100vh;
}
.left-panel {
  flex: 1;
  background-color: #0976a7; /* Blue from Spring 2025 paper */
  color: #fff;
  padding: 60px;
  display: flex;
  align-items: center;
}
.right-panel {
  flex: 1;
  padding: 60px;
  display: flex;
  flex-direction: column;
  justify-content: center;
}
.right-panel input {
  width: 100%;
  padding: 12px 16px;
  border: 1px solid #eff1f3;
  border-radius: 6px;
  background: #eff1f3;
  margin: 6px 0 14px;
  font-size: 14px;
}
.btn-signin {
  width: 100%;
  padding: 14px;
  background: #e90606; /* Red from paper */
  color: #fff;
  border: none;
  border-radius: 6px;
  font-size: 15px;
  font-weight: 700;
  cursor: pointer;
}
/* Password "Show" button */
.input-group { position: relative; }
.eye-icon {
  position: absolute; right: 12px;
  top: 50%; transform: translateY(-50%);
  font-size: 12px; color: #888; cursor: pointer;
}
.link-red { color: #e90606; }
```

---

### Pattern 3 — Feature Cards Grid (~6 Marks)
**From Paper 251 (Kitchen), Spring 2025 (Pricing), Fall 2025 (Projects).** Use `repeat(N, 1fr)`.

```html
<!-- HTML -->
<section class="features">
  <div class="features-grid">
    <div class="feature-card">
      <div class="feature-icon">👨‍🍳</div>
      <h3>Master Chefs</h3>
      <p>Diam elitr kasd sed at elitr sed ipsum justo dolor</p>
    </div>
    <div class="feature-card">
      <div class="feature-icon">🍴</div>
      <h3>Quality Food</h3>
      <p>Diam elitr kasd sed at elitr sed ipsum justo dolor</p>
    </div>
    <!-- Add more cards as needed -->
  </div>
</section>
```

```css
/* CSS */
.features { padding: 60px 40px; }

.features-grid {
  display: grid;
  grid-template-columns: repeat(4, 1fr); /* Change 4 to 3 for 3 cards */
  gap: 20px;
}
.feature-card {
  background: #fff;
  padding: 28px 20px;
  border: 1px solid #eee;
  border-radius: 8px;
}
.feature-icon {
  font-size: 32px;
  color: #f4a100; /* Orange */
  margin-bottom: 12px;
}
.feature-card h3 { font-size: 16px; font-weight: 700; margin-bottom: 8px; }
.feature-card p  { font-size: 13px; color: #666; line-height: 1.6; }
```

---

### Pattern 4 — Sidebar Dashboard + Progress Bars (15 Marks)
**From Summer 2025 Q1.** Grid with fixed sidebar + progress bars as nested divs.

```html
<!-- HTML -->
<div class="dashboard-layout">

  <!-- SIDEBAR -->
  <aside class="sidebar">
    <h2 class="sidebar-title">UIU LEARNING HUB</h2>
    <nav>
      <ul>
        <li><a href="#" class="active">Dashboard</a></li>
        <li><a href="#">My Courses</a></li>
        <li><a href="#">Assignments</a></li>
        <li><a href="#">Exams</a></li>
      </ul>
    </nav>
  </aside>

  <!-- MAIN CONTENT -->
  <main class="main-content">
    <h1>Welcome to Your Learning Dashboard</h1>

    <!-- COURSE CARDS -->
    <div class="courses-grid">
      <div class="course-card" style="background: linear-gradient(135deg, #56ab2f, #a8e063);">
        <h3>CSE 4165: Web Programming</h3>
        <p>Prof. Rahman</p>
      </div>
      <div class="course-card" style="background: linear-gradient(135deg, #f46b45, #eea849);">
        <h3>CSE 3115: Database Systems</h3>
        <p>Dr. Karim</p>
      </div>
    </div>

    <!-- PROGRESS BAR: outer div = track, inner div = fill -->
    <div class="progress-section">
      <span>Progress: 75%</span>
      <div class="progress-track">
        <div class="progress-fill" style="width: 75%"></div>
      </div>
    </div>
  </main>
</div>
```

```css
/* CSS */
.dashboard-layout {
  display: grid;
  grid-template-columns: 220px 1fr; /* Sidebar 220px, main takes rest */
  min-height: 100vh;
}
.sidebar {
  background: #1e3a5f;
  color: #fff;
  padding: 24px;
}
.sidebar ul { list-style: none; margin-top: 20px; }
.sidebar ul li a {
  display: block;
  padding: 10px 12px;
  color: #ccc;
  text-decoration: none;
  border-radius: 6px;
  margin-bottom: 4px;
}
.sidebar ul li a.active {
  background: #2a5298;
  color: #fff;
}
.main-content {
  padding: 28px;
  background: #f8f9fa;
}
.courses-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 16px;
  margin: 20px 0;
}
.course-card {
  padding: 24px 20px;
  border-radius: 10px;
  color: #fff;
  font-weight: 700;
}
/* PROGRESS BAR */
.progress-track {
  width: 100%;
  height: 6px;
  background: #ddd; /* Grey track */
  border-radius: 3px;
}
.progress-fill {
  height: 100%;
  background: #16a34a; /* Green fill */
  border-radius: 3px;
  /* Width is set inline: style="width: 75%" */
}
```

---

### Pattern 5 — Course Registration Page (15 Marks)
**From Summer 2025 Q2.** Combines Navbar + Grid layout + HTML table + HTML form all in one question.

```html
<!-- NAVBAR -->
<nav class="topnav">
  <div class="nav-left">
    <a href="#">Dashboard</a>
    <a href="#">Courses</a>
    <a href="#">Notices</a>
  </div>
  <div class="nav-right">
    <a href="#">Login</a>
    <a href="#">Sign Up</a>
  </div>
</nav>

<!-- TWO-COLUMN BODY -->
<div class="body-layout">

  <!-- LEFT: Semester list -->
  <aside class="semester-sidebar">
    <h2>Semesters</h2>
    <ul>
      <li>Spring 2025</li>
      <li>Fall 2024</li>
      <li>Summer 2024</li>
    </ul>
  </aside>

  <!-- RIGHT: Table + Form -->
  <main class="reg-main">
    <h2>Course Registration</h2>

    <!-- TABLE -->
    <table class="reg-table">
      <thead><tr>
        <th>Course</th><th>Code</th><th>Credit</th>
      </tr></thead>
      <tbody>
        <tr><td>Web Programming</td><td>CSE201</td><td>3.0</td></tr>
        <tr><td>Data Structures</td><td>CSE202</td><td>3.0</td></tr>
      </tbody>
    </table>

    <!-- SIGN UP FORM -->
    <h3>Sign Up Form</h3>
    <form>
      <label for="fname">Full Name</label>
      <input type="text" id="fname" name="fname" placeholder="Enter full name">

      <label for="sid">Student ID</label>
      <input type="text" id="sid" name="studentId" placeholder="e.g., 011233001">

      <label for="uemail">UIU Email</label>
      <input type="email" id="uemail" name="email" placeholder="name@students.uiu.ac.bd">

      <label for="pwd">Password</label>
      <input type="password" id="pwd" name="password" placeholder="Enter password">

      <button type="submit">Register</button>
    </form>
  </main>
</div>
```

```css
/* CSS */
.topnav {
  display: flex;
  justify-content: space-between;
  padding: 12px 24px;
  background: #f0f0f0;
}
.topnav a {
  text-decoration: none; margin: 0 8px;
  color: #1a5276; font-weight: 600;
}
.body-layout {
  display: grid;
  grid-template-columns: 280px 1fr;
  min-height: calc(100vh - 50px);
}
.semester-sidebar {
  background: linear-gradient(to bottom, #a8edea, #b3c8f5);
  padding: 24px;
}
.semester-sidebar ul { list-style: none; }
.semester-sidebar li {
  background: rgba(255,255,255,0.5);
  padding: 10px 14px;
  margin-bottom: 8px;
  border-radius: 6px;
}
.reg-main { padding: 28px; }
.reg-main form label {
  display: block; font-weight: 600;
  margin: 12px 0 4px;
}
.reg-main form input {
  width: 100%; padding: 10px 14px;
  border: 1px solid #ddd;
  border-radius: 6px; font-size: 14px;
}
.reg-table {
  width: 100%; border-collapse: collapse; margin-bottom: 28px;
}
.reg-table th {
  background: #c17f52;
  color: #fff; padding: 10px 14px; text-align: left;
}
.reg-table td {
  background: #f5dfc0;
  padding: 9px 14px;
  border-bottom: 1px solid #e2c9a8;
}
```

---

## 10. Quick Reference & Common Mistakes

| Task | Code to Write | Common Mistake |
|------|--------------|----------------|
| Navbar (logo left, links right) | `display:flex; justify-content:space-between` | Forgetting to set it on the navbar, not the `<ul>` |
| 3 equal columns | `display:grid; grid-template-columns:repeat(3,1fr)` | Using `repeat(3, 1px)` — always use `fr` not `px` |
| Split screen 50/50 | `display:flex` on parent; `flex:1` on both children | Setting `flex:1` on the parent instead of children |
| Fixed sidebar | `grid-template-columns: 220px 1fr` | Using `220fr` instead of `220px` |
| Center content | `display:flex; justify-content:center; align-items:center` | Forgetting `min-height:100vh` on container |
| Progress bar (75%) | Outer div (track), inner div with `width:75%` | Setting width on the outer div, not inner |
| Circle image/avatar | `border-radius:50%` on the `<img>` | Using `border-radius:50px` (not `50%`) |
| Remove link underline | `text-decoration:none` on the `<a>` | Putting it on the `<ul>` instead |
| Merge 2 columns in table | `colspan="2"` on the `<td>` | Using `colspan` on `<tr>` instead of `<td>` |
| Absolute inside relative | Parent: `position:relative` — Child: `position:absolute` | Forgetting `position:relative` on the parent |
| Vertical center with absolute | `top:50%; transform:translateY(-50%)` | Using `top:50%` alone (puts top edge at center, not middle) |
| Full-width grid item | `grid-column: 1 / -1` on the child | Setting it on the parent grid instead of the child |

---

## 📊 Exam Mark Distribution (Estimated)

| Topic | Frequency in Exam |
|-------|------------------|
| Flexbox Layouts | 95% — Almost certain |
| CSS Grid | 90% — Very likely |
| HTML Forms | 85% — Very likely |
| Box Model / Styling | 80% — Likely |
| HTML Tables | 60% — Common |
| CSS Positioning | 40% — Sometimes |

## 🔁 Recurring Exam Patterns (All 4 Papers)

| Pattern | Frequency |
|---------|-----------|
| Navbar with logo + links | 100% — Every paper |
| Two-column split layout | 90% |
| Card grid (3 or 4 cards) | 90% |
| Registration / Login form | 85% |
| Hero section (text + image) | 75% |
| Sidebar + main content | 70% |
| HTML table with data | 60% |
| Progress bars (CSS) | 50% |

---

> 🏆 **Final Exam Mindset:** You don't need to be perfect. You need to be systematic.  
> Write the boilerplate → Add the navbar (`flex` + `space-between`) → Add the main layout (grid or flex) → Fill in content.  
> Even if your colors are slightly off, the **structure scores most marks**. Good luck! 💪
