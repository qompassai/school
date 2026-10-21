# school — the School Study

A study of **schools**: coordinated groups of small AI models doing
bounded work together. (A coordinated group of models is called a
*school* here — the word is deliberate.)

## Purpose

Determine, by measurement rather than by analogy, what a school of
small local models can do on estate hardware — and what it costs
compared with one model working alone. The estate already runs the
substrate (shared attention, timeouts, an auction for work, and
deterministic label checks); this study tests the *organisation of
the models themselves*.

## The trial concept

An **assembly line of identical copies**: several copies of the same
small model, each holding one bounded station, with deterministic
checkers between stations. No free-form messaging between copies;
work passes hand to hand as structured artifacts, and a copy's
output class is admissible exactly where a checker exists to verify
it.

First workload: **image generation for light-show** — text stations
(draft, refine, seed-plan) around a local image model, with a vision
model scoring and selecting outputs, measured against a
single-model baseline at equal budget: end-to-end yield, cost per
accepted image, hand-off fidelity between stations, and an
efficiency ratio in the spirit of the "stepping on toes" λ from the
swarm-scaling literature.

## Evidence base

- Night stream A — auction/school substrate fidelity and the
  small-model platoon ladder (3B = smallest near-correct structured
  tier): `night-20261020/AUCTION/RESULTS.md` in the estate workspace.
- Night stream B — per-model routing by measured strength:
  `night-20261020/VALIDATION/RESULTS.md`.
- Candidate evaluation for this study (benchmarks, skills, tools —
  each classified fold-in / adapt / from-scratch / skip):
  `EVALUATION.md` alongside this file.
- Prior art survey method, from the estate's mcprush adoption
  reviews (2026-10-21): `mcprush-review-20261021/REPORT.md` and
  `mcprush-skills-review-20261021/REPORT.md`.

## Status

Study commissioned 2026-10-21. Evaluation complete; first-trial
design sketched in `EVALUATION.md` §5. No build authorized; open
decisions OD-1 to OD-4 await the Owner.
