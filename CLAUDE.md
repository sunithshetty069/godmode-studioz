# CLAUDE.md — GodMode Studioz

This file provides context and conventions for AI assistants (Claude, etc.) working in this repository.

---

## Project Overview

**GodMode Studioz** is a portfolio/business website for a Bangalore-based cinematic visual production and creative promo house. The site showcases the studio's film editing, motion graphics, publicity design, AI-assisted content, and campaign strategy services.

**Key facts:**
- 5+ years in operation, 80+ projects delivered
- Notable clients: Netflix, Amazon Prime Video, Hombale Films, Jio Studios, DVV Entertainment
- Notable films: KGF Chapter 2, Kantara, Salaar, 12th Fail, Empuraan 2, Lucky Bhaskar
- Languages served: Kannada, Telugu, Tamil, Malayalam, Hindi, Spanish, English

---

## Repository Structure

```
godmode-studioz/
├── index.html     # Entire application — HTML + CSS + JS in one file
└── CLAUDE.md      # This file
```

This is a **single-file static web application**. There are no subdirectories, no build output folders, no asset pipelines.

---

## Tech Stack

| Layer      | Technology                        |
|------------|-----------------------------------|
| Markup     | Pure HTML5                        |
| Styling    | CSS3 (embedded `<style>` block)   |
| Scripting  | Vanilla JavaScript (embedded `<script>`) |
| Fonts      | Google Fonts CDN (Playfair Display, DM Sans, Cormorant Garamond) |
| Build tool | None                              |
| Framework  | None                              |
| Backend    | None (static file only)           |

---

## Application Architecture

The site is a **client-side single-page application (SPA)** that simulates multi-page navigation without a router library. All pages live in `index.html` as distinct `<section>` elements, toggled visible by JavaScript.

### Pages

| Section ID    | Purpose                                      |
|---------------|----------------------------------------------|
| `#pg-home`    | Landing hero, services preview, partners     |
| `#pg-about`   | Studio philosophy and background             |
| `#pg-work`    | Filmography portfolio organised by language  |
| `#pg-services`| Full services catalogue (6 categories)       |
| `#pg-films`   | Detailed film list with language groupings   |
| `#pg-contact` | Contact info + enquiry form                  |

### JavaScript Modules (all inline)

| Function / Block         | Responsibility                                         |
|--------------------------|--------------------------------------------------------|
| Custom cursor            | Tracks mouse; lerp-based smooth trailing effect        |
| `go(name, e)`            | Switches active page; wipe transition (~400 ms total)  |
| Scroll listener          | Adds `.solid` to `<nav>` after 80 px scroll            |
| `boot()` / IntersectionObserver | Reveals `.rv` elements on viewport entry      |
| `handleSubmit(e)`        | Client-side form feedback (no backend)                 |

### CSS Design Tokens (CSS custom properties)

```css
--r       /* primary red   #D10000 */
--r2      /* bright red    #FF1A1A */
--bk, --bk2, --bk3          /* black shades  */
--wh, --wh2, --wh3, --wh4, --wh5  /* white shades */
--border  /* rgba(250,250,250,0.08) */
```

### Key Animations

| Name        | Effect                              | Duration   |
|-------------|-------------------------------------|------------|
| `breathe`   | Logo dot pulse                      | 2.5 s ∞    |
| `blobFloat` | Hero background blob morphing       | 12 s ∞     |
| `spinText`  | Circular rotating text ring         | 20 s ∞     |
| `tick`      | Horizontal ticker scroll            | 28 s ∞     |
| `up`        | Fade-in + slide-up reveal           | 0.9 s      |

Staggered reveals use delay utility classes `.d1` – `.d5`.

### Responsive Breakpoints

Single breakpoint at `max-width: 900px` for mobile layout.

---

## Development Workflow

### Prerequisites

None. No package manager, no build tool, no runtime required.

### Running locally

Any static file server works:

```bash
# Python (built-in)
python3 -m http.server 8080

# Node.js (npx)
npx serve .

# VS Code Live Server extension
# — right-click index.html → "Open with Live Server"
```

Then open `http://localhost:8080` in a browser.

### Making changes

1. Edit `index.html` directly.
2. Reload the browser to see changes — no build step needed.
3. All CSS lives inside the `<style>` tag near the top of the file.
4. All JavaScript lives inside the `<script>` tag at the bottom of the file.

---

## Conventions & Patterns

### HTML
- Each page section uses the pattern: `<section id="pg-<name>" class="page">`
- Navigation calls `go('<name>', event)` on click
- Reveal elements use class `.rv` (optionally with `.d1`–`.d5` for stagger)
- The active page has class `.active` added by `go()`

### CSS
- Use existing CSS variables — do not hard-code colour values
- Follow the existing mobile-first responsive pattern with the 900 px breakpoint
- New animations should follow the naming convention (camelCase, descriptive verb)
- Grain/noise overlay is applied via an SVG `<feTurbulence>` filter — do not remove it

### JavaScript
- Keep all JS vanilla — no frameworks or libraries
- Page transitions rely on a CSS `.wipe` class toggled for ~400 ms; maintain this timing if editing transitions
- The `boot()` function must be called once on load to initialise the intersection observer

### Content
- Film/client names must match official titles exactly (capitalisation, spacing)
- Filmography is grouped by language — maintain this structure when adding projects
- Working hours displayed on the contact page: Mon–Fri, 9 AM – 6 PM IST

---

## No Tests / No Linting

There are currently no automated tests, linters, or formatters configured. When adding these in the future:

- Prefer **HTMLHint** or **html-validate** for HTML linting
- Prefer **Stylelint** for CSS linting
- Prefer **ESLint** with a minimal config for JavaScript
- Prefer **Playwright** or **Cypress** for end-to-end tests on page navigation

---

## Deployment

The site is a single static HTML file and can be deployed to any static hosting platform:

- **GitHub Pages** — push `index.html` to the `gh-pages` branch or root of `main`
- **Netlify / Vercel** — connect repo, set publish directory to `.` (root)
- **Any CDN or web server** — copy `index.html` to the server root

No build command or output directory configuration is needed.

---

## Contact / Business Info (for content edits)

| Field            | Value                        |
|------------------|------------------------------|
| Website          | godmodestudioz.com           |
| Email            | godmodestudioz@gmail.com     |
| Instagram        | @godmodestudioz              |
| Location         | Bangalore, India             |
| Working hours    | Mon–Fri, 9 AM – 6 PM IST    |
