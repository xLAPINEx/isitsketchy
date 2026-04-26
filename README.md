# isitsketchy

An [Agent Skill](https://agentskills.io) that researches whether a metal or black metal artist has Nazi ties or engages in NSBM (National Socialist Black Metal).

## What it does

When invoked with a band or artist name, the skill searches seven sources and delivers a structured verdict:

1. **Metal Archives** — genre tags, label affiliations, member history
2. **Community-driven lists** - commonly referenced lists of bands and labels
4. **Reddit r/isitsketch** — a subreddit dedicated to exactly this question
5. **Reddit r/rabm** — the Red and Anarchist Black Metal community, which actively monitors NSBM
6. **Band interviews** — searched and read to fact-check claims and find direct political statements from members
7. **General web search** — news coverage, scene commentary, lyrics analysis

| Verdict | Meaning |
|---|---|
| CLEAN | No credible evidence of Nazi ties; interviews confirm neutral or anti-fascist stance |
| SKETCHY | Red flags present but not definitive |
| NAZI | Confirmed NSBM — tagged, explicit statements, or strong community consensus |
| INCONCLUSIVE | Insufficient information found |

## Install

```
npx skills add sketchmasta/isitsketchy --agent <your_agent_name>
```

## Usage

```
/isitsketchy <artist or band name>
```

Examples:

```
/isitsketchy Burzum
/isitsketchy Drudkh
/isitsketchy Wolves in the Throne Room
```

Agent will search the sources and return a verdict with evidence, confidence level, and a plain-language bottom line.

## Example output

```
## IsItSketchy: Wolves in the Throne Room

**Verdict:** CLEAN
**Confidence:** High

### Evidence Found
- Metal Archives: Tagged as Atmospheric Black Metal / Cascadian Black Metal. No NSBM tags.
- Black Metal Sketch List: Listed as SAFE with note "Openly left-wing / anti-fascist."
- r/isitsketch: No threads found.
- r/rabm: Mentioned favorably as anti-fascist / left-leaning.

### Red Flags
None found.

### Member/Label Connections
Signed to Relapse Records. No Nazi-associated label history.

### Interview Evidence
- [Decibel Magazine, 2014] "We are absolutely opposed to fascism and white supremacy in all forms." — https://www.decibelmagazine.com/…

### Bottom Line
Wolves in the Throne Room are a Cascadian black metal band with a documented anti-fascist stance.
No evidence of NSBM ties. Safe to support.
```

## License

[GNU General Public License v3](LICENSE)
