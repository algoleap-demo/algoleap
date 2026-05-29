# Algoleap Static Site Documentation

Welcome to the Algoleap static site repository. This document serves as a guide for future developers to easily understand, maintain, and update the project architecture, styling, and dynamic content.

---

## 1. Project Architecture

The project is a lightweight **static HTML/CSS site** enriched with Vanilla JavaScript for dynamic content fetching. It does not use any modern JS frameworks (like React or Vue) or CSS frameworks (like Tailwind or Bootstrap). 

- **Pages (`*.html`)**: Each page is an independent HTML file containing a `<header>`, `<main>`, and `<footer>`.
- **Styling (`styles.css`)**: Global styles are defined in `styles.css`. This single file contains CSS variables, typography, component styles (buttons, cards), layout grids, and responsive media queries.
- **Data (`data/*.json`)**: To avoid hardcoding repetitive content across multiple pages, data for Insights and Success Stories is stored in JSON files.
- **Assets (`assets/`)**: All images, logos, and icons are stored here, logically separated into folders by page or component.

---

## 2. Dynamic Content Management

Several sections of the site (such as grids on the Home, Our Studio, Success Stories, Who are we, and Our Insights pages) are populated dynamically using JavaScript `fetch()` calls. 

These calls retrieve data from:
- `data/insights.json`
- `data/success-stories.json`

### The Visibility Feature (`"status"`)
If you need to hide a specific insight or success story without permanently deleting it from the JSON file, use the `"status"` field.

- `"status": "visible"`: (Default) The item will render on all appropriate pages.
- `"status": "non visible"`: The JavaScript filter will intercept this item and completely hide it from the UI across the entire site.

**Example `insights.json` entry:**
```json
{
  "id": 10,
  "category": "People",
  "title": "Algoleap looking forward: 2024 year end highlights",
  "image": "assets/images/our insights/ourinsights11.png",
  "status": "visible", 
  "url": "https://www.linkedin.com/feed/update/urn:li:activity:..."
}
```
*To hide this post, simply change `"visible"` to `"non visible"`.*

---

## 3. Styling and Layout Guidelines

All core styling relies on standardizing layout classes and CSS variables.

### CSS Variables
- `--brand`: `#48a562` (The primary Algoleap green)
- `--bg`: `#f5f7f5` (The standard off-white body background)
- `--text`: `#374151` (The standard body text color)

### Grid Classes
When creating new lists of cards or items, utilize the predefined grid classes to ensure responsive behavior:
- `.card-grid`: Standard 2-column or 3-column auto-fit grid (used for general cards).
- `.card-grid-3`: Strict 3-column grid (used for Success Stories on the homepage).
- `.card-grid-4`: Strict 4-column grid (used for Featured Jobs on the Careers page).

### Component Patterns
- **Buttons**: Use `.button` for the solid green button, and `.button.button-outline` for a white button with a green border. Pill shapes are often styled with `border-radius: 40px;` or `999px`.
- **Soft Sections**: Use `<section class="section soft">` for a slightly distinct background. Often paired with an inline wavy background image (e.g., `careersbg.png`).
- **Masonry Layouts**: Used on the Contact Us, Our Studio, and Careers pages to show an elegant collage of images.
  ```html
  <div class="image-panel masonry-panel">
    <img src="..." alt="" class="masonry-img main-img">
    <div class="masonry-column">
      <img src="..." alt="" class="masonry-img small-img">
      <img src="..." alt="" class="masonry-img small-img">
    </div>
  </div>
  ```

---

## 4. Archive Directory
Any deprecated scripts, old design mockups, or unneeded markdown notes are stored in the `_archive` folder. Please refer to this folder if you need access to original batch-processing scripts (`rename_pages.ps1`, `update_footers.py`, etc.) or the original design mockup PNGs.

---

## 5. Best Practices for Future Modifications

### Adding a New Block
Always start with `<section class="section">` (or `.soft`), and immediately place `<div class="container">` inside it.

### Removing a Section
Simply delete the entire `<section>...</section>` block. Because the site does not use fragile absolute positioning between major sections (except the contact-us form), deleting a section will cause the rest of the page to naturally reflow upward.

### Changing Layouts
Avoid using inline styles for grid logic. Rely on `.card-grid`, `.card-grid-3`, `.card-grid-4`, and `.split` classes applied to `<div>` elements inside containers.