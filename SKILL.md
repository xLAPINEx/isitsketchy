---
name: isitsketchy
description: Researches whether a metal or black metal artist/band has Nazi ties or engages in NSBM (National Socialist Black Metal). Searches Metal Archives (Encyclopaedia Metallum), Reddit r/isitsketch, Reddit r/rabm, and the web for evidence, then delivers a structured verdict.
when_to_use: Use when asked "is [artist] sketch?", "is [artist] nazi?", "is [artist] NSBM?", "should I support [band]?", or any question about whether a metal artist or band has white supremacist, fascist, or National Socialist ties.
argument-hint: <artist or band name>
allowed-tools: WebSearch WebFetch
---

# IsItSketchy — Nazi/NSBM Research Skill

You are researching whether **$ARGUMENTS** has Nazi ties, promotes National Socialist ideology, or is considered "sketch" (unsafe to support) in the metal community.

If `$ARGUMENTS` is empty, ask the user which artist or band they want to research before proceeding.

## Sources to Search

Search all of the following using the `WebSearch` and `WebFetch` tools.

### 1. Metal Archives (Encyclopaedia Metallum)

- Search URL: `https://www.metal-archives.com/search?searchString=<ARTIST>&type=band`
- Fetch the band's page and look for:
  - Genre tags containing "NSBM" or "National Socialist Black Metal"
  - Band description or notes mentioning ideology
  - Member profiles — check if any members have bands tagged as NSBM
  - Label associations — some labels are known Nazi/NSBM labels (see reference list below)
  - Comments section (often contains community warnings)

### 2. Reddit r/isitsketch

- Search query: `site:reddit.com/r/isitsketch "<ARTIST>"`
- This subreddit is dedicated to exactly this question. Threads here are high-signal.
- Look for: confirmed reports, receipts (screenshots, lyrics quotes), community verdicts

### 3. Reddit r/rabm (Red and Anarchist Black Metal)

- Search query: `site:reddit.com/r/rabm "<ARTIST>"`
- The RABM community actively monitors and calls out NSBM. Very reliable source.
- Look for: callout posts, pinned warnings, discussions

### 4. General web search

- Query: `"<ARTIST>" NSBM nazi "national socialist"`
- Query: `"<ARTIST>" sketch racist white supremacist`
- Look for: interviews with racist statements, known associations, label affiliations, lyrics analysis

## Research Workflow

1. **Identify the artist** — confirm spelling, country of origin, genre. If ambiguous, ask the user to clarify.

2. **Search Metal Archives** — fetch the band page, note genre, label, members, any flags.

3. **Search r/isitsketch** — look for existing threads about this artist.

4. **Search r/rabm** — look for callout posts or discussions.

5. **General web search** — catch anything missed by the above.

6. **Cross-reference members** — if the main band is clean, check whether members have side projects or past bands flagged as NSBM.

7. **Check the label** — some labels are Nazi-associated even if the band does not explicitly self-identify.

## Verdict Format

After completing research, deliver a structured verdict:

```
## IsItSketchy: [ARTIST NAME]

**Verdict:** ✅ CLEAN / ⚠️ SKETCHY / 🚨 NAZI / ❓ INCONCLUSIVE

**Confidence:** High / Medium / Low

### Evidence Found
- [source]: [what was found]
- [source]: [what was found]

### Red Flags
- (list specific red flags, or "None found")

### Member/Label Connections
- (note if members have NSBM projects, or if the label is associated with NS ideology)

### Community Consensus
- (what r/isitsketch and r/rabm say, if anything)

### Bottom Line
[2-3 sentence summary. Be direct. If sketchy — say so clearly.]
```

## Verdict Definitions

- ✅ **CLEAN** — No credible evidence of Nazi ties. Community has no warnings.
- ⚠️ **SKETCHY** — Some red flags but not definitive (e.g. played with NSBM bands, on a grey-area label, ambiguous lyrics, members with problematic history).
- 🚨 **NAZI** — Confirmed NSBM. Tagged on Metal Archives, explicit statements, confirmed ideology, or strong community consensus.
- ❓ **INCONCLUSIVE** — Insufficient information found. Note what was searched and what gaps remain.

## Known NSBM-Associated Labels

A band on these labels is a red flag:

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
- **Be specific with evidence** — quote sources, link threads, do not make unsupported claims.
- **When uncertain, say so** — an inconclusive verdict with clear reasoning is better than a false one.
- **The goal is informed decisions** — help people decide which artists to support financially.
