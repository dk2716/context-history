# Context Style Guide - Addendum

Rules discovered during the July 2026 cleanup pass. Read this alongside CONTEXT-STYLE-GUIDE.md - these are corrections/additions, not replacements.

## 1. No dev/prototype files may ever be linked from a live page

The following filenames should never appear in an href on any live page:
context-v2.html, context-v3.html, context-v4.html, context-prototype.html, template.html, event-template.html

These are leftover scaffolding files. If a Connected Topics card seems to want one of these, the correct real filename is almost always available - check the actual site's page list before assuming a link is unfixable.

## 2. Topic card thumbnails: verified, not guessed

Every img class="topic-card-thumb" must be copied from the actual hero image src of the page it links to. This means:
- Opening the linked file directly and reading its hero image, not the value in the CONTEXT_ARTICLES thumb field (which can drift out of sync)
- Never reusing a thumbnail from a different page "because it's close enough"
- If the linked page isn't available to check, leave the thumbnail off and flag it - don't invent a URL

## 3. Search function must match the current standard

The canonical runSearch function (with thumbnail image rendering in results) lives in khalifa-haftar.html. Any page missing thumbnail rendering in its search results is running an outdated version and should have its runSearch replaced wholesale with the current one.

## 4. Quick Facts structure (person pages)

Correct format - flat, no grid wrapper: quick-facts-label followed directly by qf-item entries, with no quick-facts-grid wrapper div in between.

Incorrect (older format, still present on some pages - fix when found): quick-facts-label followed by a quick-facts-grid wrapper div, with qf-item entries nested inside that wrapper.

## 5. Image domain check applies to hero images too, not just topic cards

All images - hero images and topic card thumbnails alike - must be hosted on upload.wikimedia.org at 960px or larger. Some pages' own hero images are hosted on non-Wikimedia domains (gstatic, encrypted-tbn0, etc.) inherited from early drafts. When auditing a page for any reason, check its hero image domain too, not just its topic card thumbnails. Do not treat a gstatic hero as the "correct" reference to match against - flag it for upgrade instead.

## 6. Phantom links: remove, don't force-match

If a Connected Topics card references a topic with no real matching page, delete the card entirely rather than linking it to a loosely related page. A missing card is better than a misleading one. Log the topic in SITE-STATUS.md's planned pages list instead.

## 7. Before starting any batch edit across multiple files

Confirm the actual file list Cowork has access to matches what you intended to upload - a stale "connected folder" from an earlier session can silently override or supplement what you just attached. Ask Cowork to list every filename it can see before it starts editing anything.

## 8. Sources section citation format

Every citation in a page's Sources section must follow one consistent format, in this field order, every time:

`Author Last, First. "Title." Publisher/Journal, Year.`

Author comes first, then the title (quoted, or italicized for books - match whichever convention the citation already uses if it's internally consistent), then the publisher or journal (with volume/issue/page detail folded in as needed), then the year - and the year must be the last element, not placed in parentheses immediately after the author. Common violations found during the July 2026 pass:
- Year placed right after the author in parentheses (`Author. (Year). "Title." Journal.`) instead of at the end
- The actual title placed in the `.src-journal` span with only "Author. (Year)." left in `.src-title` - a reversed/mislabeled structure
- A title given no quotation marks or italics at all
- A citation whose "author" position is actually the publication's own name doubling as both author and publisher - acceptable for institutional/anonymous reports (e.g. Human Rights Watch, UN bodies) where the organization is the legitimate author, but do not force a real distinct author into that slot if none exists in the source material - reorder only, never invent an author, title, publisher, or year.

If a citation is missing one of the four fields entirely (no author, no year, etc.), don't guess or invent it - flag it for Dexter instead and leave the citation as-is. Multi-year primary sources (e.g. a document published across several years) and "ongoing/updated" collections don't force cleanly into a single Year field - use judgment and flag rather than fabricate a single date.

**Minimum source count:** every page should have at least 4 sources in its Sources section. Don't add placeholder sources to hit this number - flag any page below the minimum instead, for Dexter to address by adding real sources separately.
# Context Site Status

Last updated: 2026-07-03

Keep this file current after every session — Cowork sessions should read it first, and update it before finishing.

## Live pages (50 total)

**People:** 1973 Arab-Israeli War participants aside — Abdel Fattah el-Sisi, Abu Bakr al-Baghdadi, Anwar Sadat, Augusto Pinochet, Ayatollah Khomeini, Barack Obama, Bashar al-Assad, Bill Clinton, Colin Powell, Dick Cheney, Gamal Abdel Nasser, George W. Bush, Henry Kissinger, Hillary Clinton, Hugo Chávez, Joe Biden, Khalifa Haftar, Muammar Gaddafi, Osama bin Laden, Richard Nixon, Saddam Hussein, Salvador Allende, Tony Blair, Yevgeny Prigozhin

**Events:** 1973 Arab-Israeli War, Angola Civil War, Arab Spring, The Fall of the Assad Regime, Gulf War, Halabja Chemical Attack, Iran-Iraq War, Iraq War, ISIS / The Islamic State, Libyan Civil War, Northern Mali Conflict, Operation Condor, Rwandan Genocide, September 11, Suez Crisis, Syrian Civil War, Watergate

**Concepts:** Ba'athism, Democratic Socialism, Non-Aligned Movement, Pan-Arabism, Realpolitik, Resource Curse, Responsibility to Protect, Wagner Group, The War on Terror

## Session log — July 3, 2026

Built three new pages: `fall-of-assad-regime.html` (event, amber, structural template iran-iraq-war.html), `osama-bin-laden.html` (person, purple, no body class, structural template khalifa-haftar.html), `war-on-terror.html` (concept, green, structural template baathism.html). All three verified for: real hrefs only (no dev/prototype files), topic-card thumbnails copied from each linked page's actual hero image (checked by opening the linked file directly, not CONTEXT_ARTICLES thumb fields), canonical `runSearch`/`searchKeydown` copied verbatim from khalifa-haftar.html (thumbnail rendering + relevance sort both present), canonical nav/nav-actions structure, and flat `.qf-item` Quick Facts list on the bin Laden page (no grid wrapper). All hero and topic-card images are upload.wikimedia.org at 960px+.

**Not done this session (explicitly deferred):** the site-wide sync — CONTEXT_ARTICLES entries on the other 47 pre-existing pages were not updated to reference these three new pages, `index.html` was not touched, and no Connected Topics cross-links were added FROM other existing pages INTO these three. The three new pages do cross-link to each other and to pre-existing pages, but nothing pre-existing links back to them yet. This is planned as a separate follow-up session.

## Known issues / in progress

- [ ] 18 pages recovered from an old session (al-Assad, Syrian Civil War, Dick Cheney, Biden, el-Sisi, Angola, Arab Spring, Bill Clinton, Colin Powell, Halabja, Hugo Chávez, Libyan Civil War, Northern Mali, Realpolitik, Resource Curse, Rwandan Genocide, Wagner Group, Prigozhin) — still need the 3-part sync: CONTEXT_ARTICLES entries for ISIS/Baghdadi, search thumbnail rendering, Quick Facts format check
- [ ] Some pages' own hero images are hosted on gstatic/non-Wikimedia domains (e.g. Gulf War) — not yet upgraded to Wikimedia
- [x] Connected Topics audit complete on original 29 pages (broken hrefs fixed, phantom links removed, thumbnails verified against real hero images)
- [x] Stale `outputs/` folder removed from repo
- [x] Source PDFs moved to `.gitignore`d local-only `uploads/` folder

## Planned pages (priority order)

**Tier 1 — major, already referenced from multiple existing pages:**
- Cold War (concept — referenced from Kissinger, Nixon pages)
- Vietnam War (event — referenced from Nixon page)
- 1973 Chilean Coup (event, distinct from Pinochet's rule — referenced from Allende, Operation Condor)

**Tier 2 — significant, referenced once:**
- Six-Day War (referenced from Nasser)
- Camp David Accords (referenced from Sadat)
- Iran Hostage Crisis (referenced from Khomeini)
- Kosovo (referenced from Blair)
- 2008 Financial Crisis (referenced from Obama)

**Tier 3 — lower priority, conceptual/legal:**
- Velayat-e Faqih, Chicago School, Universal Jurisdiction, Enforced Disappearance, Transitional Justice, State Sovereignty, Humanitarian Intervention, Filibuster, Liberal Internationalism, The Sahel, Lockerbie Bombing, 2012 Mali Coup (possibly its own page, distinct from Northern Mali Conflict's present-day framing), Argentina's Dirty War, Argentine Junta Trial

## Rules learned the hard way (see also style guide addendum)

- Never link to `context-v2.html`, `context-v3.html`, `context-v4.html`, `template.html`, `event-template.html` — dev/prototype leftovers, not real pages
- Topic card thumbnails must be copied from the actual linked page's hero image, never guessed or copied from a CONTEXT_ARTICLES thumb field
- `runSearch` must include thumbnail rendering — copy from `khalifa-haftar.html`, don't use an older simplified version
- Quick Facts: no `.quick-facts-grid` wrapper — flat list of `.qf-item`s directly under the label
