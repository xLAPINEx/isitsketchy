---
name: isitsketchy
description: Research whether a metal artist has Nazi ties, promotes NS ideology, or is considered sketchy/unsafe to support. Searches Metal Archives, Reddit r/isitsketch and r/rabm, community spreadsheets, and interviews.
---

## ! Tool Dependencies !
This skill uses these tools in order of preference:

1. firecrawl — PRIMARY TOOL for all web search, scraping, and crawling.
   - Use this for structured data, blocked sites (Reddit, LinkedIn), and deep research.
   - Firecrawl handles JavaScript rendering automatically; do NOT attempt to install a browser.

2. bash with curl -sL — for quick, direct URL fetching.
   - Use only for simple text sites or APIs where Firecrawl is overkill.

---
CRITICAL CONSTRAINTS:
- BROWSERS: browser_navigate is DEPRECATED and UNAVAILABLE. 
- INSTALLATION: Do not use npm, pip, or apt. You are in a restricted read-only environment.
- REDDIT/METAL-ARCHIVES: Use firecrawl exclusively. Do not attempt curl retries if Firecrawl is available.
- ERROR HANDLING: If a tool fails, do not troubleshoot the environment. State the limitation and provide the best possible answer with available data.

# IsItSketchy — Nazi/NSBM Research Skill

You are researching whether **{{ARTIST}}** has Nazi ties, promotes National Socialist ideology, or is considered "sketch" (unsafe to support) in the metal community.

If no artist or band name was provided, ask the user before proceeding.

## Sources to Search

Work through all sources below. Use available web tools for queries and fetch URLs directly where needed.

---

### 1. Metal Archives (Encyclopaedia Metallum)

Metal Archives blocks direct fetches intermittently (403). Use this three-step approach:

**Step 1 — Find the band page URL:**

```
site:metal-archives.com "<ARTIST>"
```
*If `web_search` is unavailable, use `browser_navigate` to google.com and manually search `site:metal-archives.com "<ARTIST>"`, then parse the search results via `browser_snapshot`.*

This surfaces the band page URL (e.g. `https://www.metal-archives.com/bands/Artist_Name/12345`) along with genre, country, and label snippets from Google's index.

**Step 2 — Fetch the band page directly (up to 3 retries):**

Use the URL from step 1 and attempt to fetch it. If it returns 403, retry up to two more times before giving up. The block is intermittent and a retry often succeeds.
*If `curl` continues to be blocked (403), fall back to `browser_navigate` to the Metal Archives URL.*

**Step 3 — Fall back to search snippets:**

If all three `curl` attempts return 403 and `browser_navigate` is also blocked or unavailable, rely on the search snippets from step 1. They typically surface genre, country, label, and member info without needing the live page.

Look for:
- Genre tags containing "NSBM" or "National Socialist Black Metal"
- Band description or notes mentioning ideology
- Member profiles — check if any members have bands tagged as NSBM
- Label associations (see known NSBM labels below and the Labels sheet in source 4)
- Comments section (often contains community warnings)

---

### 2. Reddit r/isitsketch

Search query: `site:reddit.com/r/isitsketch "<ARTIST>"`

*Note: `curl` requests to Reddit are often blocked. Prefer `browser_navigate` for Reddit pages. Navigate to `https://www.reddit.com/r/isitsketch/search?q=<ARTIST>&restrict_sr=1` directly if `web_search` is unavailable or blocked, then use `browser_snapshot(full=true)` to get the page content.*

This subreddit is dedicated to exactly this question. Threads here are high-signal.
Look for: confirmed reports, receipts (screenshots, lyrics quotes), community verdicts.

---

### 3. Reddit r/rabm (Red and Anarchist Black Metal)

Search query: `site:reddit.com/r/rabm "<ARTIST>"`

*Note: `curl` requests to Reddit are often blocked. Prefer `browser_navigate` for Reddit pages. Navigate to `https://www.reddit.com/r/rabm/search?q=<ARTIST>&restrict_sr=1` directly if `web_search` is unavailable or blocked, then use `browser_snapshot(full=true)` to get the page content.*

The RABM community actively monitors and calls out NSBM. Very reliable source.
Look for: callout posts, pinned warnings, discussions.

---

### 4. Black Metal Sketch List — Google Sheets (community spreadsheet)

A comprehensive community-curated spreadsheet with three tabs.

**Do NOT use WebFetch for these URLs.** Google Sheets CSV exports issue a time-limited cross-domain redirect (`307 → googleusercontent.com`). WebFetch cannot follow cross-domain redirects inline, and the token in the redirect URL expires before a second request can be made (returns 400). Use **Bash with `curl -sL`** instead — it follows the entire redirect chain in a single HTTP session.
*If `curl` is blocked for these URLs, you may need to manually access and copy the content, or adjust the URL if a direct CSV download is available without redirects that cause issues.*

To search a tab, run:
```bash
curl -sL "<CSV_URL>" | grep -i "<ARTIST>"
```

#### Tab 1 — Black Metal bands

CSV export URL: `https://docs.google.com/spreadsheets/d/e/2PACX-1vSfnVZGsyxn5eEacXKJZk3-_ql3bQAkPqzdc8p3fCdxtPS9BtvNlj0yjskUQyy3eDYBL9yYTqbba_5q/pub?output=csv`

Columns: `Artist | Country | Classification | Explanation`

Classification is color-coded in the original sheet:
- 🔴 **NAZI** — Pro-fascist, far-right content, or proven fascists
- 🟠 **SKETCH** — Evidence suggesting far-right but no definitive proof
- 🟡 **QUESTIONABLE** — Debatable, shifted over time, or otherwise worth noting
- 🟢 **SAFE** — Nothing sketchy found
- *(no color)* **UNKNOWN** — Politics and views not researched

Search the CSV for the artist name and report the classification and explanation.

#### Tab 2 — Other genres

CSV export URL: `https://docs.google.com/spreadsheets/d/e/2PACX-1vSfnVZGsyxn5eEacXKJZk3-_ql3bQAkPqzdc8p3fCdxtPS9BtvNlj0yjskUQyy3eDYBL9yYTqbba_5q/pub?output=csv&gid=846668971`

Same structure. Covers metal-adjacent and non-metal genres.

#### Tab 3 — Record Labels

CSV export URL: `https://docs.google.com/spreadsheets/d/e/2PACX-1vSfnVZGsyxn5eEacXKJZk3-_ql3bQAkPqzdc8p3fCdxtPS9BtvNlj0yjskUQyy3eDYBL9yYTqbba_5q/pub?output=csv&gid=867923480`

Cross-reference the band's label against this list. A label appearing here is a significant red flag even if the band itself is not listed.

---

### 5. Band interviews (fact-checking)

Search for interviews, then fetch and read the actual interview page. **Always cite the primary source — the interview itself — not a Reddit post or community list that references it.**

Search queries:
- `"<ARTIST>" interview politics ideology`
- `"<ARTIST>" interview "national socialist" OR "white power" OR "fascist"`
- `"<ARTIST>" interview OR statement race nazi`
- `"<ARTIST>" interview site: bardomethodology.com OR site:heavymetalcitadel.com OR site:blackmetalzine.com OR site:blacforjemagazine.com OR site:nocleansinging.com OR site:metalwani.com OR site:ncs.fm OR site:blabbermouth.net OR site:metalsucks.net OR site:revolvermag.com OR site:kerrang.com`
*If `web_search` is unavailable, use `browser_navigate` to google.com and manually search these queries, then navigate to promising results.*

For each promising result:
1. Fetch the interview URL using `bash` with `curl -sL "<URL>" | sed "s/<[^>]*>//g" | head -300` to read as plain text. Only fall back to browser_navigate if curl returns empty content or a login wall
2. Find the relevant quote directly in the article
3. Cite it as: `[Publication, Year] "[direct quote]" — [URL]`

Look for:
- Direct statements about race, politics, ideology, or nationalism
- Expressions of sympathy for NS or fascist movements
- Denunciations of racism (clears a band from ambiguous imagery)
- Context for controversial lyrics or imagery the band has been asked to explain

If an interview is behind a paywall or unavailable, note that in the verdict and fall back to the next best available source.

---

### 6. General web search

- Query: `"<ARTIST>" NSBM nazi "national socialist"`
- Query: `"<ARTIST>" sketch racist white supremacist`
*If `web_search` is unavailable, use `browser_navigate` to google.com and manually search these queries.*

Look for: news coverage, scene commentary, label affiliations, lyrics analysis.

---

## Research Workflow

1. **Address browser setup (if needed)**: If `browser_navigate` or `web_search` tools are initially unavailable, prioritize setting up or troubleshooting the browser, as these are critical for comprehensive research. This may involve installing Chrome or debugging `agent-browser`.

2. **Identify the artist** — confirm spelling, country of origin, genre. If ambiguous, ask the user to clarify.

3. **Check the community spreadsheets (source 4)** — fetch all three tabs and search for the artist and their label. Note classification and explanation.

4. **Search Metal Archives (source 1)** — fetch the band page, note genre, label, members, any flags.

5. **Search r/isitsketch (source 2)** — look for existing threads.

6. **Search r/rabm (source 3)** — look for callout posts or discussions.

7. **Find and read interviews (source 5)** — search for interviews where members discuss politics or have been asked about controversial imagery. Use these to fact-check or confirm claims from the lists above.

8. **General web search (source 6)** — catch anything missed.

9. **Cross-reference members** — if the main band is clean, check whether members have side projects or past bands flagged as NSBM.

---

## Verdict Format

After completing research, deliver a structured verdict:

```
## IsItSketchy: [ARTIST NAME]

**Verdict:** ✅ CLEAN / ⚠️ SKETCHY / 🚨 NAZI / ❓ INCONCLUSIVE

**Confidence:** High / Medium / Low

### Evidence Found
- [source]: [what was found]

### Red Flags
- (list specific red flags, or "None found")

### Member/Label Connections
- (note if members have NSBM projects, or if the label appears on the Labels sheet)

### Community Consensus
- (what r/isitsketch, r/rabm, and the community spreadsheets say)

### Interview Evidence
- (direct quotes or paraphrases from interviews; note source and year)

### Bottom Line
[2-3 sentence summary. Be direct. If sketchy — say so clearly.]
```

## Verdict Definitions

- ✅ **CLEAN** — No credible evidence of Nazi ties. Community has no warnings. Interviews confirm anti-fascist or neutral stance.
- ⚠️ **SKETCHY** — Some red flags but not definitive (e.g. played with NSBM bands, on a grey-area label, ambiguous lyrics, members with problematic history, listed as SKETCH in community sheets).
- 🚨 **NAZI** — Confirmed NSBM. Tagged on Metal Archives, listed as NAZI in community sheets, explicit statements in interviews, or strong community consensus.
- ❓ **INCONCLUSIVE** — Insufficient information found. Note what was searched and what gaps remain.

## Known NSBM-Associated Labels (quick reference)

The Labels tab of the community spreadsheet (source 4, Tab 3) is the authoritative list. Quick reference for common cases:

- Darker Than Black Records
- Nebelfee Klangwerge
- W.A.R. Productions
- Oskorei Production
- Blood & Iron Records
- Nordwind Productions
- Purity Through Fire (grey area — many NSBM releases)
- Werewolf Records (Satanic Warmaster's label — not explicitly NS but known associations)

## Known NSBM Acts (for cross-referencing members)

If a band member has past or present involvement with these, flag it:

- Burzum (Varg Vikernes — convicted racist)
- Absurd (Germany)
- Goatmoon (Finland — grey area, contested)
- Nokturnal Mortum (Ukraine — early releases NSBM, later claimed to distance)
- Drudkh (members overlap with Hate Forest / related to NS scene — contested)
- Grand Belial's Key (US)
- Peste Noire (France — La sale famine de Valfunde's statements)
- Graveland (Poland — Darken's public statements)
- Leichenmei (Germany)

> Grey-area bands should be mentioned but not treated as definitive proof.

## Important Notes

- **Lyrics alone are not proof** — black metal uses dark imagery. Look for explicit NS ideology, not just darkness or paganism.
- **Paganism ≠ Nazism** — heathenry and folk themes alone are not a red flag.
- **Community lists are semi-reliable** — the spreadsheets are community-maintained and may contain errors. Always cross-reference with Metal Archives and interviews before treating a listing as definitive.
- **Be specific with evidence** — quote sources, link threads, cite interviews with year and publication. Do not make unsupported claims.
- **When uncertain, say so** — an inconclusive verdict with clear reasoning is better than a false one.
- **The goal is informed decisions** — help people decide which artists to support financially.

## Pitfalls
- **Missing Browser Tools / Blocked `web_search`**: If `web_search` is unavailable or `browser_navigate` fails due to a missing browser, this skill will be severely limited. Prioritize troubleshooting browser setup (e.g., installing Chrome if recommended by the environment). If a browser cannot be set up, web research will be highly constrained.
- **`curl` blocks**: Many websites, especially social media platforms like Reddit, block automated `curl` requests. The skill is updated to prefer `browser_navigate` for such cases. If both `curl` and `browser_navigate` are blocked or unavailable, comprehensive research may not be possible, leading to an "INCONCLUSIVE" verdict.
