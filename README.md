# README — The MM Regeneration Skies

**Part 1 — Planning & Organizing a Multipage Website**

> Purpose: This README documents the planning stage for a five‑page, accessible, high‑impact website for **The MM Regeneration Skies** — a solar energy company offering panels, inverters, batteries, installation and maintenance. It shows the site structure, page layouts, user journeys and the content & technical requirements needed before coding.
---
## Table of contents

1. Project overview
2. Target audience & goals
3. Pages (outline + purpose)
4. Page-by-page layout sketches & key components
5. Navigation map and internal linking
6. Content inventory (what we need)
7. Personas & user journeys
8. Technical architecture & folder structure
9. Reusable UI components and patterns
10. Animation & interaction plan (including glowing title)
11. Accessibility, SEO & performance notes
12. QA / testing checklist
13. Deployment & deliverables
14. Next steps (what I need from you)

---

## 1. Project overview

**Project name:** The MM Regeneration Skies — public-facing marketing & product site

**Primary goal:** Showcase products (panels, inverters, batteries), explain services (installation & maintenance), generate qualified leads (quote requests / contact), and build trust through case studies and specs.

**Top-level success metrics:**

* Visitor → Contact / Quote submission conversion
* Time on product pages (content engagement)
* Mobile responsiveness & performance score ≥ 80

---

## 2. Target audience & goals

* **Residential homeowners** — want reliable backup power, ROI and simple installation
* **Commercial buyers / facility managers** — want specs, warranties, and ROI projections
* **Installers / partners** — want product data, specs and distribution contacts
* **Curious visitors** — want brand story and proof (projects / testimonials)

Tone: professional, optimistic, and technically credible. Visual style: clean, modern, “tech meets nature” (deep blue/teal gradients with warm sunlight accents). Title should *glow* as a signature visual effect.

---

## 3. Pages (outline + purpose)

We will build **5 main pages**:

1. **Home** — high-impact hero with animated sun/solar arc, quick pitch, 3 core value propositions, CTA to products and contact (Quote)
2. **Products** — catalog overview with filtering (Panels, Inverters, Batteries). Each product entry links to a **Product Detail modal/page** with gallery and specs
3. **Services** — installation packages and maintenance plans (residential, commercial). Includes process steps and FAQs
4. **About** — mission, certifications, team, case studies, testimonials
5. **Contact** — contact form, quick quote form, phone/email, map, office locations

> Note: Product detail content can be implemented as separate pages (e.g., `product-panel-400w.html`) or as a client-side modal that fetches `data/products.json`. For SEO it is recommended to have at least one canonical product detail page per major product.

---

## 4. Page-by-page layout sketches & key components

Below are lightweight wireframes and the primary sections we will implement.

### HOME — purpose: convert & educate

* **Hero**: animated glowing title, short tagline, animated sun/solar arc visual, primary CTA `Explore products` and secondary CTA `Get a Quote`
* **Highlights**: 3 cards (High-efficiency panels, Smart monitoring, End-to-end support)
* **Featured Products**: horizontal scroll / carousel of top 3 products
* **How it works**: 3-step illustrated process (Survey → Install → Maintain)
* **Case study / testimonial**: 1-2 rotating customer stories
* **Footer**: newsletter, quick links, social

**ASCII wireframe:**

```
[Header: Logo | Nav | CTA]
[Hero: Glowing title | animated sun | CTA buttons]
[3 Feature Cards | Quick product carousel]
[How it works (3 steps)]
[Case study / testimonials]
[Footer]
```

### PRODUCTS — purpose: show product range & link to details

* **Intro**: short blurb about product standards
* **Filters / categories**: Panels / Inverters / Batteries, search box
* **Product grid**: product card (image, title, short specs, `Request quote`/`View details`)
* **Pagination / load-more**

**Key features:** image gallery, lazy-loading images, `Download spec sheet` link on each product detail.

### SERVICES — purpose: sell packages & explain process

* **Package cards**: Residential Silver/Gold, Commercial, Custom
* **Process**: interactive timeline or accordion for each step
* **Maintenance plans**: pricing tiers and SLA bullets
* **FAQ**

### ABOUT — purpose: credibility

* **Mission & values**
* **Certifications / partners logos**
* **Team**
* **Case studies**: before/after stats

### CONTACT — purpose: capture leads

* **Contact form**: name, email, phone, message, project size, preferred contact method
* **Quick quote widget**: location, roof type, estimated monthly consumption
* **Map / address / phone / social**
* **GDPR / privacy notice**

---

## 5. Navigation map and internal linking

Primary navigation (header) links to the five main pages. The footer repeats links and adds legal/privacy.

**CTA flows / important links:**

* `Explore products` → `/products.html`
* `Request quote` (from product card) → opens modal form / anchor to `/contact.html#quote` (prefilled product)
* `Contact / Phone` opens mailto or tel: link on mobile

**Simple sitemap:**

```
/ (home)
/products (products list)
  /products/:slug (product detail)  <-- recommended for SEO
/services
/about
/contact
```

---

## 6. Content inventory (what we need)

Organize content before coding — this speeds implementation.

**Brand assets**

* Logo (vector / SVG) and alternate variations (light/dark)
* Brand color hexes, typography choices (web fonts)

**Per-page content**

* Home: hero tagline, 3 features copy, 2 testimonials, 3 hero images
* Products: for each product — name, 1 long description, 3–6 images (1024px+), specs table, datasheet PDF, warranty info
* Services: package descriptions, checklist of what’s included, pricing ranges (if public), images
* About: team bios, case study copy + images, partner logos, certifications
* Contact: office address, phone numbers, support email, map coordinates

**Forms**

* Field labels, privacy/legal copy for contact/quote forms

**SEO**

* Page titles, meta descriptions, canonical URLs, open graph image for each top-level page

---

## 7. Personas & user journeys

Below are common journeys we’ll design for so information architecture supports conversion.

### Persona A — Sarah, homeowner (goal: get quote)

1. Lands on Home via search
2. Reads hero + features → clicks `Explore products`
3. Compares `Solar Panel — 400W` → opens product detail
4. Clicks `Request a quote` → prefilled quote modal → submits contact
5. Redirect to Thank You / email confirmation

### Persona B — Daniel, facility manager (goal: verify specs)

1. Arrives on Products via targeted ad
2. Filters `Inverters` → opens 5kW inverter page
3. Downloads spec sheet PDF and contacts sales via contact form

### Persona C — Installer (goal: partnership info)

1. Visits About page, reads partner program
2. Uses contact form specifically for partnerships (selects ‘partner inquiry’)

Documenting these journeys helps place the CTAs and decide what data to show on each page.

---

## 8. Technical architecture & folder structure

**Tech stack:** Plain HTML5 + modern CSS (custom properties + small utility classes) + vanilla JS. Optional: small build step (Parcel / Vite) for minification, but not required for first pass.

**Suggested folder layout:**

```
mm-regeneration-skies/
├─ index.html                  # Home
├─ products.html               # Product catalog
├─ services.html               # Services
├─ about.html                  # About & case studies
├─ contact.html                # Contact / Quote
├─ product/                    # optional product detail pages
│   └─ panel-400w.html
├─ assets/
│   ├─ img/
│   ├─ logos/
│   └─ pdfs/
├─ css/
│   └─ main.css
├─ js/
│   └─ main.js
├─ data/
│   └─ products.json
└─ README.md
```

**Notes:**

* Put shared styles & components in `css/main.css` and `js/main.js`.
* Use `data/products.json` to seed product pages if you prefer to render client-side or to keep content DRY.

---

## 9. Reusable UI components and patterns

* **Header** — brand, nav, contact CTA
* **Hero** — animated heading with small subtitle and CTAs
* **Card** — used for products, packages, testimonials
* **Product card** — thumbnail, title, primary specs, CTA
* **Gallery** — main image + thumbs
* **Modal** — quote/contact modal
* **Footer** — links, legal, newsletter

**Coding pattern:** keep components small and accessible. Prefer semantic HTML (`<header>`, `<main>`, `<section>`, `<article>`, `<nav>`, `<footer>`).

---

## 10. Animation & interaction plan (including glowing title)

Animations should be tasteful and not harm performance.

* **Glowing title:** implemented with CSS gradient text + subtle drop-shadow + `@keyframes` flicker/pulse. Accessible fallbacks: allow `prefers-reduced-motion` to reduce animation.
* **Hero sun arc / panels:** lightweight CSS keyframes for float, plus a subtle parallax for scroll.
* **On-scroll reveals:** Intersection Observer to add `is-visible` classes for fade & slide-in.
* **Gallery:** click thumb to swap main image with a smooth fade.
* **Modal:** focus trap, ARIA attributes and ESC to close.

**Accessibility note:** provide `prefers-reduced-motion` checks and avoid auto-play audio or long-running motion.

---

## 11. Accessibility, SEO & performance notes

**Accessibility (A11y)**

* Use semantic HTML and proper heading hierarchy (H1 per page only, H2 sections).
* All images must have meaningful `alt` attributes.
* Keyboard navigability for nav, gallery, and modal.
* Form labels and `aria-*` attributes where applicable.
* Color contrast: ensure text to background contrast meets WCAG AA (use tools to verify).

**SEO basics**

* Unique `<title>` and `<meta name="description">` per page
* Open Graph tags for social sharing
* Use structured data for products (JSON-LD) where appropriate
* Human-readable URLs and meaningful `h1` on each page

**Performance**

* Use optimized images (WebP fallback, responsive `srcset`)
* Lazy-load non-critical images with `loading="lazy"`
* Minify CSS & JS for production
* Use caching headers when deployed

---

## 12. QA / testing checklist

* [ ] Responsive at breakpoints: 320, 480, 768, 1024, 1440
* [ ] Keyboard navigation across the site
* [ ] Modal focus trap and ESC close
* [ ] All forms submit and validation work (client-side and server-side stubs)
* [ ] Links and downloads (PDF) working
* [ ] Lighthouse audit: accessibility, performance, best practices
* [ ] Cross-browser checks: Chrome, Firefox, Edge, Safari (mobile and desktop)

---

## 13. Deployment & deliverables

**Deliverables for the first build (Phase A):**

* 5 HTML pages (Home, Products, Services, About, Contact)
* `css/main.css` and `js/main.js` (minified versions for production)
* `assets/` with images and datasheets
* `data/products.json` (seed data)
* `README.md` (this document)

**Recommended deployment options:**

* GitHub Pages (simple: push to `main` branch, enable Pages)
* Netlify / Vercel (drag & drop or connect to repo for continuous deploy)

---

## 14. Next steps — what I need from you

Please provide the following so I can start building the site:

* High-resolution **logo** (SVG preferred) and color palette (primary/secondary)
* 3–6 **product items** with: name, short description, 3 images each (min 1200px), spec sheet PDFs
* Company contact info (email, phone, office address) and social links
* Any existing **brand copy** (mission, tagline) and case studies/testimonials
* Preference for fonts (or allow me to pick a modern web-safe pairing)

Once you drop these assets I will proceed to Part 2: Design mockups & detailed wireframes and then Part 3: implementation of the 5 pages.

---

### Appendix: Example meta & JSON-LD snippet (for developer reference)

**Meta example (Products page)**

```html
<title>Products — The MM Regeneration Skies</title>
<meta name="description" content="High-efficiency solar panels, hybrid inverters and battery backups. Request a quote today." />
<meta property="og:title" content="Products — The MM Regeneration Skies" />
```

**Product JSON-LD template (structured data)**

```json
{
  "@context": "https://schema.org",
  "@type": "Product",
  "name": "Solar Panel 400W",
  "image": "https://example.com/assets/img/panel-400w.jpg",
  "description": "High-efficiency monocrystalline 400W panel",
  "brand": "The MM Regeneration Skies",
  "offers": { "@type": "Offer", "priceCurrency": "USD", "price": "199" }
}
```

