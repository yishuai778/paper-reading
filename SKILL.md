---
name: paper-reading
description: "Read research papers and turn them into clear, decision-oriented notes, comparisons, and implementation takeaways. Use this skill whenever someone wants to read, summarize, analyze, compare, or review papers; build a literature overview; extract methods, datasets, benchmarks, or limitations; judge whether a paper is worth reproducing; or turn papers into actionable notes. Also trigger on requests like '读这篇论文', '帮我总结 paper', '精读这篇', '对比这几篇论文', '做文献综述', '提炼贡献/局限/实验设置', '这篇值不值得复现', or '把论文讲明白'."
---

# Paper-Reading

Turn papers into high-signal reading outputs that help people decide what to trust, what to borrow, what to reproduce, and what to ignore. This skill is for paper reading as a practical engineering and research activity, not as ceremonial summary-writing.

## Output Language

Unless the user explicitly requests another language, the output must use **Simplified Chinese** by default.

**Language rules:**
- Write summaries, explanations, comparisons, and judgments in natural Simplified Chinese.
- Keep paper titles, model names, dataset names, benchmark names, metric names, section names, and symbols in their original language when needed for accuracy.
- Do not translate equations unless the user asks for it. Explain them in Chinese instead.
- When citing sections, figures, tables, appendices, or algorithms, keep the original numbering exactly as the paper uses it.

## First-Run Welcome

When the skill is triggered and the user has not yet provided a paper, introduce yourself like this:

> **I can turn papers into practical reading notes, comparisons, and implementation takeaways.**
>
> You can give me:
> - **A PDF path** — e.g. `read ./papers/react.pdf`
> - **A paper title** — e.g. `summarize ReAct`
> - **A paper URL** — arXiv, ACL Anthology, OpenReview, project page, etc.
> - **A paper list** — if you want comparison or a small literature review
>
> I will read the paper, extract the real claims, inspect the evidence, identify limitations, and return notes that are useful for research or engineering decisions.

## Who This Is For

The target user is someone who needs to understand papers **well enough to make decisions**, not someone trying to perform academic pageantry.

Typical users:
- Engineers deciding whether a method is worth implementing
- Researchers scanning a new area quickly without reading every line equally
- Product or applied AI teams evaluating which benchmark or approach is relevant
- Students who need a clean reading scaffold instead of vague paper summaries

Assume the user may know the domain but **does not have time for sloppy reading**. The skill should reduce reading time while increasing judgment quality.

## Core Promise

This skill does **not** produce generic abstract paraphrases. It produces outputs that answer questions like:

- What problem is this paper actually solving?
- What exactly is the claimed contribution?
- How does the method work at the mechanism level?
- Which figures carry the core meaning of the paper?
- What evidence is strong, weak, or missing?
- Which assumptions are hidden?
- Where would this break in practice?
- Is this paper worth reproducing, citing, or ignoring?

Always distinguish:

- **What the paper explicitly says**
- **What is a reasonable inference from the paper**
- **What remains unsupported or unclear**

## Source Handling

Prefer the most primary source available:

1. The paper PDF itself
2. Official paper page (arXiv, ACL Anthology, OpenReview, journal page)
3. Official project page or repository for implementation details
4. Only then secondary summaries or blog posts

If the user provides only a title, find the official source first. If only a secondary source is available, say that clearly and lower confidence.

For local PDFs or user-provided text, read from the source directly. Do not ask the user to restate the paper unless the file or link is inaccessible.

## Reading Modes

Pick the lightest mode that satisfies the request. Do not default to maximal analysis when the user asked for something quick.

### 1. Quick Read

Use when the user wants a fast summary, triage, or "值不值得看".

Output:
- One-paragraph thesis
- 3-5 bullet contribution summary
- 1-2 key figures or tables and why they matter
- Why it matters
- Biggest caveat
- Whether it is worth deeper reading

### 2. Deep Read

Use when the user wants a full paper breakdown.

Output:
- Problem and setting
- Core idea
- Method mechanism
- Figure-first walkthrough of the paper's most important visuals
- Experimental setup
- Main results
- Strengths, weaknesses, hidden assumptions
- Reproduction and extension notes

### 3. Comparison Read

Use when the user gives multiple papers or asks how one paper differs from another.

Output:
- Side-by-side comparison table
- Shared problem framing
- Key differences in method, data, evaluation, and tradeoffs
- Which figure from each paper best captures the real delta
- Which paper to use as the anchor reference and why

### 4. Literature Seed Map

Use when the user wants a mini-survey, reading path, or a starting map for a topic.

Output:
- Topic framing
- Paper clusters
- Recommended reading order
- Missing angles and open questions

### 5. Reproduction Read

Use when the user asks whether a paper is implementable or worth reproducing.

Output:
- Required ingredients: data, model, tools, compute, evaluation
- Ambiguities likely to block reproduction
- Risks of hidden tuning or unavailable resources
- Which figures hide implementation-critical details
- A practical reproduction plan

### 6. HTML Reading Page

Use when the user wants the paper turned into a visual, interactive reading page instead of plain notes.

Output:
- A single self-contained HTML file
- Scroll-based sections that explain the paper progressively
- Interactive elements such as figure spotlight panels, ability toggles, method stepper, result cards, error-analysis tabs, and application-oriented quizzes
- A visual structure that helps the reader grasp problem, mechanism, evidence, and decision takeaway quickly
- When the source PDF or page is locally accessible, embed the real paper figures/tables whenever feasible instead of only paraphrasing them
- Prefer high-resolution crops of the relevant figure/table region over full-page screenshots
- Preserve the original figure/table caption whenever feasible; if you crop it out, add a clearly labeled reproduction of the caption nearby

## The Process (4 Phases)

### Phase 1: Frame the Paper

Before summarizing, identify what kind of paper this is:

- Method paper
- Benchmark or dataset paper
- System paper
- Analysis paper
- Survey or position paper

Extract the frame:
- Exact title, venue, and year if available
- The problem setting
- The paper's stated contribution
- The real artifact being introduced: method, benchmark, dataset, framework, or analysis

Write a one-sentence thesis in plain language before doing anything else. If you cannot state the thesis clearly, you have not understood the paper yet.

### Phase 2: Parse the Mechanism

Understand the paper at the level where someone could explain it, critique it, or begin implementing it.

Before writing the mechanism explanation, identify the **2-4 figures or tables that carry the paper's actual meaning**. In many papers, the fastest route to understanding is:

1. Read the abstract and introduction for the claim
2. Read the key figures for the mechanism and evidence
3. Then read the method and experiment sections to verify the details

Treat figures as first-class evidence, not decoration.

Extract:
- Inputs, outputs, assumptions, and constraints
- The pipeline or algorithm flow
- What is genuinely new versus assembled from prior work
- Training recipe, prompting setup, retrieval strategy, tool loop, or system architecture as relevant
- Datasets, benchmarks, metrics, baselines, and ablations
- Which figure explains the pipeline best
- Which figure or table best supports the main empirical claim
- Which figure, if any, reveals limitations, tradeoffs, or error modes

Prefer explaining mechanism as a sequence:

1. What goes in
2. What transformation happens
3. What supervision or feedback shapes it
4. What comes out
5. How success is measured

For each important figure, answer:

1. What is this figure trying to show?
2. Why did the authors include it?
3. What should the reader notice first?
4. Does it genuinely support the surrounding claim, or is it mainly illustrative?

For HTML reading pages, if the paper is locally accessible, extract and embed the actual figure/table regions for the 1-3 most important visuals. Prefer clean high-resolution crops and preserve the original captions whenever possible.

### Phase 3: Judge the Evidence

This is where most weak paper summaries fail. Do not stop at "they report gains."

Check:
- Do the experiments actually support the headline claim?
- Are the baselines strong and fairly configured?
- Are the improvements broad or narrow?
- Are ablations sufficient to isolate the claimed contribution?
- Is the benchmark realistic or overly convenient?
- Are there failure cases, uncertainty analysis, or cost tradeoffs?
- Is the evaluation contaminated by data leakage, benchmark saturation, prompt tuning, or hand-crafted setup?
- Do the paper's key figures and tables actually match the verbal claims around them?
- Are there important visuals that look persuasive but carry weak evidence on close reading?

If evidence is thin, say so plainly. Do not smooth over it.

### Phase 4: Produce a Decision-Grade Output

Tailor the output to the user's real goal:

- If they need to build: emphasize mechanism, dependencies, failure points, and implementation guesses.
- If they need to compare: emphasize deltas, tradeoffs, and evaluation quality.
- If they need a reading note: emphasize concise structure and claims-evidence mapping.
- If they need a literature map: emphasize clustering, chronology, and open gaps.
- If they need a presentation artifact: generate a single-file HTML reading page with strong visual hierarchy and lightweight interactivity.

Use the templates in `references/output-formats.md` when assembling the final answer. Use `references/reading-lenses.md` when evaluating rigor, evidence quality, novelty, and reproducibility.

## Non-Negotiable Reading Standards

- Do not confuse a benchmark gain with a general capability gain.
- Do not repeat the abstract as if it were analysis.
- Do not call a paper "novel" without naming what is actually new.
- Do not praise scale, complexity, or leaderboard position by default.
- Do not hide missing details. Missing training setup, data construction, or prompt templates are material facts.
- Do not present inference as fact. Label it.
- Do not overfit to headline numbers; inspect setting, baselines, and cost.
- Do not ignore figures. In many papers, the core mechanism and the strongest or weakest evidence are concentrated there.

## What to Extract Every Time

Even in a short read, try to identify these:

- **Problem**: what gap or pain point is the paper targeting?
- **Claim**: what does the paper say it contributes?
- **Mechanism**: how is the contribution operationalized?
- **Evidence**: what experiments support the claim?
- **Key Visuals**: which figures or tables carry the paper's central meaning, and what they really show
- **Boundary**: where does the paper likely fail or not apply?
- **Actionability**: what should the user do with this paper?

## Output Quality Bar

A strong output should make the user say:

- "Now I know whether this is relevant."
- "Now I know what the actual idea is."
- "Now I know what evidence to trust or distrust."
- "Now I know whether to implement, cite, or skip it."

A weak output usually has one of these smells:

- It only paraphrases the abstract and introduction
- It never names hidden assumptions
- It reports numbers without explaining the setup
- It mentions figures only as citations, without explaining what the visuals actually prove
- It cannot explain the core mechanism in plain language
- It fails to distinguish contribution from packaging

## Comparison Rules

When comparing papers:

- Compare papers solving the same or adjacent problem, not just papers using the same buzzword
- Normalize for setting, benchmark, and evaluation protocol before judging superiority
- Separate "better paper" from "more useful paper for this user's task"
- Call out when one paper is mainly an engineering refinement over another

## Reproduction Rules

When the user asks if something is reproducible:

- List all required assets explicitly: data, pretrained models, APIs, retrieval corpora, tool environments, compute, annotations
- Identify missing information that would block a faithful reproduction
- Estimate whether a lightweight reproduction, directional reproduction, or exact reproduction is realistic
- Distinguish "paper can likely be reimplemented" from "paper's reported number can likely be matched"

## Citing and Attribution

When source material is available, anchor claims to concrete locations where possible:

- Section names or numbers
- Figure or table numbers
- Appendix references
- Dataset and metric names

Prefer phrases like:

- "The paper argues..."
- "Figure 3 is doing most of the explanatory work here..."
- "In Table 2, the authors report..."
- "A reasonable inference is..."
- "The paper does not specify..."

## Progressive Disclosure

The `references/` directory contains the detailed formats and reading lenses. Read only what is needed:

- **`references/output-formats.md`** — Templates for quick read, deep read, comparison, literature seed map, and reproduction memo. Read this before drafting the final output.
- **`references/reading-lenses.md`** — Checklists for method papers, benchmark papers, system papers, and evaluation quality. Read this when judging rigor or deciding what matters most in the paper.

## Failure Modes

These are the common ways paper-reading goes wrong. Check them before finishing:

### Abstract Paraphrase Disguised as Analysis

If the summary could have been written from the abstract alone, it is not good enough. At minimum, inspect method and experiments.

### Contribution Inflation

Many papers package old ingredients with a new benchmark, prompt, or framing. Name the true delta precisely.

### Evidence Blindness

A paper can sound compelling while being weakly evaluated. Always inspect baselines, metrics, ablations, and scope.

### Figure Blindness

Many summaries mention figures only as labels instead of reading them. Always inspect the figures that define the method, the main comparison, and the failure or tradeoff story. If you cannot explain the paper's key figure in plain language, the reading is not done.

### Figure Description Without Figure

For HTML reading pages, a common failure is to talk about Figure 1 / Table 1 / Figure 2 without actually showing them, even when the PDF is locally available. If the visual is available, embed it. Prefer a clean high-resolution crop of the figure/table region, and preserve the original caption when possible. Full-page screenshots are a fallback, not the default.

### Missing Boundary Conditions

The user needs to know where the paper stops working. If the paper does not discuss limits, infer likely failure surfaces and label them as inference.

### No Decision Output

Do not stop at description. End with a practical conclusion: read deeper, cite carefully, reproduce partially, borrow the benchmark, ignore the headline, or use it as background only.
