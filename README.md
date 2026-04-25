# isitsketchy

A [Claude Code skill](https://code.claude.com/docs/en/skills) that researches whether a metal or black metal artist has Nazi ties or engages in NSBM (National Socialist Black Metal).

## What it does

When invoked with a band or artist name, the skill:

1. Searches **Metal Archives** for genre tags, label affiliations, and member history
2. Searches **Reddit r/isitsketch** — a community dedicated to this exact question
3. Searches **Reddit r/rabm** — the Red and Anarchist Black Metal community, which actively monitors NSBM
4. Runs **targeted web searches** for statements, associations, and receipts

It then delivers a structured verdict:

| Verdict | Meaning |
|---|---|
| CLEAN | No credible evidence of Nazi ties |
| SKETCHY | Red flags present but not definitive |
| NAZI | Confirmed NSBM — tagged, explicit statements, or strong community consensus |
| INCONCLUSIVE | Insufficient information found |

## Install

**Via GitHub CLI** (requires [gh](https://cli.github.com/) with the `skill` extension):

```sh
gh skill install sketchmasta/isitsketchy
```

**Manually** — copy `SKILL.md` into your personal skills folder:

```sh
mkdir -p ~/.claude/skills/isitsketchy
curl -o ~/.claude/skills/isitsketchy/SKILL.md \
  https://raw.githubusercontent.com/sketchmasta/isitsketchy/main/SKILL.md
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

Claude will search the sources and return a verdict with evidence, confidence level, and a plain-language bottom line.

## Example output

```
## IsItSketchy: Wolves in the Throne Room

**Verdict:** CLEAN
**Confidence:** High

### Evidence Found
- Metal Archives: Tagged as Atmospheric Black Metal / Cascadian Black Metal. No NSBM tags.
- r/isitsketch: No threads found.
- r/rabm: Mentioned favorably as anti-fascist / left-leaning.
- Web: Band members have spoken publicly against racism in metal.

### Red Flags
None found.

### Member/Label Connections
Signed to Relapse Records. No Nazi-associated label history.

### Bottom Line
Wolves in the Throne Room are a Cascadian black metal band with a documented anti-fascist stance.
No evidence of NSBM ties. Safe to support.
```

## License

[GNU General Public License v3](LICENSE)
