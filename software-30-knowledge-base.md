# KNOWLEDGE BASE: Software 3.0 Developer Framework
<!-- kb:domain=ai-development kb:source=karpathy-talks-2026 kb:type=framework kb:version=1.0 -->

## Document Purpose and Usage

This document is structured for retrieval by an AI assistant working on software development projects. It encodes a framework for evaluating, designing, and building AI-native software based on Andrej Karpathy's Software 3.0 paradigm. Reference this document when:

- Evaluating whether a project or feature idea is worth building
- Advising on AI-native architecture or infrastructure design
- Reviewing agentic engineering workflows
- Helping a developer find a defensible niche for an AI product
- Discussing the shift from traditional software to LLM-native development

**Source:** Andrej Karpathy's public talks on Software 3.0 and agentic development (2026). Expanded with related best practices. Where a point originates with Karpathy directly, it is attributed. Expansions are noted as general guidance.

---

## Core Concept: The Software Paradigm Shift

### Paradigm Definitions

| Label | Paradigm | Programming Model |
|---|---|---|
| Software 1.0 | Explicit rules | Hand-written code operating over structured data |
| Software 2.0 | Learned weights | Curating datasets and training neural networks |
| Software 3.0 | LLM as interpreter | Prompting; the context window is the control lever |

### Key Properties of Software 3.0

- The LLM **is** the programmable computer
- The prompt **is** the code
- The context window **is** how execution is controlled
- Enables processing of unstructured information in ways traditional code cannot
- Not just faster development — a categorically different set of things can be built

### The December 2025 Inflection Point (Karpathy)

- Around December 2025, agentic workflow outputs became consistently reliable without requiring correction
- Qualitative step-change, not gradual improvement — particularly in end-to-end coherence
- Many developers still carry a pre-December mental model; that model is outdated
- Implication: if a developer has not built something end-to-end with an agentic tool since this point, their capability assessment is stale

---

## Core Concept: The Menu Gen Problem

### Definition

The "Menu Gen problem" refers to building applications that orchestrate what a single multimodal prompt can now accomplish natively.

### Origin (Karpathy)

Karpathy built "Menu Gen": an application that photographed restaurant menus and generated images of each dish, involving OCR, image generation pipeline, Vercel deployment, and DNS configuration. The same outcome later became achievable with a single multimodal prompt asking a model to overlay dish images onto the menu photo. The entire application had been rendered obsolete by a model capability update.

### Implication

A large proportion of applications currently being built are Software 1.0 plumbing — orchestration layers, API wrappers, UI shells — around things models can now do natively. These will be absorbed by future model releases.

---

## Decision Framework: The Menu Gen Test

### Purpose

Evaluate whether a project or feature deserves to be built before committing resources.

### Part A — The Kill Test

**Question:** Could this be replaced by a single multimodal prompt plus one or two tool calls or an MCP integration?

- Answer YES → stop or pivot. This is plumbing the next model release will absorb.
- Answer NO → proceed to Part B.

### Part B — The Build Test

**Question:** Does this only exist because of Software 3.0 capabilities — things genuinely impossible before LLMs?

- Answer YES → worth pursuing. Should also embed domain expertise or proprietary context the model cannot replicate alone.
- Answer NO → weak position. May be building a faster version of something that already existed.

### Cadence

Re-run at every significant model release. What passes the test today may fail in three months.

### Examples That Pass

- LLM-generated knowledge bases / dynamic wikis
- Agents that inspect and adapt to their own environment
- Workflows operating over unstructured language rather than structured data
- Systems that synthesise information across unstructured sources on demand

### Examples That Fail

- UI wrapper around a single API call the model could make directly
- Orchestration layer between a user and a model capability that already exists natively
- App that formats or routes content a prompt could handle in one step

---

## Decision Framework: Finding a Verifiable Niche

### Core Principle

Frontier labs apply RL to broad domains. They cannot apply it to every industry-specific niche. Domains with verifiable outputs are defensible because RL can be applied effectively and fine-tuned models can be meaningfully superior to general-purpose ones.

### Why Verifiability Matters

Models excel at code because code is deterministic and verifiable — the feedback loop is tight. The same applies to any domain: measurable correctness enables effective training and creates a moat.

### 6-Step Process

1. **List expertise domains** — industries, workflows, functions, or technical specialisations with genuine deep knowledge
2. **Apply verifiability filter** — can outputs be objectively evaluated? (correct/incorrect, better/worse, faster/slower) If no clear verifiability → weaker position
3. **Check lab coverage** — are frontier labs specifically applying RL to this niche? If no → timing window is open
4. **Map the RL environment** — define reward, penalty, and what "better" means concretely; identify available training data
5. **Validate before fine-tuning** — confirm the niche with a well-prompted general agent first; fine-tuning is a significant investment and should follow validation, not precede it
6. **Build, fine-tune, own** — the defensible moat is the trained capability, not the application layer

### Example Verifiable Niches (with opportunity as of 2025)

- Financial trading signal evaluation
- Supply chain routing optimisation
- Regulatory compliance and audit checking
- CI/CD pipeline health and failure classification
- Data labeling quality assessment
- Domain-specific code review (legal, scientific, medical)

---

## Framework: The Four-Phase Development Cycle

### Overview

The phases are sequential on first pass, then become a continuous loop. The cycle is the operating model, not a one-time completion.

```
Phase 1: Audit → Phase 2: Orient → Phase 3: Build → Phase 4: Stay Sharp → ↻ back to Phase 1
```

### The Knowledge Brain (runs across all phases)

A knowledge brain is a folder of structured markdown documents, generated and maintained through an agent, capturing domain knowledge, strategic context, goals, and accumulated thinking. It is not phase-specific — it supports all four phases.

**Setup:**
1. Create a dedicated folder for strategy/knowledge documents
2. Write an initial context prompt: company, product, domain, goals — in detail
3. Generate foundational docs via agent (market positioning, technical direction, opportunity map, risk register) as markdown files
4. Feed it articles and resources continuously; agent updates relevant sections
5. Regularly ask it to generate new projections: different angles, analogies, counterarguments, gap analyses

**Usage patterns:**
- Strategic filtering: "Here is what I'm considering — how does it fit with where I'm going?"
- Understanding development: "What do I know about X? What are the gaps? What should I read next?"
- Focus maintenance: flag drift from stated goals
- Context provision: supply as context to agents during builds for domain-coherent outputs

---

### Phase 1: Audit — Does the App Deserve to Exist?

**Goal:** Evaluate all active and proposed projects against the Menu Gen test before investing further.

**Actions:**
- Apply Menu Gen test (Part A and B) to every active project and new idea
- Kill or pivot anything that is Software 1.0 plumbing around natively-available model capabilities
- Double down on projects that pass: only exist because of SW 3.0, embed genuine domain expertise, solve something the model alone cannot

**Mindset:** Killing a project that fails the test is a better outcome than shipping it and watching it become obsolete.

**Cadence:** At every significant model release.

---

### Phase 2: Orient — Find the Verifiable Niche

**Goal:** Identify a durable edge that frontier labs will not cover.

**Actions:**
- Run the 6-step verifiable niche process (see above)
- Develop a clear thesis: what is being built, why it passes the SW 3.0 test, what verifiable capability makes it defensible
- Use knowledge brain as a focus filter to flag drift

**Output:** A focused direction defensible against the Menu Gen test, exploiting a gap the frontier labs are not filling.

---

### Phase 3: Build — Agent-First from the Start

**Goal:** Build in the Software 3.0 paradigm — not SW 1.0 with AI bolted on.

**Framing shift:** Stop asking "how do I make this faster with AI?" Start asking "what computing paradigm does this problem belong to, and am I building it correctly for that paradigm?"

**Agentic engineering workflow:**

*Before handing off to an agent:*
- Write a spec; define "done" before the agent starts
- Scope tightly: one agent, one contained objective
- Define pass/fail criteria — tests, expected outputs, observable behaviour
- Ask: "what is the text I copy-paste to my agent?" (the SW 3.0 setup pattern — see below)

*While agents are running:*
- Manage context window actively; remove stale context
- Cap at 3–4 parallel agents (human review bandwidth bottleneck, not a technical constraint)
- Check in regularly; no open-ended mandates
- Provide knowledge brain as context where domain relevance matters

*After — reviewing output:*
- Treat as a draft, not a deployment
- Watch specifically for: bloat, excessive copy-paste, brittle abstractions, silent logic errors
- Agent-produced code is often functional but inelegant; this is a current RL limitation, not a fundamental property
- Unit tests and smoke tests must pass
- CI blockers gate production — automated gates are more reliable than manual review alone

---

### Phase 4: Stay Sharp — Protect Understanding

**Goal:** Maintain and compound the understanding that makes a developer a capable director of agents.

**Core principle (Karpathy):** "You can outsource your thinking but you can't outsource your understanding." Direction quality is the scarce resource. You cannot direct well without genuine domain understanding.

**Actions:**
- Actively feed the knowledge brain — every article consumed should update relevant sections
- Regularly interrogate knowledge gaps: "What do I know about X? What are the gaps?"
- Maintain ability to evaluate agent output critically — know what "good" looks like in the domain
- Build for capabilities 3–6 months ahead of today's baseline
- Schedule Phase 1 audit for next model release

---

## Concept: Agent-First Infrastructure

### Mental Model: Sensors and Actuators (Karpathy)

Agents need:
- **Sensors** — ways to perceive and read the world: data access, context retrieval, state observation
- **Actuators** — ways to act on the world: API calls, state mutations, process triggers

Agent-first design optimises both for LLM legibility and use.

### For External-Facing Products

| Element | Requirement |
|---|---|
| `llms.txt` | Plain-text file at domain root (like `robots.txt`); tells agents what the product does, how the API works, and how to interact with it — without parsing human marketing copy |
| Documentation | Agent-readable first: clear structure, no assumed context, direct instruction format, explicit examples |
| Functionality exposure | Via MCP, clean REST/GraphQL API, or agent-compatible tool calls — not only through human UI |
| Test | Can an agent understand and use this within one context window, without human translation? |

### For Internal Tooling

| Element | Requirement |
|---|---|
| UI | Stripped where agent is the primary consumer, not a person |
| Data structures | LLM-legible: descriptive field names, explicit schemas, no reliance on visual layout |
| Documentation | Written as agent briefs, not employee onboarding material |
| Benchmark | Agent completes primary workflow end-to-end; no human mediation at any step |

### The Software 3.0 Setup Pattern

When configuring a system, tool, or environment:
- Write a block of natural-language instructions to give to an agent — not a shell script for a human to run
- The agent uses its own intelligence to inspect the environment, handle variation, debug in the loop
- This is more powerful because agents handle edge cases that shell scripts break on
- The test: "what is the text I copy-paste to my agent?" — that is the new script
- Deployment benchmark: could an agent set up DNS, configure services, and deploy end-to-end without a human touching any setting?

---

## Concept: Agentic Engineering vs Vibe Coding

### Definitions

**Vibe coding:** Building by prompting an AI agent and accepting output with minimal correction. Coined by Karpathy. Useful for exploration and rapid prototyping.

**Agentic engineering:** The disciplined production practice — spec-first, structured review, test coverage, CI enforcement, context window management. What Karpathy identifies as the professional evolution beyond vibe coding.

### The 10x Claim (Karpathy, calibrated)

- Karpathy attributes 10x speed gains to practitioners who are good at agentic engineering
- Source is the combination of capable tools AND disciplined practice — not prompt volume alone
- Claims of running 10–20 agents simultaneously (common on social media) are inflated; practical limit for someone who reviews output before production is 3–4 concurrent agents
- The bottleneck is human review bandwidth, not technical capacity

---

## Concept: LLM Nature — Ghosts, Not Animals (Karpathy)

### The Framing

LLMs are not animal intelligences shaped by evolution, embodiment, intrinsic motivation, or survival. They are statistical systems shaped by pre-training data and refined by RL. Karpathy describes them as "ghosts."

**Practical implication:** Emotional pressure, rapport, or persuasion do not improve LLM output. The substrate is statistical circuits, not psychology.

**Karpathy's own caveat:** He notes this framing is somewhat philosophical and he is not certain of all its practical implications — useful as an orientation, not a firm conclusion.

### Jagged Intelligence

LLMs have uneven capability profiles:
- Highly capable on some tasks
- Inexplicably limited on adjacent ones
- Hard edges where performance drops sharply
- Example (Karpathy): repeatedly prompting a model to simplify a training codebase failed entirely — felt like "pulling teeth," clearly outside the model's RL circuits
- Developers should plan for hard edges, not assume linear capability scaling across a task space

### Agent Code Quality (current limitation)

- Agent-produced code is often functional but inelegant
- Common issues: bloated implementations, excessive copy-paste, brittle abstractions that work now but break under change
- This is a current RL training limitation, not a fundamental LLM property
- Implication for review: structured code review is necessary; a scan is insufficient

---

## Reference: All Tests and Decision Questions

| Situation | Test / Question | Positive outcome |
|---|---|---|
| Evaluating a project | Can one multimodal prompt + 1–2 tool calls replace this? | NO → continue evaluating |
| SW 3.0 validity | Does this only exist because of LLMs — impossible before? | YES → worth building |
| Agent-native readiness | Can an agent deploy and use this without human translation? | YES → agent-native |
| Finding a niche | Domain expertise + verifiable outputs + no lab RL coverage? | YES to all → pursue |
| Understanding check | Outsourcing execution or outsourcing understanding? | Execution only → healthy |
| Setup approach | What is the text I copy-paste to my agent? | Able to state it → SW 3.0 pattern |
| Direction quality | Can I evaluate what the agent produced — do I know what good looks like? | YES → capable director |

---

## Reference: Glossary

| Term | Definition |
|---|---|
| Software 3.0 | Computing paradigm where LLM is interpreter, prompt is code, context window is lever |
| Vibe coding | Building by accepting agent output with minimal correction; good for exploration, insufficient for production |
| Agentic engineering | Production-grade agent practice: spec-first, structured review, tests, CI; Karpathy's term |
| Menu Gen test | Two-part kill/build test for whether an application deserves to exist |
| Knowledge brain | Agent-maintained folder of markdown docs capturing domain, strategy, and accumulated thinking; used as advisor and understanding repository |
| Agent-native / agent-first | Infrastructure, APIs, and docs designed for agents as primary consumers |
| `llms.txt` | Plain-text file at domain root telling agents what a product does and how to use it; open spec |
| Verifiable niche | Domain with objectively measurable outputs; supports effective RL and defensible fine-tuning |
| Sensors and actuators | Agent architecture framing: sensors = perceive world; actuators = act on world |
| Jagged intelligence | Uneven LLM capability profile — highly capable in some areas, hard edges in others |
| December inflection | ~Dec 2025 step-change when agentic workflows became consistently trustworthy end-to-end |
| 10x claim | Karpathy's observation that strong agentic engineering practitioners achieve ~10x speed; from tools + discipline combined |

---

## Reference: The Cycle at a Glance

```
┌─────────────────────────────────────────────────────────┐
│  ① AUDIT          Apply Menu Gen test to everything      │
│  ② ORIENT         Find verifiable niche + write thesis   │
│  ③ BUILD          Agent-first, agentic engineering       │
│  ④ STAY SHARP     Compound understanding, not just speed │
│  ↻ REPEAT         At every significant model release     │
└─────────────────────────────────────────────────────────┘
Knowledge brain runs continuously across all four phases.
```

---

<!-- 
kb:tags=software-3.0,ai-development,agentic-engineering,vibe-coding,karpathy,llm-native,agent-first,verifiable-niche,menu-gen-test,knowledge-brain
kb:last-updated=2025
kb:related=ai-architecture,prompt-engineering,llm-deployment,developer-workflow
-->
