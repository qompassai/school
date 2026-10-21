# Framework — the three layers under a school

Every school run in this study sits on three framework layers.
They are not background assumptions; they are part of what the
trials measure. This file is the short map. The full application
to the first trial is `EVALUATION.md` §7 alongside this file.

## 1. Shared attention

Attention is the scarcest resource in the estate's economy, and it
is claimed, never grabbed. Jobs publish a bid for the shared
resource (`attention_publish`), the winner holds it as a lease
(`attention_focus`), and a deterministic award function decides
(`attention_decide`). In the image trial the shared resource is
concrete: the single GPU generation slot. One floor with 120 s
holds serves at most ~30 holders/hour (measured useful fraction
~75%); past sustained saturation, attention shards into boards
(one board tracks at most 64 agents). Both trial arms share the
one floor, and floor-seconds are accounted per arm in the run
record.

## 2. Auction + timeouts

Work is allocated by auction and governed by time:

- **Awards expire** (R9): an award not started inside its
  start-by window is void and re-bids. Expiry is weather, not
  failure.
- **Claims are leases, renewed by evidence** (R10): a lease
  renews only on output produced — silence never renews. Expiry
  is the system's death detection. Every re-award increments a
  fencing generation; a revived holder's late writes are rejected
  against the stale generation, never merged.
- **Bids decay** (R11): a queued bid has a shelf life. Work that
  cannot attract a live bid inside its horizon is archived
  visibly, never silently dropped.
- **Award ≠ authority** (R7): at dispatch, a deterministic
  `decide()` re-runs against the live label join and policy
  fingerprint; drift voids the award.

Standings are learned from measured outcomes in the ledger, never
from an executor's self-report, and they move monotonically: down
on a failure immediately, up only through verified passes.

## 3. OpenAPPA labels

Every artifact carries a label — **audience × trust** — computed
by deterministic code and recorded in the ledger. A model never
labels its own output.

- Labels gate eligibility: an executor may only bid on work its
  clearance covers, and sees only the labelled abstract of work
  it is not cleared for.
- At each hand-off, the output's label is the **join** of its
  inputs' labels: reader-set intersection on audience, minimum on
  trust. Downgrade is unrepresentable — nothing leaves a station
  labelled broader or more trusted than what entered it, and no
  automated check can launder trust upward. Only a human
  acceptance act re-labels, by authority.
- A label block is final: no bid, award, or approval lifts it.
  Correctness lives in the checker net between stations; labels
  govern who may touch what and how far it may travel. Neither
  substitutes for the other.

## Sources

- Protocol (R1–R11, incl. the OpenAPPA layer and time
  discipline): `~/workspace/orchestration-20261018/AUCTION-PROTOCOL.md`
- Measured fidelity of this substrate (robust at 40 agents;
  checkpointed decide; floor saturation): night stream A,
  `~/workspace/night-20261020/AUCTION/RESULTS.md`
- Attention ladder and digest discipline: the estate's MATE
  ladder skill (`local-mate-ladder`).

## Status

Framework description for the school study, 2026-10-21. Two
carried caveats, on the record in EVALUATION.md §7.5: the market's
price machinery presupposes heterogeneous executors and runs at
station-class level in a trial of identical copies; and the
time-discipline semantics are implemented by the trial runner per
this protocol until phlow's scheduler work (S3) lands them in
code — trial results measure the protocol, not that
implementation.
