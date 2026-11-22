# Additional Concepts

Short notes on topics that appear in practical interview questions.

## Deterministic Experiment Bucketing

Users must be assigned to treatment/control (or multiple arms) in a way that is:

- **Stable**: the same user always lands in the same bucket for a given experiment.
- **Independent across experiments**: different salts produce different assignments.
- **Uniform**: the hash should distribute users roughly evenly across buckets.

A common implementation hashes a string that combines an experiment-specific salt with the user ID (e.g., MD5 of `"{salt}:{user_id}"`) and reduces the digest modulo the number of buckets. Avoid Python’s built-in `hash()`, which is randomized per process.

## Bayes' Rule for Rare Events

Even a highly sensitive detector can produce mostly false alarms when the event is rare.

$$ P(\text{event} \mid \text{alarm}) = \frac{\text{sensitivity} \cdot \text{prior}}{\text{sensitivity} \cdot \text{prior} + \text{FPR} \cdot (1 - \text{prior})} $$

Example: prior = 0.001, sensitivity = 0.99, FPR = 0.01 → only about 9% of alarms are real events.

## Expected Value of a Sequential Dice Game

With a limited number of rolls, the optimal policy is found by backward induction:

- With one roll left, the value is simply the average face.
- With more rolls left, the value of continuing is the value computed for one fewer roll. Keep a face only if it exceeds that continuation value.

This is a classic dynamic-programming / optimal-stopping problem.

## Regression Discontinuity Design (RDD)

When a treatment is assigned based on a running variable crossing a cutoff, the causal effect can be estimated by comparing outcomes just above and just below the cutoff.

Local linear regression on each side of the cutoff (within a bandwidth) yields two fitted values at the cutoff. Their difference is the estimated jump (treatment effect), under the assumption that the outcome would have been continuous at the cutoff in the absence of treatment.

## Exact Binomial Test

A two-sided exact binomial test using the minimum-likelihood definition sums the probabilities of every outcome that is no more likely than the observed outcome. A small relative tolerance (1e-7) treats floating-point ties as equal. The resulting p-value is capped at 1.

This is useful when n is modest and a normal approximation is unreliable.

## Comparing Two Poisson Rates

For two Poisson processes with event counts and exposures, the rate ratio is

$$ \frac{\text{rate}_B}{\text{rate}_A} = \frac{\text{events}_B / \text{exposure}_B}{\text{events}_A / \text{exposure}_A} $$

The log of the rate ratio is approximately normal with standard error √(1/events_A + 1/events_B). A two-sided z-test then checks whether the ratio differs from 1.

## Recommendation System Design

A typical production system separates:

1. **Candidate generation** — retrieve a few hundred to a few thousand items from a large catalog.
2. **Ranking** — score the candidates with a richer model.
3. **Re-ranking / diversity** — enforce business rules, diversity, and freshness.

Key challenges include cold start, exploration vs exploitation, evaluation (offline metrics vs online A/B tests), and serving latency.

## MapReduce Join + Top-N

To join two large files and produce a top-N result:

1. Map both files so the join key is the MapReduce key.
2. Reduce per key: aggregate (e.g., sum sales) and emit (aggregate, payload).
3. Obtain the global top N either by collecting the aggregated results (if they fit) or with a second top-N MapReduce job that keeps local heaps.

---

See [practical_interview_solutions.md](practical_interview_solutions.md) for implementations and [ab_testing.md](ab_testing.md) for experiment design.
