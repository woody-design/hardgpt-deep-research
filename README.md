# HardGPT — Deep Research for Claude Code & Cowork

[License: CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/)
[Version](https://github.com/woody-design/hardgpt-deep-research)
[No Code Execution](#under-the-hood)

> "Rewrite this paragraph" — ChatGPT handles that fine. But *"Should I refinance my house now?"* is a **hard problem** — the answer depends on rates, policy, timeline, and goals all at once. HardGPT makes AI clarify your situation first, then cross-references official sources with real community experiences to give you an answer that actually fits.

## 🤯 Hard Problem

When you ask AI a complex real-world question, it jumps straight to an answer. No clarification, no context-gathering — just an overconfident response that's often **wrong**.

- **Lands on conclusions too fast** — skips the questions that would change the answer entirely
- **Researches the wrong thing** — misunderstands your actual goal, wastes effort in the wrong direction
- **Technically correct, practically useless** — a generic answer that doesn't fit your specific situation

## Example Questions

> [!TIP]
>
> 1. "Should I buy or rent in New York City on my salary?"
> 2. "My landlord is raising rent 15%. What are my rights?"
> 3. "I'm comparing 3 health insurance plans during open enrollment. Which is actually cheapest for my situation?"
> 4. "Planning a 2-week Japan trip with a toddler. What's realistic?"
> 5. "I want to set up a will and basic estate plan. What do I actually need?"
> 6. "I want to freelance on the side while employed full-time. What should I watch out for?"
> 7. "Comparing two job offers: $180K base vs $140K + equity. Which is actually worth more?"
> 8. "I have 10,000 RSUs vesting next month. Should I sell immediately or hold?"
> 9. "My H-1B expires in 8 months and I want to switch jobs. What are my options?"
> 10. "A startup offered me $150K + 0.5% equity. How do I evaluate this?"

## How It Works

```mermaid
flowchart LR
    U["1. Understand"] --> C["2. Clarify"] --> P["3. Plan"] --> R["4. Research"] --> D["5. Deliver"]
```




| Phase          | What happens                                                                             |
| -------------- | ---------------------------------------------------------------------------------------- |
| **Understand** | Restates your actual goal to make sure it's right                                        |
| **Clarify**    | Asks 3–5 targeted questions (max 3 rounds, then moves on)                                |
| **Plan**       | Proposes a research plan you can adjust before execution                                 |
| **Research**   | Searches official sources AND community experiences, then cross-references for conflicts |
| **Deliver**    | Conclusion first, evidence second, caveats and sources last                              |


## Before vs After

**"Can I bring 2 bags on my Tokyo flight?"**

Without HardGPT — ChatGPT searches generic baggage policies and gives you a one-size-fits-all answer from a random airline.

With HardGPT — asks which airline and booking class first, then gives you the **exact** baggage allowance for your specific ticket, plus whether your credit card adds any benefits.

---

**"Register an LLC in the US"**

Without HardGPT — ChatGPT picks one state and walks you through the steps, missing the fact that state choice has major tax and cost implications.

With HardGPT — surfaces the key decisions first (state matters for taxes, fees, and dual-filing requirements), asks about your situation, then compares options side by side with a clear recommendation.

See [full conversation examples](skills/hardgpt/SKILL.md#examples) for detailed walkthroughs.

## Get Started

**Download:**

Go to the [GitHub repo](https://github.com/woody-design/hardgpt-deep-research), click **Code** → **Download ZIP**, and unzip. Or clone with git if you prefer (`git clone https://github.com/woody-design/hardgpt-deep-research.git`).

**Install in Claude desktop app (Cowork):**

1. Open the Claude desktop app
2. Go to **Settings** → **Plugins**
3. Click **Install from folder...**
4. Select the `hardgpt-deep-research` folder

**Use it:**

```
/hardgpt Should I register my LLC in New York or New Jersey?
```

HardGPT will ask a few clarifying questions, propose a research plan, then deliver a structured, cross-referenced answer tailored to your situation.

## Under the Hood

**Pure prompt engineering** — no code execution, no scripts, no API keys, no MCP servers. The entire plugin is a single `[SKILL.md](skills/hardgpt/SKILL.md)` file you can read in 2 minutes. Nothing is installed, compiled, or run on your machine.

**Adaptive routing** — profiles each question (factual vs. decision vs. plan vs. exploration) and adjusts clarification depth, source selection, search orchestration, and output format accordingly.

**Dual-track research** — official sources (policies, regulations, documentation) are cross-referenced with community experiences (forums, reviews, real-world reports). Conflicts between the two are flagged explicitly.

**Honest about uncertainty** — sources older than 1 year are annotated. Single-source facts are flagged. High time-sensitivity answers include verification warnings. Every source gets a clickable link with a publication date.

## FAQ

**What kinds of questions does it work for?**

Any question where the answer depends on your specific context: travel logistics, legal decisions, health questions, financial comparisons, product research, local services, technical trade-offs, and more. It's especially useful for questions where a generic answer would be misleading.

**Can I customize the research workflow?**

Yes. Fork the repo and edit `[skills/hardgpt/SKILL.md](skills/hardgpt/SKILL.md)`. The entire workflow — clarification rules, routing logic, source strategies, delivery formats — is defined in that single file. No build step needed.

**Does it work with Cursor / other Claude integrations?**

HardGPT is built as a Claude Code plugin. Compatibility with other Claude integrations depends on their plugin support. For Cursor, you can use the `SKILL.md` file directly as an agent skill.

## Contributing

Issues and PRs welcome. If you have ideas for improving the research workflow, please [open an issue](https://github.com/woody-design/hardgpt-deep-research/issues).

## License

This project is licensed under [CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/) — free for non-commercial use with attribution. You may share and adapt this work, but not for commercial purposes, and any derivatives must use the same license.

For commercial licensing, visit [woodydesign.io](https://woodydesign.io).