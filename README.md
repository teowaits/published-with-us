# Published With Us Yet?

Single-file HTML tool for editorial workflows: given a CSV of authors (with **OpenAlex author IDs**), check who has already published in a **target journal** within a **publication-year window**, who has not, and export either group while **preserving every original CSV column**.

Sibling to [journal-overlap](https://github.com/teowaits/journal-overlap) and [journal-profiler](https://github.com/teowaits/journal-profiler). Data from the [OpenAlex](https://openalex.org) API (CC0).

**Current file:** `published-with-us.html` (v0.2) — no build step, no dependencies.

---

## Quick start

1. Clone or download this folder.
2. Open `published-with-us.html` in a modern desktop browser (Chrome, Firefox, Safari, Edge).
3. Upload a CSV that includes an **OpenAlex ID** column (header matching `OpenAlex ID` or similar).
4. Choose the target journal via **search** or use a **preset** pill (instant, no API).
5. Set the publication window and click **Check authors**.
6. Use **Export CSV** on either results panel; exports use the **same headers and column order** as your upload.

For static hosting (e.g. GitHub Pages), publish the repo root or this folder and link to `published-with-us.html`.

---

## Features

| Area | Behaviour |
|------|-----------|
| **Journal selection** | Live search against OpenAlex `/sources` (journals only), or hardcoded presets for *Advanced Intelligent Systems* and *Advanced Intelligent Discovery*. |
| **Checks** | One OpenAlex `/works` query per author for publications in the chosen source and year range; `sort=publication_year:desc` so the on-card sample is the **newest** match in-window. |
| **New prospects** | After the main pass, optional second pass: latest work **anywhere** (one request per new prospect), shown as a **Latest:** line with journal and year. |
| **UX** | Dark UI (IBM Plex), two glass result panels, progress log, **Cancel** via `AbortController` (cancelling during the second pass skips rendering that run). |
| **CSV** | Exports are row subsets of the original file only — **no extra columns**, full fidelity for downstream tools. |

---

## CSV requirements

- UTF-8 text CSV with a header row.
- At least one column that resolves to an OpenAlex author ID (values like `A1234567890`). Recognised header names include **`OpenAlex ID`** and flexible variants containing “openalex” and “id”.
- Other columns (name, institution, citations, ORCID, etc.) are optional for the check but are **kept on export**.

---

## OpenAlex usage

- **Base URL:** `https://api.openalex.org`
- Requests append `mailto=editorial-tools@placeholder.org` (polite pool). Replace with your team’s address if you fork the tool.
- The script waits **80 ms** between requests (`DELAY_MS`) to stay within reasonable client-side rate limits.

---

## Project layout

| Path | Purpose |
|------|---------|
| `published-with-us.html` | The entire app (markup, styles, script). |
| `CLAUDE.md` | Maintainer context: tokens, API notes, architecture, **changelog**, testing checklist. |
| `authors-overlap.csv` | Sample input (when present) for manual QA. |

---

## Changelog (high level)

See **`CLAUDE.md`** for the full **Changelog** (v0.1 baseline → **v0.2**: title/layout, instant presets, card enrichment, second-pass “latest work”, OpenAlex `select` notes).

---

## License

MIT License — see repository footer in `published-with-us.html` and attribution to **teowaits**.

When this repo goes public on GitHub, add a root `LICENSE` file if you want the standard GitHub license badge (text can match MIT).
