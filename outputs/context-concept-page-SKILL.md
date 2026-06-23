---
name: context-concept-page
description: >
  Build a "Context" concept page — a single-file HTML deep-read on a historical, legal, or
  political concept, matching the Context website's dark editorial design system with green
  accents. Use this skill whenever the user asks to create a concept page or add a concept
  to the Context history website. Triggers include "build a page for [concept]", "explain
  [doctrine/principle/theory]", "write up [idea]", or "add [concept] to Context". The output
  is a polished, self-contained .html file ready to open in a browser, cross-linked to related
  person and event pages.
---

# Context Concept Page Skill

You are building a page for **Context** — a history website for young, curious readers who want
to understand the ideas that shaped history without academic jargon. The tone is authoritative
but accessible: confident, clear prose, honest about complexity and contested evidence.

## What to produce

A single self-contained `.html` file named `[slug].html` (e.g. `responsibility-to-protect.html`,
`mutually-assured-destruction.html`, `non-aligned-movement.html`), saved to the outputs folder.
Everything — content and JS — lives in one file. CSS comes from the shared `styles.css`.

---

## Design system

Concept pages use `<body class="concept-page">`, which flips all purple accents to green
(`--green: #3dba7e`). Do NOT embed a `<style>` block — all styling comes from `styles.css`.

```
Person pages:  purple (#9b7fe8)  →  <body class="person-page"> (default, no class needed)
Event pages:   amber  (#e8a838)  →  <body class="event-page">
Concept pages: green  (#3dba7e)  →  <body class="concept-page">
```

The hero image border for concept pages is `rgba(61,186,126,0.25)`.

---

## Page structure

Concept pages are flexible — adapt the sections to fit the concept. The core sections are:

### 1. Fixed nav bar
- Logo "Context" linking to `context-v4.html`
- Nav type chip: "Concept" — green, auto from `body.concept-page`
- "Save article" button with JS toast
- Scroll-progress bar (green on concept pages)

### 2. Hero
- Breadcrumb: Home › Concepts › [Domain] › [Concept Name]
- Domain tag: `.hero-region-tag` — label the intellectual domain e.g. "International Law · Established 2005"
  (on concept pages this tag is green, not blue — it labels the domain, not a geography)
- Two-column flex layout if a photo is provided (image right, text left, `align-items:center`):

```html
<div style="display:flex;align-items:center;gap:2.5rem;margin-top:0.5rem;">
  <div style="flex:1;min-width:0;">
    <h1 style="margin-top:0;">[Concept Name]</h1>
    <p class="hero-sub">[One sharp sentence on what the concept claims and why it matters.]</p>
    <div class="hero-meta">
      <span>~N min read</span><span>·</span><span>N academic sources</span><span>·</span>
      <span>Last updated [Month Year]</span>
    </div>
  </div>
  <div style="flex-shrink:0;">
    <img src="[URL]" alt="[Concept]"
      style="width:340px;height:240px;object-fit:cover;border-radius:10px;
             border:1px solid rgba(61,186,126,0.25);display:block;">
  </div>
</div>
```

  Omit the image div entirely if no photo is provided.

### 3. What Is [Concept]? (no Quick Facts box)
Unlike person and event pages, concept pages do **not** use a Quick Facts box. Instead open
with 2–3 paragraphs defining the concept precisely, stating what it claims, and explaining
why it matters. Include one `.callout.concept` box for a key definition or sub-distinction
that readers often miss.

### 4. Origins & Development
2–4 paragraphs on where the concept came from: who coined it, what problem it was responding
to, how it evolved over time. End with a 4-item `.stat-row` of key dates or numbers.

For concepts with a clear intellectual genealogy, use an accordion timeline (`.tl-item`) for
the key moments in the concept's development. For simpler concepts, prose paragraphs suffice.

### 5. The [Core Structure] — Pillars / Dimensions / Principles
Use `.ideology-card` grid (3–4 cards) to lay out the concept's main components or distinctions.
This section adapts to the concept: "The Three Pillars" for R2P, "The Four Freedoms" for
Atlantic Charter, "The Two-State Logic" for partition theory, etc.

Follow with a `.callout.info` or `.callout.warning` highlighting a structural limitation or
common misunderstanding.

### 6. [Concept] in Practice — Case Studies
5–7 `.tl-item` accordion entries showing how the concept has been applied (or failed to be
applied) in real historical situations. Structure each entry as:
- `.tl-date`: the date or period
- `.tl-title`: what happened — name the specific case, not "Early Application"
- `.tl-body`: 2–3 paragraphs: what happened, whether the concept "worked", what it revealed
- `.tl-sources`: 1–3 source chips

### 7. Why It Matters Today
Short framing paragraph, then `.matters-grid` with 3–4 `.matters-card` entries. Each card has
a specific `<h3>` title and `.matters-subpoints` list. Focus on live, current relevance —
ongoing cases, active debates, recent applications.

### 8. Legacy & Debate
The intellectually honest section. Find the live scholarly argument.

- Opening paragraph framing the core contested question
- `.scholars-row` with 2–4 `.scholar-card` entries (`.pro/.critical/.nuanced`)
- Prose paragraphs (2–4) engaging the evidence — where does the weight of evidence sit?
- `.perspectives` grid (`.for/.against`) with sourced argument lists
- Closing synthesis paragraph
- Closing `.pull-quote` capturing the essential tension

### 9. Connected Topics
Group as: "People who shaped this concept," "Events where it was applied," "Related Concepts."
Use `.topics-group` + `.topics-grid` with `.topic-card` entries. Link to real Context pages
where they exist; `href="#"` for pages not yet built.

### 10. Sources
Numbered `.sources-list`. Each entry: `.src-num`, `.src-title`, `.src-journal`, `.src-note`
(1–2 italic sentences on what this source contributes and whether it's freely accessible).

---

## Required JavaScript

Copy verbatim from another Context page. Key points:
- `CONTEXT_ARTICLES`: use the full current array from any existing page, then add the new
  concept entry at the top (before the event entries)
- After building, run the Python sync script to add the entry to all existing pages:

```python
import glob

new_entry = "    { type: 'concept', title: '[Title]', desc: '[Desc]', url: '[slug].html' },"

for page in glob.glob('*.html'):
    with open(page) as f: content = f.read()
    if 'CONTEXT_ARTICLES' not in content or '[slug].html' in content: continue
    anchor = "    { type: 'event',  title: 'The Libyan Civil War',"
    if anchor not in content: continue
    idx = content.index(anchor)
    content = content[:idx] + new_entry + '\n' + content[idx:]
    with open(page, 'w') as f: f.write(content)
    print(f'Updated: {page}')
```

---

## Content guidelines

**Tone.** Write the way a well-read journalist would explain a complex idea to a smart
17-year-old. Define every technical term on first use. Prefer concrete examples over abstract
description — show the concept in action in a specific historical moment.

**No quick facts.** Concepts don't have dates of birth or death tolls. Open instead with a
precise, engaging definition that states what the concept actually claims.

**Structure cards, then prose.** The ideology cards, callout boxes, and matters-cards are
visual anchors — but the surrounding prose is what gives the page its intellectual weight.
Don't let the cards substitute for argument.

**Contested ideas.** Most important concepts are contested — different scholars mean different
things by the same term, or dispute whether the concept describes anything real. The Legacy &
Debate section should reflect the live argument, not present the concept as settled truth.

**Case studies over abstract exposition.** Readers understand concepts through examples.
The case studies section is the most important on a concept page — it's where the concept
becomes concrete and its limitations become visible.

**Section length targets:**
- What Is It: 2–3 paragraphs + 1 callout
- Origins: 2–4 paragraphs + stat-row or accordion
- Core Structure: 3–4 ideology cards + 1 callout
- Each case study entry: 2–3 paragraphs
- Legacy/Debate prose: 2–4 paragraphs minimum
- Aim for 3,000–5,000 words total

---

## Key CSS component reference

| Component | Class | Notes |
|-----------|-------|-------|
| Concept body class | `body.concept-page` | Flips all accents to green |
| Domain tag | `.hero-region-tag` | Green on concept pages (not blue) |
| Ideology/pillar cards | `.ideology-grid` > `.ideology-card` | Green left border + green title on concept pages |
| Callout boxes | `.callout.concept/.warning/.info/.amber` | Use `.callout.concept` for definitions |
| Accordion timeline | `.tl-item` + `.tl-header/.tl-body` | Same as event pages |
| Stat row | `.stat-row` > `.stat-box` | `.stat-number` is green on concept pages |
| Scholars row | `.scholars-row` > `.scholar-card.pro/.critical/.nuanced` | |
| Perspectives | `.perspectives` > `.perspective-card.for/.against` | |
| Why it matters | `.matters-grid` > `.matters-card` | |
| Pull quote | `.pull-quote` > `blockquote` + `cite` | Green left border on concept pages |

---

## What to do when the user asks for a concept page

1. If the user hasn't specified the concept — ask: "Which concept should this page cover?"
2. Check whether the user has uploaded source PDFs — read them before writing.
3. Note whether the user has provided a photo URL — use the two-column hero if so.
4. Write the complete HTML file using the structure above, linking to `styles.css`.
5. Save it as `[concept-slug].html` in the outputs folder.
6. Present the file using the `present_files` tool.
7. Run the Python sync script to add the concept to `CONTEXT_ARTICLES` on all existing pages.
8. Note (1–2 sentences) any sections that would benefit from additional sources.
