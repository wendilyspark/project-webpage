# Project Webpage — Consulting Case Study HTML Generator

**Turn a consulting project write-up into a professional portfolio page — no HTML skills required.**

## The Problem

Most consultants document their work in PowerPoint and Word. When it's time to build a portfolio, those files sit in a folder that's impossible to share with a potential client or employer. Writing a clean, professional web page from scratch takes days — and requires design and HTML skills most consultants don't have.

The alternative — a PDF export or a plain text summary — doesn't do the work justice. Analysis frameworks, deliverable breakdowns, and quantitative insights lose all their visual impact when flattened into paragraphs.

## What This Skill Does

Project Webpage reads your consulting project materials and generates a self-contained, professionally designed HTML portfolio page. Drop in a Word doc, a PowerPoint, or just describe the project in conversation — the skill handles structure, design, and content sanitization.

**What you get:**

- **A complete single-file HTML page** — no build step, no dependencies, opens in any browser
- **Professional navy-and-gold design** — Playfair Display headings, clean section layouts, subtle scroll animations
- **Full content fidelity** — every analysis section, deliverable, and metric from your source material, reorganized for visual impact
- **Built-in client anonymization** — real client names are replaced with neutral descriptors ("Leading State-Owned Developer", "BRICS Multilateral Development Bank") — safe to publish publicly
- **Component-rich layouts** — card grids, layer stacks, stat callouts, benchmark tables, and tag clouds map your content to the right visual pattern automatically

## Input / Output

### Input

Provide any of:
- **A Word doc** (`.docx`) — project case study, engagement summary, or final report
- **A PowerPoint** (`.pptx`) — final deck or working slides
- **Conversation** — describe the project context, analysis areas, and key deliverables
- **An existing project folder** — the skill can scan and summarize before generating

Minimum needed: project title, client context, 2–3 analysis areas or deliverables, and any key metrics.

**Sample input (conversation):**

```
Project: Post-Acquisition Integration Planning for a Canadian gold mine
Client: Mining company transitioning to full ownership after PE acquisition
Duration: 3 months
Key deliverables:
  - 100-day integration roadmap across Finance, Technology, and Legal
  - IFRS compliance workplan (IFRS 15 revenue recognition, Big Four coordination)
  - Activity-level program tracker with RACI and milestone flags
Sector: Mining / Private Equity
```

### Output

A single `.html` file (~200–400 KB) that opens in any browser. No server, no internet connection required after the initial Tailwind CDN load.

**Page structure:**
```
Hero section
  └── Project title, client descriptor, duration, engagement type, key stats

Project Background
  └── Context paragraph in a highlight box

Analysis Sections (ANALYSIS 01, 02, 03…)
  └── Each area gets a serif heading + bullet cards or list

Deliverables (DELIVERABLE 01, 02…)
  └── Card grids, layer stacks, or stat callouts depending on content type

Skills & Domains
  └── Gold tag cloud on dark background

Footer
```

**Sample output structure (from a real engagement, client name sanitized):**

```html
<!-- Hero -->
<h1>
  Canadian Gold Mine Operator<br>
  <span>Post-Acquisition Integration & Compliance Planning</span>
</h1>
<div class="stats-grid">
  <div>3 Months</div>
  <div>15 Workstreams</div>
  <div>3 Functional Areas</div>
</div>

<!-- Analysis section -->
<div class="section-label">ANALYSIS 01</div>
<h2>Integration Scope & Workstream Mapping</h2>
<ul>
  <li>Finance: IFRS currency transition, revenue recognition redesign,
      Purchase Price Accounting with Big Four auditors</li>
  <li>Technology: systems migration timeline and data governance protocol</li>
  <li>Legal: regulatory filings, contract assignments, compliance calendar</li>
</ul>
```

**Sample page (screenshot):**

![Project Webpage Sample](references/sample-preview.jpg)

*(Navy/gold palette, serif headings, card-based deliverable layouts with scroll-reveal animations)*

## Installation

```bash
git clone https://github.com/wendilyspark/project-webpage.git ~/.claude/skills/project-webpage
```

**Prerequisites:** [Claude Code](https://docs.anthropic.com/en/docs/claude-code) CLI installed.

No other dependencies — the generated HTML uses CDN-hosted Tailwind CSS and Google Fonts.

## Usage

Once installed, trigger the skill by describing what you want:

```
> Make an HTML portfolio page for my integration planning project

> Turn this Word doc into a consulting case study webpage

> Generate a project showcase page — I'll describe the engagement

> /project-webpage
```

You can also invoke it directly with `/project-webpage` in any Claude Code session.

**The skill will:**
1. Ask for (or read) your source material
2. Extract all content — every bullet, every metric, every deliverable
3. Propose a sanitized client descriptor for your review
4. Generate the HTML file and save it to the location you specify
5. Offer to iterate on layout, color balance, or content depth

## Companion Skills

Works well with [**summarize-deliverables**](https://github.com/wendilyspark/summarize-deliverables) — scan a project folder (decks, spreadsheets, reports) first to generate a structured project summary, then feed that directly into this skill.

Also pairs with [**project-value**](https://github.com/wendilyspark/project-value) — use project-value to generate portfolio card copy for your homepage, and project-webpage to generate the full detail page it links to.

## License

MIT
