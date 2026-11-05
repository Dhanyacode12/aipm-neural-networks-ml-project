# Project Handout: Neural Network or Traditional ML?

Extend the machine learning project your team already completed. Build one
reasonable neural-network challenger, compare it fairly with the existing model,
and recommend traditional ML, the neural network, or no ML. The deliverable is
an evidence-based product decision, not the most complex architecture.

## Core Deliverables

Add the following to the existing ML project repository:

- `model-comparison-plan.md`, completed before training the challenger;
- one clearly named neural-network notebook or script;
- `model-comparison-report.md` with reproducible evidence and limitations;
- `decision-memo.md` with the final recommendation; and
- an updated project `README.md` linking both approaches and the decision.

Start from the files in `templates/`. Keep generated model files and large
experiment artifacts out of Git unless the project explicitly requires them.

## Core Quality Rules

- Preserve the original problem, dataset, target, and product context.
- Use the same untouched test observations and primary metric.
- Never use the test set for early stopping, architecture selection, threshold
  tuning, or preprocessing decisions.
- Fit every preprocessing step on training data only.
- Keep the submitted traditional model as the historical baseline.
- Give additional challengers bounded and documented tuning budgets.
- Record seeds, software versions, hardware, and important hyperparameters.
- Measure trade-offs beyond predictive performance.
- Keep “no ML” as a legitimate decision option.

## Project Sequence

### 1. Recover the Existing Baseline

Run the existing pipeline and record:

- the product decision it supports;
- dataset version and split logic;
- model and preprocessing pipeline;
- primary and secondary metrics;
- decision threshold when applicable;
- tuning history if known; and
- known limitations.

If the result cannot be reproduced, document the difference between the
submitted claim and the current run. Restore the minimum missing information
needed for a credible comparison before adding the neural network.

### 2. Freeze the Comparison Plan

Complete `model-comparison-plan.md`. Define the split, metrics, practical
difference, error costs, tuning budget, repeated-run policy, timing method, and
decision constraints before seeing neural-network test results.

Choose a split strategy appropriate to the data. Preserve groups or time order
when random splitting would leak information.

### 3. Build a Reasonable Neural Network

Start with the simplest architecture appropriate to the input:

- a small feed-forward network for ordinary tabular classification or
  regression;
- a convolutional or pretrained vision model for images;
- an appropriate sequence or pretrained representation for text, audio, or
  time-dependent inputs.

TensorFlow/Keras is recommended because it follows the preceding course, but it
is not mandatory. PyTorch is a valid alternative. Document why the chosen
framework and architecture fit the data.

Use a validation strategy, sensible regularisation, and early stopping. Do not
add CNNs, recurrent networks, transformers, or many layers only because they
sound more advanced.

### 4. Run a Comparable Search

Tune a bounded set of decisions such as learning rate, width, regularisation,
batch size, and stopping patience. Do not repeatedly inspect the final test set.

If the original traditional model had little or unknown tuning, you may add one
strong traditional challenger under the same search budget. Keep it distinct
from the historical baseline.

Select the final configuration on validation evidence. Repeat that configuration
with at least three seeds when resources permit. Otherwise disclose the
single-run limitation.

### 5. Evaluate the Frozen Test Set

Evaluate each final candidate on the same test observations. Report:

- primary and secondary metrics with unrounded values;
- absolute and relative differences;
- variability across seeds or resamples;
- confusion matrices or residual analysis;
- examples of costly errors;
- subgroup or operating-condition performance where relevant; and
- calibration and threshold evidence for probability-based decisions.

Do not claim that a tiny numerical difference is meaningful without evidence.

### 6. Measure the System Trade-Offs

Use the same hardware and workload where possible. Record:

- training time for one final fit and total tuning effort;
- inference latency with warm-up and repetition;
- model artifact size and important memory or hardware requirements;
- preprocessing and serving complexity;
- retraining, monitoring, and debugging needs;
- interpretability and audit constraints; and
- limitations of every measurement.

### 7. Complete the Comparison Report

Populate the evidence table in `model-comparison-report.md`. Keep facts,
interpretations, and missing evidence distinct. Include results that weaken the
preferred option.

The report should make it possible for another practitioner to understand what
was compared and why the result is credible.

### 8. Make and Communicate the Decision

Use `decision-memo.md` to recommend one option now:

- ship or keep the traditional model;
- ship the neural network;
- do not use ML for this decision; or
- run a clearly defined next experiment because current evidence is
  insufficient.

State the strongest evidence, the most important trade-off, remaining
uncertainty, and the conditions that would reverse the recommendation.

## Required Comparison Table

| Dimension | Historical ML | Optional ML challenger | Neural network | No ML / rule |
|---|---|---|---|---|
| Primary metric | | | | |
| Practical difference reached? | | | | |
| Costly error profile | | | | |
| Calibration / probability quality | | | | |
| Stability across runs | | | | |
| Training and tuning effort | | | | |
| Inference latency and throughput | | | | |
| Model size and hardware | | | | |
| Interpretability and auditability | | | | |
| Maintenance and monitoring | | | | |
| Product value and risk | | | | |
| Evidence confidence | | | | |

Use `Not applicable` with a reason when a dimension does not fit the project.
Do not invent a metric for the no-ML option when qualitative comparison is more
honest.

## Optional Extensions

Complete the core deliverables first. Choose extensions that answer a real open
question rather than adding architecture for its own sake.

### Build Learning Curves

Train the strongest candidates on increasing fractions of the training data.
Use the curves to assess whether additional data may change the model choice.

### Test Robustness

Evaluate missing values, mild noise, shifted categories, changed image quality,
or another plausible operating condition without corrupting the original test
evidence.

### Calibrate Probabilities

Compare reliability diagrams and a probability metric such as log loss or Brier
score. Fit any calibration method on validation data, then evaluate once on the
test set.

### Explore Threshold and Business Utility

Translate false positives and false negatives into product consequences. Plot
utility or workload across candidate thresholds and recommend an operating
point.

### Estimate Compute Impact

Record total experiment time, hardware, and trial count. Use a transparent tool
such as [Green Algorithms](https://www.green-algorithms.org/) for an approximate
footprint, and explain the estimate's assumptions.

### Create a Lightweight Model Card

Document intended use, users, evaluation data, relevant subgroups, limitations,
ethical considerations, and monitoring needs for the recommended model.

### Evaluate a Hybrid System

Test a cascade, rules plus model, human-review threshold, or ensemble only when
it addresses a documented failure mode. Compare its added operating complexity.

### Run an Independent Reproduction

Ask a teammate who did not build the neural network to reproduce one final run
from the repository instructions. Turn missing steps into concrete documentation
improvements.

## Final Quality Gate

- The original and neural models use identical test observations.
- Validation and test responsibilities are clearly separated.
- Model-specific preprocessing is justified and fitted without leakage.
- Tuning effort and repeated-run policy are visible.
- Predictive, system, product, and governance evidence are included.
- The report states uncertainty and unfavourable evidence.
- The recommendation includes a no-ML alternative and flip conditions.
- Another person can locate the code, evidence, and decision from the README.
