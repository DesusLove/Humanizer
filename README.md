# Humanizer

[![skills.sh installs](https://skills.sh/b/blader/humanizer)](https://skills.sh/blader/humanizer)

A **portable agent skill** that strips signs of AI-generated writing from text and makes it sound natural. No build step, no dependencies, no lock-in — just Markdown that works in any agent harness.

Based on [Wikipedia's "Signs of AI writing"](https://en.wikipedia.org/wiki/Wikipedia:Signs_of_AI_writing) guide, maintained by WikiProject AI Cleanup.

---

## Quick Start

```bash
npx skills add blader/humanizer --global --agent '*'
```

Then, in any agent session:

```
/humanizer

[paste your AI-generated text here]
```

Or point it at a file:

```
Humanize the prose in docs/launch-post.md
```

---

## Installation

### Skills CLI (recommended)

Install globally — available in every project:

```bash
npx skills add blader/humanizer --global
```

Update an existing install:

```bash
npx skills update humanizer --global
```

Omit `--global` for a project-local install you can commit and share.

### Claude Code plugin

```text
/plugin marketplace add blader/humanizer
/plugin install humanizer@humanizer
```

Invoke as `/humanizer:humanizer`.

### Manual

Clone or copy `SKILL.md` wherever your harness expects skill files:

```bash
git clone https://github.com/blader/humanizer.git /path/to/your/skills/humanizer
```

---

## How It Works

The skill is a two-pass editor:

1. **Draft** — rewrite the text, removing AI tells while preserving every claim from the source.
2. **Audit** — scan the draft for anything that *still* reads like AI, then rewrite again.

A **no-fabrication rule** governs both passes: the rewrite never adds facts, names, dates, quotes, or citations that weren't in the source. Specificity comes from the author, not the LLM.

### Voice Calibration

Provide a sample of your own writing and the skill matches your sentence rhythm, word choice, and quirks instead of producing generic clean output:

```
/humanizer

Here's a sample of my writing for voice matching:
[paste 2-3 paragraphs]

Now humanize this text:
[paste AI text]
```

---

## 33 Patterns Detected

### Content

| # | Pattern | Before | After |
|---|---------|--------|-------|
| 1 | **Significance inflation** | "marking a pivotal moment in the evolution of..." | "was established in 1989 as part of a wider decentralization" |
| 2 | **Notability name-dropping** | "cited in NYT, BBC, FT, and The Hindu" | Trim the list; keep only sourced context |
| 3 | **Superficial -ing analyses** | "symbolizing... reflecting... showcasing..." | Remove, or keep only what the source supports |
| 4 | **Promotional language** | "nestled within the breathtaking region" | "is a town in the Gonder region" |
| 5 | **Vague attributions** | "Experts believe it plays a crucial role" | Name a real source or cut the claim |
| 6 | **Formulaic challenges** | "Despite challenges... continues to thrive" | Keep the sourced facts; cut the boosterism |

### Language

| # | Pattern | Before | After |
|---|---------|--------|-------|
| 7 | **AI vocabulary** | "Actually... additionally... testament... landscape... showcasing" | "also... remain common" |
| 8 | **Copula avoidance** | "serves as... features... boasts" | "is... has" |
| 9 | **Negative parallelisms** | "It's not just X, it's Y" | State the point directly |
| 10 | **Rule of three** | "innovation, inspiration, and insights" | Use natural number of items |
| 11 | **Synonym cycling** | "protagonist... main character... central figure" | "protagonist" (repeat when clearest) |
| 12 | **False ranges** | "from the Big Bang to dark matter" | List topics directly |
| 13 | **Passive voice / fragments** | "No configuration file needed" | Name the actor when it helps clarity |

### Style

| # | Pattern | Before | After |
|---|---------|--------|-------|
| 14 | **Em/en dashes** | "institutions—not the people—yet this continues—" | Periods, commas, colons, or parens |
| 15 | **Boldface overuse** | "**OKRs**, **KPIs**, **BMC**" | "OKRs, KPIs, BMC" |
| 16 | **Inline-header lists** | "**Performance:** Performance improved" | Convert to prose |
| 17 | **Title Case Headings** | "Strategic Negotiations And Partnerships" | "Strategic negotiations and partnerships" |
| 18 | **Emojis** | "🚀 Launch Phase: 💡 Key Insight:" | Remove emojis |
| 19 | **Curly quotes** | `said "the project"` | `said "the project"` |
| 26 | **Hyphenated word pairs** | "cross-functional, data-driven, client-facing" | Drop hyphens on common pairs |
| 27 | **Persuasive authority tropes** | "At its core, what matters is..." | State the point directly |
| 28 | **Signposting announcements** | "Let's dive in", "Here's what you need to know" | Start with the content |
| 29 | **Fragmented headers** | "## Performance" + "Speed matters." | Let the heading do the work |
| 30 | **Diff-anchored writing** | "This function was added to replace..." | Describe what it does, not what changed |
| 31 | **Manufactured punchlines** | "It had no preference. No prior. No nostalgia." | Use varied lengths and concrete claims |
| 32 | **Aphorism formulas** | "Symmetry is the language of trust" | Replace formula with the actual claim |
| 33 | **Conversational rhetorical openers** | "Honestly? It depends..." | Remove the fake-candid setup |

### Communication

| # | Pattern | Before | After |
|---|---------|--------|-------|
| 20 | **Chatbot artifacts** | "I hope this helps! Let me know if..." | Remove entirely |
| 21 | **Cutoff disclaimers** | "While details are limited in available sources..." | Find sources or remove |
| 22 | **Sycophantic tone** | "Great question! You're absolutely right!" | Respond directly |

### Filler & Hedging

| # | Pattern | Before | After |
|---|---------|--------|-------|
| 23 | **Filler phrases** | "In order to", "Due to the fact that" | "To", "Because" |
| 24 | **Excessive hedging** | "could potentially possibly" | "may" |
| 25 | **Generic conclusions** | "The future looks bright" | Specific plans or facts |

---

## Example

**Before (AI-generated):**

> I recently spent five unforgettable days in Lisbon, and let me tell you — this city completely stole my heart. From the moment I arrived, I knew I was somewhere truly special.
>
> Nestled along the banks of the Tagus River, Lisbon stands as a vibrant testament to Portugal's enduring spirit, where rich history and modern energy intertwine at every turn. Yes, the famous hills are challenging — my legs certainly felt it! — but every climb rewards you with breathtaking, panoramic views that make it all worthwhile.
>
> No trip would be complete without riding the iconic Tram 28, winding through the city's most historic neighborhoods. And the food? Simply divine. The original pastéis de nata at Pastéis de Belém are a beloved national treasure, and savoring one still warm was a moment I will never forget.
>
> What truly makes Lisbon special isn't just the sights — it's the feeling. Wander a few steps off the main squares and you'll discover a quieter, more authentic side: sun-drenched alleys, charming tiled facades, and friendly locals going about their daily lives.

**After (humanized):**

> I spent five days in Lisbon last October and still have mixed feelings about it. Beautiful, yes. Also harder on the knees than anyone warned me.
>
> The hills are the whole story and somehow never make the brochures. My hotel was up in Alfama, which photographs beautifully and translates, in practice, to climbing what felt like a six-story staircase every time I wanted coffee. By the second day my calves had opinions.
>
> Everyone says to ride Tram 28, so I did, wedged against a stranger's backpack for forty minutes while three tour groups filmed the same corner. The custard tarts, though, earn the fuss. I had one at a plain little place in Graça, still warm, and for about thirty seconds I understood why people build trips around pastry.
>
> What I did not expect was how quiet the city gets away from the main squares. Two blocks uphill from any plaza it turns into laundry lines, chipped tile, open windows, and old men watching football with the sound turned up. That is the Lisbon I keep thinking about, not the castle.

---

## References

- [Wikipedia: Signs of AI writing](https://en.wikipedia.org/wiki/Wikipedia:Signs_of_AI_writing)
- [WikiProject AI Cleanup](https://en.wikipedia.org/wiki/Wikipedia:WikiProject_AI_Cleanup)

---

## Version History

| Version | Notes |
|---------|-------|
| **2.9.1** | Improved distribution: portable frontmatter, global install as default, package validation |
| **2.9.0** | No-fabrication rule; information-over-shape rewrite rule; voice sample outranks em dash ban |
| **2.8.3** | Version moved to `metadata.version` for Agent Skills compatibility |
| **2.8.2** | New first-person Lisbon example replacing the old before/after |
| **2.8.1** | Cross-agent install docs, Claude Code plugin packaging, false-positive guard |
| **2.8.0** | Patterns #31-33: punchlines, aphorisms, rhetorical openers (33 total) |
| **2.7.0** | Pattern #30: diff-anchored writing; em dashes become a hard cut |
| **2.6.0** | Cleanup: consolidated workflows, gated personality guidance |
| **2.5.1** | Pattern #13: passive voice / subjectless fragments (29 total) |
| **2.5.0** | Persuasive framing, signposting, fragmented headers; expanded negative parallelisms |
| **2.4.0** | Voice calibration from user writing samples |
| **2.3.0** | Pattern #25: hyphenated word pair overuse |
| **2.2.0** | Final "obviously AI generated" audit + second-pass rewrite |
| **2.1.1** | Fixed pattern #18 example (curly quotes) |
| **2.1.0** | Before/after examples for all 24 patterns |
| **2.0.0** | Complete rewrite from Wikipedia article |
| **1.0.0** | Initial release |

---

MIT License
