# Template Guide — Component Pattern Library

This file contains copy-pasteable code patterns for building consulting project portfolio HTML pages. Every page is a single self-contained HTML file.

## Table of Contents

1. [HTML Boilerplate & Config](#boilerplate)
2. [CSS Custom Classes](#css-classes)
3. [Hero Section](#hero)
4. [Project Background](#project-background)
4a. [ANALYSIS 00 — Strategic Positioning (equal-height two-column)](#analysis-00)
5. [Insight Cards (Icon + Title + Content)](#insight-cards)
6. [Card Grid with Hover Lift](#card-grid)
7. [Layer Stack (L1/L2/L3)](#layer-stack)
8. [Numbered List with Gold Borders](#numbered-list)
9. [Evolution / Progression Visual (1.0 → 2.0 → 3.0)](#evolution)
10. [Data Pipeline Steps](#data-pipeline)
11. [Metric Cards (Dark Gradient)](#metric-cards)
12. [Monetization Box (Dark Gradient Panel)](#monetization-box)
13. [Three-Party Revenue Table](#revenue-table)
14. [Four-Scenario Service Cards](#service-cards)
15. [Implementation Roadmap Grid](#roadmap-grid)
16. [Tag Cloud — Skills & Domains (Dark Section)](#tag-cloud)
17. [Footer](#footer)
18. [Scroll Reveal Script](#scroll-reveal)
19. [Section Label Pills](#section-labels)
20. [Two-Column Layout Tricks — equal height, ratio, icon centering, compact timeline](#layout-tricks)

---

<a id="boilerplate"></a>
## 1. HTML Boilerplate & Config

Every page starts with this exact boilerplate. The Tailwind config defines the color palette — do not change these values.

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>[Project Title] | [Phase/Type]</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link href="https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@0,400..700;1,400..700&family=Plus+Jakarta+Sans:wght@300..700&display=swap" rel="stylesheet">
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <script>
        tailwind.config = {
            theme: {
                extend: {
                    fontFamily: {
                        serif: ['Playfair Display', 'serif'],
                        sans: ['Plus Jakarta Sans', 'sans-serif'],
                    },
                    colors: {
                        primary:  '#0f2d3e',   /* Blue-900 — headings, dark text */
                        secondary: '#d4a055',  /* Amber — accent ~10% usage */
                        accent:   '#a6cde2',   /* Icon blue — decorative icons */
                        blue800:  '#1d4a63',   /* Blue-800 — metric cards, dark feature sections */
                        blue100:  '#d9edf5',   /* Blue-100 — highlight bg */
                        blue50:   '#f0f7fb',   /* Blue-50 — page background */
                        muted:    '#4a5a6a',   /* Body secondary text */
                    }}}}}
    </script>
    <!-- ⚠️ The 5 closing braces above are: colors } extend } theme } config-obj } end.
         DO NOT add extra braces — a JS syntax error silently breaks ALL custom color
         classes (bg-primary, text-accent, from-secondary, etc.) with no console warning. -->
    <!-- CSS classes go here — see Section 2 -->
</head>
<body class="font-sans antialiased" style="background:#f0f7fb;color:#333;">
    <!-- Sections go here -->
    <!-- Scroll reveal script at the very bottom — see Section 18 -->
</body>
</html>
```

---

<a id="css-classes"></a>
## 2. CSS Custom Classes

Place inside a `<style>` tag in `<head>`, after the Tailwind config script.

```html
<style>
    /* Page background — Blue-50 */
    body { background: #f0f7fb; }

    /* Hero — light gradient + amber plus grid pattern */
    .hero-bg {
        background: linear-gradient(135deg, #e8f4fb 0%, #e8f4fb 50%, #f5ede0 100%);
        position: relative;
        overflow: hidden;
    }
    .hero-bg::before {
        content: '';
        position: absolute; inset: 0;
        background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='24' height='24'%3E%3Cpath d='M12 4v16M4 12h16' stroke='%23d4a055' stroke-width='0.6' stroke-opacity='0.22'/%3E%3C/svg%3E");
        background-size: 24px 24px;
        pointer-events: none;
    }

    /* Card hover lift */
    .card-hover { transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1); }
    .card-hover:hover {
        transform: translateY(-4px);
        box-shadow: 0 20px 40px -15px rgba(15, 45, 62, 0.12);
    }

    /* Layer cards — white base, amber left border */
    .layer-card { background: #ffffff; border-left: 4px solid #d4a055; }

    /* Metric cards — Blue-800 gradient */
    .metric-card { background: linear-gradient(135deg, #1d4a63 0%, #2a5f7a 100%); }

    /* Insight cards — white, subtle border */
    .insight-card { background: #ffffff; border: 1px solid rgba(15, 45, 62, 0.08); }

    /* Icon circle — small round badge for insight/positioning cards */
    .icon-circle { background: linear-gradient(135deg, #0f2d3e, #1a4a63); }

    /* Section label pill */
    .section-pill {
        display: inline-flex; align-items: center;
        padding: 4px 14px; border-radius: 999px;
        font-size: 11px; font-weight: 700; letter-spacing: 0.08em;
        background: rgba(212, 160, 85, 0.14); border: 1px solid rgba(212, 160, 85, 0.35);
        color: #7a4a10;
    }

    /* Scroll reveal animation */
    .scroll-reveal { opacity: 0; transform: translateY(28px); transition: all 0.8s ease-out; }
    .scroll-reveal.active { opacity: 1; transform: translateY(0); }
</style>
```

---

<a id="hero"></a>
## 3. Hero Section

The hero uses a **light Blue→Cream gradient** with an amber plus grid pattern overlay. Text is dark (Blue-900 heading, amber subtitle, muted body, icon-blue icons). No fade-to-dark at bottom.

```html
<header class="hero-bg">
    <div class="relative max-w-7xl mx-auto px-6 pt-10 pb-20 lg:pt-14 lg:pb-28" style="z-index:2;">

        <!-- Pills -->
        <div class="flex flex-wrap items-center gap-2 mb-5">
            <span style="display:inline-flex;align-items:center;padding:4px 14px;border-radius:999px;font-size:11px;font-weight:600;letter-spacing:0.1em;background:rgba(15,45,62,0.08);border:1px solid rgba(15,45,62,0.14);color:#0f2d3e;">
                JAN — JUN 2021
            </span>
            <span style="display:inline-flex;align-items:center;padding:4px 14px;border-radius:999px;font-size:11px;font-weight:600;letter-spacing:0.08em;background:rgba(212,160,85,0.14);border:1px solid rgba(212,160,85,0.32);color:#7a4a10;">
                DIGITAL STRATEGY
            </span>
        </div>

        <!-- H1: smaller than before — text-5xl max, tight leading -->
        <h1 class="font-serif text-4xl lg:text-5xl font-bold leading-[1.1] tracking-tight mb-5" style="color:#0f2d3e;">
            Project Title Line 1<br/>
            <span style="color:#d4a055;">Project Subtitle in Amber</span>
        </h1>

        <!-- Description: base/lg, muted blue-grey -->
        <p class="text-base lg:text-lg max-w-2xl leading-relaxed mb-7" style="color:#4a5a6a;">
            One to two lines describing the project scope at a high level
        </p>

        <!-- Meta stats: icon-blue icons, muted text -->
        <div class="flex flex-wrap gap-6 text-sm" style="color:#4a5a6a;">
            <div class="flex items-center gap-2">
                <i class="fas fa-building text-xs" style="color:#a6cde2;"></i>
                <span>Key Stat 1</span>
            </div>
            <div class="flex items-center gap-2">
                <i class="fas fa-layer-group text-xs" style="color:#a6cde2;"></i>
                <span>Key Stat 2</span>
            </div>
            <div class="flex items-center gap-2">
                <i class="fas fa-users text-xs" style="color:#a6cde2;"></i>
                <span>Key Stat 3</span>
            </div>
        </div>
    </div>
</header>
```

**Color reference:**
| Element | Value |
|---|---|
| Hero bg | `linear-gradient(135deg, #e8f4fb 0%, #e8f4fb 50%, #f5ede0 100%)` |
| Pattern | Amber plus grid via `::before` (see §2) |
| H1 | `#0f2d3e` |
| Subtitle | `#d4a055` |
| Description | `#4a5a6a` |
| Date pill | `rgba(15,45,62,0.08)` bg / `#0f2d3e` text |
| Type pill | `rgba(212,160,85,0.14)` bg / `#7a4a10` text |
| Icons | `#a6cde2` |

---

<a id="project-background"></a>
## 4. Project Background

Plain text on white background — **one paragraph only**. Strategic context (market evolution, role shifts, industry architecture) belongs in a separate ANALYSIS 00 section, not here. A thin divider line separates it from the next section.

```html
<section class="pt-16 pb-0" style="background:#ffffff;">
    <div class="max-w-7xl mx-auto px-6">
    <div class="scroll-reveal mb-10">
        <h2 class="font-serif text-3xl font-bold mb-6" style="color:#0f2d3e;">Project Background</h2>
        <p class="text-lg leading-relaxed max-w-4xl" style="color:#4a5a6a;">
            Context paragraph about the client, engagement scope, and objectives...
        </p>
    </div>
    </div>
    <hr style="border:none; border-top: 1px solid rgba(0,0,0,0.18); margin: 0;">
</section>
```

> **Rule:** Project Background = one paragraph, scope/objective only. If overflow content exists (market evolution, industry architecture, role transformation), overflow goes into **ANALYSIS 00** — see §4a. Don't force-fit extra context here.

> **Note:** The full-width `<hr>` sits outside the `max-w-7xl` container so it bleeds edge-to-edge.

---

<a id="analysis-00"></a>
## 4a. ANALYSIS 00 — Strategic Positioning *(optional — use only when needed)*

**When to use:** Only when Project Background has excess context that doesn't fit one paragraph — e.g. market evolution, industry architecture, role transformation. Do not add this section by default.

Uses light gray background (`#f8f9fa`) immediately after Project Background. For layout and card techniques, see the general **§20 Two-Column Layout Tricks** which apply here and in any other section.

```html
<section class="py-16" style="background:#f8f9fa;">
    <div class="max-w-7xl mx-auto px-6">
    <div class="scroll-reveal mb-10">
        <span class="section-pill mb-4" style="display:inline-block;">ANALYSIS 00</span>
        <h2 class="font-serif text-3xl font-bold mt-3 mb-2" style="color:#0f2d3e;">Strategic Positioning</h2>
    </div>
    <!-- For equal-height columns with icon cards + panel, apply §20 techniques -->
    <div class="grid lg:grid-cols-[1fr_1.1fr] gap-12 items-stretch">
        <div class="scroll-reveal flex flex-col">
            <!-- Optional: compact inline timeline (§9) -->
            <!-- Icon cards using flex-1 to fill height (§20) -->
        </div>
        <div class="scroll-reveal">
            <!-- Numbered panel (§8) -->
        </div>
    </div>
    </div>
</section>
```

---

<a id="insight-cards"></a>
## 5. Insight Cards (Icon + Title + Content)

Three-column grid for competitive analysis, pain points, success factors, etc. White cards with subtle border. Icon circle backgrounds use palette tints.

```html
<div class="grid md:grid-cols-2 lg:grid-cols-3 gap-6">
    <div class="card-hover insight-card rounded-2xl p-6">
        <div class="flex items-center gap-3 mb-4">
            <div class="w-10 h-10 rounded-lg flex items-center justify-center"
                 style="background:rgba(166,205,226,0.18);color:#3a80a6;">
                <i class="fas fa-sync-alt"></i>
            </div>
            <h4 class="font-bold text-sm" style="color:#0f2d3e;">Card Title</h4>
        </div>
        <p class="text-xs leading-relaxed" style="color:#4a5a6a;">Card content text</p>
    </div>

    <div class="card-hover insight-card rounded-2xl p-6">
        <div class="flex items-center gap-3 mb-4">
            <div class="w-10 h-10 rounded-lg flex items-center justify-center"
                 style="background:rgba(212,160,85,0.12);color:#9a6010;">
                <i class="fas fa-shield-alt"></i>
            </div>
            <h4 class="font-bold text-sm" style="color:#0f2d3e;">Card Title</h4>
        </div>
        <p class="text-xs leading-relaxed" style="color:#4a5a6a;">Card content text</p>
    </div>

    <!-- Use other palette tints for variety: green rgba(34,130,80,0.1), slate rgba(15,45,62,0.07) -->
</div>
```

---

<a id="card-grid"></a>
## 6. Card Grid with Hover Lift

Used for user segments, service categories, scenario overviews. Cards use `card-hover` for the lift effect.

```html
<div class="grid md:grid-cols-2 lg:grid-cols-3 gap-6">
    <div class="card-hover insight-card rounded-2xl p-6">
        <div class="w-12 h-12 rounded-xl flex items-center justify-center text-white mb-4"
             style="background:#0f2d3e;">
            <i class="fas fa-briefcase"></i>
        </div>
        <h4 class="font-bold mb-2" style="color:#0f2d3e;">Card Title</h4>
        <p class="text-sm" style="color:#4a5a6a;">Card description text</p>
    </div>

    <div class="card-hover insight-card rounded-2xl p-6">
        <div class="w-12 h-12 rounded-xl flex items-center justify-center text-white mb-4"
             style="background:#1d4a63;">
            <i class="fas fa-user-tie"></i>
        </div>
        <h4 class="font-bold mb-2" style="color:#0f2d3e;">Card Title</h4>
        <p class="text-sm" style="color:#4a5a6a;">Card description text</p>
    </div>
</div>
```

---

<a id="layer-stack"></a>
## 7. Layer Stack (L1/L2/L3)

Used for deliverables with hierarchical layers. Each card has a left border (amber / accent / amber), a dark icon badge, heading, and description.

```html
<div class="space-y-5">
    <!-- Layer 1: amber border, Blue-900 badge -->
    <div class="layer-card rounded-2xl p-8 shadow-sm card-hover">
        <div class="flex items-start gap-6">
            <div class="w-14 h-14 rounded-2xl flex items-center justify-center text-white text-lg shrink-0"
                 style="background:#0f2d3e;">
                <i class="fas fa-handshake"></i>
            </div>
            <div>
                <h3 class="text-lg font-bold mb-2" style="color:#0f2d3e;">Layer Title</h3>
                <p class="text-sm leading-relaxed" style="color:#4a5a6a;">Layer description</p>
            </div>
        </div>
    </div>

    <!-- Layer 2: accent (icon-blue) border, Blue-800 badge -->
    <div class="layer-card rounded-2xl p-8 shadow-sm card-hover" style="border-left-color:#a6cde2;">
        <div class="flex items-start gap-6">
            <div class="w-14 h-14 rounded-2xl flex items-center justify-center text-white text-lg shrink-0"
                 style="background:#1d4a63;">
                <i class="fas fa-exchange-alt"></i>
            </div>
            <div>
                <h3 class="text-lg font-bold mb-2" style="color:#0f2d3e;">Layer Title</h3>
                <p class="text-sm leading-relaxed" style="color:#4a5a6a;">Layer description</p>
            </div>
        </div>
    </div>

    <!-- Layer 3: amber border, amber tint badge -->
    <div class="layer-card rounded-2xl p-8 shadow-sm card-hover" style="border-left-color:#d4a055;">
        <div class="flex items-start gap-6">
            <div class="w-14 h-14 rounded-2xl flex items-center justify-center text-lg shrink-0"
                 style="background:rgba(212,160,85,0.14);color:#7a4a10;">
                <i class="fas fa-book"></i>
            </div>
            <div>
                <h3 class="text-lg font-bold mb-2" style="color:#0f2d3e;">Layer Title</h3>
                <p class="text-sm leading-relaxed" style="color:#4a5a6a;">Layer description</p>
            </div>
        </div>
    </div>
</div>
```

---

<a id="numbered-list"></a>
## 8. Numbered List with Amber Borders

Used for ordered items like industry layers, architecture tiers, etc.

```html
<div class="space-y-4">
    <div class="flex items-center gap-4 p-4 rounded-lg border-l-4"
         style="background:rgba(212,160,85,0.08);border-left-color:#d4a055;">
        <span class="text-2xl font-bold" style="color:#d4a055;">01</span>
        <div>
            <div class="font-semibold" style="color:#0f2d3e;">Item Title</div>
            <div class="text-sm" style="color:#4a5a6a;">Description</div>
        </div>
    </div>
    <div class="flex items-center gap-4 p-4 rounded-lg border-l-4"
         style="background:rgba(212,160,85,0.05);border-left-color:rgba(212,160,85,0.6);">
        <span class="text-2xl font-bold" style="color:rgba(212,160,85,0.7);">02</span>
        <div>
            <div class="font-semibold" style="color:#0f2d3e;">Item Title</div>
            <div class="text-sm" style="color:#4a5a6a;">Description</div>
        </div>
    </div>
</div>
```

---

<a id="evolution"></a>
## 9. Evolution / Progression Visual (1.0 → 2.0 → 3.0)

Stage-based evolution with amber phase badges and icon-blue arrows.

```html
<div class="flex flex-col md:flex-row items-stretch gap-4">
    <div class="flex-1 bg-white rounded-xl p-6 shadow-sm" style="border:1px solid rgba(15,45,62,0.08);">
        <div class="flex items-center gap-3 mb-3">
            <span class="w-10 h-10 rounded-lg flex items-center justify-center font-bold text-sm"
                  style="background:rgba(212,160,85,0.14);color:#d4a055;">1.0</span>
            <h5 class="font-bold" style="color:#0f2d3e;">Stage Name</h5>
        </div>
        <p class="text-sm leading-relaxed" style="color:#4a5a6a;">Description of stage 1...</p>
    </div>
    <div class="hidden md:flex items-center text-2xl" style="color:#a6cde2;">
        <i class="fas fa-arrow-right"></i>
    </div>
    <!-- Repeat for 2.0, 3.0 -->
</div>
```

---

<a id="data-pipeline"></a>
## 10. Data Pipeline Steps

Sequential system architecture layers (collection → analytics → application).

```html
<div class="space-y-3">
    <div class="flex items-center gap-3 p-3 rounded-lg" style="background:#f0f7fb;">
        <span class="w-8 h-8 text-white rounded-full flex items-center justify-center text-xs font-bold"
              style="background:#0f2d3e;">1</span>
        <div class="flex-1">
            <div class="font-semibold text-sm" style="color:#0f2d3e;">Collection Layer</div>
            <div class="text-xs" style="color:#4a5a6a;">Data sources description</div>
        </div>
    </div>
    <div class="flex items-center gap-3 p-3 rounded-lg" style="background:#f0f7fb;">
        <span class="w-8 h-8 text-white rounded-full flex items-center justify-center text-xs font-bold"
              style="background:#1d4a63;">2</span>
        <div class="flex-1">
            <div class="font-semibold text-sm" style="color:#0f2d3e;">Analytics Layer</div>
            <div class="text-xs" style="color:#4a5a6a;">Processing description</div>
        </div>
    </div>
    <div class="flex items-center gap-3 p-3 rounded-lg" style="background:#f0f7fb;">
        <span class="w-8 h-8 rounded-full flex items-center justify-center text-xs font-bold"
              style="background:rgba(212,160,85,0.2);color:#7a4a10;">3</span>
        <div class="flex-1">
            <div class="font-semibold text-sm" style="color:#0f2d3e;">Application Layer</div>
            <div class="text-xs" style="color:#4a5a6a;">Output/usage description</div>
        </div>
    </div>
</div>
```

---

<a id="metric-cards"></a>
## 11. Metric Cards (Dark Gradient)

Key financial or impact metrics. Blue-800 gradient, icon-blue sub-labels.

```html
<div class="grid md:grid-cols-3 gap-6">
    <div class="metric-card rounded-2xl p-6 text-white text-center">
        <div class="text-4xl font-bold mb-2">37</div>
        <div class="text-sm mb-1" style="color:#a6cde2;">Interview Sessions</div>
        <div class="text-xs" style="color:rgba(166,205,226,0.65);">Supporting detail</div>
    </div>
    <div class="metric-card rounded-2xl p-6 text-white text-center">
        <div class="text-4xl font-bold mb-2">7</div>
        <div class="text-sm mb-1" style="color:#a6cde2;">System Walkthroughs</div>
        <div class="text-xs" style="color:rgba(166,205,226,0.65);">Supporting detail</div>
    </div>
    <!-- Third card can use a slightly lighter variant: background:linear-gradient(135deg,#2a5f7a,#3a7090) -->
    <div class="rounded-2xl p-6 text-white text-center"
         style="background:linear-gradient(135deg,#2a5f7a 0%,#3a7090 100%);">
        <div class="text-4xl font-bold mb-2">100+</div>
        <div class="text-sm mb-1" style="color:#d4a055;">Issues Identified</div>
        <div class="text-xs" style="color:rgba(212,160,85,0.65);">Supporting detail</div>
    </div>
</div>
```

---

<a id="monetization-box"></a>
## 12. Monetization Box (Dark Gradient Panel)

Business model / monetization details. Uses Blue-800 gradient with translucent inner cards.

```html
<div class="rounded-2xl p-8 text-white"
     style="background:linear-gradient(135deg,#1d4a63 0%,#2a5f7a 100%);">
    <h4 class="font-bold mb-6 flex items-center gap-2">
        <i class="fas fa-chart-pie" style="color:#a6cde2;"></i>
        Monetization Model
    </h4>
    <div class="space-y-4">
        <div class="rounded-xl p-4" style="background:rgba(255,255,255,0.1);">
            <div class="font-semibold mb-1">Revenue Stream Name</div>
            <p class="text-sm" style="color:#d9edf5;">Description of the revenue stream</p>
        </div>
        <!-- More items... -->
    </div>
</div>
```

---

<a id="revenue-table"></a>
## 13. Three-Party Revenue Table

Multi-stakeholder financial breakdowns. Three columns with icon + title + items list.

```html
<div class="grid lg:grid-cols-3 gap-8">
    <div class="space-y-4">
        <div class="flex items-center gap-3 mb-4">
            <div class="w-10 h-10 rounded-lg flex items-center justify-center text-white"
                 style="background:#0f2d3e;">
                <i class="fas fa-landmark"></i>
            </div>
            <h5 class="font-bold" style="color:#0f2d3e;">Platform Revenue</h5>
        </div>
        <ul class="space-y-2 text-sm">
            <li class="flex justify-between items-center p-3 rounded-lg" style="background:#f0f7fb;">
                <span>Revenue Share</span>
                <span class="font-bold" style="color:#0f2d3e;">~20%</span>
            </li>
        </ul>
    </div>
    <!-- Repeat for other parties, using #1d4a63 and #d4a055 for badge colors -->
</div>
```

---

<a id="service-cards"></a>
## 14. Four-Scenario Service Cards

Service categories in a four-column grid.

```html
<div class="grid md:grid-cols-2 lg:grid-cols-4 gap-6">
    <div class="bg-white rounded-2xl p-6 shadow-sm card-hover" style="border:1px solid rgba(15,45,62,0.08);">
        <div class="w-12 h-12 rounded-xl flex items-center justify-center mb-4"
             style="background:#f0f7fb;color:#0f2d3e;">
            <i class="fas fa-robot text-xl"></i>
        </div>
        <h4 class="font-bold mb-2" style="color:#0f2d3e;">Scenario Name</h4>
        <p class="text-sm mb-3" style="color:#4a5a6a;">Description with key detail</p>
    </div>
    <!-- 3 more cards -->
</div>
```

---

<a id="roadmap-grid"></a>
## 15. Implementation Roadmap Grid

Phased roadmap cards with amber phase labels and icon-blue arrows.

```html
<div class="flex flex-col md:flex-row items-stretch gap-4">
    <div class="flex-1 bg-white rounded-xl p-6 shadow-sm" style="border:1px solid rgba(15,45,62,0.08);">
        <div class="flex items-center gap-3 mb-3">
            <span class="w-10 h-10 rounded-lg flex items-center justify-center font-bold text-sm"
                  style="background:rgba(212,160,85,0.14);color:#d4a055;">P1</span>
            <div class="text-xs font-semibold tracking-wider" style="color:#d4a055;">0–12 MONTHS</div>
        </div>
        <h5 class="font-bold mb-2" style="color:#0f2d3e;">Phase Name</h5>
        <p class="text-sm leading-relaxed" style="color:#4a5a6a;">Phase description</p>
    </div>
    <div class="hidden md:flex items-center text-2xl" style="color:#a6cde2;">
        <i class="fas fa-arrow-right"></i>
    </div>
    <!-- P2, P3 with same structure -->
</div>
```

---

<a id="tag-cloud"></a>
## 16. Tag Cloud — Skills & Domains (Dark Section)

Always the second-to-last section. Blue-900 background. **Tag labels must match the exact strings in `CONSULTING_SKILLS` and `CONSULTING_SECTORS` from `shared/constants.ts`** — use only the skills and sectors actually tagged to the project.

```html
<section class="py-16" style="background:#0f2d3e;">
    <div class="max-w-7xl mx-auto px-6">
        <div class="grid lg:grid-cols-2 gap-12">

            <div>
                <h3 class="font-serif text-2xl font-bold mb-6 flex items-center gap-3" style="color:#ffffff;">
                    <i class="fas fa-tools" style="color:#a6cde2;"></i>Core Competencies
                </h3>
                <div class="flex flex-wrap gap-3">
                    <!-- Use project's actual skills from consulting-projects.ts -->
                    <span class="px-4 py-2 rounded-full text-sm"
                          style="background:rgba(166,205,226,0.1);color:#d9edf5;border:1px solid rgba(166,205,226,0.2);">
                        Digital Strategy
                    </span>
                    <span class="px-4 py-2 rounded-full text-sm"
                          style="background:rgba(166,205,226,0.1);color:#d9edf5;border:1px solid rgba(166,205,226,0.2);">
                        Operating Model
                    </span>
                </div>
            </div>

            <div>
                <h3 class="font-serif text-2xl font-bold mb-6 flex items-center gap-3" style="color:#ffffff;">
                    <i class="fas fa-industry" style="color:#d4a055;"></i>Industry Domains
                </h3>
                <div class="flex flex-wrap gap-3">
                    <!-- Use project's actual sectors from consulting-projects.ts -->
                    <span class="px-4 py-2 rounded-full text-sm"
                          style="background:rgba(212,160,85,0.15);color:#d4a055;border:1px solid rgba(212,160,85,0.3);">
                        Real Estate
                    </span>
                    <span class="px-4 py-2 rounded-full text-sm"
                          style="background:rgba(212,160,85,0.15);color:#d4a055;border:1px solid rgba(212,160,85,0.3);">
                        Technology
                    </span>
                </div>
            </div>

        </div>
    </div>
</section>
```

> **Rule:** Tag text must exactly match the label strings in `CONSULTING_SKILLS` / `CONSULTING_SECTORS` (e.g. `"Digital Strategy"`, `"Real Estate"`) — not custom free-text descriptions.

---

<a id="footer"></a>
## 17. Footer

Simple centered text on darkest navy.

```html
<footer class="py-8" style="background:#0a1e2a;">
    <div class="max-w-7xl mx-auto px-6 text-center">
        <p class="text-sm" style="color:rgba(166,205,226,0.5);">
            2022 Consulting Project | Deliverables Showcase
        </p>
    </div>
</footer>
```

---

<a id="scroll-reveal"></a>
## 18. Scroll Reveal Script

Place at the very bottom of `<body>`, before `</body>`.

```html
<script>
    /* threshold:0 + rootMargin:'0px' — ensures elements trigger even inside iframes.
       The 1200ms setTimeout fallback forces all elements visible if observer misfires. */
    const observer = new IntersectionObserver((entries) => {
        entries.forEach(entry => { if (entry.isIntersecting) entry.target.classList.add('active'); });
    }, { threshold: 0, rootMargin: '0px' });
    const revealEls = document.querySelectorAll('.scroll-reveal');
    revealEls.forEach(el => observer.observe(el));
    setTimeout(() => revealEls.forEach(el => el.classList.add('active')), 1200);
</script>
```

---

<a id="section-labels"></a>
## 19. Section Label Pills

All section labels (ANALYSIS 01, DELIVERABLE 01, etc.) use the amber tint pill style — **not** a solid gold fill.

```html
<!-- Amber tint pill — use .section-pill class (defined in §2) -->
<span class="section-pill">ANALYSIS 01</span>
<span class="section-pill">DELIVERABLE 01</span>
```

Every section heading follows this pattern:

```html
<div class="scroll-reveal mb-12">
    <div class="flex items-center gap-4 mb-4">
        <span class="section-pill">ANALYSIS 01</span>
    </div>
    <h2 class="font-serif text-3xl lg:text-4xl font-bold mb-4" style="color:#0f2d3e;">
        Section Title in Serif
    </h2>
    <p class="text-base max-w-3xl leading-relaxed" style="color:#4a5a6a;">
        Brief description of what this section covers
    </p>
</div>
```

---

## Section Background Alternation

Alternate section backgrounds for visual rhythm. The page background is Blue-50 (`#f0f7fb`).

| Section | Background | Usage |
|---|---|---|
| Hero | Blue→Cream gradient | Always first |
| Project Background | White `#ffffff` + bottom `<hr>` | Always second |
| ANALYSIS 00 (Strategic Positioning) | Light gray `#f8f9fa` | Optional, immediately after Project Bg |
| Analysis/Content sections | White `bg-white` or page bg (Blue-50) | Alternate |
| Skills & Domains | Blue-900 `#0f2d3e` | Always second-to-last |
| Footer | `#0a1e2a` | Always last |

**Pattern:** Hero → White (Project Bg) → `#f8f9fa` (ANALYSIS 00, if used) → White → Blue-50 → White → Blue-50 → … → Blue-900 (Skills) → `#0a1e2a` (Footer)

Within Blue-50 sections, wrap content: `<div class="max-w-7xl mx-auto px-6">`
Within White sections, use: `<section class="bg-white py-16"><div class="max-w-7xl mx-auto px-6">…</div></section>`

---

<a id="layout-tricks"></a>
## 20. Two-Column Layout Tricks

These techniques apply to **any** two-column section, not just ANALYSIS 00.

### Equal-height columns
When left and right columns have different amounts of content, use `items-stretch` on the grid and `flex flex-col` + `flex-1` on the shorter column's cards so they stretch to fill.

```html
<!-- Grid: items-stretch instead of items-start -->
<div class="grid lg:grid-cols-2 gap-12 items-stretch">

    <!-- Lighter column: flex-col so children can stretch -->
    <div class="scroll-reveal flex flex-col">
        <!-- Fixed-height element at top (e.g. timeline, intro block) -->
        <div class="mb-4 ...">...</div>
        <!-- Cards: flex-1 makes each card grow equally to fill remaining height -->
        <div class="flex flex-col gap-4 flex-1">
            <div class="... flex-1">Card A</div>
            <div class="... flex-1">Card B</div>
        </div>
    </div>

    <!-- Heavier column: no special treatment needed -->
    <div class="scroll-reveal">...</div>
</div>
```

### Asymmetric column ratio
When one column has denser content than the other, use a custom fraction instead of `grid-cols-2`:

```html
<!-- Right column slightly wider -->
<div class="grid lg:grid-cols-[1fr_1.1fr] gap-12 items-stretch">
<!-- Left column wider -->
<div class="grid lg:grid-cols-[1.2fr_1fr] gap-12 items-stretch">
```

### Icon cards — vertical centering
Icon + text cards inside a column use `items-center` (not `items-start`) when the text is short:

```html
<!-- items-center: icon and text vertically centered -->
<div class="flex items-center gap-4 p-4 bg-white rounded-xl shadow-sm border border-slate-100 flex-1">
    <div class="icon-circle w-10 h-10 rounded-full flex items-center justify-center text-white shrink-0">
        <i class="fas fa-chart-line text-sm"></i>
    </div>
    <div>
        <h4 class="font-semibold" style="color:#0f2d3e;">Card Title</h4>
        <p class="text-sm mt-1" style="color:#4a5a6a;">Short description</p>
    </div>
</div>
```

Use `items-start` instead when the description is multi-line (3+ lines) and top-alignment looks better.

### Compact inline progression timeline
Use inside a column when the evolution/phase story is supporting context (not the main focus). The last stage is highlighted in amber.

```html
<div class="p-5 bg-white rounded-xl border border-slate-100 shadow-sm">
    <p class="text-xs font-semibold uppercase tracking-wider mb-4" style="color:#9ca3af;">Evolution Path</p>
    <div class="flex items-stretch gap-1">
        <div class="flex-1 text-center p-3 bg-slate-50 rounded-l-lg border border-slate-200">
            <div class="text-base font-bold" style="color:#9ca3af;">1.0</div>
            <div class="text-xs mt-1 leading-snug" style="color:#9ca3af;">Stage One<br/>Label</div>
        </div>
        <div class="flex items-center px-1 text-sm" style="color:#d1d5db;">›</div>
        <div class="flex-1 text-center p-3 bg-slate-50 border border-slate-200">
            <div class="text-base font-bold" style="color:#9ca3af;">2.0</div>
            <div class="text-xs mt-1 leading-snug" style="color:#9ca3af;">Stage Two<br/>Label</div>
        </div>
        <div class="flex items-center px-1 text-sm" style="color:#d4a055;">›</div>
        <!-- Current/highlighted stage: amber -->
        <div class="flex-1 text-center p-3 rounded-r-lg" style="background:rgba(212,160,85,0.07);border:1px solid rgba(212,160,85,0.3);">
            <div class="text-base font-bold" style="color:#d4a055;">3.0</div>
            <div class="text-xs mt-1 leading-snug" style="color:#7a4a10;">Current<br/>Stage</div>
        </div>
    </div>
</div>
```

> For the full-width card-based evolution visual (main section focus), use §9 instead.
