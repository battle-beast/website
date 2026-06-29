# Implementation Plan: Battle Beast — battlebeast.online

## Overview

A multi-page static marketing site for Battle Beast playing cards. Built with Astro (component-based, zero JS by default, outputs pure HTML/CSS). Hosted on GitHub, deployed to GitHub Pages via GitHub Actions. Custom domain: battlebeast.online.

## Brand (confirmed)

| Token | Value |
|---|---|
| Background | `#0D0D0D` |
| Primary | `#C0392B` (crimson red) |
| Accent | `#D4AF37` (gold) |
| Text | `#F5F5F5` |
| Heading font | Cinzel (Google Fonts) |
| Body font | Inter (Google Fonts) |
| Logo | Beast skull / animal head in card frame + wordmark (TBD asset) |

## Architecture Decisions

- **Astro** — shared Layout component handles nav/footer once; each page is a `.astro` file. No framework overhead.
- **GitHub Pages** — free static hosting, custom domain support via CNAME. Deploy on push to `main` via `withastro/action`.
- **CSS custom properties** — no CSS framework; one `global.css` with brand tokens (color, font, spacing). Keeps the bundle tiny.
- **No JS unless needed** — Astro ships zero JS by default. Add only for mobile menu toggle if needed.

## Pages

| Page | Path | Purpose |
|---|---|---|
| Home | `/` | Hero, product teaser, primary CTA |
| Cards | `/cards` | Gallery — card artwork & descriptions |
| How to Play | `/how-to-play` | Rules overview |
| About | `/about` | Brand story |
| Buy | `/buy` | Where/how to purchase (links out) |

---

## Task List

### Phase 1: Foundation

- [ ] Task 1: Scaffold Astro project + GitHub repo + Pages workflow
- [ ] Task 2: Layout component (shared nav + footer)
- [ ] Task 3: Global styles (brand tokens, typography, reset)

### Checkpoint: Foundation
- [ ] `npm run build` succeeds locally
- [ ] GitHub Actions deploy succeeds (site live at `<username>.github.io/battlebeast`)
- [ ] Nav links render on every page

### Phase 2: Core Pages

- [ ] Task 4: Home page (hero + tagline + CTA button)
- [ ] Task 5: Cards gallery page (grid of card images + names)
- [ ] Task 6: How to Play page (rules content)
- [ ] Task 7: About page (brand story)
- [ ] Task 8: Buy page (purchase links, pricing info)

### Checkpoint: Core Pages
- [ ] All 5 pages render without errors
- [ ] Navigation works between all pages
- [ ] Site is usable on mobile (no overflow, no broken layout)

### Phase 3: Polish + Launch

- [ ] Task 9: Mobile responsiveness (hamburger menu if needed, fluid grids)
- [ ] Task 10: SEO + meta (title, description, OG image per page, favicon)
- [ ] Task 11: Custom domain config (CNAME file → battlebeast.online, DNS records)

### Checkpoint: Launch-ready
- [ ] `https://battlebeast.online` loads the site
- [ ] No console errors
- [ ] Lighthouse score ≥ 90 performance, 100 accessibility

---

## Task Details

### Task 1: Scaffold Astro project + GitHub repo + Pages workflow

**Description:** Create the Astro project, push to GitHub, wire up the GitHub Actions workflow so every push to `main` deploys to GitHub Pages.

**Acceptance criteria:**
- [ ] `npm create astro` scaffold committed to repo
- [ ] GitHub Actions workflow using `withastro/action` present at `.github/workflows/deploy.yml`
- [ ] Push to `main` triggers a successful Pages deployment

**Verification:**
- [ ] `npm run build` exits 0 locally
- [ ] GitHub Actions run shows green
- [ ] Site accessible at `https://<username>.github.io/<repo>`

**Dependencies:** None

**Files likely touched:**
- `package.json`, `astro.config.mjs`
- `.github/workflows/deploy.yml`

**Estimated scope:** Small

---

### Task 2: Layout component (shared nav + footer)

**Description:** Single `Layout.astro` wrapping every page. Includes site nav (logo + page links) and footer (copyright, social links). All pages slot content into this layout.

**Acceptance criteria:**
- [ ] `src/layouts/Layout.astro` exists and wraps `<slot />`
- [ ] Nav shows logo and links to all 5 pages
- [ ] Footer shows copyright and placeholder social links
- [ ] Active page link is visually indicated

**Verification:**
- [ ] Build passes
- [ ] Nav renders on Home and one other page

**Dependencies:** Task 1

**Files likely touched:**
- `src/layouts/Layout.astro`
- `src/pages/index.astro` (updated to use layout)

**Estimated scope:** Small

---

### Task 3: Global styles (brand tokens, typography, reset)

**Description:** One `global.css` defining CSS custom properties for brand colors, fonts, and spacing. Applied via the Layout. No CSS framework — just variables and a minimal reset.

**Acceptance criteria:**
- [ ] CSS variables defined: `--color-primary`, `--color-bg`, `--color-text`, `--font-heading`, `--font-body`
- [ ] Google Fonts (or system font) loaded for heading and body
- [ ] Box-sizing reset applied globally

**Verification:**
- [ ] Styles apply on the live site
- [ ] No FOUC (flash of unstyled content)

**Dependencies:** Task 2

**Files likely touched:**
- `src/styles/global.css`
- `src/layouts/Layout.astro`

**Estimated scope:** Small

---

### Task 4: Home page

**Description:** Landing page with a full-width hero (product name, tagline, hero image), a brief product teaser section, and a primary CTA button linking to `/buy`.

**Acceptance criteria:**
- [ ] Hero section visible above the fold on desktop and mobile
- [ ] CTA button links to `/buy`
- [ ] Page title is "Battle Beast — Playing Cards"

**Verification:**
- [ ] Manual: open `/`, verify hero renders, click CTA goes to Buy page

**Dependencies:** Tasks 2, 3

**Files likely touched:**
- `src/pages/index.astro`

**Estimated scope:** Small

---

### Task 5: Cards gallery page

**Description:** Grid of card images with names/descriptions. Uses placeholder images until real assets are provided.

**Acceptance criteria:**
- [ ] Responsive grid (2-col mobile, 3-4 col desktop)
- [ ] Each card shows image + name
- [ ] Page accessible at `/cards`

**Verification:**
- [ ] Build passes
- [ ] Grid displays on mobile without horizontal scroll

**Dependencies:** Tasks 2, 3

**Files likely touched:**
- `src/pages/cards.astro`
- `src/components/CardGrid.astro` (if extracted)
- `public/images/cards/`

**Estimated scope:** Small–Medium

---

### Task 6: How to Play page

**Description:** Rules overview — structured content (sections, lists). Static prose page.

**Acceptance criteria:**
- [ ] Page accessible at `/how-to-play`
- [ ] Content organized with headings and readable typography

**Verification:**
- [ ] Manual: read through on mobile, no text overflow

**Dependencies:** Tasks 2, 3

**Files likely touched:**
- `src/pages/how-to-play.astro`

**Estimated scope:** Small

---

### Task 7: About page

**Description:** Brand story — who made Battle Beast, why it exists, any team info.

**Acceptance criteria:**
- [ ] Page accessible at `/about`
- [ ] At minimum one paragraph of content (placeholder OK)

**Verification:**
- [ ] Manual: page renders, no broken layout

**Dependencies:** Tasks 2, 3

**Files likely touched:**
- `src/pages/about.astro`

**Estimated scope:** Small

---

### Task 8: Buy page

**Description:** Where to purchase — links out to external shop (Kickstarter, Gamefound, Shopify, etc.), pricing if available, shipping info if known.

**Acceptance criteria:**
- [ ] Page accessible at `/buy`
- [ ] At least one external purchase link
- [ ] Link opens in new tab

**Verification:**
- [ ] Manual: click purchase link, opens external site

**Dependencies:** Tasks 2, 3

**Files likely touched:**
- `src/pages/buy.astro`

**Estimated scope:** Small

---

### Task 9: Mobile responsiveness

**Description:** Audit all pages on mobile viewport. Add hamburger menu if nav overflows. Fix any layout issues.

**Acceptance criteria:**
- [ ] All pages usable at 375px width
- [ ] Nav accessible on mobile (hamburger or condensed)
- [ ] No horizontal overflow on any page

**Verification:**
- [ ] Chrome DevTools mobile emulation on all 5 pages
- [ ] Real device check if available

**Dependencies:** Tasks 4–8

**Files likely touched:**
- `src/layouts/Layout.astro`
- `src/styles/global.css`

**Estimated scope:** Small–Medium

---

### Task 10: SEO + meta

**Description:** Each page gets a unique `<title>`, `<meta description>`, and Open Graph tags. Favicon added. OG image added (shared or per-page).

**Acceptance criteria:**
- [ ] Each page has unique title and description
- [ ] `og:title`, `og:description`, `og:image` set on all pages
- [ ] Favicon shows in browser tab

**Verification:**
- [ ] `<head>` tags visible in page source
- [ ] [opengraph.xyz](https://www.opengraph.xyz) preview check (manual)

**Dependencies:** Tasks 4–8

**Files likely touched:**
- `src/layouts/Layout.astro`
- `public/favicon.ico`
- `public/og-image.png`

**Estimated scope:** Small

---

### Task 11: Custom domain (battlebeast.online)

**Description:** Add CNAME file to repo for GitHub Pages. Configure DNS at registrar (A records or CNAME to GitHub). Enable HTTPS in GitHub Pages settings.

**Acceptance criteria:**
- [ ] `public/CNAME` file contains `battlebeast.online`
- [ ] DNS records point to GitHub Pages IPs
- [ ] `https://battlebeast.online` loads the site with valid TLS

**Verification:**
- [ ] `curl -I https://battlebeast.online` returns 200
- [ ] Browser shows padlock (no cert warning)

**Dependencies:** Task 1 (Pages workflow must be working)

**Files likely touched:**
- `public/CNAME`

**Estimated scope:** XS (code side) + DNS config (manual)

---

## Risks and Mitigations

| Risk | Impact | Mitigation |
|---|---|---|
| No brand assets yet (logo, card images, colors) | Med | Use placeholders; site structure ships first |
| DNS propagation delay for custom domain | Low | Plan 24–48h for propagation; test on `.github.io` URL meanwhile |
| Card artwork not ready for gallery | Low | Ship gallery with placeholder grid; swap in real images |

## Open Questions

- What are the brand colors / font preferences?
- Do you have a logo file (SVG preferred)?
- Where will customers actually buy? (Kickstarter, Shopify, other?)
- How many distinct cards are in the set?
- Do you need a contact/inquiry form? (requires a form service like Formspree — still static)
