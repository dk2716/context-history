# Context Site Status

Last updated: 2026-07-03

Keep this file current after every session — Cowork sessions should read it first, and update it before finishing.

## Live pages (48 total — see note below)

**People:** Abdel Fattah el-Sisi, Abu Bakr al-Baghdadi, Anwar Sadat, Augusto Pinochet, Ayatollah Khomeini, Barack Obama, Bashar al-Assad, Bill Clinton, Colin Powell, Dick Cheney, Gamal Abdel Nasser, George W. Bush, Henry Kissinger, Hillary Clinton, Hugo Chávez, Joe Biden, Khalifa Haftar, Muammar Gaddafi, Richard Nixon, Saddam Hussein, Salvador Allende, Tony Blair, Yevgeny Prigozhin

**Events:** 1973 Arab-Israeli War, Angola Civil War, Arab Spring, Gulf War, Halabja Chemical Attack, Iran-Iraq War, Iraq War, Libyan Civil War, Northern Mali Conflict, Operation Condor, Rwandan Genocide, September 11, Suez Crisis, Syrian Civil War, Watergate

**Concepts:** Ba'athism, Democratic Socialism, Non-Aligned Movement, Pan-Arabism, Realpolitik, Resource Curse, Responsibility to Protect, Wagner Group

**Note:** `isis-islamic-state.html` exists on disk and is a real, working page (linked from Baghdadi's CONTEXT_ARTICLES entry), but it was never added to this list — bringing the true live-page count to 48, not 47. Add "ISIS / The Islamic State" to the Events list above once confirmed intentional; flagged this session, not yet resolved.

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
- [ ] `isis-islamic-state.html` needs to be formally added to the live-pages list (or confirmed as intentionally excluded)
- [x] The 18-page "recovered from old session" nav/search sync — resolved this session (see above)
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
- `runSearch` must include thumbnail rendering AND relevance sorting — copy from `khalifa-haftar.html` in full, don't assume thumbnail rendering alone means a page is current (9 pages this session had thumbnails but were missing the sort logic)
- Quick Facts: no `.quick-facts-grid` wrapper — flat list of `.qf-item`s directly under the label
- When bulk-replacing the nav block, check that the `onkeydown` handler name in the new nav matches a function actually defined on that page — some older pages named it `searchKey` instead of `searchKeydown`, and a blind nav swap will silently break keyboard navigation in search
- This Cowork sandbox cannot fetch `wikimedia.org` / `commons.wikimedia.org` (empty response, no error) — don't attempt to construct hash-prefixed `upload.wikimedia.org` URLs from memory for pages not already using them; verify first or ask for the URL directly
