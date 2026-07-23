# 🧠 Humanizer

> *Make AI text sound like it came from a person, not a language model.*

[![skills.sh installs](https://skills.sh/b/blader/humanizer)](https://skills.sh/blader/humanizer)

**Humanizer** is a portable agent skill that strips the telltale signs of AI-generated writing and replaces them with natural, human-sounding prose. It's plain Markdown — zero dependencies, zero build step, works in any agent harness that loads skills.

Inspired by [Wikipedia's "Signs of AI writing"](https://en.wikipedia.org/wiki/Wikipedia:Signs_of_AI_writing) guide (WikiProject AI Cleanup), it catches **33 patterns** across content, language, style, communication, and hedging.

---

## ⚡ Quick Start

```bash
npx skills add blader/humanizer --global --agent '*'
```

Then in any agent session:

```
/humanizer

[paste your AI-generated text here]
```

Or point it at a file:

```
Humanize the prose in docs/launch-post.md
```

---

## 📦 Installation

### 🛠 Skills CLI (recommended)

```bash
npx skills add blader/humanizer --global
```

Update an existing install:

```bash
npx skills update humanizer --global
```

Leave off `--global` for a project-local install you can commit and share with your team.

### 🤖 Claude Code

```text
/plugin marketplace add blader/humanizer
/plugin install humanizer@humanizer
```

Then invoke as `/humanizer:humanizer`.

### 📄 Manual

Clone the repo wherever your harness expects skill directories:

```bash
git clone https://github.com/blader/humanizer.git /path/to/your/skills/humanizer
```

Or just copy `SKILL.md` — that's the whole runtime.

---

## 🔄 How It Works

Humanizer runs a **two-pass edit** on your text:

| Pass | What happens |
|------|-------------|
| **1. Draft** | Rewrites the text, stripping AI tells while preserving every claim, fact, and detail from the source. |
| **2. Audit** | Scans the draft for anything that *still* reads like AI, then rewrites again until it passes the smell test. |

### 📏 The Golden Rule: No Fabrication

The rewrite **never** adds facts, names, dates, quotes, or citations that weren't in the source. Specificity comes from the author — not the LLM.

### 🎯 Voice Calibration

Want it to sound like *you*? Drop in a writing sample:

```
/humanizer

Here's a sample of my writing for voice matching:
[paste 2-3 paragraphs of your own writing]

Now humanize this:
[paste AI text]
```

The skill analyzes your sentence rhythm, word choice, and quirks — then matches them instead of producing generic "clean" output. Your voice takes priority over the pattern rules.

---

## 🕵️ 33 Patterns Detected

### 📰 Content Patterns

| # | Pattern | ❌ AI-Speak | ✅ Human Fix |
|---|---------|------------|-------------|
| 1 | **Significance inflation** | "marking a pivotal moment in the evolution of..." | "was established in 1989 as part of a wider decentralization" |
| 2 | **Notability name-dropping** | "cited in NYT, BBC, FT, and The Hindu" | Trim the list; keep only sourced context |
| 3 | **Superficial -ing analyses** | "symbolizing... reflecting... showcasing..." | Remove, or keep only what the source supports |
| 4 | **Promotional language** | "nestled within the breathtaking region" | "is a town in the Gonder region" |
| 5 | **Vague attributions** | "Experts believe it plays a crucial role" | Name a real source or cut the claim |
| 6 | **Formulaic challenges** | "Despite challenges... continues to thrive" | Keep the facts; cut the boosterism |

### 💬 Language Patterns

| # | Pattern | ❌ AI-Speak | ✅ Human Fix |
|---|---------|------------|-------------|
| 7 | **AI vocabulary** | "Actually... additionally... testament... landscape... showcasing" | "also... remain common" |
| 8 | **Copula avoidance** | "serves as... features... boasts" | "is... has" |
| 9 | **Negative parallelisms** | "It's not just X, it's Y" | Say it straight |
| 10 | **Rule of three** | "innovation, inspiration, and insights" | Use a natural number of items |
| 11 | **Synonym cycling** | "protagonist... main character... central figure" | "protagonist" — repeat the clearest word |
| 12 | **False ranges** | "from the Big Bang to dark matter" | List topics directly |
| 13 | **Passive voice / fragments** | "No configuration file needed" | Name the actor when it helps |

### ✨ Style Patterns

| # | Pattern | ❌ AI-Speak | ✅ Human Fix |
|---|---------|------------|-------------|
| 14 | **Em/en dashes** | "institutions—not the people—yet this continues—" | Periods, commas, colons, or parens |
| 15 | **Boldface overuse** | "**OKRs**, **KPIs**, **BMC**" | "OKRs, KPIs, BMC" |
| 16 | **Inline-header lists** | "**Performance:** Performance improved" | Convert to prose |
| 17 | **Title Case Headings** | "Strategic Negotiations And Partnerships" | "Strategic negotiations and partnerships" |
| 18 | **Emojis** | "🚀 Launch Phase: 💡 Key Insight:" | Removed |
| 19 | **Curly quotes** | `said "the project"` | `said "the project"` |
| 26 | **Hyphenated word pairs** | "cross-functional, data-driven, client-facing" | Drop hyphens on common pairs |
| 27 | **Persuasive authority tropes** | "At its core, what matters is..." | State the point directly |
| 28 | **Signposting announcements** | "Let's dive in", "Here's what you need to know" | Start with the content |
| 29 | **Fragmented headers** | "## Performance" + "Speed matters." | Let the heading do the work |
| 30 | **Diff-anchored writing** | "This function was added to replace..." | Describe what it does |
| 31 | **Manufactured punchlines** | "It had no preference. No prior. No nostalgia." | Vary sentence length; be concrete |
| 32 | **Aphorism formulas** | "Symmetry is the language of trust" | Replace with the actual claim |
| 33 | **Conversational rhetorical openers** | "Honestly? It depends..." | Lose the fake-candid setup |

### 📞 Communication Patterns

| # | Pattern | ❌ AI-Speak | ✅ Human Fix |
|---|---------|------------|-------------|
| 20 | **Chatbot artifacts** | "I hope this helps! Let me know if..." | Remove entirely |
| 21 | **Cutoff disclaimers** | "While details are limited in available sources..." | Find sources or remove |
| 22 | **Sycophantic tone** | "Great question! You're absolutely right!" | Respond directly |

### 🧩 Filler & Hedging

| # | Pattern | ❌ AI-Speak | ✅ Human Fix |
|---|---------|------------|-------------|
| 23 | **Filler phrases** | "In order to", "Due to the fact that" | "To", "Because" |
| 24 | **Excessive hedging** | "could potentially possibly" | "may" |
| 25 | **Generic conclusions** | "The future looks bright" | Specific plans or facts |

---

## 🎬 Before & After

**Before — AI-generated:**
> I recently spent five unforgettable days in Lisbon, and let me tell you — this city completely stole my heart. From the moment I arrived, I knew I was somewhere truly special.
>
> Nestled along the banks of the Tagus River, Lisbon stands as a vibrant testament to Portugal's enduring spirit, where rich history and modern energy intertwine at every turn. Yes, the famous hills are challenging — my legs certainly felt it! — but every climb rewards you with breathtaking, panoramic views that make it all worthwhile.
>
> No trip would be complete without riding the iconic Tram 28, winding through the city's most historic neighborhoods. And the food? Simply divine.

**After — humanized:**
> I spent five days in Lisbon last October and still have mixed feelings about it. Beautiful, yes. Also harder on the knees than anyone warned me.
>
> The hills are the whole story and somehow never make the brochures. My hotel was up in Alfama, which photographs beautifully and translates, in practice, to climbing what felt like a six-story staircase every time I wanted coffee. By the second day my calves had opinions.
>
> Everyone says to ride Tram 28, so I did, wedged against a stranger's backpack for forty minutes while three tour groups filmed the same corner. The custard tarts, though, earn the fuss.

---

## 📚 References

- [Wikipedia: Signs of AI writing](https://en.wikipedia.org/wiki/Wikipedia:Signs_of_AI_writing)
- [WikiProject AI Cleanup](https://en.wikipedia.org/wiki/Wikipedia:WikiProject_AI_Cleanup)

---

## 📋 Changelog

| Version | Highlights |
|---------|------------|
| **2.9.1** | 📦 Portable frontmatter, global install as default, package validation |
| **2.9.0** | 🚫 No-fabrication rule, 🎯 voice sample overrides em dash ban |
| **2.8.3** | 🔧 Version moved to `metadata.version` for Agent Skills compatibility |
| **2.8.2** | ✏️ New Lisbon example replacing the old before/after |
| **2.8.1** | 🔗 Cross-agent install docs, Claude Code plugin |
| **2.8.0** | 🆕 Patterns #31-33: punchlines, aphorisms, rhetorical openers |
| **2.7.0** | 🆕 Pattern #30: diff-anchored writing; em dashes are a hard cut |
| **2.6.0** | 🧹 Cleanup: consolidated workflows, gated personality guidance |
| **2.5.1** | 🆕 Pattern #13: passive voice / subjectless fragments |
| **2.5.0** | 🆕 Persuasive framing, signposting, fragmented headers |
| **2.4.0** | 🎯 Voice calibration from user writing samples |
| **2.3.0** | 🆕 Pattern #25: hyphenated word pairs |
| **2.2.0** | 🔄 Final audit pass + second rewrite |
| **2.1.1** | 🐛 Fixed pattern #18 example (curly quotes) |
| **2.1.0** | 📝 Before/after examples for all 24 patterns |
| **2.0.0** | ♻️ Complete rewrite from Wikipedia article |
| **1.0.0** | 🎉 Initial release |

---

## 📄 License

MIT
