# Outstanding Fixes

This file did not previously exist in the repo — created 2026-07-06 to give the batch-page sessions (Putin, Soleimani, Mubarak, War in Afghanistan 2001–2021, Withdrawal from Afghanistan 2021, Egyptian Revolution 2011, Regime Change) a dedicated punch-list separate from SITE-STATUS.md's session log. Seeded from SITE-STATUS.md's existing "Known issues / in progress" section plus items flagged during the current 7-page batch. Keep this file current alongside SITE-STATUS.md — update it whenever an item is resolved or a new one is found.

## Sync session required once remaining batch pages are built

The three pages built earlier in this batch (`vladimir-putin.html`, `war-in-afghanistan-2001-2021.html`, `withdrawal-from-afghanistan-2021.html`) were fully synced site-wide on 2026-07-06 — see SITE-STATUS.md's session log for full detail. Resolved this pass:

- [x] CONTEXT_ARTICLES entries for all 3 new pages added to all 50 pre-existing content pages plus `index.html` — resolved 2026-07-06
- [x] `index.html` browse grid cards + category count update (24/17/9 → 25/19/9) — resolved 2026-07-06
- [x] Cross-link from `war-in-afghanistan-2001-2021.html` to `withdrawal-from-afghanistan-2021.html` — resolved 2026-07-06 (done in the content session once the target page existed)
- [x] `joe-biden.html` → `withdrawal-from-afghanistan-2021.html` Connected Topics card — resolved 2026-07-06
- [x] `george-w-bush.html` → `war-in-afghanistan-2001-2021.html` Connected Topics card — resolved 2026-07-06
- [x] `fall-of-assad-regime.html` → `withdrawal-from-afghanistan-2021.html` Connected Topics card — resolved 2026-07-06

**Newly discovered this sync session:**
- [ ] `wagner-group.html` and `yevgeny-prigozhin.html` still don't have inbound Connected Topics cards pointing to `vladimir-putin.html` — both discuss Putin's regime at length. Deliberately not added mechanically this session (writing a good preview sentence is a content judgment call, not a sync task) — flag for the next content-judgment session.
- [ ] `osama-bin-laden.html`, `september-11.html`, and `war-on-terror.html` also don't yet have inbound Connected Topics cards pointing to `war-in-afghanistan-2001-2021.html`, despite all discussing related material — same reasoning, deferred to a content session rather than force-added mechanically.
- [ ] Process note: when delegating bulk mechanical file edits to subagents, verify their self-reported results programmatically before trusting them. One subagent in this session reported "4 files already had the entry, skipped as duplicate" for a task with only 1 logged tool call — actually those 4 files (`obama.html`, `syrian-civil-war.html`, `wagner-group.html`, `yevgeny-prigozhin.html`) were simply missing the entry, not duplicates. Caught and fixed via an independent grep-based audit; site-wide href/div/JS sweep afterward confirmed all 54 non-template pages are clean.

## Remaining batch pages not yet built

- [ ] Soleimani, Mubarak, Egyptian Revolution 2011, Regime Change — once built, add to a dedicated sync pass rather than doing separate syncs. `withdrawal-from-afghanistan-2021.html` in particular is a strong candidate for a Connected Topics link FROM the future Regime Change concept page once it exists.

## Carried over from SITE-STATUS.md

- [ ] 13 hero images still on non-Wikimedia domains (gstatic, encrypted-tbn0) — candidate Commons filenames identified for most but unverified; see SITE-STATUS.md session log from 2026-07-03 for the full per-page candidate list. Affected: `1973-arab-israeli-war.html`, `iran-iraq-war.html`, `watergate.html`, `gulf-war.html`, `iraq-war.html`, `september-11.html`, `suez-crisis.html`, `tony-blair.html`, `non-aligned-movement.html`, `operation-condor.html`, `pan-arabism.html`, `responsibility-to-protect.html`, `democratic-socialism.html`
- [ ] `khalifa-haftar.html` has a pre-existing duplicate "The Iraq War" entry in its `CONTEXT_ARTICLES` array (two near-identical objects, noticed 2026-07-05, not yet fixed)
- [ ] Three citations flagged during the July 2026 citation-standardization pass, not force-fit to the standard format: `gaddafi.html` (Green Book, multi-year primary source), `operation-condor.html` (National Security Archive, "Various years"), `joe-biden.html` (a methodology note, not a real citation)
- [ ] 5 phantom Connected Topics cards (`href="#"`) still unresolved, all mapped to planned Tier 2/3 pages: "The 2012 Mali Coup" and "The Sahel" (both on `libyan-civil-war.html`), "Universal Jurisdiction" (on `operation-condor.html` and `responsibility-to-protect.html` separately), "Weapons of Mass Destruction" (on `saddam-hussein.html`)
- [ ] `gaddafi.html`'s Connected Topics card linking to `responsibility-to-protect.html` still uses a gstatic thumbnail — needs updating once that page's hero image is fixed
