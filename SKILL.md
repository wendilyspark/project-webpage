---
name: project-webpage
description: >
  Generate professional, visually polished single-page HTML portfolio pages for consulting project case studies.
  Use this skill whenever the user wants to: turn project summaries (from Word docs, PPTs, or conversation) into
  showcase HTML pages; create portfolio webpages for consulting engagements; build case study pages with sanitized
  client names; generate project showcase pages with professional visual design.
  Trigger when the user mentions "project page", "case study HTML", "portfolio webpage", "project showcase",
  "项目网页", "项目展示页", "案例页面", converting project write-ups into web pages, or creating HTML pages
  from consulting project summaries. Also trigger when the user says things like "make an HTML page for this project",
  "generate a webpage to showcase this engagement", or "turn this project summary into a portfolio page".
---

# Project Webpage — Consulting Case Study HTML Generator

This skill turns consulting project summaries into professional, single-page HTML portfolio pages. The pages are designed to showcase project scope, analytical work, deliverables, and expertise — while sanitizing sensitive client information.

## Workflow

### Step 1: Gather the Project Input

Before anything else, ask the user for the material the page will be built from. Any of these works:

- A Word document or PowerPoint deck about the project
- A project folder to scan
- A description in the conversation

Then check what arrived against this minimum:

| Needed | What "enough" looks like |
|---|---|
| Project theme | A working title, or a sentence saying what the engagement was about |
| Client context | The kind of organisation and its situation; the real name is fine, it gets sanitized in Step 4 |
| Timing | Duration or dates |
| Substance | At least two or three analysis areas or deliverables, each with real detail rather than a heading alone |
| Evidence | Some numbers, such as interviews run, sites benchmarked, figures modelled or outcomes achieved |

If anything in the table is missing, or the material is too thin to fill a page, **stop and ask for more before generating.** Name exactly what is missing, for example "I have the three workstreams but nothing on what each one produced — what were the deliverables?" A thin page cannot be fixed by design. Never invent content to fill a gap.

### Step 2: Choose a Style

Ask the user which style they want. There are thirteen, all built from the same sample case study:

| Style | Reference file | Character |
|---|---|---|
| Harbour *(default)* | `references/themes/harbour.html` | Navy, sky blue and brass gold; the original design |
| Editorial | `references/template.html` | Canonical editorial design system |
| Accented | `references/themes/accented.html` | Navy section bands on a cool blue-grey ground |
| Mat | `references/themes/mat.html` | Forest green and cream environments |
| Raw Grid | `references/themes/raw-grid.html` | Neobrutalist block grid with offset shadows |
| Monochrome | `references/themes/monochrome.html` | An accounting ledger in black on white |
| Cartesian | `references/themes/cartesian.html` | Museum monograph with framed plates |
| Cobalt Grid | `references/themes/cobalt-grid.html` | Engineering drawing sheet on graph paper |
| Emerald Editorial | `references/themes/emerald-editorial.html` | Magazine feature with masthead and columns |
| Blue Professional | `references/themes/blue-professional.html` | Product docs with a sidebar table of contents |
| Editorial Tri-Tone | `references/themes/editorial-tri-tone.html` | Poster report in blush, butter and crimson |
| Biennale Yellow | `references/themes/biennale-yellow.html` | Exhibition catalogue with alternating rooms |
| Signal | `references/themes/signal.html` | Sticky side rail, navy bands on cream |

**If the user names a style**, confirm the match and continue.

**If they are unsure, or ask what the options are, open the style browser for them:** `references/style-browser.html`, resolved to an absolute path inside this skill's directory. Open it in their browser (`open` on macOS, `xdg-open` on Linux, `start` on Windows). It is a single page: thumbnails of every style, plus a button for each style across the top that shows it full size. The arrow keys step through them. Tell the user that, and ask them to come back with the name of the style they like.

Do **not** hand the user a list of the individual HTML files to open one by one — that is the experience this step exists to avoid. If the environment cannot open a browser, show the thumbnails in `references/thumbnails/` inline instead.

If the user says they have no preference, use Harbour.

### Step 3: Extract Project Content

Read the source material (Word doc, PPT, or text provided in conversation). Identify and extract:

- Project title and subtitle
- Client name (to be sanitized)
- Duration and engagement type
- Project background / context
- Analysis sections (numbered, with bullet points)
- Core deliverables / products designed
- Monetization or business model details (if any)
- Key metrics and financial figures
- Core skills / competencies applied
- Sector / domain coverage

Preserve ALL detail from the source — every bullet point, every sub-point, every figure. The HTML page should contain the complete content, not a summarized version. Users care deeply about content completeness.

### Step 4: Sanitize Sensitive Information

Replace real client names with generic descriptors. The goal is to make the project presentable in a public portfolio without revealing confidential client identities.

#### 4a. Client Name Sanitization

Use a **client type descriptor** — a short English phrase that conveys the client's nature without revealing identity. The descriptor should reflect the client's ownership structure, industry position, or organizational type.

**Example sanitization patterns:**

| Client in the source material | Sanitized Descriptor | Rationale |
|----------------|---------------------|-----------|
| *A multilateral development bank* | "Multilateral Development Bank" | Org type — multilateral bank |
| *A state-owned property developer* | "Leading State-Owned Developer" | Ownership (state-owned) + sector (developer) |
| *A listed property-services company* | "Listed Property Services Co." | Listed status + sector |
| *A government–developer joint-venture zone* | "Government × Industrial Park Developer" | Joint venture nature (govt + developer) |
| *A named CBD mixed-use complex* | "Premium CBD Mixed-Use Complex" | Asset type + positioning |
| *An overseas-listed international property group* | "Leading International Real Estate Group" | Ownership origin + scale |

**General sanitization rules for other entities:**

| Original Type | Replacement Pattern |
|--------------|-------------------|
| Tech partner / platform vendor | "Top-Tier Cloud & AI Platform", "Leading IoT Platform Provider" |
| Competitor names in benchmarks | "A leading domestic developer's membership app", "Competitor A/B/C" |
| Government bodies | "Municipal government", "District-level science & technology commission" |
| Specific competitor product names | "Leading cross-format loyalty platform" |
| Sub-brands or project codenames | Remove or replace with generic ("Project Alpha", "Flagship Product Line") |

#### 4b. Hero Title Naming Convention

The hero section `<h1>` must include the **client type descriptor** to give readers immediate context. Format:

```
<Client Type Descriptor>
<Project Theme> & <Secondary Theme>
```

**Examples:**

| Engagement type | Hero H1 |
|---------|---------|
| Building digitalization programme | **Multilateral Bank** / Smart Building & Process Digitalization |
| Smart-home product strategy | **State-Owned Developer** / Smart Home Innovation & Monetization Strategy |
| Multi-year growth plan | **Listed Property Services Co.** / Three-Year Strategic Growth Blueprint |
| Industrial zone planning | **Government × Industrial Park Developer** / Industrial Planning & Investment Strategy |
| Luxury residential product study | **State-Owned Developer** / Luxury Residential Product Strategy |
| Digital transformation roadmap | **Premium CBD Mixed-Use Complex** / Digital Transformation Roadmap |

The client type descriptor appears on its own line (using `<br>` or as a separate element) in a slightly different style from the project theme line, creating a two-line hero title.

#### 4c. File Naming Convention

HTML files use kebab-case English names that reflect the project's core theme:

```
<client-short>-<project-theme>.html
```

**Examples:**
- `acme-smart-building.html`
- `acme-luxury-residential.html`
- `northwind-property-strategy.html`
- `contoso-digital-roadmap.html`

Use commonly recognized English abbreviations for client names in filenames (these are not visible to readers). The actual HTML content uses the sanitized descriptor.

#### 4d. What to Keep As-Is

- International landmark names used as benchmarks (Hudson Yards, Roppongi Hills, ICONSIAM) — these are public knowledge
- Generic industry terms and methodologies
- Financial figures and metrics (these don't identify the client)
- City/district names when they are the project location (e.g., a named waterfront or CBD district) rather than the client identity
- Public frameworks and standards when they are context rather than the client (e.g., "ESG" or "IFRS")

### Step 5: Generate HTML

Build the page in the style chosen in Step 2. That style's reference file is a complete, finished page for a sample case study: reuse its CSS, layout system and component vocabulary wholesale, and replace the sample content with the user's. Do not blend styles or restyle the reference.

Every style must also follow the binding rules in `references/themes/TECH-RULES.md`. For **Harbour**, `references/template-guide.md` and the Color System, Tech Stack and Component Pattern Library sections below are the detailed source of truth; for every other style, its reference file is.

**Structural approach — map content to sections:**

1. **Hero** — Project title, subtitle, client descriptor, duration, engagement type, key stats
2. **Project Background** — Context paragraph(s) in a highlight box
3. **Analysis Sections** — Each numbered analysis area gets its own section with:
   - Numbered section label (ANALYSIS 01, ANALYSIS 02, etc.) in the style's own label treatment
   - Serif heading
   - Bullet points in card or list format for detailed content
4. **Deliverables / Products** — Each major deliverable gets a dedicated section with:
   - Numbered pill label (DELIVERABLE 01, etc.)
   - Icon-differentiated cards for different product types
   - Layer visualizations for hierarchical concepts
   - Stats cards for key financial metrics
   - Monetization boxes for business model details
5. **Skills & Domains** — Tag-cloud style footer section on dark background
6. **Footer** — Simple project attribution line

**Key principles:**

- Every bullet point from the source material should appear in the HTML
- Use visual components (cards, grids, layer stacks, stat cards) to make dense information scannable
- Keep the section rhythm of the chosen style's reference file (in Harbour, white and light-gray backgrounds alternate)
- Keep the reference file's interaction and animation behaviour (in Harbour, content sections use the `scroll-reveal` class)
- The page must hold up when the user's content is longer or shorter than the sample — never hard-code heights or column counts to fit the sample's text

### Step 6: Review and Iterate

After generating, ask the user to review. Common adjustment requests include:
- Color usage tweaks (see Color Rules below)
- Adding more visual breakdowns for dense text sections
- Adjusting the level of content sanitization

---

## Color System & Rules

*This section and the two after it describe Harbour, the default style. Other styles carry their own system in their reference file.*

The design uses a navy-blue + gold palette. Getting the color balance right is critical — this was the most iterated aspect of the design.

### The Palette

```
primary:   #1e3a5f  (deep navy — headings, main content boxes)
secondary: #c9a227  (gold — decorative accents, indicators)
accent:    #2d5a87  (medium blue — secondary content elements)
cream:     #faf9f6  (warm white — body background)
```

### Gold Color Rules

Gold (`secondary`) adds warmth and visual interest to an otherwise blue-heavy page. But it must be used carefully:

**USE gold for small decorative elements:**
- Section label pills (ANALYSIS 01, DELIVERABLE 02, etc.)
- Small icon accents inside content boxes (e.g., a gold crown icon inside a navy icon circle)
- Star ratings / checkmarks in benchmark lists
- Numbered indicators (01, 02, 03) and left-border bars on list items
- Stage/phase indicator boxes (1.0, 2.0, 3.0 progression markers)
- Connecting arrows between visual elements
- Footer section: skill/domain tag backgrounds
- Hero section: subtitle text, meta icons

**DO NOT use gold for content box backgrounds when boxes are parallel:**
- If three cards represent B/E/T or three user segments, they should all use the same color family (blues/neutrals) — not two blue + one gold. Gold on one card implies that card is more important, which misleads the reader.
- Content card backgrounds, icon circles on parallel cards, and bullet point colors should stay in the blue/neutral family when the items are peers.

**The test:** Ask "does this gold element suggest this item is more important than its siblings?" If yes, don't use gold there. If the element is purely decorative or structural (a label, an indicator, a border), gold is fine.

### Section Label Consistency

All section labels (ANALYSIS 01–05, DELIVERABLE 01–04, etc.) must use the same style. Use gold pills: `bg-secondary text-primary text-sm font-bold rounded-full`.

---

## Tech Stack

Every page is a self-contained single HTML file using:

- **Tailwind CSS** via CDN (`https://cdn.tailwindcss.com`) with custom config for the color palette
- **Google Fonts**: Playfair Display (serif, for headings) + Plus Jakarta Sans (sans-serif, for body)
- **Font Awesome 6** via CDN for icons
- **Scroll-reveal animation** via IntersectionObserver (vanilla JS at bottom of file)

No build step required. The HTML file works by opening directly in a browser.

---

## Component Pattern Library

Refer to `references/template-guide.md` for copy-pasteable code patterns for:

- Hero section with grid overlay SVG
- Highlight boxes (left-border accent)
- Card grids (hover-lift effect)
- Layer stacks (L1/L2/L3 with side badges)
- Stat/metric cards (dark gradient background)
- Pain point grids (small category cards)
- Insight cards (icon + title + content)
- Three-party revenue tables
- Evolution/progression visuals (1.0 → 2.0 → 3.0)
- Four-layer numbered list with gold borders
- Tag clouds for skills/domains
- Dark footer section with two-column layout

---

## Language

Default output language is **English**. The source material may be in Chinese — translate all content to English for the HTML page. Maintain professional consulting terminology. If the user explicitly requests Chinese or bilingual output, accommodate accordingly.
