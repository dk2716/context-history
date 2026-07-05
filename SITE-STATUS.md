# Context Site Status

Last updated: 2026-07-05 (citation standardization pass)

Keep this file current after every session — Cowork sessions should read it first, and update it before finishing.

## Session log — 2026-07-05 (later session): Sources section citation standardization

Standardized every page's Sources section to one citation format: `Author Last, First. "Title." Publisher/Journal, Year.` — see Style Guide Addendum rule 8 for the full rule (added this session).

**Scope:** all 50 content pages, 318 citations total, confirmed present before starting.

**Result: 241 citations reformatted across 41 pages; 77 citations across 9 pages were already compliant and left untouched.**

Reformatted counts per page (41 pages touched):
`abdel-fattah-el-sisi` 5, `abu-bakr-al-baghdadi` 7, `anwar-sadat` 6, `arab-spring` 6, `augusto-pinochet` 7, `ayatollah-khomeini` 6, `bashar-al-assad` 5, `bill-clinton` 5, `colin-powell` 5, `dick-cheney` 6, `fall-of-assad-regime` 6, `gaddafi` 6, `gamal-abdel-nasser` 6, `george-w-bush` 6, `gulf-war` 5, `halabja-chemical-attack` 5, `henry-kissinger` 6, `hillary-clinton` 5, `iraq-war` 3, `joe-biden` 5, `khalifa-haftar` 6, `libyan-civil-war` 8, `non-aligned-movement` 6, `obama` 7, `operation-condor` 8, `osama-bin-laden` 4, `pan-arabism` 6, `realpolitik` 5, `resource-curse` 6, `responsibility-to-protect` 7, `richard-nixon` 6, `saddam-hussein` 8, `salvador-allende` 5, `september-11` 8, `suez-crisis` 7, `syrian-civil-war` 5, `tony-blair` 5, `wagner-group` 5, `war-on-terror` 6, `watergate` 7, `yevgeny-prigozhin` 5.

**Already fully compliant (0 changes needed):** `1973-arab-israeli-war`, `angola-civil-war`, `baathism`, `democratic-socialism`, `hugo-chavez`, `iran-iraq-war`, `isis-islamic-state`, `northern-mali-conflict`, `rwandan-genocide`.

**Common violation patterns found and fixed:**
1. Year in parentheses right after the author, before the title (`Author. (Year). "Title." Journal.`) — moved to the end.
2. Title mislabeled into the `.src-journal` span with only "Author. (Year)." left in `.src-title` — swapped so the real title moved to `.src-title` in quotes, and the real publisher/journal (previously sitting as unstructured trailing text) moved into `.src-journal` with the year appended.
3. A handful of `<strong class="src-title">` citations on `joe-biden.html` that put the title first, then " — Author. Publisher, Year." in the journal span — fully rebuilt to Author → "Title." → Publisher, Year, and the tag normalized from `<strong>` to `<span>` to match every other citation on the site.
4. Institutional/self-published citations (Human Rights Watch, U.S. Dept of Defense, etc.) with an empty publisher field — publisher set to the same organization name, which is the correct, non-invented value already present as the author.

**Flagged, not touched (per the "don't guess" rule):**
- `gaddafi.html` citation 5 — Gaddafi's *The Green Book*, originally published 1975–1979 across three volumes; forcing a single Year would lose real information already in the citation.
- `operation-condor.html` citation 7 — National Security Archive collection marked "(Various years)"; an ongoing archive with no single publication year.
- `joe-biden.html` citation 6 — "Notes on the claims in this article" is a methodology/sourcing note, not a real citation to an external work; has no Author/Title/Journal/Year fields to reformat.

**Pages below the 4-source minimum:** only `iraq-war.html`, with 3 sources. Flagged per Dexter's instruction — no placeholder sources added; needs a real fourth source added separately.

**Verification performed:** re-extracted and re-counted every Sources section after editing (318 citations before and after — none lost or duplicated); div/span/strong tag-balance check on all 41 touched files' Sources sections (all balanced); Node `new Function()` syntax check across all 52 HTML files' inline scripts (zero errors); a second full-site regex sweep specifically for the `Author (YYYY).` early-year pattern inside `.src-title` spans confirmed zero remaining violations after fixes.

## Live pages (51 total: 50 content pages + index.html)

**People (24):** Abdel Fattah el-Sisi, Abu Bakr al-Baghdadi, Anwar Sadat, Augusto Pinochet, Ayatollah Khomeini, Barack Obama, Bashar al-Assad, Bill Clinton, Colin Powell, Dick Cheney, Gamal Abdel Nasser, George W. Bush, Henry Kissinger, Hillary Clinton, Hugo Chávez, Joe Biden, Khalifa Haftar, Muammar Gaddafi, Osama bin Laden, Richard Nixon, Saddam Hussein, Salvador Allende, Tony Blair, Yevgeny Prigozhin

**Events (17):** 1973 Arab-Israeli War, Angola Civil War, Arab Spring, The Fall of the Assad Regime, Gulf War, Halabja Chemical Attack, Iran-Iraq War, Iraq War, ISIS / The Islamic State, Libyan Civil War, Northern Mali Conflict, Operation Condor, Rwandan Genocide, September 11, Suez Crisis, Syrian Civil War, Watergate

**Concepts (9):** Ba'athism, Democratic Socialism, Non-Aligned Movement, Pan-Arabism, Realpolitik, Resource Curse, Responsibility to Protect, Wagner Group, The War on Terror

**Note:** `isis-islamic-state.html` is now formally included in the Events list above (resolved this session — previously flagged as missing from the written list despite being a real, live page).

## Session log — 2026-07-05: site-wide integration of the three new pages

The three pages built in the 2026-07-03 session (`fall-of-assad-regime.html`, `osama-bin-laden.html`, `war-on-terror.html`) have now been fully integrated site-wide:

1. **CONTEXT_ARTICLES entries added to all 47 pre-existing content pages plus `index.html`** (48 files touched) — each now carries all three new entries with `thumb` fields copied from each new page's actual hero image src (verified by opening each new page directly, not guessed): `fall-of-assad-regime.html` → `HTS_Rebels_coordinating_at_Hama.png`, `osama-bin-laden.html` → `Osama_bin_Laden,_portræt.jpg`, `war-on-terror.html` → `1_CEB_Clears_Rout_611_During_Operation_Outlaw_Wrath.jpg`, all at 960px Wikimedia URLs. Insertion done via a single anchored, verified-unique-per-file string replacement (`CONTEXT_ARTICLES = [`), not a full-file rewrite. The three new pages themselves were skipped (they already cross-link to each other from the prior session).
2. **`index.html` browse grid updated:** added `osama-bin-laden.html` to the People tab (alphabetically between Muammar Gaddafi and Richard Nixon), `fall-of-assad-regime.html` to the Events tab (between Arab Spring and Gulf War), `war-on-terror.html` to the Concepts tab (after Wagner Group, last alphabetically). Category counts in the hero tagline updated 23/16/8 → 24/17/9. `entry-card-thumb` images added for all three using the same verified hero-image URLs. `homeRunSearch` required no direct code change — it already reads from `CONTEXT_ARTICLES`, which now includes all three entries.
3. **Connected Topics cards added** (all targets confirmed to exist on disk before linking):
   - `bashar-al-assad.html` ↔ `fall-of-assad-regime.html` (added to "The Syrian Crisis" group)
   - `syrian-civil-war.html` ↔ `fall-of-assad-regime.html` (added to "Related Events & Concepts" group)
   - `september-11.html` ↔ `osama-bin-laden.html` (added to "People at the centre of the response") and ↔ `war-on-terror.html` (added to "Events that followed directly")
   - `isis-islamic-state.html` ↔ `osama-bin-laden.html` (added to "People at the centre of this event")
   - `abu-bakr-al-baghdadi.html` ↔ `osama-bin-laden.html` (added to "People directly connected")
   - `george-w-bush.html` ↔ `war-on-terror.html` (added to "Events")
   - `iraq-war.html` ↔ `war-on-terror.html` (added to "Related Events")
   All cards use each page's existing markup pattern (some pages use `topic-card-thumb-wrap` div wrapper, others put the `<img>` directly inside the `<a>` — matched per-file rather than forcing one style) and real hero-image thumbnails, not guessed URLs.
4. **Verification performed:** Node `new Function()` syntax check across all 51 HTML files' inline `<script>` blocks (zero errors); div-tag balance check on all 8 directly-edited files (all balanced); confirmed each new page is now referenced exactly 51 times site-wide (48 newly-touched files + the 3 new pages' pre-existing mutual self-references); confirmed no dev/prototype filenames (`context-v2/v3/v4.html`, `template.html`, `event-template.html`) were introduced into any live page (the only match was `template.html`'s own pre-existing, untouched internal scaffold links).

**Not done / out of scope this session:** no new pages were built, no hero images were changed, the 13 non-Wikimedia hero images flagged in the prior session remain unresolved (still blocked on verified Commons URLs from Dexter), and the pre-existing duplicate "The Iraq War" entry inside `khalifa-haftar.html`'s `CONTEXT_ARTICLES` array (two near-identical entries, lines ~481–482 in the pre-session file) was noticed but left alone as out of scope for this pass — flagging it below.

## Session log — 2026-07-03 (later session): three new pages built

Built and verified three new pages per Dexter's spec:
- `fall-of-assad-regime.html` — event, amber, `class="event-page"`, structural template `iran-iraq-war.html`. Covers the December 2024 collapse of the Assad regime: the 11-day military collapse, geopolitical winners/losers (Iran, Russia, Israel, Turkiye, U.S., Gulf states), and HTS's post-takeover "radicals' dilemma."
- `osama-bin-laden.html` — person, purple, no body class, structural template `khalifa-haftar.html`. Covers his radicalization, al-Qaeda's ideology, key attacks, the Abbottabad raid, and the empirical evidence that his killing did not produce a global deterrent effect on terrorism.
- `war-on-terror.html` — concept, green, `class="concept-page"`, structural template `baathism.html`. Covers the Bush Doctrine, the just-war case for Afghanistan vs. Iraq, domestic threat-perception psychology, the "victory trap," and the al-Qaeda-to-ISIS ideological comparison. Deliberately kept at the doctrinal level per Dexter's instruction, since dedicated Iraq War and (future) Afghanistan pages exist separately.

Verification performed before sign-off: every href checked against the actual file list on disk (no `context-v2/v3/v4.html`, `template.html`, or `event-template.html`); every topic-card thumbnail copied from the actual linked page's real hero image (checked by opening each linked file directly — `bashar-al-assad.html`, `syrian-civil-war.html`, `iraq-war.html`, `isis-islamic-state.html`, `september-11.html`, `george-w-bush.html`, `abu-bakr-al-baghdadi.html`, `dick-cheney.html`, `colin-powell.html`, `obama.html`, `baathism.html` — rather than trusting any CONTEXT_ARTICLES thumb field); `runSearch`/`searchKeydown` copied verbatim from `khalifa-haftar.html` (thumbnail rendering + relevance sort both present, confirmed via grep); nav uses the canonical `nav`/`nav-actions` structure; bin Laden's Quick Facts use a flat `.qf-item` list with no `.quick-facts-grid` wrapper; all images are `upload.wikimedia.org` at 960px+; div-tag balance and internal link resolution checked programmatically.

**Explicitly not done this session (deferred to a follow-up):** no CONTEXT_ARTICLES entries were added to the other 48 pre-existing pages, `index.html` was not touched, and no Connected Topics cards were added FROM pre-existing pages INTO these three new ones. The three new pages cross-link to each other and to pre-existing pages, but nothing pre-existing links back yet — a site-wide sync pass is needed in a separate session.

**Update 2026-07-05: this deferred sync pass is now complete — see the session log above.**

## Completed this session (2026-07-03)

- [x] Item 1 — four diagnosed fixes applied: el-Sisi nav structure (old `nav.nav`/`nav-right` → canonical `nav`/`nav-actions`), Biden's `runSearch` replaced wholesale with thumbnail-rendering version, Ba'athism hero image swapped to the verified Wikimedia flag graphic (`object-fit:contain` + dark background, since it's a flag not a photo), Realpolitik's Bismarck hero given `object-position:top` to stop cropping his head.
- [x] Item 2 — site-wide nav audit: found **21 pages** still running the old `nav.nav`/`nav-right` structure (beyond el-Sisi): `1973-arab-israeli-war`, `angola-civil-war`, `arab-spring`, `baathism`, `bill-clinton`, `democratic-socialism`, `gulf-war`, `halabja-chemical-attack`, `hillary-clinton`, `hugo-chavez`, `iran-iraq-war`, `iraq-war`, `isis-islamic-state`, `northern-mali-conflict`, `pan-arabism`, `realpolitik`, `resource-curse`, `rwandan-genocide`, `september-11`, `suez-crisis`, `watergate`. All 21 rewritten to the canonical `khalifa-haftar.html` nav structure (topic-type text preserved per page).
  - Side effect caught and fixed: rewriting the nav hardcoded `onkeydown="searchKeydown(event)"`, but 7 of those pages (`1973-arab-israeli-war`, `baathism`, `democratic-socialism`, `iran-iraq-war`, `iraq-war`, `isis-islamic-state`, `realpolitik`) had their keyboard handler defined as `function searchKey(e)` instead of `searchKeydown`. Renamed the function in all 7 so keyboard nav in search doesn't silently break. Verified with a Node syntax check across all 48 pages afterward.
- [x] Item 3 — site-wide `runSearch` audit: all pages already had thumbnail rendering (`a.thumb`) except Biden (fixed in item 1). However, comparing against the *full* canonical function (thumbnail + relevance sort) turned up **9 more pages** running an intermediate version (dedup logic, no relevance sort): `abdel-fattah-el-sisi`, `angola-civil-war`, `arab-spring`, `bill-clinton`, `halabja-chemical-attack`, `hugo-chavez`, `northern-mali-conflict`, `realpolitik`, `resource-curse`. Replaced wholesale with the exact `khalifa-haftar.html` version. Confirmed no JS syntax errors site-wide after the change.
- [x] Item 4 (partial) — hero image upgrades:
  - 5 "wrong size" Wikimedia pages converted from full-resolution originals to the standard `/thumb/.../960px-` pattern: `augusto-pinochet`, `henry-kissinger`, `richard-nixon`, `saddam-hussein`, `salvador-allende`. This is a same-file URL transform (not a new image), applied globally — the same 5 people's `thumb` fields inside every page's `CONTEXT_ARTICLES` search index were updated too (48 files touched total).
  - 13 non-Wikimedia hero images **not yet replaced** — flagged, not fixed, at Dexter's request. This Cowork sandbox cannot fetch `wikimedia.org`/`commons.wikimedia.org` (fetches return empty with no error), so any hash-prefixed `upload.wikimedia.org` URL I constructed could not be verified and risked a silent 404. Rather than guess, candidates found via web search are listed below for Dexter to confirm and drop in:
    - `1973-arab-israeli-war.html` (currently mwi.westpoint.edu) — subject is the Yom Kippur/October War; Commons category `Category:Yom_Kippur_War` has usable combat photos, no single obvious infobox file identified.
    - `iran-iraq-war.html` (currently atlanticcouncil.org) — no strong single candidate found; Commons has scattered war photos under Iran-Iraq War categories.
    - `watergate.html` (gstatic) — Commons `Category:Watergate_scandal` has hearing photos (e.g. "House Banking Committee hearing on Watergate Incident.jpg"); Library of Congress also holds 1973 hearing photos that may be mirrored on Commons.
    - `gulf-war.html` (gstatic) — candidate: `File:Gulf War Photobox.jpg` (composite image already used as the Wikipedia infobox for Gulf War).
    - `iraq-war.html` (gstatic) — no single strong infobox candidate found; Commons has a `Category:Iraq_War` with many individual photos, no widely-used single montage confirmed.
    - `september-11.html` (gstatic) — Commons has `Category:September_11_attacks_at_the_World_Trade_Center`; no single confirmed infobox file identified this session.
    - `suez-crisis.html` (gstatic) — candidate imagery: the sunken blockships at Port Said (widely reproduced), but no confirmed exact Commons filename found this session.
    - `tony-blair.html` (gstatic, on the person's own hero/avatar) — candidate: `File:Tony_Blair_Downing_Street_portrait.jpg`.
    - `non-aligned-movement.html` (gstatic) — subject is the 1961 Belgrade founders (Tito, Nasser, Nehru, Nkrumah, Sukarno); no single confirmed group photo filename found this session.
    - `operation-condor.html` (gstatic) — no single strong candidate found; would need a Pinochet/Videla-era joint photo from Commons.
    - `pan-arabism.html` (gstatic) — not researched this session, still needs a candidate.
    - `responsibility-to-protect.html` (gstatic) — subject is the 2005 World Summit; not researched further, still needs a candidate.
    - `democratic-socialism.html` (gstatic) — not researched this session, still needs a candidate.
  - **Action for Dexter:** confirm/find the exact `upload.wikimedia.org/wikipedia/commons/.../960px-...` URL for each of the 13 above and paste them back in; I'll drop them in directly with `str_replace` once verified links are available (also need to re-check Connected Topics cards elsewhere that reference these 13 pages' thumbnails once their heroes change, per Style Guide rule 2).
  - Also noticed in passing (not yet actioned): `gaddafi.html`'s Connected Topics card linking to `responsibility-to-protect.html` still uses a gstatic thumbnail — will need updating once that page's hero is fixed.
- [x] Item 5 — re-confirmed the 5 phantom Connected Topics cards (`href="#"`) are still the only ones site-wide: "The 2012 Mali Coup" and "The Sahel" (both on `libyan-civil-war.html`; `gaddafi.html` does NOT currently have phantom cards for these, contrary to the prior note — it already links out correctly), "Universal Jurisdiction" (on `operation-condor.html` and `responsibility-to-protect.html` separately), "Weapons of Mass Destruction" (on `saddam-hussein.html`). No new phantoms introduced by this session's edits. All 5 still map to Tier 2/3 planned pages below.

## Known issues / in progress

- [ ] 13 hero images still on non-Wikimedia domains — see candidate list above, blocked on verified URLs
- [x] `isis-islamic-state.html` formally added to the live-pages list — resolved 2026-07-05
- [x] The 18-page "recovered from old session" nav/search sync — resolved this session (see above)
- [x] Connected Topics audit complete on original 29 pages (broken hrefs fixed, phantom links removed, thumbnails verified against real hero images)
- [x] Stale `outputs/` folder removed from repo
- [x] Source PDFs moved to `.gitignore`d local-only `uploads/` folder
- [x] Site-wide integration of `fall-of-assad-regime.html`, `osama-bin-laden.html`, `war-on-terror.html` (CONTEXT_ARTICLES, index.html, Connected Topics) — resolved 2026-07-05
- [ ] `khalifa-haftar.html` has a pre-existing duplicate "The Iraq War" entry in its `CONTEXT_ARTICLES` array (two near-identical objects) — noticed 2026-07-05, not fixed, out of scope for that session
- [ ] `STYLE-GUIDE-ADDENDUM.md` appears to have an old, stale copy of `SITE-STATUS.md` (dated content, pre-July-3 session, "50 total" page count) appended after its own rule #7 — looks like an accidental paste, not intentional content; flagged 2026-07-05, not cleaned up
- [x] Sources section citation format standardized site-wide — resolved 2026-07-05 (later session), see session log above
- [ ] `iraq-war.html` has only 3 sources, below the new 4-source minimum (Style Guide Addendum rule 8) — flagged 2026-07-05, needs a real fourth source added
- [ ] Three citations flagged during the citation-standardization pass rather than force-fit to the new format: `gaddafi.html` (Green Book, multi-year primary source), `operation-condor.html` (National Security Archive, "Various years"), `joe-biden.html` (a methodology note, not a real citation) — see session log above for detail

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
- `runSearch` must include thumbnail rendering AND relevance sorting — copy from `khalifa-haftar.html` in full, don't assume thumbnail rendering alone means a page is current (9 pages this session had thumbnails but were missing the sort logic)
- Quick Facts: no `.quick-facts-grid` wrapper — flat list of `.qf-item`s directly under the label
- When bulk-replacing the nav block, check that the `onkeydown` handler name in the new nav matches a function actually defined on that page — some older pages named it `searchKey` instead of `searchKeydown`, and a blind nav swap will silently break keyboard navigation in search
- This Cowork sandbox cannot fetch `wikimedia.org` / `commons.wikimedia.org` (empty response, no error) — don't attempt to construct hash-prefixed `upload.wikimedia.org` URLs from memory for pages not already using them; verify first or ask for the URL directly
- Sources section citations: Author → "Title." → Publisher/Journal → Year, in that order, every time — see Style Guide Addendum rule 8. When a citation's title has been mislabeled into the wrong span (title text sitting in `.src-journal` while `.src-title` holds only "Author. (Year)."), the fix is a full swap, not just a reorder — check which span actually holds the title text before assuming a simple find-and-replace will work
- Institutional/anonymous citations where the author name and the publisher name are the same organization (Human Rights Watch, UN bodies, government agencies) are legitimate, not errors — don't flag or "fix" these by inventing a distinct human author
