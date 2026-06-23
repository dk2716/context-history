---
name: context-event-page
description: >
  Build a "Context" event page — a single-file HTML deep-read on a historical event, matching
  the Context website's dark editorial design system with amber accents. Use this skill whenever
  the user asks to create an event page, build a page for a historical event, or add an event
  to the Context history website. Triggers include "build a page for [event]", "write up
  [conflict/operation/crisis]", or "add [event] to Context". The output is a polished,
  self-contained .html file ready to open in a browser, cross-linked to related person pages.
---

# Context Event Page Skill

You are building a page for **Context** — a history website for young, curious readers who want
to understand historical events without academic jargon. The tone is authoritative but accessible:
confident, clear prose, no bullet-point padding, honest about complexity and contested evidence.

## What to produce

A single self-contained `.html` file named `[slug].html` (e.g. `iran-iraq-war.html`,
`suez-crisis.html`, `arab-spring.html`), saved to the outputs folder. Everything — content and
JS — lives in one file. CSS comes from the shared `styles.css` stylesheet.

---

## Design system

Event pages link to the shared `styles.css` file. The key difference from person pages is:

```html
<body class="event-page">
```

This single class automatically flips all purple accents to amber (`--accent: #e8a838`), changes
the hero gradient to warm amber-dark, and keeps geographic region tags blue. Do NOT embed a
`<style>` block — all styling comes from `styles.css`.

**Event pages use `--accent` amber as their primary colour** (not purple). This distinguishes them
from person pages (purple). The `body.event-page` class handles the switch automatically.

---

## Page structure

Build these sections in order. Each maps to a `<section id="...">` linked from the sticky sidebar.

### 1. Fixed nav bar
- Logo "Context" linking to `context-v4.html`
- Nav type chip: amber background/border, text "Event" — auto from `body.event-page`
- "Save article" button (with JS toast — see JS section below)
- Scroll-progress bar: handled by `styles.css`

### 2. Hero
- Background: dark amber gradient — auto from `body.event-page`
- **No** `.hero-person-layout` or `.hero-avatar` — events don't have a single person to show
- Breadcrumb: Home › Events › [Region] › [Event Name]
- Region tag (blue, geographic): `.hero-region-tag` e.g. "Middle East · 1980–1988"
- Then a **two-column flex layout** with the title/sub/meta on the left and the event photo on
  the right, vertically centered:

```html
<div style="display:flex;align-items:center;gap:2.5rem;margin-top:0.5rem;">
  <div style="flex:1;min-width:0;">
    <h1 style="margin-top:0;">[Event Name]</h1>
    <p class="hero-sub">[One sharp sentence on what was at stake.]</p>
    <div class="hero-meta">
      <span>~N min read</span><span>·</span>
      <span>N academic sources</span><span>·</span>
      <span>Last updated [Month Year]</span>
    </div>
  </div>
  <div style="flex-shrink:0;">
    <img src="[URL]" alt="[Event Name]"
      style="width:340px;height:240px;object-fit:cover;border-radius:10px;
             border:1px solid rgba(232,168,56,0.25);display:block;">
  </div>
</div>
```

  If no photo is provided by the user, omit the image div and use the simple stacked layout
  (breadcrumb → region tag → h1 → hero-sub → hero-meta). Never use a placeholder or broken image.

  The hero photo border colour should match the page type:
  - Event pages: `rgba(232,168,56,0.25)` (amber)
  - If the event is geographically themed and the user specifies a blue image: `rgba(74,158,255,0.25)`

### 3. Quick Facts box
`.quick-facts` grid with event-specific fields:
- Date / Duration
- Location / Region
- Parties involved (both sides + key external actors)
- Death toll (with "(contested)" note if estimates vary)
- Displaced (if applicable)
- Outcome (brief)
- Current status
- Key trigger (the immediate cause)

Optionally follow with a `.stats-grid` (4-column) of contextual at-a-glance numbers (population,
GDP, a key economic figure, government structure). Include when geographic or demographic context
matters. Omit when the stats wouldn't add meaningful understanding.

### 4. Background
2–4 paragraphs. Answer: What was the situation BEFORE the event? Who held power, how, and why
did conditions exist for this event to happen? End with a 4-item `.stat-row` of key numbers.

Don't start with "In [YEAR]." Start with a human detail or structural observation that draws the
reader in. Name specific people, places, and dates.

### 5. Key Figures
`.figures-grid` of 4–6 `.figure-card` entries. Include:
- Main leaders on each side
- Key external actors (foreign powers, international bodies)
- 1–2 figures whose role is often misunderstood or overlooked (a victim, a whistleblower, a
  foreign enabler who rarely gets named in textbook accounts)

Each card: `.figure-name`, `.figure-role`, `.figure-desc` (2–3 sentences, specific).

### 6. Key Events (Accordion Timeline)
5–7 `.tl-item` accordion entries in chronological order. First entry gets `class="tl-item active"`.

Each entry needs:
- `.tl-date`: specific date or range (MONTH YEAR format)
- `.tl-title`: descriptive — NOT "Phase 1" or "The Beginning." Say what actually happened:
  "Saddam's Forces Breach the Shatt al-Arab" not "The Invasion Begins"
- `.tl-body`: 2–4 paragraphs. Paragraph 1: what happened (specific). Paragraph 2: why it mattered.
- `.tl-sources`: 1–3 source chips (`.src-chip`)

### 7. Turning Points
**This section is distinct from the timeline.** Turning points are analytical, not chronological.
They are the moments where history could plausibly have gone differently.

Use `.turning-points` grid with 3–4 `.turning-card` entries. Each has:
- `.turning-card-num`: "Turning Point 1", "Turning Point 2", etc.
- `.turning-card-title`: a decisive, specific name for the hinge moment
- `<p>`: 2–3 sentences on what choice was made, what the alternative was, and what futures that
  foreclosed or opened. Always name who made the decision.

Follow with a `.pull-quote` from a participant or scholar on a key turning point.

### 8. Why It Matters Today
Short framing paragraph (2–3 sentences), then `.matters-grid` with 3–4 `.matters-card` entries.

Each card: `<h3>` with a specific title (not "Ongoing Conflict" — say "The Border Dispute Over
Shatt al-Arab Remains Unresolved"), 2–3 sentences, then `.matters-subpoints` `<ul>` with 3–4
specific ongoing facts or developments.

The colour cycling on matters cards is automatic from CSS.

### 9. Legacy & Debate
The intellectually honest section. Find the live scholarly argument — not the settled history.

Structure:
- Opening paragraph framing the core contested question (what do historians actually argue about?)
- `.scholars-row` with 2–4 `.scholar-card` entries:
  - `.pro` (green left border) — a scholar arguing the optimistic/exculpatory case
  - `.critical` (red left border) — a scholar making the strongest critical case
  - `.nuanced` (amber left border) — a scholar presenting a qualified or mixed position
  - Each needs `.scholar-card-name`, `.scholar-card-title` (affiliation + work), `.scholar-card-verdict`
- `<h3>` naming the specific contested question, then 2–4 prose paragraphs engaging the evidence
- `.perspectives` grid with `.perspective-card.for` and `.perspective-card.against`, each with a
  `.perspective-label` and `<ul>` of arguments with `.perspective-attr` source tags
- Closing synthesis paragraph (where does the weight of evidence actually sit?)
- Closing `.pull-quote` that captures the essential tension

### 10. Connected Topics
Group into "People directly connected," "Related Events," "Concepts." Use `.topics-group` with
`.topics-group-label` and `.topics-grid`.

Each `.topic-card` has a `.topic-type-tag` (`.person`, `.event`, `.region`, `.concept`),
`.topic-name`, and `.topic-preview` (1 sentence on the specific connection). Link to real Context
pages where they exist (e.g. `augusto-pinochet.html`); use `href="#"` for pages not yet built.

### 11. Sources
Numbered list using `.sources-list`. For each source: `.src-num`, `.src-title`, `.src-journal`
(journal/publisher name in the run of text), and `.src-note` (1–2 italic sentences on what this
source contributes and whether it's freely accessible online).

---

## Required JavaScript

Include this block verbatim at the bottom of `<body>`. It handles scroll progress, sidebar
active tracking, accordion, search, and save toast. Fill in the CONTEXT_ARTICLES array with the
current full list from another Context page, then add the new event's entry at the top.

```javascript
const CONTEXT_ARTICLES = [
  // Full list from existing pages — add new event entry here
  { type: 'event', title: 'The Libyan Civil War', desc: '...', url: 'context-v4.html' },
  { type: 'event', title: 'Operation Condor', desc: '...', url: 'operation-condor.html' },
  // ... all person entries ...
];

let _searchOpen = false, _focusIdx = -1;
function toggleSearch() {
  const btn = document.getElementById('searchIconBtn'), dd = document.getElementById('searchDropdown'), inp = document.getElementById('searchInput');
  _searchOpen = !_searchOpen;
  btn.classList.toggle('active', _searchOpen); dd.classList.toggle('open', _searchOpen);
  if (_searchOpen) { inp.focus(); runSearch(''); } else { inp.value = ''; _focusIdx = -1; }
}
function runSearch(q) {
  const box = document.getElementById('searchResults'), term = q.trim().toLowerCase();
  const hits = term === '' ? CONTEXT_ARTICLES : CONTEXT_ARTICLES.filter(a =>
    a.title.toLowerCase().includes(term) || a.desc.toLowerCase().includes(term) || a.type.includes(term));
  _focusIdx = -1;
  if (!hits.length) { box.innerHTML = '<div class="search-empty">No articles yet — more coming soon.</div>'; return; }
  box.innerHTML = hits.map((a,i) =>
    `<a class="search-result" href="${a.url}" data-i="${i}">
       <div class="search-result-top"><span class="topic-type-tag ${a.type}">${a.type}</span>
       <span class="search-result-title">${a.title}</span></div>
       <div class="search-result-desc">${a.desc}</div></a>`).join('');
}
function searchKeydown(e) {
  const items = document.querySelectorAll('.search-result');
  if (e.key==='ArrowDown') { e.preventDefault(); _focusIdx=Math.min(_focusIdx+1,items.length-1); }
  else if (e.key==='ArrowUp') { e.preventDefault(); _focusIdx=Math.max(_focusIdx-1,0); }
  else if (e.key==='Enter'&&_focusIdx>=0) { items[_focusIdx].click(); return; }
  else if (e.key==='Escape') { toggleSearch(); return; }
  items.forEach((r,i)=>r.classList.toggle('focused',i===_focusIdx));
}
document.addEventListener('click', e => { if (_searchOpen && !document.getElementById('searchWrap').contains(e.target)) toggleSearch(); });
window.addEventListener('scroll', () => {
  document.getElementById('progressBar').style.width = Math.min((window.scrollY/(document.body.scrollHeight-window.innerHeight))*100,100)+'%';
  const sections=document.querySelectorAll('section[id]'), navItems=document.querySelectorAll('.sidebar-nav li'); let current='';
  sections.forEach(s=>{if(window.scrollY>=s.offsetTop-120)current=s.id;});
  navItems.forEach(item=>{const link=item.querySelector('a');item.classList.toggle('active',link&&link.getAttribute('href')==='#'+current);});
});
function toggleItem(el) { const w=el.classList.contains('active'); document.querySelectorAll('.tl-item').forEach(i=>i.classList.remove('active')); if(!w)el.classList.add('active'); }
function toggleSave() {
  const btn=document.getElementById('saveBtn'), toast=document.getElementById('toast'), isSaved=btn.classList.contains('saved');
  if(!isSaved){btn.classList.add('saved');btn.innerHTML=`<svg width="12" height="12" viewBox="0 0 24 24" fill="currentColor" stroke="none"><path d="M9 16.17L4.83 12l-1.42 1.41L9 19 21 7l-1.41-1.41L9 16.17z"/></svg> Saved`;toast.classList.add('show');setTimeout(()=>toast.classList.remove('show'),3000);}
  else{btn.classList.remove('saved');btn.innerHTML=`<svg width="12" height="12" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M19 21H5a2 2 0 0 1-2-2V5a2 2 0 0 1 2-2h11l5 5v11a2 2 0 0 1-2 2z"/><polyline points="17 21 17 13 7 13 7 21"/><polyline points="7 3 7 8 15 8"/></svg> Save article`;}
}
```

**After building the page**, add the new event to `CONTEXT_ARTICLES` on all existing pages by
running this Python sync script from the outputs folder:

```python
import re, glob

new_entry = "    { type: 'event', title: '[Title]', desc: '[Desc]', url: '[slug].html' },"

for page in glob.glob('*.html'):
    with open(page) as f: content = f.read()
    if 'CONTEXT_ARTICLES' not in content or '[slug].html' in content: continue
    # Insert after the first entry
    anchor = "    { type: 'event',  title: 'The Libyan Civil War',"
    idx = content.index(anchor)
    end = content.index('\n', idx) + 1
    content = content[:end] + new_entry + '\n' + content[end:]
    with open(page, 'w') as f: f.write(content)
    print(f'Updated: {page}')
```

---

## Sources workflow

**If the user uploads academic PDFs:** read them with the Read tool before writing. Synthesise
their arguments — don't just quote. Attribute every significant factual claim with a `.src-chip`.
Add each uploaded PDF as a numbered source in the Sources section.

**If no PDFs are provided:** write from well-established historical knowledge. Note in the Sources
section which claims need verification. Be clear about confidence levels.

**Photo:** If the user provides a photo URL, use the hero two-column layout above at 340×240px.
The image border colour for event pages is `rgba(232,168,56,0.25)`. If no photo is provided,
omit the image entirely — do not use placeholders.

---

## Content guidelines

**Tone.** Write the way a well-read journalist would explain this event to a smart 17-year-old.
No jargon without definition. Use concrete specifics: numbers, dates, names, places. Say "270
people killed" not "many were killed." Say "1980" not "in the late 20th century."

**Contested evidence.** When death tolls, casualty figures, or historical claims are disputed,
say so explicitly. Name the source of each estimate. Don't present the highest or most dramatic
figure as settled fact.

**Moral honesty.** Don't take political sides, but don't pretend all positions are equally
well-supported by evidence. The Legacy & Debate section should reflect the real scholarly argument.

**Depth over breadth.** 5 events explained well > 12 events listed superficially. The accordion
timeline exists to let readers go deep on what interests them.

**Prose, not bullets.** Section body text is written paragraphs. The structured components
(turning-cards, matters-cards, perspectives) are visual aids — not replacements for prose.

**Section length targets:**
- Background: 3–4 paragraphs + stat-row
- Each timeline entry: 2–4 paragraphs
- Each turning point card: 2–3 sentences
- Legacy/Debate prose: 2–4 paragraphs minimum
- Aim for 3,000–5,000 words total

---

## Key CSS component reference

All classes defined in `styles.css`. Do not redefine inline.

| Component | Class | Notes |
|-----------|-------|-------|
| Stats grid | `.stats-grid` > `.stat-card` | 4-col; use `.stat-card-label/value/sub` |
| Figures grid | `.figures-grid` > `.figure-card` | Auto-fit min 200px; `.figure-name/.figure-role/.figure-desc` |
| Accordion timeline | `.tl-item` + `.tl-header/.tl-body/.tl-date/.tl-title` | First item: `class="tl-item active"` |
| Turning points | `.turning-points` > `.turning-card` | `.turning-card-num/title` + `<p>` |
| Perspectives | `.perspectives` > `.perspective-card.for/.against` | Green/red top border |
| Scholars row | `.scholars-row` > `.scholar-card.pro/.critical/.nuanced` | Green/red/amber left border on verdict |
| Why it matters | `.matters-grid` > `.matters-card` | Top border colour auto-cycles by nth-child |
| Pull quote | `.pull-quote` > `blockquote` + `cite` | Amber left border on event pages |
| Callout boxes | `.callout.concept/.warning/.info/.amber` | Concept/warning/info callout boxes |
| Stat row | `.stat-row` > `.stat-box` | `.stat-number` (amber on event pages), `.stat-label` |

---

## What to do when the user asks for an event page

1. If the user hasn't specified the event — ask: "Which event should this page cover?"
2. Check whether the user has uploaded source PDFs — read them before writing.
3. Note whether the user has provided a photo URL — use the two-column hero if so.
4. Write the complete HTML file using the structure above, linking to `styles.css`.
5. Save it as `[event-slug].html` in the outputs folder.
6. Present the file using the `present_files` tool.
7. Run the Python sync script to add the event to `CONTEXT_ARTICLES` on all existing pages.
8. Note (1–2 sentences) any sections that could be strengthened with additional sources.
