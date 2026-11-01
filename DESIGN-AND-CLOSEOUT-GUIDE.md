# Mission Designer: Evidence, Prompt Design, and Completion Reports

**Companion to Mission Designer v3.1 · November 1, 2026**

This is a reference for authors and reviewers, **not a second prompt to paste alongside** `MISSION-DESIGNER.md`. The main prompt is self-contained. This document explains why its mission and reporting contracts look the way they do, with examples that can be adapted to Codex or another implementation agent.

The goal is **a capable implementation agent doing useful work with minimum unnecessary steering**, then reporting an outcome that a creator can understand and a reviewer can inspect.

## 1. Design prompts around outcomes, not a prescribed coding ritual

A mission is an engineering assignment, not a disguised list of commands for the agent to obey blindly.

| Dimension | Include when it matters | Common failure |
| --- | --- | --- |
| **Goal** | Who can do what after the change and why | “Make it better” without observable value |
| **Starting state** | Actual repository/workspace, known behavior, authoritative docs, relevant examples | Guessing files, versions, or how the existing app works |
| **Desired experience** | Primary user journeys, important edge cases, failure/recovery, quality qualities | A feature checklist with no user outcome |
| **Constraints** | Compatibility, rights, data, cost, performance, production and approval boundaries | Forcing incidental architecture or missing a consequential risk |
| **Acceptance** | Independent, observable outcome conditions, including a few revealing negative cases | “Tests pass” or “looks professional” without a meaningful test |
| **Return** | Outcome status, what changed, actual verification, gaps and next action | A reassuring narrative or a huge unfiltered command log |

### Practical design sequence

1. **Find the real user outcome.** Ask only product-level questions that would materially change it; recommend sensible defaults for minor uncertainty.
2. **Investigate the starting point.** Reference existing behavior, conventions, nearby working examples, repository documents and relevant prior decisions. Treat unavailable or stale information as an assumption for the implementer to check.
3. **Choose the smallest valuable next outcome.** It might be a small fix, feasibility test, user-visible vertical slice or complete release, depending on the risk and value. Do not fragment work merely to create tasks.
4. **Specify meaningful acceptance.** Use happy-path behavior, critical failures and preservation constraints. Include performance, security, accessibility and visual quality only where relevant. Make key checks feasible in the actual environment.
5. **Separate outcome from method.** Permit the engineer/agent to choose libraries, tests, architecture and steps unless a specific boundary or existing standard justifies constraining them.
6. **Set return evidence and authority.** Specify what must be observable at handoff and which actions require prior approval. Prefer links to actual artifacts over copied logs.
7. **Check the mission for contradictions.** If the acceptance conditions cannot be observed or a major decision is unresolved, narrow the mission to a proof or surface the product decision.

**Do not:** require every mission to use a planning agent, a fixed number of subtasks, mandatory TDD, a fixed sequence of tools, a swarm of agents, or multiple model-graded reviews. Different engineering reports and experiments find these mechanisms helpful in some conditions and costly or harmful in others. Make them optional engineering choices.

## 2. Two usable mission examples

These are **illustrative assignments**, not logs of real deployments or experiments.

### Example A: small, reversible change

```markdown
# MISSION: Include the date in export filenames

**Goal:** People can tell exported files apart by the day they were generated.
**Context:** Existing export behavior and filename conventions are authoritative; inspect the current implementation.
**Expected experience:** The normal export works as before except its filename includes the date in the project's existing convention.
**Boundaries:** Preserve file contents, extension, existing user data, and supported export flows. Do not deploy.
**Done when:** An export produces the intended dated filename; existing export behavior and relevant regression checks remain intact. Include a test for date formatting if justified.
**Return:** Say what changed, show the observed filename and relevant check result, mention any caveat, and identify the next action only if one exists.
```

No separate research phase, evidence directory or architecture essay is needed unless the actual implementation reveals complexity.

### Example B: substantial visual web work

```markdown
# MISSION: Build a distinctive preview website for an artisan business

**Goal:** A potential customer can understand the business's capabilities, inspect examples of work, and send an inquiry from a compelling mobile-first website.
**Context:** [Verified business brief, factual/source ledger, asset permissions, existing repository and site-quality standard]. Confirm the checkout and missing facts before committing to a design.
**Expected experience:** Clear homepage and service/project journey; coherent art direction based on this business rather than a generic card template; usable phone navigation; understandable form success and failure states.
**Boundaries:** No invented testimonials, credentials, completed projects, or rights. Create an unofficial preview only. Keep live services unchanged. Owner approves creative direction and any later publication.
**Done when:** The brief and approved visual direction are reflected in real rendered phone and desktop pages; major customer tasks work; project-specific factual/rights checks and meaningful functional, accessibility and performance tests are recorded. A test-green but visually generic site fails the professional-quality criterion. Failed delivery, missing rights, or inaccessible primary actions are explicit blockers.
**Return:** Give a concise mission receipt with status, work delivered, actual verification, remaining issues, and next approval/action. Link to screenshots, checks, source revision and any durable evidence record. Mark production readiness NOT TESTED until authorized.
```

The design agent can use relevant installed skills and seek appropriate independent visual review, but the mission does not require a universal design, architecture or tool sequence.

## 3. The completion-reporting contract

### Human-facing Mission Receipt

Lead with one of four statuses:

- **Complete and verified:** The required outcomes are met with sufficient applicable evidence. This **does not** imply publication approval.
- **Ready for review:** The implementation meets its currently testable requirements, but a specified creative, subjective or consequential approval remains.
- **Partially complete:** At least one required result is unfinished or not sufficiently verified, although useful work was delivered.
- **Blocked:** A real missing dependency, resource, permission or decision prevents meaningful progress.

Then communicate, in plain language, only:

1. **Outcome:** What the user can now do or what was actually delivered.
2. **Important changes:** Significant implementation and relevant proactive decisions, not every file.
3. **Verification:** Observed checks and their results. Separate local/mocked, real-browser, integrated and live behavior.
4. **Risks and gaps:** Critical failures, untested properties, limitations, pending approvals or regressions.
5. **Next action:** Exactly what should happen next, or “none.”

Individual checks use **PASS / FAIL / NOT TESTED / BLOCKED / NOT APPLICABLE** when their distinctions matter. A check marked NOT TESTED cannot silently count as passed.

**Never claim:** tests or external operations occurred based only on intent; a UI is excellent based only on a build passing; a skill was actually invoked because it was installed; a prototype is production-ready because local checks worked; a model review is independent proof of reliability.

### Durable evidence for substantial missions

Prefer the project's existing report convention over a newly invented global folder. The supporting record should be small but sufficient to resume or independently review:

- Mission ID/goal and original acceptance conditions.
- Repository/branch/revision and relevant run or preview instructions.
- Deliverables, deviations and significant engineering decisions.
- Acceptance-case matrix: requirement, PASS/FAIL/NOT TESTED/BLOCKED/N/A, check method, observed result and evidence reference.
- Test output, screenshots, browser evidence or external-action receipts **linked**, not duplicated.
- Significant failures, outstanding risks, dependencies and required approvals.
- State/recovery information: existing rollback checkpoint, uncommitted work and precise next step.
- A short verified lesson when justified.

A minor local edit needs only a short receipt. A multi-session or high-risk mission justifies more traceability. **An evidence document is not a request to re-run every test or to install a telemetry platform.**

### Reporting as part of mission design

The creator-facing AI writes a concise **Return** clause into the mission before handoff. The implementer then supplies the receipt and evidence. Upon return, the creator-facing AI compares it with the **original experience and acceptance cases**, not merely with the implementer's summary, and distinguishes reported claims from independently inspected artifacts.

For work such as websites, assess the actual rendered output and relevant interactions. If the live environment or form-delivery route was not tested, do not elevate a local preview to production-ready.

### Learning without a new bureaucracy

After meaningful work, note a useful verified solution, recurring failure or hard-to-discover root cause. Leave one-off anecdotes as project notes; propose a regression check or small skill/document change only when generalization is justified. Keep original records and existing project instructions authoritative. Seek the creator's approval before altering globally shared guidance.

## 4. Research-to-design traceability

The research below combines practitioner reports, product documentation and empirical studies. It supports **design considerations**, not proof that a particular prompt or reporting format is the one universally best option.

| Research source and finding | Design implication | Limit |
| --- | --- | --- |
| [How OpenAI uses Codex](https://openai.com/business/guides-and-resources/how-openai-uses-codex/): issue-shaped assignments, concrete repository context. | Give goal, existing examples, important boundaries and evidence of completion. | Practitioner report, not a controlled prompt-template trial. |
| [Codex best practices](https://learn.chatgpt.com/guides/best-practices): goal/context/constraints/done conditions and proportional planning. | Make those fields legible; plan when the mission warrants it. | Advice evolves with models and clients. |
| [OpenAI harness engineering](https://openai.com/index/harness-engineering/): repository knowledge, structural checks, feedback loops. | Prefer authoritative, current source references and observable quality checks. | Particular team and environment. |
| [Anthropic's long-running-agent harness](https://www.anthropic.com/engineering/effective-harnesses-for-long-running-agents): durable artifacts and recovery between sessions. | Record revision, unresolved work and resume instructions for substantial missions. | Harness experience, not a universal requirement. |
| [Demystifying evals for AI agents](https://www.anthropic.com/research/demystifying-evals-for-ai-agents): environment state vs transcript claims; grader pitfalls and disproportionate process checks. | Evaluate observable results, keep uncertainties visible and avoid overprescribed tool order. | Evaluators and task distributions require calibration. |
| [Testing Agent Skills Systematically](https://developers.openai.com/blog/eval-skills): distinguish outcome, process, style, efficiency; cheap checks first. | Report task success separately from skill activation and reserve expensive evaluation for material risk. | Example workflow, not an obligatory skill test suite. |
| [Thoughtworks internal-quality example](https://martinfowler.com/articles/exploring-gen-ai/ccmenu-quality.html): a passing feature can damage code structure. | Consider integration and maintainability at closeout when relevant. | Single practitioner case. |
| [MCP Inspector's agent factory](https://github.com/modelcontextprotocol/inspector/blob/main/docs/ai-software-factory.md): inspectable CI gate and human release authority. | Attach actual check output and keep external publication approval separate. | Particular project's process and self-report. |
| [GitHub: better tools initially worsened code review](https://github.blog/ai-and-ml/github-copilot/better-tools-made-copilot-code-review-worse-heres-how-we-actually-improved-it/): targeted trace-based improvement. | Improve rules based on observed failures, not speculation or adding steps reflexively. | Task- and tool-specific effects. |
| [Are Harnesses Worth the Cost?](https://martinfowler.com/articles/are-harnesses-worth-the-cost.html): added structure helped one tested model but cost more without improving the stronger model in that experiment. | Favor the minimum effective instructions, especially on strong implementation agents. | Small experimental scope; no universal performance ranking. |
| [GitHub repository-memory report](https://github.blog/ai-and-ml/github-copilot/building-an-agentic-memory-system-for-github-copilot/): reported benefits from scoped persistent memory. | Keep verified lessons near the relevant repo rather than stuffing all history into each prompt. | Vendor A/B metrics and memory systems differ. |

## 5. What to measure before declaring this approach superior

Try it on several real missions with different levels of complexity. Examine task acceptance, missed requirements, independent verification, owner comprehension, useful lessons, and unnecessary report overhead. Compare against earlier or simpler prompts where feasible. A successful first run proves **it can work**, not that the added format caused the success.

**Principle:** Minimal sufficient mission; maximal honesty about the result.
