---
name: isitsketchy
description: Researches whether a metal or black metal artist/band has Nazi ties or engages in NSBM (National Socialist Black Metal). Searches Metal Archives, community spreadsheets, Reddit r/isitsketch and r/rabm, band interviews, and the web for evidence, then delivers a structured verdict.
when_to_use: Use when asked "is [artist] sketch?", "is [artist] nazi?", "is [artist] NSBM?", "should I support [band]?", or any question about whether a metal artist or band has white supremacist, fascist, or National Socialist ties.
argument-hint: <artist or band name>
allowed-tools: WebSearch WebFetch
---

# IsItSketchy — Nazi/NSBM Research Skill

You are researching whether **$ARGUMENTS** has Nazi ties, promotes National Socialist ideology, or is considered "sketch" (unsafe to support) in the metal community.

If `$ARGUMENTS` is empty, ask the user which artist or band they want to research before proceeding.

## Sources to Search

Work through all sources below. Use `WebSearch` for queries and `WebFetch` for direct URL access.

---

### 1. Metal Archives (Encyclopaedia Metallum)

Search URL: `https://www.metal-archives.com/search?searchString=<ARTIST>&type=band`

Fetch the band's page and look for:
- Genre tags containing "NSBM" or "National Socialist Black Metal"
- Band description or notes mentioning ideology
- Member profiles — check if any members have bands tagged as NSBM
- Label associations (see known NSBM labels below and the Labels sheet in source 5)
- Comments section (often contains community warnings)

---

### 2. Reddit r/isitsketch

Search query: `site:reddit.com/r/isitsketch "<ARTIST>"`

This subreddit is dedicated to exactly this question. Threads here are high-signal.
Look for: confirmed reports, receipts (screenshots, lyrics quotes), community verdicts.

---

### 3. Reddit r/rabm (Red and Anarchist Black Metal)

Search query: `site:reddit.com/r/rabm "<ARTIST>"`

The RABM community actively monitors and calls out NSBM. Very reliable source.
Look for: callout posts, pinned warnings, discussions.

---

### 4. Hellseatic Sketchy Metal Bands PDF

URL: `https://www.hellseatic.de/wp-content/uploads/Sketchy-Metal-Bands.pdf`

A community-maintained PDF list of metal bands with political red flags. **Semi-reliable — requires fact-checking and cross-referencing with Metal Archives and interviews.**

Fetch the URL with `WebFetch`. The PDF may not render as readable text — if it returns binary or garbled content, fall back to:
- `WebSearch` query: `site:hellseatic.de "<ARTIST>"`
- `WebSearch` query: `hellseatic "sketchy metal" "<ARTIST>"`

---

### 5. Black Metal Sketch List — Google Sheets (community spreadsheet)

A comprehensive community-curated spreadsheet with three tabs. **Each tab is a CSV export — fetch the URL, and if it redirects to a different host, follow that redirect URL with a second `WebFetch` call.**

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

### 6. Band interviews (fact-checking)

Use `WebSearch` to locate interviews, then `WebFetch` to read the actual interview page. **Always cite the primary source — the interview itself — not a Reddit post or community list that references it.**

Search queries:
- `"<ARTIST>" interview politics ideology`
- `"<ARTIST>" interview "national socialist" OR "white power" OR "fascist"`
- `"<ARTIST>" interview OR statement race nazi`
- `"<ARTIST>" interview site:metalwani.com OR site:ncs.fm OR site:blabbermouth.net OR site:metalsucks.net OR site:revolvermag.com OR site:kerrang.com`

For each promising result:
1. Use `WebFetch` on the interview URL to read the full text
2. Find the relevant quote directly in the article
3. Cite it as: `[Publication, Year] "[direct quote]" — [URL]`

Look for:
- Direct statements about race, politics, ideology, or nationalism
- Expressions of sympathy for NS or fascist movements
- Denunciations of racism (clears a band from ambiguous imagery)
- Context for controversial lyrics or imagery the band has been asked to explain

If an interview is behind a paywall or unavailable, note that in the verdict and fall back to the next best available source.

---

### 7. General web search

- Query: `"<ARTIST>" NSBM nazi "national socialist"`
- Query: `"<ARTIST>" sketch racist white supremacist`

Look for: news coverage, scene commentary, label affiliations, lyrics analysis.

---

## Research Workflow

1. **Identify the artist** — confirm spelling, country of origin, genre. If ambiguous, ask the user to clarify.

2. **Check the community spreadsheets (source 5)** — fetch all three tabs and search for the artist and their label. Note classification and explanation.

3. **Check the Hellseatic PDF (source 4)** — fetch and search for the artist.

4. **Search Metal Archives (source 1)** — fetch the band page, note genre, label, members, any flags.

5. **Search r/isitsketch (source 2)** — look for existing threads.

6. **Search r/rabm (source 3)** — look for callout posts or discussions.

7. **Find and read interviews (source 6)** — search for interviews where members discuss politics or have been asked about controversial imagery. Use these to fact-check or confirm claims from the lists above.

8. **General web search (source 7)** — catch anything missed.

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

The Labels tab of the community spreadsheet (source 5, Tab 3) is the authoritative list. Quick reference for common cases:

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
- **Community lists are semi-reliable** — the spreadsheets and PDF are community-maintained and may contain errors. Always cross-reference with Metal Archives and interviews before treating a listing as definitive.
- **Be specific with evidence** — quote sources, link threads, cite interviews with year and publication. Do not make unsupported claims.
- **When uncertain, say so** — an inconclusive verdict with clear reasoning is better than a false one.
- **The goal is informed decisions** — help people decide which artists to support financially.
