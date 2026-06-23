---
name: context-person-page
description: >
  Build a "Context" person page — a single-file HTML biography of a historical figure or leader,
  matching the Context website's dark editorial design system. Use this skill whenever the user
  asks to create a person page, leader page, biography page, or figure page for the Context
  history website. Also trigger when the user says things like "build a page for [person]",
  "write up [leader]", or "add [historical figure] to Context". The output is a polished,
  self-contained .html file ready to open in a browser, cross-linked to related event pages.
---

# Context Person Page Skill

You are building a page for **Context** — a history website for young, curious readers who want
to understand historical figures without academic jargon. The tone is authoritative but accessible:
confident, clear sentences, no bullet-point padding, honest about complexity and moral ambiguity.

## What to produce

A single self-contained `.html` file named `[firstname-lastname].html` (e.g. `gaddafi.html`,
`nasser.html`), saved to the outputs folder. Everything — CSS, JS, content — lives in one file.
No external dependencies.

---

## Design system

Copy this CSS verbatim as your `<style>` block. Do not invent new variables or override the palette.

```css
:root {
  --bg: #0e0e10;
  --surface: #18181c;
  --surface2: #222228;
  --surface3: #2a2a32;
  --accent: #e8a838;       /* amber — used for the logo and global highlights */
  --accent2: #c4392d;
  --text: #f0efe8;
  --muted: #8a8a96;
  --green: #3dba7e;
  --blue: #4a9eff;
  --purple: #9b7fe8;       /* PRIMARY accent for person pages */
  --red: #e05252;
}

*, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
body {
  background: var(--bg); color: var(--text);
  font-family: 'Georgia', 'Times New Roman', serif;
  font-size: 18px; line-height: 1.75;
}
```

**Person pages use `--purple` as their primary accent** (not amber). This distinguishes them from
event pages (amber) and region pages (blue). Every place you'd use amber on an event page — the
progress bar, sidebar active state, nav tag, hero border — use purple here instead.

---

## Page structure

Build these sections in order. Each maps to a `<section id="...">` that the sticky sidebar links to.
Adapt the section titles to fit the person (e.g. "Ideology" might be "Military Strategy" for a general).

### 1. Fixed nav bar
- Logo "Context" in amber (`--accent`) — `font-family: Georgia`
- Nav type chip: purple background/border, text "Person"
- "Save article" button (with JS toast on click — see JS section)
- Scroll-progress bar at the very top of the page: 3px, purple

### 2. Hero
- Background gradient: `linear-gradient(160deg, #14091e 0%, #0e0e10 100%)` with a purple bottom border
- Layout: two columns — avatar circle on left, content on right
- Avatar: 120×120px circle, gradient fill (`linear-gradient(135deg, #2a1a40, #1a1a30)`), purple border,
  a relevant emoji inside (🪖 for military leaders, 👑 for monarchs, ✊ for revolutionaries, 🎓 for intellectuals, etc.)
- Hero content: breadcrumb → purple type tag → h1 (person's name) → name in native script if non-English
  → one-sentence hook sub-heading → meta row (read time · years active · country/region)

### 3. Quick Facts box
A compact grid (2–4 columns, `repeat(auto-fit, minmax(180px, 1fr))`) of key biographical facts.
Always include: full name, born, died (or "b. [year], alive"), in power / active years, how they came
to power, ideology or role, and 1–2 distinctive facts. Use `border: 1px solid rgba(155,127,232,0.15)`.

### 4. Origins & Rise
2–4 paragraphs on background, family/class/tribe, formative influences, and the path to power.
Include a 4-item stat row (`.stat-row`) with significant numbers — age at key milestone, year of
first major act, years in exile, etc.

### 5. Ideology / Worldview / Doctrine
(Rename to fit: "Military Doctrine", "Economic Vision", "Religious Outlook", etc.)
Use an `.ideology-grid` of 3–4 cards, each covering one pillar of the person's worldview. Each card
has a bold purple title + 2–3 sentences of explanation. Include at least one pull-quote from the
person or a close observer.

### 6. How They Acted / Ruled / Operated
The practical mechanics of their power or influence. 3–5 sub-sections (h3). This is where you cover:
how they maintained control, their management style, notable methods, human rights record, key
decisions. Include at least one `.callout.warning` for the darkest documented act.

### 7. [Domain-specific section]
This section adapts to who the person is:
- Political leader → "Foreign Policy" or "Wars & Conflicts"
- Military figure → "Key Campaigns"
- Intellectual → "Major Works & Ideas"
- Business figure → "Companies & Decisions"
Use the accordion timeline (`.tl-item`) for a sequence of key events — 3–5 entries, each with a
date label, title, 2–3 paragraphs, and source chips.

### 8. The Fall / Death / Late Career
What ended their story — overthrow, death, retirement, exile, disgrace. 1–3 timeline accordion entries.
Be specific: where, how, what they said or did at the end. The manner of ending often reveals
something important about the system they built.

### 9. Legacy & Debate
The most intellectually honest section. Structure it as:
- A `.legacy-grid` (2 columns): `.legacy-card.positive` and `.legacy-card.negative`, each with a
  bullet list of 5–7 items
- A third `.legacy-card.complex` below the grid for genuinely contested points
- 1–2 paragraphs of prose synthesising the debate — don't let the cards do all the work
- A closing pull-quote that captures the essential tension

### 10. Connected Topics
Group cards into 2–3 rows: People, Events, then Concepts/Regions. Each card has a type tag
(`.topic-type-tag.person/.event/.region/.concept`), a bold name, and a 1-sentence preview.
If there's an existing Context page for a topic, link `href` to it (e.g. `context-v4.html`).
Otherwise `href="#"`.

### 11. Sources
Numbered list. Purple source number chips. For each source: author, year, title, journal/publisher,
and a 1–2 sentence italic note explaining what this source contributes and whether it's free to access.

---

## Key CSS components

Copy these component classes exactly — they are shared across Context pages:

```css
/* Pull quote */
.pull-quote { border-left: 3px solid var(--purple); padding: 1rem 1.5rem;
  margin: 2rem 0; background: rgba(155,127,232,0.04); border-radius: 0 6px 6px 0; }
.pull-quote blockquote { font-size: 1.05rem; line-height: 1.6; color: var(--text);
  font-style: italic; margin-bottom: 0.5rem; }
.pull-quote cite { font-family: sans-serif; font-size: 0.75rem; color: var(--muted); font-style: normal; }

/* Callout boxes */
.callout { border-radius: 8px; padding: 1.25rem 1.5rem; margin: 2rem 0; border: 1px solid; }
.callout.concept { background: rgba(155,127,232,0.06); border-color: rgba(155,127,232,0.2); }
.callout.warning { background: rgba(196,57,45,0.06); border-color: rgba(196,57,45,0.2); }
.callout.info { background: rgba(74,158,255,0.06); border-color: rgba(74,158,255,0.2); }
.callout.amber { background: rgba(232,168,56,0.05); border-color: rgba(232,168,56,0.2); }
.callout-label { font-family: sans-serif; font-size: 0.65rem; text-transform: uppercase;
  letter-spacing: 0.12em; font-weight: bold; margin-bottom: 0.5rem; }
.callout.concept .callout-label { color: var(--purple); }
.callout.warning .callout-label { color: var(--red); }
.callout.info .callout-label { color: var(--blue); }
.callout.amber .callout-label { color: var(--accent); }
.callout h4 { font-size: 0.95rem; margin-bottom: 0.5rem; color: var(--text); }
.callout p { font-size: 0.85rem; margin-bottom: 0; font-family: sans-serif; line-height: 1.6; }

/* Stat row */
.stat-row { display: grid; grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
  gap: 1rem; margin: 1.5rem 0; }
.stat-box { background: var(--surface); border: 1px solid rgba(255,255,255,0.06);
  border-radius: 8px; padding: 1.1rem; text-align: center; }
.stat-number { font-size: 1.8rem; font-weight: bold; color: var(--purple); line-height: 1;
  margin-bottom: 0.3rem; font-variant-numeric: tabular-nums; font-family: sans-serif; }
.stat-label { font-family: sans-serif; font-size: 0.72rem; color: var(--muted); line-height: 1.3; }

/* Ideology cards */
.ideology-grid { display: grid; grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 1rem; margin: 1.5rem 0; }
.ideology-card { background: var(--surface); border: 1px solid rgba(255,255,255,0.06);
  border-left: 3px solid var(--purple); border-radius: 0 8px 8px 0; padding: 1.1rem 1.2rem; }
.ideology-card-title { font-family: sans-serif; font-size: 0.78rem; font-weight: bold;
  color: var(--purple); text-transform: uppercase; letter-spacing: 0.06em; margin-bottom: 0.4rem; }
.ideology-card p { font-family: sans-serif; font-size: 0.82rem;
  color: rgba(240,239,232,0.75); line-height: 1.5; margin-bottom: 0; }

/* Legacy grid */
.legacy-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 1.25rem; margin: 1.5rem 0; }
.legacy-card { background: var(--surface); border: 1px solid rgba(255,255,255,0.06);
  border-radius: 8px; padding: 1.25rem; }
.legacy-card.positive { border-top: 3px solid var(--green); }
.legacy-card.negative { border-top: 3px solid var(--red); }
.legacy-card.complex { border-top: 3px solid var(--accent); }
.legacy-label { font-family: sans-serif; font-size: 0.68rem; text-transform: uppercase;
  letter-spacing: 0.1em; margin-bottom: 0.75rem; font-weight: bold; }
.legacy-card.positive .legacy-label { color: var(--green); }
.legacy-card.negative .legacy-label { color: var(--red); }
.legacy-card.complex .legacy-label { color: var(--accent); }
.legacy-card ul { list-style: none; font-family: sans-serif; font-size: 0.82rem;
  color: rgba(240,239,232,0.8); }
.legacy-card ul li { padding: 0.4rem 0 0.4rem 1.1rem; border-bottom: 1px solid rgba(255,255,255,0.05);
  position: relative; line-height: 1.4; }
.legacy-card ul li:last-child { border-bottom: none; }
.legacy-card ul li::before { content: '→'; position: absolute; left: 0;
  color: var(--muted); font-size: 0.7rem; top: 0.45rem; }

/* Accordion timeline */
.tl-item { border-left: 2px solid rgba(255,255,255,0.08); margin-left: 0.5rem;
  padding-left: 1.5rem; position: relative; cursor: pointer; }
.tl-item::before { content: ''; position: absolute; left: -5px; top: 22px;
  width: 8px; height: 8px; border-radius: 50%; background: var(--surface2);
  border: 2px solid rgba(255,255,255,0.2); transition: all 0.2s; }
.tl-item.active::before { background: var(--purple); border-color: var(--purple); }
.tl-header { padding: 1rem 0 0.5rem; display: flex; align-items: flex-start;
  justify-content: space-between; gap: 1rem; }
.tl-header-left { flex: 1; }
.tl-date { font-family: sans-serif; font-size: 0.72rem; text-transform: uppercase;
  letter-spacing: 0.08em; color: var(--purple); margin-bottom: 0.3rem; }
.tl-title { font-size: 1rem; font-weight: bold; color: var(--text); line-height: 1.3; }
.tl-chevron { color: var(--muted); font-size: 0.8rem; margin-top: 0.35rem;
  transition: transform 0.25s; flex-shrink: 0; }
.tl-item.active .tl-chevron { transform: rotate(180deg); }
.tl-body { max-height: 0; overflow: hidden; transition: max-height 0.4s ease; }
.tl-item.active .tl-body { max-height: 2000px; padding-bottom: 1.25rem; }
.tl-body p { font-size: 0.92rem; margin-bottom: 0.85rem; }
.tl-sources { display: flex; gap: 0.4rem; flex-wrap: wrap; margin-top: 0.5rem; }
.src-chip { font-family: sans-serif; font-size: 0.68rem; background: rgba(255,255,255,0.05);
  border: 1px solid rgba(255,255,255,0.1); padding: 0.15rem 0.5rem;
  border-radius: 3px; color: var(--muted); }

/* Two-col layout with sticky sidebar */
.outer { max-width: 1160px; margin: 0 auto; padding: 2.5rem 2rem;
  display: grid; grid-template-columns: 200px 1fr; gap: 3rem; align-items: start; }
.sidebar { position: sticky; top: 80px; }
.sidebar-label { font-family: sans-serif; font-size: 0.65rem; text-transform: uppercase;
  letter-spacing: 0.1em; color: var(--muted); margin-bottom: 0.75rem; }
.sidebar-nav { list-style: none; }
.sidebar-nav li { border-left: 2px solid rgba(255,255,255,0.08); }
.sidebar-nav a { display: block; padding: 0.4rem 0.8rem; font-family: sans-serif;
  font-size: 0.78rem; color: var(--muted); text-decoration: none;
  transition: all 0.2s; line-height: 1.3; }
.sidebar-nav li.active { border-left-color: var(--purple); }
.sidebar-nav li.active a { color: var(--purple); }
```

---

## Required JavaScript

Include this JS at the bottom of `<body>`. It handles: scroll progress bar, sidebar active
tracking, timeline accordion, and save button toast.

```javascript
window.addEventListener('scroll', () => {
  const progress = (window.scrollY / (document.body.scrollHeight - window.innerHeight)) * 100;
  document.getElementById('progressBar').style.width = Math.min(progress, 100) + '%';
  updateSidebar();
});

function updateSidebar() {
  const sections = document.querySelectorAll('section[id]');
  const navItems = document.querySelectorAll('.sidebar-nav li');
  let current = '';
  sections.forEach(s => { if (window.scrollY >= s.offsetTop - 120) current = s.id; });
  navItems.forEach(item => {
    const link = item.querySelector('a');
    item.classList.toggle('active', link && link.getAttribute('href') === '#' + current);
  });
}

function toggleItem(el) {
  const wasActive = el.classList.contains('active');
  document.querySelectorAll('.tl-item').forEach(i => i.classList.remove('active'));
  if (!wasActive) el.classList.add('active');
}

document.addEventListener('DOMContentLoaded', () => {
  const first = document.querySelector('.tl-item');
  if (first) first.classList.add('active');
});

function toggleSave() {
  const btn = document.getElementById('saveBtn');
  const toast = document.getElementById('toast');
  const isSaved = btn.classList.contains('saved');
  if (!isSaved) {
    btn.classList.add('saved');
    btn.innerHTML = `<svg width="12" height="12" viewBox="0 0 24 24" fill="currentColor"><path d="M9 16.17L4.83 12l-1.42 1.41L9 19 21 7l-1.41-1.41L9 16.17z"/></svg> Saved`;
    toast.classList.add('show');
    setTimeout(() => toast.classList.remove('show'), 3000);
  } else {
    btn.classList.remove('saved');
    btn.innerHTML = `<svg width="12" height="12" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M19 21H5a2 2 0 0 1-2-2V5a2 2 0 0 1 2-2h11l5 5v11a2 2 0 0 1-2 2z"/><polyline points="17 21 17 13 7 13 7 21"/><polyline points="7 3 7 8 15 8"/></svg> Save article`;
  }
}
```

---

## Content guidelines

**Tone.** Write the way a well-read journalist would explain this person to a smart 17-year-old.
No jargon without definition. Use concrete specifics (dates, numbers, places, names) rather than
vague generalisations. Say "270 people killed" not "many were killed." Say "1996" not "in recent years."

**Moral honesty.** Don't sanitise. If someone killed a lot of people, say so, with evidence.
If their legacy is genuinely mixed, show both sides rather than taking a position. The Legacy &
Debate section should feel like you engaged with the real historical argument, not settled it.

**Depth over breadth.** It's better to explain 5 things well than 15 things superficially. If the
user provides academic PDFs, synthesise them — don't just quote. Use the sources to build an
argument, not to tick a box.

**Prose, not bullets.** The body text of each section should be written paragraphs. The structured
components (ideology cards, legacy lists, stat rows) break things up visually — but the surrounding
prose is what gives the page its voice.

**Section length.** Origins & Rise: ~3–4 paragraphs. Each ideology card: 2–4 sentences. Each
timeline entry: 2–4 paragraphs. Legacy debate: prose + card grid. Aim for ~2,500–4,000 words total.

---

## Sources workflow

If the user uploads academic PDFs, read them and synthesise their arguments. Attribute every
significant factual claim to a numbered source with a chip (`<span class="src-chip">Author (Year)</span>`).

If no PDFs are provided, write from well-established historical knowledge, note which claims need
verification, and create a sources section citing the standard academic references for this person.
Be clear about confidence levels when working from training knowledge alone.

---

## What to do when the user asks for a person page

1. If the user hasn't specified who — ask: "Who should this page be about?"
2. Check whether the user has uploaded any source PDFs — read them before writing.
3. Write the complete HTML file using the structure and design system above.
4. Save it as `[firstname-lastname].html` in the outputs folder.
5. Present the file using the `present_files` tool so the user can open it.
6. Briefly note (1–2 sentences) what the page covers and any sections that could be improved
   with additional source material.
