# Reading Lenses

Use these lenses to decide what matters in a paper. Do not apply every lens with equal depth; select based on the paper type and the user's goal.

## Method Paper Lens

Questions to answer:

- What exact bottleneck is the method targeting?
- What is actually new: objective, architecture, data construction, retrieval loop, tool interaction, training signal, or evaluation framing?
- Which components are essential versus optional packaging?
- Does the ablation isolate the new ingredient?
- Does the gain hold across multiple settings or only one narrow benchmark?

Red flags:

- "Novel framework" language without a concrete mechanism delta
- Gains only against weak or outdated baselines
- Missing ablations on the claimed core component
- High prompt or pipeline sensitivity hidden in appendices or omitted entirely

## Benchmark / Dataset Paper Lens

Questions to answer:

- What real capability does the benchmark claim to measure?
- Is the task realistic or synthetic to the point of distortion?
- How was the data collected, filtered, and labeled?
- Is there leakage risk from pretraining data or public benchmarks?
- Are scoring rules stable and hard to game?

Red flags:

- Benchmark difficulty created mainly by annotation artifacts
- Narrow domain framed as general intelligence
- No evidence that benchmark scores correlate with real downstream utility
- Hidden manual curation that is hard to reproduce

## System Paper Lens

Questions to answer:

- What pieces are composed, and where is the actual systems contribution?
- What assumptions does the system make about infrastructure, tools, latency, or users?
- Are cost, latency, and reliability discussed, or only accuracy?
- Does the paper expose failure handling and fallback behavior?

Red flags:

- System wins driven by hidden prompt engineering or heavy manual scaffolding
- No cost or latency accounting
- Evaluation uses idealized environments unlike real deployment

## Evaluation Quality Lens

Always inspect:

- Baseline strength
- Metric suitability
- Train/test separation
- Number of seeds or runs if relevant
- Confidence intervals or variance discussion if relevant
- Error analysis or failure cases
- Statistical significance only when the setting actually warrants it

Questions:

- Are the baselines reproduced faithfully?
- Is the evaluation protocol comparable across systems?
- Could the main result be explained by extra data, extra tools, or extra tuning rather than the claimed idea?
- Does the paper report tradeoffs, or only the best metric?

## Reproducibility Lens

Check whether the following are specified:

- Data sources and splits
- Preprocessing
- Prompt templates or system messages
- Retrieval corpus and indexing details
- Tool APIs and parameters
- Hyperparameters or decoding settings
- Model versions
- Hardware / compute scale
- Stopping criteria and evaluation scripts

Missing two or more core ingredients usually means exact reproduction is doubtful.

## Transfer Lens

Use when the user wants to apply the paper to a real project.

Ask:

- Which assumptions from the paper hold in the user's environment?
- Does the method require unavailable tools, labels, or compute?
- Is the benchmark close to the user's use case?
- Is the reported gain worth the added complexity?

Good transfer notes usually end with:

- what to borrow directly
- what to simplify
- what to validate before full adoption
