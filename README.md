# Toolanity - Premium Privacy-First Browser Tools

Toolanity is a fast, lightweight, and modern utility website containing a collection of client-side browser tools. The platform is styled in a custom **Obsidian & Emerald** visual identity, fully supporting dark/light theme switching with instant localStorage state preservation.

Every conversion, calculation, generation, or text formatting tool runs **100% client-side**. No inputs, strings, passwords, or documents are ever uploaded to a server, providing a massive security and speed advantage.

---

## Folder & File Structure

```
/
├── index.html                  # Homepage (interactive search, dynamic tools grid)
├── about-us.html               # Mission and project values statement
├── contact-us.html             # Contact form with placeholder console logging
├── privacy-policy.html         # Legal policy detailing client-side executions
├── disclaimer.html            # Limitation of liability and informational statement
├── README.md                   # This instruction guide
├── tools/
│   ├── _template.html          # Starter master template for all future tools
│   ├── word-counter.html
│   ├── password-generator.html
│   ├── qr-code-generator.html
│   ├── age-calculator.html
│   └── percentage-calculator.html
└── assets/
    ├── css/
    │   ├── variables.css       # Color palettes, transitions, grids, breakpoints
    │   ├── base.css            # resets, default typography, scrollbars, focus halos
    │   ├── components.css      # Standardized header, search inputs, mobile drawers, footers
    │   └── tools.css           # Workspace panel cards, tabs, and details accordions
    ├── js/
    │   ├── tools-data.js       # SINGLE SOURCE OF TRUTH (Metadata of all tools)
    │   ├── header.js           # JS-rendered responsive header, mega menu, and header search
    │   ├── footer.js           # JS-rendered 4-column footer and copyright
    │   ├── theme-toggle.js     # Light/Dark mode switcher and localStorage controller
    │   ├── nav-mega-menu.js    # Accordion panel drawers, hover links and ARIA updates
    │   ├── qrcode.min.js       # Local vanilla QR code generation library (QRious)
    │   └── tools/              # Scoped tool controllers
    │       ├── word-counter.js
    │       ├── password-generator.js
    │       ├── qr-code-generator.js
    │       ├── age-calculator.js
    │       └── percentage-calculator.js
    └── images/
        ├── favicon.ico         # System favicon file
        └── og-image.png        # Unified Open Graph social sharing banner
```

---

## How to Add a New Tool Page (Step-by-Step)

To expand the Toolanity catalog with additional tools in future phases, follow this simple checklist:

### Step 1: Add Entry to `tools-data.js`
Open `assets/js/tools-data.js` and add a configuration object inside the `toolsData` array. Set `status` to `"active"` (or `"coming-soon"` if drafting). Provide a custom SVG icon markup.
```javascript
{
  name: "My New Tool",
  slug: "my-new-tool",
  category: "Converters", // Text Tools, Calculators, PDF Tools, Generators, Converters
  description: "Brief 1-sentence tagline describing what the new tool outputs.",
  status: "active",
  icon: `<svg>...</svg>` // Sleek, stroke-based SVG markup
}
```
*Adding this object immediately updates the homepage cards, header mega menu columns, and search queries.*

### Step 2: Copy the Starter Template
Duplicate `tools/_template.html` and rename the copy to match the slug: `tools/my-new-tool.html`.

### Step 3: Configure Head Metadata & SEO Schemas
Open `tools/my-new-tool.html` and update:
1. `<title>`: 50-60 characters, lead with primary target keywords.
2. `<meta name="description">`: 150-160 characters naturally containing secondary keywords.
3. Canonical URL: Set `<link rel="canonical" href="https://toolanity.com/tools/my-new-tool.html">`.
4. Open Graph links (`og:url`, `og:title`, etc.).
5. **WebApplication Schema**: Update `name`, `description`, and set `applicationCategory` (e.g. `CalculatorApplication`, `UtilityApplication`).
6. **FAQPage Schema**: Update JSON arrays with 4-6 real, high-intent user questions and answers.

### Step 4: Write the Workspace HTML
In `tools/my-new-tool.html`, inside `<main>`:
- Update category name, title text, and descriptions.
- Construct custom forms or panels in the `.tool-grid` container (standard split is `.panel-card` for inputs, and `.panel-card` for outputs). Keep tag IDs clear and semantic.

### Step 5: Implement Javascript Logic
1. Create a script file: `assets/js/tools/my-new-tool.js`.
2. Wrap execution code in a `DOMContentLoaded` event listener.
3. Keep logic 100% local (use standard DOM manipulation and modern Browser APIs). No API fetch calls to external backends.
4. Hook up a "Copy to Clipboard" button if the tool provides string values.
5. Reference your new script file at the bottom of `tools/my-new-tool.html` replacing `[tool-slug].js` with `my-new-tool.js`.

---

## Local Development & Styling Guidelines

- **Typography**: The layout utilizes system sans-serif headers and body fonts (Inter / Segoe UI hierarchy).
- **Paths**: The JavaScript layout renderers (`header.js` and `footer.js`) automatically analyze `window.location.pathname` to calculate relative roots (`./` vs `../`). This ensures links, style definitions, and script tags work correctly whether run locally (`file:///`) or on domain roots.
- **Focus Rings**: For accessibility, never strip outline focus outlines without replacement. The base styles apply a customized green glowing ring:
  ```css
  *:focus-visible {
    outline: 2px solid var(--color-accent-hover);
    outline-offset: 3px;
  }
  ```
- **Colors**: Never hardcode hex colors in CSS files. Use variables defined in `variables.css` to respect light/dark modes.
