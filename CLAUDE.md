# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this repository is

A coursework repo (NCHU AIoT, assignment "DIC3 – Project Proposal Refactor using OpenSpec", due 2026-11-13). It holds no application code yet. The goal is to refactor an existing final-project proposal into OpenSpec spec-driven artifacts.

The project being refactored is **DietSense**, a conversational calorie and nutrition Domain AI Agent for Taiwanese food (night-market food, 便當, compound dishes). The user writes in Traditional Chinese, so proposal content should be in Traditional Chinese unless asked otherwise.

## Assignment tasks (from `docs/DIC3-Project Proposal Refactor using Openspec.pdf`)

1. Install OpenSpec and learn spec-driven development (done: `openspec/` and `.claude/` were created by `openspec init --tools claude`).
2. Make the project clear from A to F (abstract), plus **5 cores, 3 trade-offs and 10 details**. These map to the Deep Research section: 5 core mindsets, 3 professional controversies and 10 deep-understanding questions.
3. Convert `design.md` into the OpenSpec workflow.
4. Refactor the Introduction.
5. Refactor the Related Work.

## Source material in `docs/`

- `期末專題提案作業規範.pdf`: the grading rubric. **Treat it as the authoritative requirements** for any proposal artifact.
- `期中Proposal_熱量AI_Agent.docx` and `DietSense_Proposal_Presentation.pptx`: the original DietSense proposal and slides. This is the content to refactor.
- `1.NBLM output 熱量AI提案解析.pdf`: a NotebookLM analysis that maps the proposal onto the rubric and the A2Z outline. It is the fastest summary of what the proposal already contains.
- `A2Z outline example.pdf`: the 26-letter (A–Z, PA–PM) research-outline template.
- `2.DietSense資訊圖表.png`: an infographic of the proposal.

Read `.docx` and `.pptx` files with the `docx` and `pptx` skills.

## Rules from the rubric that every proposal artifact must follow

- **Abstract story** follows A–F: Attention Getter → But → Cure → Development → Experiments → Findings.
- **Introduction** follows A–F: Attention Getter, Background, Problem, Existing Limitations, Innovation, Contributions. Back claims with sources, preferably from 2025–2026.
- **Related Work** is about half AI technology and half domain know-how (nutrition science). It must include an Article Summary Table with the columns Ref / Year / Problem / AI Method / Domain Knowledge / Dataset / Findings / Limitation. It ends with Existing Research → Limitations → Research Gap → Our Project.
- **Proposed Scheme** uses an eight-module architecture numbered ①–⑧: User Scenario → Query/Input → Planner & Reasoning Agent → Data Acquisition/Retrieval → Analytics Engine → Domain Knowledge Integration → Decision/Recommendation → Output. It needs an architecture diagram, a flowchart (with decisions, loops and exceptions), and pseudocode with line numbers.
- **Do not fabricate results.** At proposal stage, write Expected Outcomes only. DietSense's targets (±20% calorie accuracy > 85%, 60% shorter logging time, SUS > 70) are planned targets, not measured results.
- **Verify citations.** The NBLM analysis notes that some citations in the original draft are placeholders. Do not invent references, DOIs or statistics. If a source cannot be verified, say so.
- **Keep `DESIGN.md` up to date.** The final handover needs Problem → Requirements → Architecture → Components → Data → AI/Analytics → Domain Knowledge → Algorithm → Implementation → How to Run → Results.

## DietSense design anchors (keep consistent across artifacts)

- The LLM acts as planner. NER extracts food entities, and a Clarification Loop asks follow-up questions when confidence is below 80%. Portion ambiguity is resolved by asking, not guessing.
- Numbers come from deterministic tools, never from LLM free text. Data sources are USDA FoodData Central, the Taiwan MOHW food composition database, and RAG over a custom Taiwanese-dish vector store. Energy = portion(g) × kcal/100g ÷ 100. BMR and TDEE use Mifflin-St Jeor.
- Estimates are reported as uncertainty intervals, not single precise numbers.
- A safety gate warns on intake below 1,200 kcal/day and on possible eating-disorder signals.
- Evaluation plan: a 500-item annotated Taiwanese-dish set, a MyFitnessPal baseline, and a 7-day user study with 20 participants.

## OpenSpec workflow

- `openspec/config.yaml` uses `schema: spec-driven`. Project-wide constraints for artifacts, such as language or rules for each artifact, go in its `context:` and `rules:` keys.
- Changes are created under `openspec/changes/<name>/` (proposal, design, specs, tasks). Main specs live in `openspec/specs/`. Finished changes move to `openspec/changes/archive/`.
- Slash commands: `/opsx:propose`, `/opsx:explore`, `/opsx:new`, `/opsx:continue`, `/opsx:ff`, `/opsx:apply`, `/opsx:verify`, `/opsx:sync`, `/opsx:archive`. Each one has a matching skill in `.claude/skills/openspec-*`.
- CLI: `openspec list` (add `--specs` to list specs), `openspec show <name>`, `openspec validate <name>`, `openspec status --change <name>`, `openspec archive <change>`. Run `openspec --help` for the full list.

## Not project content

`receipts/` and `review-receipts/` hold tool-call audit logs written automatically by the `protect-mcp` and `review-agent-governance` plugin hooks. Do not edit them or treat them as project files.
