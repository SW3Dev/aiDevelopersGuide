# The Software 3.0 Developer Guide
### A practical guideline for AI developers based on Andrej Karpathy's talks on the future of software

---

## About This Document

This guide synthesises the key insights, practical methods, and strategic framework drawn from Andrej Karpathy's recent public talks on the future of software development and AI — including a keynote delivered at a developer conference in early 2026 and related commentary. Karpathy co-founded OpenAI, built Tesla's Autopilot system, and coined the term "vibe coding." He is one of the most credible and widely followed voices on how AI is changing the practice of software development.

His central argument is that we are not in a faster version of software development. We are in a fundamentally different computing paradigm — one that renders a significant portion of current development practice obsolete and opens up entirely new categories of what can be built.

This document uses Karpathy's talks as its foundation and expands where relevant with related best practices from the broader AI development community. Where a point originates with Karpathy directly, it is attributed. Where the guide expands beyond the source material, it is written as general guidance.

The guide is organised as follows:

1. **The Context** — what has changed and why it matters
2. **Key Principles** — the mental models every AI developer needs
3. **Practical Methods** — specific how-tos, tests, and step-by-step procedures
4. **The Framework** — a four-phase cycle for building in the Software 3.0 era
5. **Quick Reference** — a condensed table for day-to-day use
6. **Glossary** — definitions of key terms used throughout

A note on pace: the field is moving fast enough that specific model names and time references age quickly. This guide is written around durable principles and methods rather than point-in-time benchmarks. Treat it as a living document and revisit it as the frontier advances.

---

## Section 1: The Context — What Has Changed

### The December Inflection Point

Around December 2025, something qualitatively shifted in agentic AI tools. Karpathy describes sitting down during a break with the latest models and noticing that the output from end-to-end agentic workflows simply came out right — consistently, without requiring correction. He stopped editing. He started trusting the system. He entered what he calls a "vibe coding bender," accumulating a folder full of side projects.

This was not a gradual improvement. It was a step change — particularly in the coherence and reliability of multi-step agentic workflows. Karpathy stresses that many developers still carry a mental model of AI shaped by ChatGPT-adjacent experiences from 2023–24. That model is out of date. If you have not seriously attempted to build something end-to-end with an agentic tool — Claude Code, Cursor, Codex in agent mode, or similar — since that shift, your understanding of current capability is behind. The most important thing you can do is go build something.

### Software 1.0 → 2.0 → 3.0

Karpathy's framework for the evolution of software:

| Version | Paradigm | How you program |
|---|---|---|
| Software 1.0 | Explicit rules | Writing code by hand |
| Software 2.0 | Learned weights | Curating datasets and training neural networks |
| Software 3.0 | LLM as interpreter | Prompting; the context window is your lever |

In Software 3.0, the large language model *is* the programmable computer. Your prompt is the code. Your context window is how you control execution. Karpathy is explicit that this is not simply about programming becoming faster — it is about a broader category of information processing that is now automatable: things that are not even programs in the traditional sense, because they work over unstructured information in ways that no prior code could handle.

His example: an LLM knowledge base that generates wikis for your organisation on demand. This is not a faster version of a database. It is something that could not have existed before, because there was no code capable of doing it.

### Why This Is Uncomfortable

A large proportion of applications being built right now should not exist. They are Software 1.0 plumbing — orchestration layers, API wrappers, UI shells — wrapped around things a model can now do natively with a single prompt and a tool call or two.

Karpathy's own application, Menu Gen, illustrated this. He built a full application that took a photo of a restaurant menu and generated images of each dish, involving OCR, an image generation pipeline, a Vercel deployment, and DNS configuration. Some time later, he saw the Software 3.0 version: give the photo directly to a multimodal model, ask it to use an image generation tool to overlay pictures of the dishes onto the menu — and receive back a single image with everything rendered. The entire application had become a single prompt. It was not badly built. The paradigm had simply changed around it.

The uncomfortable implication is that many developers are currently building the equivalent of Menu Gen. Shipping them, then watching them become obsolete within months, is a worse outcome than identifying this now and pivoting.

### Where This Is Going

Karpathy's forward view is that we are moving toward a world in which agents have genuine representation for people and organisations — where scheduling a meeting, negotiating terms, or coordinating tasks happens agent-to-agent, not person-to-person. The infrastructure implications of this are significant: everything that currently assumes a human at one end of an interaction will need to be redesigned.

This is not a near-term reality for most teams, but it is the direction of travel, and it should inform the infrastructure and API design decisions being made today.

---

## Section 2: Key Principles

### Principle 1: The Model Does More of the Work Now

Stop thinking about AI as a speed-up for existing workflows. Think instead about what is *newly possible* — things that could not have existed before because no traditional code could do them. LLM-generated knowledge bases, intelligent agents that inspect and adapt to their environment, dynamic document synthesis, workflows that operate over unstructured language rather than structured data — these are Software 3.0-native ideas.

The right question is not "how do I use AI to do this faster?" It is "what computing paradigm does this problem belong to, and am I solving it in the right one?"

### Principle 2: Verifiability Is the Moat

Models excel at code because code is deterministic and verifiable. The feedback loop is tight: run the code, see if it works, update. The same principle points toward where durable competitive advantages can be built.

Domains where outputs are objectively measurable — correct or incorrect, faster or slower, better or worse — are domains where reinforcement learning can be applied effectively and where fine-tuned models can be meaningfully superior to general-purpose ones. Financial trading signal evaluation, supply chain routing, data labeling quality, CI/CD pipeline health, regulatory compliance checking: in niches like these, you can build a reinforcement learning environment, fine-tune a model, and own a capability that the frontier labs are not going to specifically target.

### Principle 3: Everything Is Still Built for Humans

The entire internet — documentation, dashboards, install flows, DNS settings, APIs — is designed for human eyes and human hands. Agents arriving at a product waste significant time and capability parsing marketing copy, navigating human-oriented UIs, and inferring structure that was never made explicit.

The shift to agent-native infrastructure has barely begun. A useful mental model from Karpathy: think about workloads in terms of *sensors* (how an agent perceives the world — reads data, understands context) and *actuators* (how an agent acts on the world — calls APIs, modifies state, triggers processes). Designing for agents means making both as clean and legible as possible.

### Principle 4: You Can Outsource Execution, Not Understanding

As agents take over more execution, the bottleneck shifts to direction. Knowing what to build and why, being able to evaluate what the agent produced, recognising when it has gone wrong, and knowing how to correct it — these become the scarcest and most valuable resources. Deep domain knowledge and genuine understanding of your field compound in value as execution becomes cheap.

Karpathy noted a tweet that stayed with him: *"You can outsource your thinking but you can't outsource your understanding."* His observation was that he increasingly felt like the bottleneck in his own systems — not because of execution, but because understanding is what determines the quality of direction. You cannot be a good director of agents without genuinely understanding the domain you are directing them in.

### Principle 5: Vibe Coding Has a Ceiling

Vibe coding raised the floor. Almost anyone can build now, and that democratisation is real and valuable. But professionals operating in production environments are practising something Karpathy calls *agentic engineering* — a more disciplined approach involving specs written before work begins, structured code review, test coverage, and CI enforcement.

The 10x speed gains that Karpathy attributes to strong practitioners come from the combination of capable tools and disciplined practice — not from prompt volume. There is also significant hype on social media about running 10–20 agents simultaneously. Karpathy's own experience, and the experience of practitioners who are genuinely good at this, suggests 3–4 concurrent agents is the practical limit for someone who reviews the output before it touches production. The bottleneck is human review bandwidth, not technical capacity. If you feel behind because you are not running 20 agents at once, you are measuring yourself against an inflated benchmark.

### Principle 6: LLMs Are Ghosts, Not Animals

Karpathy has written about the importance of having an accurate mental model of what LLMs are — and specifically what they are not. He describes them as "ghosts" rather than "animals": not intelligences shaped by evolution, embodiment, intrinsic motivation, curiosity, or survival. They are statistical systems shaped by pre-training data and refined by reinforcement learning.

Karpathy himself notes this framing is somewhat philosophical and he is not certain of its practical implications — but the orientation is useful. Treating an LLM as though emotional pressure, persuasion, or rapport will improve its output is a category error. More practically: LLMs have *jagged* capability profiles. They can be remarkably capable on some tasks and inexplicably poor on adjacent ones. Karpathy tried repeatedly to prompt a model to simplify a training codebase and found it simply could not — it felt, he said, like pulling teeth, clearly outside the model's RL circuits. Developers should expect and plan for these hard edges rather than assume linear capability across a task space.

Agent-produced code also tends to be functional but inelegant — bloated, copy-paste heavy, with brittle abstractions. This is a current limitation of the RL training process, not a fundamental property of LLMs, but it has real implications for code review practice today.

---

## Section 3: Practical Methods

### 3.1 The Menu Gen Test — Evaluating Whether to Build

Before committing to any project, run this two-part test. It is designed to catch both the projects you should kill and the ones worth pursuing.

**Part A — The kill test:**
Could this be replaced by a single multimodal prompt plus one or two tool calls or an MCP integration?
- If **yes** → stop or pivot. You are building plumbing that the next model release will absorb. This applies regardless of how well-built or differentiated the application feels today.

**Part B — The build test:**
Does this only exist because of Software 3.0 capabilities — things that genuinely could not have been built before LLMs?
- If **yes** → this is worth pursuing. You are working in the right paradigm.
- If **no** → you may be building a faster version of something that already existed, which is a weaker position.

Apply this test to every active project and project idea. Repeat it at every major model release — what passes today may fail in three months as model capabilities expand. Note that the test has two directions: Part A eliminates what shouldn't be built; Part B filters toward what should.

### 3.2 Building and Using a Knowledge Brain

A knowledge brain is a folder of structured markdown documents, generated and maintained through an agent, that captures your company, product domain, strategic context, goals, and accumulated thinking. It serves two distinct purposes: as a strategic advisor (keeping you focused and filtering opportunities) and as a personal understanding repository (compounding your reading and thinking over time). These uses are complementary and share the same underlying structure.

This is distinct from general AI chat. The value is accumulated context that persists and grows, rather than being reset each session.

**Setting it up:**

1. Choose your agent environment — Claude Code, Cursor, or any agentic tool with file access
2. Create a dedicated folder for the documents
3. Write an initial context prompt describing your company, product, domain, and goals in as much detail as you can
4. Ask the agent to generate a set of foundational documents from that context: market positioning, technical direction, opportunity map, risk register, or whatever fits your situation
5. Save all outputs as markdown files in the folder
6. Feed it articles and resources you read; ask the agent to update relevant sections and surface connections
7. Regularly ask it to generate new projections on the same information: different angles, analogies, counterarguments, gap analyses

**Using it day-to-day:**

- **Strategic filtering:** Before pursuing a new project or opportunity, run it past the brain — "Here is what I am considering. How does it fit with where I am going? What am I missing?"
- **Content and context:** When generating any output (docs, plans, communications), provide the brain as context so the agent understands your world, not just the immediate topic
- **Understanding development:** Ask "What do I now know about X? What are the gaps? What should I be reading?" — use it to identify the edges of your own knowledge
- **Focus maintenance:** Let it flag when a proposed direction contradicts your stated goals or introduces scope that doesn't serve your core thesis

Karpathy describes this kind of knowledge base as among the most powerful tools he has built for himself — not because it speeds up execution, but because it enhances and preserves understanding.

### 3.3 The Software 3.0 Setup Pattern

When setting up a system, tool, or environment, write a block of natural-language instructions designed to be given to an agent — not a shell script designed for a human to run.

**The reasoning:** A shell script must precisely specify every step and breaks on edge cases or environmental variation. An agent given natural-language instructions uses its own intelligence to inspect the environment, handle variations, debug in the loop, and make things work without hand-holding. This is a fundamentally more powerful approach in the Software 3.0 paradigm.

**The question to ask:** *What is the text I copy-paste to my agent?* That is the new script.

This principle extends to deployment. The benchmark for agent-native infrastructure: could an agent set up DNS, configure services, and deploy this end-to-end without a human touching any setting? If not, the infrastructure is not yet agent-native. For the broader picture of how to design that infrastructure, see Section 3.5.

### 3.4 Agentic Engineering Workflow

Agentic engineering is what professionals do at production scale — it is the discipline that sits between vibe coding (useful for exploration) and the rigour needed for systems that matter.

**Before handing off to an agent:**
- Write a spec and plan. Define what "done" looks like before the agent starts. Ambiguous briefs produce ambiguous outputs.
- Scope each task tightly. One agent, one contained objective.
- Establish what a passing result looks like — what tests should pass, what behaviour should be observable, what the output should include.

**During agent work:**
- Manage your context window actively. Stale or bloated context degrades output quality significantly.
- Run 3–4 agents in parallel at most. This limit is about *human review bandwidth*, not technical capacity. More concurrent agents than you can properly review creates a false sense of productivity while accumulating debt.
- Give each agent a scoped task and check in regularly rather than letting it run open-endedly.
- Provide your knowledge brain as context where domain relevance matters — agents with accumulated domain context produce more coherent, on-strategy outputs (see Section 3.2).

**After agent work — reviewing the output:**
- Treat agent output as a draft, not a deployment. Review code before it touches production systems.
- Watch specifically for: bloated implementations with excessive copy-paste, brittle abstractions that work now but will break under change, logic errors that are functionally invisible but semantically wrong. Models produce working code more reliably than elegant code.
- Maintain unit-level smoke tests, end-to-end tests, and CI blockers. Automated gates that prevent bad code from reaching production are more reliable than manual review alone — and they apply regardless of whether the code was written by a human or an agent.

### 3.5 Building Agent-First Infrastructure

The shift from human-first to agent-first infrastructure is one of the largest practical opportunities in the current moment. The approach differs slightly for external products versus internal tooling.

**Mental model — sensors and actuators:**
Think about what an agent needs to function: *sensors* (ways to perceive and read the world — data access, context, state) and *actuators* (ways to act on the world — API calls, state mutations, process triggers). Agent-first infrastructure makes both as clean, explicit, and well-documented as possible.

**For external-facing products:**
- Add an `llms.txt` file to your website or product. This is a plain-text file (analogous to `robots.txt`) placed at the root of your domain that tells agents, in structured natural language, what your product does, how your API works, what tools are available, and how to trust and interact with your service — without requiring them to parse marketing copy. The specification is open and increasingly adopted.
- Design documentation as agent-readable first: clear structure, no assumed context, direct instruction format, explicit examples
- Expose core functionality via MCP, clean REST or GraphQL APIs, or agent-compatible tool calls — not only through human UIs that require navigation and visual interpretation
- Ask: *when an agent arrives at my product, can it understand what to do within a single context window, without human translation?*

**For internal tooling:**
- Strip human UI wherever an agent, not a person, is the primary consumer
- Design data structures to be LLM-legible: descriptive field names, explicit schemas, consistent formats, no reliance on visual layout to convey meaning
- Write internal documentation in the format you would use to brief an agent, not in the format you would use to onboard a new employee
- Test agent-native readiness end-to-end: can an agent complete the primary workflow without a human mediating any step?

### 3.6 Finding and Owning a Verifiable Niche

The frontier labs are applying enormous resources to general capability. They are not, and cannot be, applying deep RL to every domain-specific niche. This is where individual developers and small teams have a genuine structural advantage.

**Step 1 — Map your expertise.**
List the domains you understand deeply: industries, workflows, functional areas, or technical specialisations where you have real knowledge that is not widely held.

**Step 2 — Apply the verifiability filter.**
For each domain, ask: can outputs be objectively evaluated? Can you measure correct versus incorrect, better versus worse, faster versus slower? Domains without clear verifiability are harder to train against and harder to defend. Domains with verifiable outputs can support RL environments with real feedback signals.

**Step 3 — Check lab coverage.**
Are any of the major frontier labs specifically applying RL resources to this niche? If yes, competing on general capability is difficult. If no, you have a timing window.

**Step 4 — Map the RL environment.**
What would reward and penalty look like in your domain? What data do you have access to, or could you generate? What does "better" mean concretely to a model training on this task? This thinking should precede any building — a poorly defined reward function produces a poorly aligned model.

**Step 5 — Start narrow before training.**
Before investing in fine-tuning, validate the niche with a well-prompted specialised agent using strong system prompts and domain context. If a general model with the right context produces genuinely useful outputs, you have confirmed the niche is real. Fine-tuning is the next step to deepen and own the capability — but it is a significant investment and should follow, not precede, validation.

**Step 6 — Build, fine-tune, and own the capability.**
The defensible moat in this paradigm is not the application layer — it is the trained capability. An application can be replicated; a fine-tuned model with proprietary training data and a well-designed RL environment is considerably harder to replicate.

**Examples with opportunity:** financial trading signal evaluation, supply chain routing optimisation, regulatory compliance and audit checking, CI/CD pipeline health and failure classification, data labeling quality assessment, domain-specific code review (legal, scientific, medical).

---

## Section 4: The Four-Phase Framework

This framework organises the principles and methods above into a practical cycle for AI developers. The phases are sequential on first pass and then become a continuous loop — Phase 4 feeds back into Phase 1 at every model release cycle. The cycle, not the linear pass, is the operating model.

The knowledge brain described in Section 3.2 is a continuous practice that runs across all four phases. It is not specific to any single phase — it supports auditing (Phase 1), focusing (Phase 2), building (Phase 3), and understanding (Phase 4) equally.

```
Phase 1: Audit → Phase 2: Orient → Phase 3: Build → Phase 4: Stay Sharp → back to Phase 1
```

---

### Phase 1 — Audit: Does Your App Deserve to Exist?

**Goal:** Ruthlessly evaluate what you are building before investing further.

**Actions:**
- Apply the Menu Gen test (Section 3.1) to every active project and project idea
- Kill or pivot anything that is Software 1.0 plumbing — API orchestration, UI shells — around things the model now does natively
- Double down on anything that passes: projects that only exist because of Software 3.0 capabilities, that embed genuine domain expertise or proprietary context, and that solve something the model alone cannot

**Mindset:** This is uncomfortable. Developers who have applied this test honestly have found that a meaningful proportion of their active projects do not survive it. Killing a project that fails the test is a better outcome than shipping it and watching it become obsolete. The goal is to direct effort toward what will still matter after the next model release.

**Cadence:** Run this audit at every significant model release, not just once.

**Supported by:** Knowledge brain (Section 3.2) — use it to evaluate fit with your direction before committing to anything new.

---

### Phase 2 — Orient: Find Your Verifiable Niche

**Goal:** Identify where you have a durable edge that frontier labs will not cover.

**Actions:**
- Map your domain expertise against verifiability: where can outputs be objectively measured? (See Section 3.6 for the full six-step process)
- Identify niches the big labs are not focusing RL resources on
- Develop a clear thesis: what are you building, why does it pass the Software 3.0 test, and what verifiable capability makes it defensible over time?

**Output of this phase:** A focused direction that you can defend against the Menu Gen test and that exploits a gap the frontier labs are not filling.

**Supported by:** Knowledge brain (Section 3.2) — use it as a focus filter to flag drift and stress-test your thesis.

---

### Phase 3 — Build: Agent-First from the Start

**Goal:** Build in the Software 3.0 paradigm — not the Software 1.0 paradigm with AI bolted on.

**Actions:**
- Apply agentic engineering discipline throughout: spec first, structured review, CI enforcement, active context window management (see Section 3.4 for the full workflow)
- Design every interface, API, and deployment workflow to be agent-native from day one (see Section 3.5)
- Add `llms.txt` and machine-legible documentation before launch, not as an afterthought
- Use the Software 3.0 setup pattern for configuration and deployment (Section 3.3)
- Benchmark continuously: *can an agent use this without human translation at any step?*

**The shift in thinking:** Stop asking "how do I make this faster with AI?" Start asking "what computing paradigm does this problem belong to, and am I building it correctly for that paradigm?"

**Supported by:** Knowledge brain (Section 3.2) — provide it as context to agents during build to ensure outputs are coherent with your domain and goals.

---

### Phase 4 — Stay Sharp: Protect Your Understanding

**Goal:** Maintain and compound the understanding that makes you a capable director of agents.

**Actions:**
- Actively use your knowledge brain to compound your reading and thinking — every article you consume should feed back into your understanding repository (Section 3.2)
- Invest in genuine depth in your domain: this is what allows you to evaluate agent output accurately, catch errors, and course-correct effectively
- Skate to where the puck is going: build for capabilities 3–6 months ahead of today's baseline. The agentic harnesses that feel unreliable today will reach their own inflection point — design for that state, not the current one
- Return to Phase 1 at every significant model release

**The principle:** Execution is being commoditised. Direction and understanding are becoming more valuable, not less. You can outsource execution to agents. You cannot outsource the understanding that makes their output useful.

---

## Section 5: Quick Reference

### Strategic Tests

| Situation | The test or question |
|---|---|
| Evaluating a project idea | Can this be replaced by one multimodal prompt + one or two tool calls? |
| Checking for Software 3.0 validity | Does this only exist because of LLMs — could it not have been built before? |
| Assessing agent-native readiness | Can an agent deploy, configure, and use this without human translation at any step? |
| Finding a niche | Where do I have domain expertise + verifiable outputs + no frontier lab RL focus? |
| Protecting understanding | Am I outsourcing execution, or am I outsourcing understanding? |
| Deciding on setup approach | What is the text I copy-paste to my agent? |
| Evaluating agent output | Can I assess whether this is good — do I know what "good" looks like in this domain? |

### Agentic Engineering Checklist

| Stage | Action |
|---|---|
| Before | Write a spec. Define "done" before the agent starts. |
| Before | Scope tightly. One agent, one contained objective. |
| Before | Establish pass/fail criteria — tests, expected outputs. |
| During | Manage the context window. Remove stale context actively. |
| During | Cap parallel agents at 3–4 (human review bandwidth, not technical limit). |
| During | Check in regularly rather than letting agents run open-endedly. |
| During | Provide knowledge brain as context where domain relevance matters. |
| After | Review code as a draft, not a deployment. |
| After | Watch for: bloat, copy-paste, brittle abstractions, logic errors. |
| After | CI blockers and automated tests gate production — not manual review alone. |

---

## Section 6: Glossary

**Software 3.0** — The computing paradigm in which the LLM is the interpreter, the prompt is the code, and the context window is the lever. Contrasted with Software 1.0 (hand-written rules) and Software 2.0 (neural network training via curated datasets). Term and framework from Karpathy.

**Vibe coding** — Building by prompting an AI agent and accepting its output with minimal correction, relying on the model's capability rather than hand-writing code. Coined by Karpathy. Valuable for exploration and rapid prototyping; insufficient as a sole practice for production systems.

**Agentic engineering** — The disciplined practice of building with AI agents at production scale: spec-first development, structured code review, test coverage, CI enforcement, and active context window management. What Karpathy identifies as the professional evolution beyond vibe coding.

**Menu Gen test** — A two-part test for whether an application deserves to exist. Part A (kill test): can a single prompt and tool calls replace it? Part B (build test): does it only exist because of Software 3.0 capabilities? Named after Karpathy's own Menu Gen app, which failed its own test.

**Knowledge brain** — A folder of structured markdown documents, generated and maintained through an agent, capturing domain knowledge, strategic context, goals, and accumulated thinking. Used both as a strategic advisor and as a personal understanding repository. Sometimes referred to as a "strategy brain" or "LLM knowledge base" depending on emphasis.

**Agent-native / agent-first** — Infrastructure, APIs, and documentation designed with agents as the primary consumer rather than humans. Includes `llms.txt` files, machine-legible docs, explicit schemas, and deployment workflows an agent can execute without human mediation.

**`llms.txt`** — A plain-text file placed at the root of a domain (analogous to `robots.txt`) that tells AI agents, in structured natural language, what a product does, how its API works, and how to interact with it. An open specification designed to make web products legible to agents without requiring them to parse human-oriented marketing content.

**Verifiable niche** — A domain where outputs can be objectively evaluated (correct/incorrect, better/worse, faster/slower), enabling effective reinforcement learning. The basis for building defensible AI capabilities in areas the frontier labs are not specifically targeting.

**Sensors and actuators** — Karpathy's framing for agent architecture: sensors are the ways an agent perceives and reads the world (data access, context retrieval, state observation); actuators are the ways it acts on the world (API calls, state mutations, process triggers). Agent-first design optimises both.

**December inflection** — The term used in this guide for the step-change in agentic AI reliability that occurred around December 2025, when end-to-end agentic workflows became consistently trustworthy without requiring constant correction. Based on Karpathy's description of his own experience at that time. A reference point for the shift from AI-assisted to AI-native development.

**Jagged intelligence** — The uneven capability profile of current LLMs: highly capable on some tasks, inexplicably limited on adjacent ones. Relevant to production engineering because it means capability does not scale linearly across a task space — developers should plan for hard edges rather than assume consistent performance.

**10x claim** — Karpathy's observation that practitioners who are good at agentic engineering achieve roughly 10x development speed. Attributed to the combination of capable tools and disciplined practice, not prompt volume alone. The practical ceiling on parallelism (3–4 agents) is a human review bandwidth constraint, not a technical one.

---

*This document is based on Andrej Karpathy's public talks on Software 3.0 and agentic development (2026), synthesised and expanded in collaboration with Claude (Anthropic). It is intended as a living reference: the core paradigm shifts described here are durable, but specific tool recommendations and capability benchmarks should be revisited as the field evolves. Readers are encouraged to apply their own judgement, particularly where the guide expands beyond Karpathy's direct statements into broader best practice.*
