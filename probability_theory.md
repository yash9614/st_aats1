# Probability Theory

## Probability Basics

**Probability** is a measure of the chance of an event happening.

- It ranges from **0** (impossible) to **1** (certain).
- It is calculated by dividing the number of favorable outcomes by the total number of possible outcomes:

\[
P(E) = \frac{\text{Number of favorable outcomes}}{\text{Total number of possible outcomes}}
\]

---

## Addition Rule

### Non-overlapping (Mutually Exclusive) Events
When events E and F cannot happen at the same time:

\[
p(E \cup F) = p(E) + p(F)
\]

### Overlapping Events
When events E and F can happen together:

\[
p(E \cup F) = p(E) + p(F) - p(E \cap F)
\]

---

## Multiplication Rule

### Independent Events ("And" Rule)
When the occurrence of one event does not affect the other:

\[
p(E \cap F) = p(E) \times p(F)
\]

### Dependent Events (Conditional Rule)
When the occurrence of one event affects the probability of the other:

\[
p(E \cap F) = p(E) \times p(F \mid E)
\]

---

## Complement Rule

The probability of the complement of event E (E not happening):

\[
p(E') = 1 - p(E)
\]

where \( E' \) is the complement of event E.

---

## Conditional Probability

**Conditional probability** means finding the chance of an event happening when we already know that another related event has occurred.

\[
p(E \mid F) = \frac{p(E \cap F)}{p(F)}
\]

---

## Bayes’ Theorem

**Bayes’ Theorem** is a mathematical formula for determining conditional probability (updating the probability of an event based on new evidence).

\[
p(E \mid F) = \frac{p(F \mid E) \cdot p(E)}{p(F)}
\]

- \( p(E) \): Prior probability of E
- \( p(F \mid E) \): Likelihood
- \( p(F) \): Total probability of F
- \( p(E \mid F) \): Posterior probability of E given F

---

*Source: Codebasics Probability Theory lectures*
