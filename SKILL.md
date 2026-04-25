---
name: isitsketch
description: >
  Researches whether a metal/black metal artist or band is a nazi, has nazi ties,
  or engages in NSBM (National Socialist Black Metal). Searches Metal Archives (Encyclopaedia Metallum),
  Reddit r/isitsketch and r/rabm for evidence. Use when asked "is [artist] sketch?",
  "is [artist] nazi?", "is [artist] NSBM?", or any variation thereof.
---

# IsItSketch — Nazi/NSBM Research Skill

You are researching whether a given artist or band has nazi ties, promotes National Socialist ideology, or is considered "sketch" (unsafe to support) in the metal community.

## Sources to Search

Search all of the following. Use `web_search` tool with targeted queries.

### 1. Metal Archives (Encyclopaedia Metallum)
- URL pattern: `https://www.metal-archives.com/search?searchString=<ARTIST>&type=band`
- Fetch the band's page. Look for:
  - Genre tags containing "NSBM" or "National Socialist Black Metal"
  - Band description/notes mentioning ideology
  - Member profiles — check if any members have bands tagged as NSBM
  - Label associations — some labels are known nazi/NSBM labels (e.g. Darker Than Black, Nebelfee Klangwerke, W.A.R. Productions)
  - Comments section (often contains community warnings)

### 2. Reddit r/isitsketch
- Search query: `site:reddit.com/r/isitsketch "<ARTIST>"`
- This subreddit is dedicated to exactly this question. Threads here are high-signal.
- Look for: confirmed reports, receipts (screenshots, lyrics quotes), community verdicts

### 3. Reddit r/rabm (Red and Anarchist Black Metal)
- Search query: `site:reddit.com/r/rabm "<ARTIST>"`
- RABM community actively monitors and calls out NSBM. Very reliable source.
- Look for: callout posts, pinned warnings, discussions

### 4. General web search
- Query: `"<ARTIST>" NSBM nazi "national socialist"`
- Query: `"<ARTIST>" sketch racist white supremacist`
- Look for: interviews with racist statements, known associations, label affiliations, lyrics analysis

## Research Workflow

1. **Identify the artist** — confirm spelling, country of origin, genre. If ambiguous, ask user to clarify.

2. **Search Metal Archives** — fetch band page, note genre, label, members, any flags.

3. **Search r/isitsketch** — look for existing threads about this artist.

4. **Search r/rabm** — look for callout posts or discussions.

5. **General search** — catch anything missed by the above.

6. **Cross-reference members** — if main band is clean, check if members have side projects or past bands flagged as NSBM.

7. **Check label** — some labels are nazi-associated even if the band themselves doesn't explicitly self-identify.

## Verdict Format

After research, deliver a structured verdict:

```
## IsItSketch: [ARTIST NAME]

**Verdict:** ✅ CLEAN / ⚠️ SKETCHY / 🚨 NAZI / ❓ INCONCLUSIVE

**Confidence:** High / Medium / Low

### Evidence Found
- [source]: [what was found]
- [source]: [what was found]

### Red Flags
- (list specific red flags if any)

### Member/Label Connections
- (note if members have NSBM projects, or label is associated with NS ideology)

### Community Consensus
- (what r/isitsketch and r/rabm say, if anything)

### Bottom Line
[2-3 sentence summary. Be direct. If sketchy — say so clearly.]
```

## Verdict Definitions

- ✅ **CLEAN** — No credible evidence of nazi ties. Community has no warnings.
- ⚠️ **SKETCHY** — Some red flags but not definitive (e.g. played with NSBM bands, on a grey-area label, ambiguous lyrics, band members with problematic history).
- 🚨 **NAZI** — Confirmed NSBM. Tagged on Metal Archives, explicit statements, confirmed ideology, or strong community consensus.
- ❓ **INCONCLUSIVE** — Insufficient information found. Note what was searched and what gaps remain.

## Known NSBM-Associated Labels (reference list)

These labels are known for releasing NSBM. A band on these labels is a red flag:
- Darker Than Black Records
- Nebelfee Klangwerke
- W.A.R. Productions
- Oskorei Production
- Blood & Iron Records
- Nordwind Productions
- Purity Through Fire (grey area — many NSBM releases)
- Werewolf Records (Satanic Warmaster's label — not explicitly NS but known associations)

## Known NSBM Acts (for cross-referencing members)

If a band member has past/present involvement with these, flag it:
- Burzum (Varg Vikernes — convicted racist)
- Absurd (Germany)
- Goatmoon (Finland — grey area, contested)
- Nokturnal Mortum (Ukraine — early releases NSBM, later claimed to distance)
- Drudkh (members overlap with Hate Forest / related to NS scene — contested)
- Grand Belial's Key (US)
- Peste Noire (France — La sale famine de Valfunde's statements)
- Graveland (Poland — Darken's public statements)
- Leichenmei (Germany)

> Note: "grey area" bands should be mentioned but not treated as definitive proof.

## Important Notes

- **Lyrics alone are not always proof** — black metal uses dark imagery. Look for explicit NS ideology, not just darkness/paganism.
- **Paganism ≠ nazism** — heathenry/folk themes alone are not a red flag.
- **Be specific with evidence** — quote sources, link threads, don't make unsupported claims.
- **When uncertain, say so** — an inconclusive verdict with clear reasoning is better than a false verdict.
- **The goal is to help people make informed decisions** about which artists to support financially.
