# Software 3.0 Developer Guide — Concise Edition
*Based on Karpathy's framework for AI-native development*

---

## The Paradigm Shift

| | What it is | How you program |
|---|---|---|
| SW 1.0 | Explicit rules | Write code |
| SW 2.0 | Learned weights | Curate datasets, train networks |
| SW 3.0 | LLM as interpreter | Prompt; context window is the lever |

**The inflection:** ~Dec 2025, agentic workflows became reliably trustworthy end-to-end. If you haven't built something agentic since then, your mental model is outdated.

**The uncomfortable truth:** Most apps being built now shouldn't exist. They're SW 1.0 plumbing around things a prompt can do. Karpathy's own Menu Gen app — OCR + image gen + Vercel deployment — became a single multimodal prompt. Same will happen to yours.

---

## 6 Principles

**1. New paradigm, not faster old one.**
Don't ask "how do I use AI to do this faster?" Ask "what computing paradigm does this belong to?"

**2. Verifiability is the moat.**
Models excel where outputs are objectively measurable. That's where RL works, fine-tuning is defensible, and frontier labs can't cover every niche.

**3. Everything is still built for humans.**
Agents need sensors (read the world) and actuators (act on the world). Design for those — not for human eyes.

**4. Outsource execution, not understanding.**
Direction quality is now the scarce resource. You can't direct well without genuine domain depth.

**5. Vibe coding has a ceiling.**
Great for exploration. Production needs agentic engineering: spec-first, structured review, tests, CI. 3–4 parallel agents max (human review bottleneck, not technical).

**6. Ghosts, not animals.**
LLMs are statistical circuits shaped by pre-training + RL. Not animal intelligences. Capability is jagged — hard edges exist. Agent code is often functional but bloated and brittle; review accordingly.

---

## The Cycle

```
① Audit → ② Orient → ③ Build → ④ Stay Sharp → ↻ repeat each model release
```

---

## Phase 1 — Audit

**Kill test (Part A):** Can this be replaced by one multimodal prompt + 1–2 tool calls?
- YES → stop or pivot. Plumbing the next release will absorb.

**Build test (Part B):** Does this only exist because of SW 3.0 — impossible before LLMs?
- YES → proceed. Embed domain expertise or proprietary context the model can't replicate alone.

**Cadence:** Re-run at every major model release.

---

## Phase 2 — Orient

**Finding a verifiable niche — 6 steps:**

1. List domains where you have genuine deep expertise
2. Confirm outputs are objectively verifiable (correct/incorrect, better/worse)
3. Check: are frontier labs applying RL here? If no → window is open
4. Map the RL environment: reward, penalty, what "better" means concretely
5. Validate with a well-prompted agent *before* committing to fine-tuning
6. Build, fine-tune, own the capability — the moat is the trained model, not the app layer

**Knowledge brain setup:**
1. Create a folder for strategy/knowledge docs
2. Write an initial context prompt: company, product, domain, goals
3. Generate foundational markdown docs via agent (positioning, direction, opportunity map)
4. Feed it every article you read; ask for new projections on the same data
5. Run every new idea past it before committing

---

## Phase 3 — Build

**Before handing off:**
- Write a spec. Define "done" before the agent starts.
- Scope tightly. One agent, one contained objective.
- Define pass/fail criteria — tests, expected outputs.
- Ask: *what is the text I copy-paste to my agent?* (Not a script for a human.)

**While running:**
- Actively manage context window. Remove stale context.
- ≤ 3–4 parallel agents (review bandwidth, not technical limit).
- Check in regularly; no open-ended mandates.

**After — reviewing output:**
- It's a draft, not a deployment.
- Watch for: bloat, copy-paste, brittle abstractions, silent logic errors.
- Unit tests + smoke tests must pass.
- CI blockers gate production — not manual review alone.

**Agent-first infrastructure:**

*External product:*
- `llms.txt` at root — tells agents what you do, how your API works, how to trust you (open spec, analogous to `robots.txt`)
- Docs are agent-readable: clear structure, no assumed context, direct instruction format
- Core functionality via MCP, clean API, or tool calls — not just human UI
- Test: can an agent use this within one context window, no human translation?

*Internal tooling:*
- Strip human UI where agents are the consumer
- LLM-legible data: descriptive field names, explicit schemas, no visual-layout dependency
- Write docs as agent briefs, not employee onboarding
- Benchmark: agent completes primary workflow end-to-end, no human mediation

---

## Phase 4 — Stay Sharp

- Knowledge brain is actively fed — reading → agent updates relevant sections
- Regularly ask: "What do I know about X? Gaps? What to read next?"
- Can critically evaluate agent output — know what "good" looks like in your domain
- Building for capabilities 3–6 months ahead, not today's baseline
- Phase 1 audit scheduled for next model release

---

## Quick Reference

| Test | Question |
|---|---|
| Kill | Can one prompt + tool calls replace this? |
| Build | Does this only exist because of LLMs? |
| Agent-native | Can an agent deploy and use this without human translation? |
| Niche | Domain expertise + verifiable outputs + no lab RL coverage? |
| Understanding | Outsourcing execution or outsourcing understanding? |
| Setup | What's the text I copy-paste to my agent? |
| Direction | Can I evaluate what the agent produced — do I know what good looks like? |

---

## Glossary

**SW 3.0** — LLM as interpreter; prompt = code; context window = lever.
**Vibe coding** — Accept agent output with minimal correction. Good for exploration; insufficient for production.
**Agentic engineering** — Spec-first, structured review, tests, CI. Professional practice at production scale.
**Menu Gen test** — Two-part kill/build test for whether an app deserves to exist.
**Knowledge brain** — Folder of agent-maintained markdown docs capturing domain, strategy, and accumulated thinking. Used as advisor and understanding repository.
**Agent-native** — Infrastructure designed for agents as consumers: `llms.txt`, LLM-legible schemas, no human UI dependency.
**`llms.txt`** — Plain-text file at domain root (like `robots.txt`) telling agents what a product does and how to use it.
**Verifiable niche** — Domain with objectively measurable outputs; supports RL and defensible fine-tuning.
**Sensors/actuators** — Agent architecture framing: sensors = perceive world; actuators = act on world.
**Jagged intelligence** — LLM capability is uneven. Highly capable on some tasks, hard edges on adjacent ones. Plan for both.
**December inflection** — ~Dec 2025 step-change when agentic end-to-end workflows became consistently reliable without requiring correction. The reference point for the current AI-native development era. Described by Karpathy; the label is used in this guide.
**10x claim** — Karpathy's observation that strong agentic engineering practitioners achieve ~10x speed. From tools + discipline combined, not prompt volume. Practical parallel-agent ceiling (3–4) is a review bandwidth constraint, not technical.

---

*Based on Karpathy's public talks on SW 3.0 and agentic development (2026). Living document — revisit at each model release.*
