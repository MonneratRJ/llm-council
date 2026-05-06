# LLM Council

A GitHub Copilot skill that runs your question through 5 AI advisors who independently analyze it, peer-review each other anonymously, and synthesize a final verdict.

Adapted from [Andrej Karpathy's LLM Council](https://github.com/karpathy/llm-council) methodology.

---

## What it does

Instead of getting one AI answer, the council:

1. Frames your question with relevant workspace context
2. Sends it to 5 advisors simultaneously, each thinking from a different angle
3. Has each advisor anonymously peer-review all 5 responses
4. Produces a chairman synthesis with a clear recommendation
5. Saves an HTML report and a full Markdown transcript to your workspace

---

## How to trigger it

Say one of the following phrases followed by your question:

| Trigger              | Example                                              |
| -------------------- | ---------------------------------------------------- |
| `council this`       | "Council this: should I charge $97 or $297?"         |
| `run the council`    | "Run the council on my product launch plan"          |
| `war room this`      | "War room this: I'm thinking of hiring a VA"         |
| `pressure-test this` | "Pressure-test this positioning angle"               |
| `stress-test this`   | "Stress-test this pricing strategy"                  |
| `debate this`        | "Debate this: async vs sync architecture for my API" |

The council also activates on strong decision signals like:

- "Should I X or Y?"
- "Which option is better?"
- "I can't decide between..."
- "Validate this idea"
- "Get me multiple perspectives on..."

---

## When to use it (and when not to)

**Use the council when:**

- You're facing a real decision with meaningful stakes
- Multiple reasonable options exist and you're unsure which to pick
- You want your idea pressure-tested before committing
- You want perspectives you haven't thought of

**Don't use the council for:**

- Factual lookups ("What's the capital of France?")
- Creation tasks ("Write me a tweet")
- Trivial yes/no questions without real tradeoffs
- Simple processing tasks ("Summarize this article")

---

## The five advisors

| Advisor                          | Role                                                                 |
| -------------------------------- | -------------------------------------------------------------------- |
| **The Contrarian**               | Hunts for fatal flaws, what's missing, what will fail                |
| **The First Principles Thinker** | Strips assumptions, rebuilds the problem from scratch                |
| **The Expansionist**             | Finds upside and adjacent opportunities everyone else is missing     |
| **The Outsider**                 | Sees it with fresh eyes — no context, no bias, no curse of knowledge |
| **The Executor**                 | Cuts theory and asks "what do you do Monday morning?"                |

These five create natural tensions: Contrarian vs. Expansionist (downside vs. upside), First Principles vs. Executor (rethink vs. just do it), and the Outsider keeping everyone honest.

---

## What you get

After each council session, two files are saved to your workspace:

```
council-report-[timestamp].html      # Visual report — start here
council-transcript-[timestamp].md    # Full transcript — for deep dives
```

The **HTML report** includes:

- The chairman's verdict at the top
- An agreement/disagreement visual across advisors
- Collapsible sections for each advisor's full response
- Collapsible peer review highlights

The **Markdown transcript** includes:

- The original question and framed version
- All 5 advisor responses
- All 5 peer reviews (with anonymization map revealed)
- The chairman's full synthesis

---

## Output structure (chairman's verdict)

Every council session ends with the chairman producing:

1. **Where the council agrees** — high-confidence signals from independent convergence
2. **Where the council clashes** — genuine disagreements, presented without smoothing them over
3. **Blind spots the council caught** — things that only surfaced during peer review
4. **The recommendation** — a direct answer, not "it depends"
5. **The one thing to do first** — a single concrete next step

---

## Workspace context

Before framing your question, the council automatically scans for context files in your workspace:

- `CLAUDE.md` or `claude.md` (business context, constraints, preferences)
- Any `memory/` folder (audience profiles, past decisions, business details)
- Files you explicitly referenced or attached
- Previous council transcripts (to avoid re-counciling the same ground)

This means the advisors give specific, grounded advice instead of generic takes. The richer your workspace context, the better the council output.

---

## Installation

1. Copy `SKILL.md` into your project or workspace folder.
2. In VS Code with GitHub Copilot, open Agent mode.
3. Reference the skill by triggering any of the phrases above.

> The skill is self-contained. No dependencies, no API keys beyond your existing Copilot subscription.

---

## Example

**You:** "Council this: I'm thinking of building a $297 course on Claude for beginners. My audience is mostly non-technical solopreneurs. Is this the right move?"

**Council output (abridged):**

- **Contrarian:** Market is flooded. At $297, you're competing with free YouTube content. High support burden from non-technical audience.
- **First Principles Thinker:** What are you actually trying to achieve? If it's revenue, a course is one of the slowest paths.
- **Expansionist:** Beginner AI for solopreneurs is massively underserved. You could own the entry point. $297 might be too low.
- **Outsider:** "Claude for beginners" means nothing to someone outside your world. Sell the outcome, not the tool.
- **Executor:** Validate with a $97 live workshop before building anything. If 50 people won't buy the workshop, 500 won't buy the course.

**Chairman's recommendation:** Don't build the course yet. Reframe around the outcome (automate your business, get 10 hours back per week), not the tool. Run a $97 live workshop first to validate demand.

**One thing to do first:** Run a live workshop called "How to automate your first business task with AI" for $97. Don't mention the tool in the title.
