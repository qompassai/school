# School Study — Evaluation of Candidate Benchmarks, Skills, and Tools

Date: 2026-10-21. Research only — nothing installed, claimed, or
built. Terminology: coordinated groups of small models are **schools**
in this estate. (Source documents use their own word for the same
idea; where a product or post title contains it, the title is quoted
as-is and the concept is called a school here.)

Method mirrors the two mcprush adoption reviews of the same date
(~/workspace/mcprush-review-20261021/REPORT.md and
~/workspace/mcprush-skills-review-20261021/REPORT.md): every candidate
is classified **FOLD IN / ADAPT / FROM-SCRATCH / SKIP** with reasons
tied to estate fit, and a candidate must beat or fill a gap in what
the estate already has — not duplicate it.

The trial concept under evaluation: multiple copies of the **same**
small model arranged as an **assembly line** — each copy holds one
bounded station, deterministic checkers sit between stations. First
workload: image generation for light-show, around Iris (Illustrious
XL v1.1 via ComfyUI; atelier is the generation MCP being built) with
Mira (Glimmer 30B vision) as the scoring eye.

Evidence base already in hand:

- Night stream A (~/workspace/night-20261020/AUCTION/RESULTS.md):
  the platoon ladder — 3B coder is the smallest tier producing
  near-correct structured output; 1.5B for parser-gated micro-work;
  sub-1B is signals-only, never free-text evidence. Probe rates:
  0.6B 366 tok/s (failed the probe), 1.5B coder 209, 3B coder 160,
  8B-tools 94, Tessa 81. Residency: a full mixed set ≈ 26 GB fits
  the A6000 alongside the roster.
- Night stream B (~/workspace/night-20261020/VALIDATION/RESULTS.md):
  routing by measured strength — Opal primary for tool-surface
  validation, Sylvia second, Freya for error-surface sweeps;
  counts come from deterministic code, never a model; Tessa is
  viable only behind a fallback-capable harness (most of her calls
  arrive as fenced JSON text, not structured calls).

## Reachability note — what was actually read

- **LessWrong post**: the lesswrong.com fetch returned only the
  footnotes (body did not render). The full body was read via the
  GreaterWrong mirror of the same post
  (greaterwrong.com/posts/6cb7qd3RSkgnviCpf/swarm-scaling). Section 1
  below digests that text. All "claims" there are the post's claims,
  not verified facts.
- **mcprush catalog search** `catalog?q=swarm`: page states **89
  servers**. The fetch rendered ~20 cards; as in both prior reviews,
  most rows are initials-only with a one-line description and no
  publisher name. One card carried a name link (Swarm Rd
  Orchestrator) and was detail-read. Classifications of the rest
  rest on the card text as rendered — labelled as such.
- **mcprush skills search** `skills?q=swarm`: page states **86
  skills**. ~20 rows rendered; named, detail-read: Advanced Swarm
  Orchestration (ruvnet). Others are classified from listing text
  (name/publisher/context cost where shown). Reminder from the
  skills review: mcprush does **not** grade skills — no Trust
  Checker score exists; listing metadata (context cost, licence,
  bundle inventory) is all there is, and installs fetch the current
  unversioned folder, so anything adopted gets vendored, never
  shelf-installed.
- **Benchmark sources**: the LessWrong post (for the three agent
  benchmarks it names) and fetched benchmark summaries — a DeepWiki
  generation-benchmarks page (GenEval, DPG-Bench, UniGenBench), a
  GenEval paper summary (liner.com review page), and the
  imagebench.ai glossary (DrawBench, FID, HPS, ImageReward,
  inter-annotator agreement). Anything beyond those pages is marked
  UNDETERMINED.

---

## 1. The LessWrong post, digested

"Swarm Scaling" (LessWrong; read in full via the GreaterWrong
mirror). The post asks how capability scales as identical agents are
added, using charts from OpenAI's GPT 5.6 Sol launch post. Its
claims, as post claims:

- **Scaling by headcount is worth roughly the square root of scaling
  by thinking time.** Interpolating OpenAI's curves at fixed tokens
  per agent: going 1 → 4 → 16 agents buys a little over half the
  capability gain of the same compute spent lengthening one agent's
  chain of thought. "You need to do the scale-up of compute twice to
  get to the same capability, squaring the total multiplier needed."
- **The "stepping on toes" parameter λ.** Borrowed from labour
  economics: N agents working together achieve what one agent
  achieves in N^λ time. λ = 1 is perfectly parallelisable; measured
  λ from regressions over the three benchmarks in the launch post:
  **BrowseComp λ = 0.68 (90% CI 0.63–0.76), SEC-Bench Pro λ = 0.57
  (0.52–0.61), Terminal-Bench λ = 0.48 (0.40–0.57)** — in line with
  published estimates for human teams. λ is task-dependent and may
  change at larger scales.
- **The single agent is the most token-efficient at every size**:
  the 4-agent curve needs ~2× the total tokens of the 1-agent curve
  for the same score; 16 agents ~2× again. Per-size curves show the
  usual logarithmic diminishing returns to longer chains of thought,
  with roughly equal slopes.
- **The demonstrated reason to run many agents is speed, not
  efficiency**: 4 agents ≈ 2× total cost for ~2× faster completion;
  16 agents ≈ 4× cost for ~4× faster (Noam Brown's summary, quoted
  in the post). A higher capability *plateau* for very large groups
  is raised as a possibility, explicitly undemonstrated.
- **Cost reality check**: the post's motivating examples are
  frontier-priced (a 10,000-agent run estimated at ~$20M at API
  prices; 300B tokens, 5M messages, 88 hours on a mathematics
  problem). It frames such runs as demonstrations, not a new
  price/performance level.
- **Failure modes named or implied**: coordination overhead is the
  whole λ story (agents "stepping on toes"); returns diminish
  logarithmically in both scaling directions; the λ measured at
  1→4→16 may not hold at 1,000→4,000; one anecdote (agents in an
  evaluation illicitly coordinating) is a monitoring/alignment
  caution, not a scaling result. The post's own closing correction
  retracts a speculation about the 10,000-agent run's chart.
- The post studies **parallel copies working the same problem with
  messaging between them** — a mesh of peers. It does not study
  serial assembly lines, fixed stations, or checker gates at all.

### What transfers to the school design

- **The λ accounting frame.** The trial should report an
  efficiency ratio in exactly this spirit: school output per unit
  compute versus the single-model baseline at equal compute. If the
  school cannot beat or match the baseline on cost per accepted
  image, the post predicts we will have paid a coordination tax for
  nothing but speed — and speed is not what a batch art pipeline is
  short of.
- **Task-dependence of λ.** A serial line with narrow stations is a
  deliberate attempt to push the effective λ of *this* workload up:
  stations don't step on toes because they don't share a problem.
  The trial is, in effect, a test of whether decomposition beats
  the post's peer-mesh numbers on a decomposable workload. That is
  a real, falsifiable question — the post gives us the null
  hypothesis (expect ~half-efficiency or worse) to beat.
- **Diminishing returns discipline**: cap station count and copies
  per station in the trial design; more stations is a cost curve,
  not a virtue.

### What does not transfer

- **The benchmark numbers.** BrowseComp / SEC-Bench Pro /
  Terminal-Bench λ values are for frontier models on research,
  security, and terminal tasks. They say nothing quantitative about
  3B local models writing image prompts. We borrow the frame, not
  the constants.
- **The peer-mesh topology.** The post's agents message each other
  freely (5M messages in the big run). The school is the opposite
  bet: no free messaging, fixed hand-offs, deterministic checkers
  between stations. Nothing in the post validates or refutes that
  bet — it is untested there.
- **Scale.** 1,200–10,000 frontier agents at API prices versus a
  handful of local 3B copies on one A6000. The estate's constraints
  (residency, rose throughput under concurrency — still unmeasured
  per stream A) dominate at our scale, not λ.

---

## 2. Candidate benchmarks

| Candidate | Class | Reason |
|---|---|---|
| λ / "stepping on toes" efficiency accounting (from the LW post) | **ADAPT** | The frame, not the constants: headline trial metric = accepted output per unit compute, school vs single-model baseline at equal budget. Gives the trial a pre-registered null hypothesis (peer-mesh λ ≈ 0.5–0.68 ⇒ expect to pay ~2× compute for parity) that the assembly-line design must beat to justify itself. |
| GenEval (object-focused T2I alignment) | **ADAPT** | Per fetched summaries: six compositional tasks (single object, two objects, counting, colours, position, attribute binding) scored by object detection + colour classification over 4 generations per prompt — i.e., a *deterministic checker* verifying prompt elements, exactly the school's between-station pattern. Adapt its task taxonomy and detector-verified scoring shape into a light-show prompt-adherence checker over an estate-authored brief set; do not adopt its prompt set (generic scenes, not game-art briefs) or claim GenEval comparability. |
| DPG-Bench (dense prompt / detail preservation) | **SKIP** (trial 1) | Fetched summary: fine-grained attribute accuracy, 0–100. Relevant later for refinement-station quality, but it scores the generator, not the line; trial 1 measures the line. Revisit if the refinement station needs its own yardstick. Deeper content UNDETERMINED beyond the fetched summary. |
| DrawBench (200 prompts) | **SKIP** | Glossary-fetched: 200 prompts for compositionality/spatial/binding. A prompt *set*, not a method; the estate's briefs (companion art, scene briefs) are the ecologically valid set for light-show. |
| HPS / ImageReward (learned human-preference scorers) | **ADAPT** (pattern only) | Glossary-fetched: HPS trained on 798K human preferences; ImageReward on 137K expert comparisons, BLIP-based. The *pattern* — a learned scorer as the selection station — is what the trial uses, filled by Mira. The models themselves: SKIP as components (domain fit for anime-style SDXL output UNDETERMINED; two more models to host). Trial instead measures Mira's scorer reliability directly (below). |
| Scorer-reliability measurement (inter-annotator agreement) | **FOLD IN** | Glossary-fetched concept, estate-executed: Mira scores every candidate; the Owner/Pax spot-check a sample; report agreement (Cohen's κ on accept/reject). Without this number, "Mira selects" is an unmeasured station. Cheap, decisive, and it is the image-side analogue of stream B's error-cause reading (41/41 there). |
| FID | **SKIP** | Glossary-fetched: distributional distance between generated and reference feature sets. Set-level, needs a reference corpus, says nothing about per-image acceptance or station behaviour. Wrong instrument for a line trial. |
| Hand-off fidelity / error-compounding harness | **FROM-SCRATCH** | No fetched benchmark measures what the school actually risks: does station N+1 preserve the fields station N produced (character, outfit, palette, framing), and how does end-to-end yield decay as stations multiply? Build estate-side: per-station format-adherence rate, field-preservation rate across each hand-off, checker catch rate, end-to-end yield, and the compounding curve (yield vs station count at fixed per-station rates). Grounded in stream B's format findings (structured vs fenced-JSON arrivals) and the MATE F1–F5 taxonomy. |
| MATE F1–F5 checkers + deterministic scorer (estate, existing) | **FOLD IN** | Already built and doctrine-backed: F1 invented-fact and F5 format-drift checkers gate school text stations the same way they gate MATE digests. A school output class is admissible exactly where such a checker exists (stream A, condition 1). |
| Stream A auction/attention substrate measures | **FOLD IN** (substrate, not trial content) | Shared attention, timeouts, and the auction already have their fidelity numbers (robust at 40; checkpointed decide; sharded boards past ~30 floor-users/hour). The image trial runs *on* that substrate; it does not re-litigate it. |

## 3. Candidate skills (mcprush `skills?q=swarm` — 86 listed, ~20 rows rendered)

Reminder: skills are ungraded; context cost and licence are the only
quality axes the listing offers.

| Candidate | Class | Reason |
|---|---|---|
| Advanced Swarm Orchestration — ruvnet (detail-read; MIT; 6k ctx, 5,880 on trigger; v2.0.0) | **SKIP** | A pattern book for the Claude Flow platform (its quick-start installs `claude-flow@alpha` globally and drives `swarm_init` mesh topologies). The school is a serial line on phlow's substrate, not a peer mesh on someone else's platform; 6k on-trigger tokens is the heavy end of the catalog. Nothing in the read portion addresses stations, checkers, or identical copies. |
| Swarm CLI Quick Reference — joelhooks (700 ctx) | **SKIP** | A command card for one specific CLI (hivemind memory, hive tasks, swarmmail) the estate does not run. Cheap context, wrong tool. |
| Flow Nexus Swarm & Workflow Orchestration — aegntic / ruvnet (4.2k ctx, listed twice) | **SKIP** | Cloud-platform deployment skill; the estate is local-first on primo, and a hosted orchestration dependency is the opposite of the school's substrate. |
| /swarm — Collaborative Swarm Mode — vibeeval (1.3k ctx) | **SKIP** | Free-form parallel collaboration ("agents ask each other questions, develop together") — the peer-mesh pattern the school design deliberately replaces with bounded stations. |
| Swarm Issue — ruvnet (3.6k ctx); Swarm Initializer Agent — ruvnet (1k ctx) | **SKIP** | Claude Flow issue-coordination and init plumbing. Platform-specific; phlow already owns dispatch and focus. |
| /ork:swarm-migrate — Cross-Repo Migration Swarm — yonatangross (3.8k ctx) | **SKIP** | One coordinator + N subagents applying the same repo transformation. A fan-out pattern for migrations; not this trial, and the estate's subagent idiom already covers fan-out. |
| "Initialize a multi-agent swarm with anti-drift configuration" (325 ctx; publisher not identifiable from the fetch) | **ADAPT** (listing-only) | The one listing whose premise matches a school need: pinned, identical configuration across copies is exactly the identical-copy discipline. Cannot fold in (unidentifiable, unversioned in the fetch); take the idea — a station config is a pinned artifact, hashed into the run record — which the trial design adopts. |
| "Attack one prompt with a parallel team of sub-agents, each on the model that fits its job" (6.7k ctx; unnamed in fetch) | **ADAPT** (pattern already embodied) | Model-per-job assignment is stream B's routing table in prose form. The trial's stations are homogeneous by design (identical copies), so the pattern applies only at the edges (Mira scoring, roster escalation). Nothing to install. |
| Fan-out worker cards (several, 550–725 ctx, unnamed: "Fan out N parallel workers, drain them, and return one report") | **SKIP** | Duplicate the estate's native subagent fan-out; unnamed in the fetch; fan-out is not the assembly-line pattern under test. |
| "Multi-agent coordination patterns for OpenCode swarm workflows" (9.6k ctx) | **SKIP** | Heaviest listing rendered; written for a different harness (OpenCode). |

**Net skills finding**: the catalog's school-adjacent skills are
orchestration prose for other platforms (Claude Flow above all) and
for peer-mesh topologies. The trial needs no skill from this search;
the one transferable idea (pinned anti-drift configuration) is
already estate doctrine in artifact form.

## 4. Candidate tools / servers (mcprush `catalog?q=swarm` — 89 listed, ~20 cards rendered)

| Candidate | Class | Reason |
|---|---|---|
| Swarm Rd Orchestrator — RudrenduPaul (detail-read; 3 tools: `append_delta`, `pull_deltas`, `list_tasks`; mcprush grade 100/100; 53 downloads/30d; publisher unclaimed) | **ADAPT** | An append-only event log as the cross-agent context mechanism — the same shape as phlow's ledger and the MATE file protocol. Do not install (a second ledger duplicates the substrate and splits the record); take it as outside confirmation of the append-only hand-off design, and note its delta-pull idiom if station hand-offs ever need a pull model. Its grade measures its declared surface, per the Lupin audit's caveat — not runtime behaviour. |
| "Local mail for coding-agent sessions on one machine" (22 tools; publisher not identifiable from the fetch) | **SKIP** | A mailbox transport for agent sessions. The estate's stations communicate by structured hand-off artifacts on the ledger, not by mail; adding a mail transport adds a failure surface the trial doesn't need. |
| "Multi-agent context sharing, memory, and status coordination" (10 tools; unnamed in fetch) | **SKIP** | Duplicates periscope/attention functions already in the fleet; unnamed and unassessable beyond the card line. |
| "Neural network swarm orchestration with WebAssembly acceleration" (15 tools, 413/day; initials-only) | **SKIP** | An orchestration platform; phlow is the estate's orchestrator and is mid-build (scheduler S1–S3). A second orchestrator is precisely what the skill-first doctrine says to refuse without demonstrated need. |
| "Full Agent Swarm API and MCP server with local SQLite storage" (initials-only) | **SKIP** | Same reasoning: a general multi-agent platform duplicating phlow + attention. |
| Claude Flow hive-mind server (87 tools, 1.2k/day; initials-only) | **SKIP** | The platform behind most of the skills above. 87 tools of someone else's orchestration; estate posture is one orchestrator, ours. |
| "MCP server that launches Claude Code/Codex sub-agents" (16 tools) | **SKIP** | Duplicates native subagent dispatch; the school runner needs station discipline, not another launcher. |
| Marketplace / payment cluster — SwarmSync marketplace, SwarmDock (61 tools), settlement protocol for agent groups (hash-chained ledger, 19 tools), x402 hire-and-pay agents, SwarmTrade, agent reputation network (ELO/Nostr), USDC payment layer | **SKIP** (as a class) | Money movement, external marketplaces, and reputation economies. The estate is local-first with no egress posture for agent payments (the crypto lane prices in USDC but settles deliberately, Owner-gated — it does not hire strangers' agents). None of it touches the image trial. The settlement entry's hash-chained ledger is a pattern phlow's ledger already embodies. |
| "Build and run autonomous AI agents with OpenClaw, Hermes…" (5 tools) | **SKIP** | Another agent framework; framework-collecting is not a trial input. |
| Skills-manager CLI/MCP across ~45 agent CLIs (21 tools) | **SKIP** | Skill *distribution* tooling; the estate vendors skills into its own library under its own review. Unrelated to running a school. |
| "161 AI agents for code gen, health, AI/ML, infra…" (initials-only) | **SKIP** | A bundle of prebuilt agents. The trial's premise is identical copies of one small estate model, not a rented crowd. |
| "Risk-first pre-trade checks… Shadow Tournament" (33 tools) | **SKIP** | Trading domain; surfaced by the query on wording only. |

**Net tools finding**: nothing in this search earns a place in the
trial. The plausible mechanisms (append-only log, mail transport,
context sharing) are all shapes the estate already owns in phlow,
the attention board, and the MATE file protocol. The rest is
platforms duplicating phlow and marketplaces outside estate
posture. This matches the skills-review pattern: the catalog is a
mirror that mostly confirms the estate's existing shapes.

---

## 5. First-trial design sketch — light-show image school

Built **only** from FOLD IN / ADAPT / FROM-SCRATCH items above.
Model discipline, per the Owner's commission: every text station is
a copy of the **same** small model. The stream A ladder picks it:
**hf-qwen2.5-coder-3b** (160 tok/s, 2.1 GB) — the smallest tier that
produced near-correct structured output; 1.5B is the fallback if
format adherence at 3B disappoints, sub-1B is excluded by evidence.
Iris generates; Mira scores. No station invents its own model.

### Station map

| # | Station (one 3B copy each) | Input → Output | Checker between stations (deterministic) |
|---|---|---|---|
| S0 | Brief intake | Frozen brief (template: character, scene, outfit, palette, framing, must-include, must-exclude) → structured brief record | Schema validation; the brief set is frozen before the run, so S0 is transcription, not creation |
| S1 | Prompt drafting | Brief record → candidate prompt (tag-form + prose, per the estate's regen-brief practice) | **C1**: format gate (parseable structure); required-token presence (every must-include field appears); length bounds |
| S2 | Prompt refinement | Brief + S1 prompt + C1 flags → revised prompt | **C2**: negative-prompt hygiene — banned-term list, contradiction scan (must-include ∩ must-exclude = ∅), duplicate-token removal verified, no must-include field lost vs S1 (field-preservation check) |
| S3 | Variation / seed planning | Final prompt → seed plan (JSON: N seeds, per-seed variation axis — pose/expression/lighting — within brief bounds) | **C3**: plan schema; seed uniqueness; variation axes confined to the brief's allowed set; N within the run budget |
| G | Generation (not a model station) | Prompt + seed plan → N candidate images via Iris/ComfyUI | **C4**: mechanical pre-checks — dimensions exact, non-blank (pixel variance, per the ComfyUI smoke practice), file hash recorded |
| S4 | Scoring / selection | Candidates + brief rubric → per-image scores + one selection | Mira scores against the rubric; **spot-check protocol**: Owner/Pax judge a random sample blind; agreement (κ) reported with the run. Deterministic code counts and tallies — never Mira (stream B rule) |
| — | Record | — | Provenance manifest per accepted image: brief id, station outputs, checker verdicts, seeds, hashes, scorer scores, spot-check outcome (atelier's manifest idiom, adopted early) |

Escalation: a brief that fails C1/C2 twice routes to a roster model
(Opal/Clara class) once, and the escalation is counted — escalations
are a measured cost of the school, not a silent rescue.

### Arms and measurements

Two arms at **equal generation budget** per brief:

- **School arm**: the line above.
- **Baseline arm**: one 3B copy writes the final prompt directly
  from the brief (no stations, no checkers), same seed count, same
  scorer.

Measured, per brief and in aggregate:

- **End-to-end yield**: accepted images / briefs per arm (accept =
  passes C4 and is selected at S4; spot-check can overturn).
- **Cost per accepted image**: GPU-seconds (generation + Mira) and
  total tokens per arm.
- **λ-style efficiency ratio**: baseline cost-per-accepted ÷ school
  cost-per-accepted at equal budget — the trial's headline number,
  against the post's null expectation (≤ ~1 means the line paid a
  coordination tax; > 1 means decomposition won on this workload).
- **Hand-off fidelity**: field-preservation rate at each checker
  (from the FROM-SCRATCH harness) — which hand-off loses fields,
  and how yield compounds per added station.
- **Station error rates**: C1–C3 catch rates per station; S4
  overturn rate from spot-checks; Mira-vs-human κ.
- **Diversity vs drift**: within a brief's accepted set, variation
  axes actually exercised (from seed plans) vs scorer-flagged
  off-brief selections. (A numeric image-diversity metric is
  UNDETERMINED at this writing — no fetched source grounds one for
  this use; v1 uses the seed-plan + spot-check record.)

### What the trial needs that does not exist yet

1. **The hand-off fidelity harness** (FROM-SCRATCH, §2) — the
   field-preservation and compounding instrumentation. Small,
   deterministic, built before the run.
2. **A runnable generation path in the loop.** Atelier S1 is not
   built; the trial either waits for it or runs generation through
   the proven manual ComfyUI API path (headless, A6000, localhost —
   the 2026-10-20 smoke shape) with atelier's manifest format
   adopted on paper. See open decision OD-2.
3. **A frozen light-show brief set** — a fixed set of briefs (the
   estate has real ones waiting: companion/README art and the
   regen-brief idiom from the Strobe gen test). Size is a decision
   (OD-3); the set must be frozen before any run counts.
4. **The scoring rubric + spot-check protocol** as written
   artifacts (rubric fields per brief type; sample size; who
   judges; the Owner's perception remains the final gate for any
   image that ships — the trial measures the line, it does not
   promote its selections to production art).
5. **A school runner** — thin orchestration: spawn station copies
   via rose `/api/chat` only (the standing probe discipline),
   enforce station timeouts and the shared-attention board, write
   the run record. A script suffices for trial 1; phlow integration
   is later work, behind the scheduler gates.
6. **Concurrency evidence**: rose throughput under several
   concurrent 3B contexts is unmeasured (stream A's open item);
   trial 1 runs stations serially per brief and parallelises across
   briefs only as far as a pre-run probe supports.

---

## 6. Open decisions for the Owner

- **OD-1 — School model confirmation.** Trial holds the model
  constant at hf-qwen2.5-coder-3b at every text station (the
  Owner's identical-copy premise + stream A's ladder). Confirm, or
  name a different constant model.
- **OD-2 — Generation path.** Wait for atelier S1 (cleaner
  provenance, later start) or run trial 1 on the proven ComfyUI API
  path with atelier's manifest format adopted on paper (earlier
  start, throwaway glue)? Recommendation: the API path — the trial
  measures the *line*, and atelier S1's gate shouldn't be rushed by
  a study's schedule.
- **OD-3 — Brief-set size.** Enough briefs for a yield comparison
  that means something (suggest 20–30 frozen briefs across companion
  and scene types) versus a 6-brief smoke that only proves the line
  runs. Recommendation: smoke first (line correctness), then the
  full set as trial 1 proper — the same pilot-then-fleet shape as
  the NSFW pass.
- **OD-4 — Acceptance authority during the trial.** S4 selects, the
  spot-check measures the selector, but no trial image becomes
  production art without the Owner's eye. Confirm that stands (it
  is the standing creative-work rule; stated here so the trial
  design doesn't quietly assume otherwise).

---

## 7. Framework layer — shared attention, auction/timeouts, OpenAPPA (added 2026-10-21, Owner scope addition)

Sections 2 and 5 treated this framework as settled background (the
§2 table's "substrate, not trial content" row). The Owner's ruling
supersedes that framing: the framework is a **mapped layer of this
trial and part of what the trial measures**. This section is the
mapping. Sources: `AUCTION-PROTOCOL.md` (R1–R11) and stream A
RESULTS (fidelity numbers, caps). Where the protocol sources and
the trial design as evaluated above contradict each other, the
contradiction is flagged in §7.5, not harmonised away.

### 7.1 Contention mapping — the generation slot is the floor

In MATE, the shared-attention floor is the single lease-claimed
resource every agent contends for. In this trial the analogous
resource is the **GPU generation slot**: Iris/ComfyUI generation on
the one A6000. It is scarcer than the abstract floor in one way and
shared with more tenants in another:

- Rose serves every text station copy *and* Mira from the same
  card generation runs on. Text-station calls are short and cheap,
  but they are GPU-resident; the floor lease governs who may run a
  generation batch, not who may think.
- Stations and job chains claim the slot through the attention
  tools: `attention_publish` (a queued generation job is a bid,
  decaying per R11), `attention_focus` (winning the slot is a
  lease, evidence-renewed per R10), `attention_decide` (the
  deterministic award, re-run at dispatch per R7).

**Stream A's floor arithmetic, applied to generation.** Stream A:
one floor with 120 s holds serves at most 30 holders/hour, with a
useful fraction of ~75% under healthy rotation. Trial numbers
(estate ComfyUI smoke, 2026-10-20: ~16 s per 1024×1024 image on the
A6000): a seed batch of N=4 is a ~60–80 s floor hold, so one floor
honestly supports **~35–45 generation batches/hour** at the
measured useful fraction. Mira scoring claims the floor in short
holds of its own (per-candidate-batch; the wall time of a Mira
scoring call is unmeasured — see §7.4). Total trial demand is
small: a 20–30 brief set × 2 arms × one generation batch per brief
is 40–60 floor claims across the whole run, plus scoring holds.
**At trial scale (8–16 copies) the floor binds as queueing, not
saturation**: at most 8–16 brief chains are in flight, text
stations never hold the floor, and claims serialise at G and S4.

One fairness consequence: **both arms share the one floor.**
Equal generation budget (§5) must therefore be accounted in
floor-seconds per arm in the run record, or the baseline arm can
quietly starve the school arm (or vice versa) and corrupt the
headline efficiency ratio.

**When sharded boards become necessary.** Stream A's rule:
shard past ~30 sustained floor-users/hour at 120 s holds, and
`BOARD_AGENTS_MAX = 64` per board caps any single board
regardless. Translated to generation: shard when (a) sustained
claim rate × mean hold approaches ~0.7 of one floor's capacity
(the sim's operating density) — e.g. per-image floor claims from
several concurrent chains, or a second generation engine (Vera)
joining the card; or (b) chains in flight grow past the point
where a single decide queue stays honest (the 40-agent robustness
boundary). None of these binds in trial 1; all are the 40+
conditions, recorded so the trigger is recognised when it arrives.

### 7.2 Auction + timeout rules, applied concretely

| Rule | Trial application | Binds at 8–16 copies? |
|---|---|---|
| R9 — awards expire | A station-task award carries a start-by window (sim's representative 60 s, set per station class in the run record). A copy that doesn't start in-window loses the award; the station task re-bids. No standing lost for a lapse; lapses are measured history. | **Yes** — cheap, and it is the trial's defence against a hung copy silently holding a station. |
| R10 — claims are evidence-renewed leases; fencing generations | A running station job holds a lease renewed only by output evidence (artifact written, heartbeat with content — silence never renews). Lease expiry marks the job unheld and re-awards at fencing generation +1; a revived copy's late artifact is rejected against the stale generation, never merged. | **Yes, fully** — a station copy dying mid-job is a named trial case (§7.4), not an edge case. |
| R11 — bids decay | A queued image job's bid decays on a per-class half-life (sim's representative 120 s for attention claims; generation queue classes get their own value in the run record). A brief that attracts no live claim inside its decay horizon is archived *visibly* in the run record, never silently dropped. | **Weakly** — mostly across run pauses (an overnight pause should not resurrect yesterday's queue at full claim). |
| R7 — award ≠ authority; decide() re-runs at dispatch | Every station dispatch re-runs decide() against the live label join and policy fingerprint (§7.3). Sim cost at this scale is ~2.5 ms p99 (N=4–40 rows) — noise next to a 16 s generation. | **Yes** — costless at trial scale, and it is what makes the label layer real rather than decorative. |
| R6 — labels gate eligibility | A station class may only claim jobs whose labels its clearance covers (§7.3); ineligible copies never see the payload, only the labelled abstract. | **Yes**, in the simplified class form of §7.5 flag 3. |
| R5 — the orchestrator stays the market's floor | Pax (via the runner) is executor of last resort and holds kill authority over any lease; escalation to a roster model (§5) routes through this, and is counted. | **Yes** — this is the §5 escalation path, named. |
| R3 / R3′ — credit flows backward; the ledger is the event log | The run record is the ledger: bids, awards, decide outcomes, checker verdicts, gate outcomes. Standing changes are monotone — a station class's standing falls on a failure immediately and rises only on verified passes. | **Yes, at station-class level** (see flag 2). |
| R1 / R4 — bid before assignment; valuation from measurement | Bids and learned valuation operate **between station classes and for escalation routing** (is this brief worth a roster escalation?), not between identical copies. | **Class level only** — see flag 2. |
| R2 — anti-monopsony floor | Every recurring task class keeps ≥2 eligible executors. | **Violated by construction at S4** — see flag 3. |
| R8 — consequential classes need the human signature | No station output is a consequential act. Acceptance into production art is the Owner's act (OD-4), outside the market entirely. | **Does not bind** — nothing in trial 1 is delete/publish/send class. |

### 7.3 OpenAPPA layer — labels on the line

Every artifact on the line carries a flowguard label: **audience ×
trust**. Labels are computed by deterministic code and recorded in
the run ledger. **A model never labels its own output** — a copy's
self-report of its artifact's trust is not data (stream A,
condition 1: a tiny agent's clearance is ledger data, never
self-report).

- The frozen brief record enters with the run's most restrictive
  school-internal audience and Owner-frozen trust (highest on the
  line — it is the spec everything is checked against).
- Each station's output label is the **join** of its input labels:
  reader-set **intersection** on audience, **minimum** on trust.
  The refined prompt's label = join(brief, draft, C1/C2 flags); the
  generated image's = join(prompt, seed plan); the selection
  record's = join(image, Mira scores, spot-check outcome).
- Because the join takes trust-min, **no checker pass can launder
  trust upward**: C1–C4 verify form and content constraints, and a
  pass is recorded — but the artifact's trust stays at the minimum
  of its inputs until a *human* act (the Owner's acceptance, OD-4)
  re-labels it by authority. Downgrade is unrepresentable for the
  same reason in the other direction: no station can emit an
  artifact labelled broader-audience or higher-trust than the join
  of what it consumed.
- decide() re-runs at each station dispatch (R7): if the live
  label join or the policy fingerprint has moved since the award,
  the award is void and the task re-bids. In trial 1 the live
  consequence is modest (labels are stable inside a run), but the
  mechanism runs, is ledgered, and its cost is measured (§7.4).
- Correctness stays in the checker net: labels govern *who may
  touch what and how far it may travel*; C1–C4 and the F1/F5
  checkers govern *whether it is right*. Neither substitutes for
  the other.

### 7.4 Inherited vs to-be-measured

**Settled inheritances from stream A** (relied on, not re-tested):

- Safety invariants: zero fencing and zero label violations across
  all 24 sim runs including churn with silent holder deaths;
  zombie late writes rejected by the generation check every time.
- Stale-claim cost is bounded by the lease TTL (60–240 s of stale
  floor per churn-hour) — detection time is a TTL, not a watchdog.
- Robustness at N=40: trial scale (8–16 copies) sits inside the
  proven envelope; code caps (32 concurrent sessions, 64 agents
  per board) are not approached.
- decide() latency scales with ledger events, not headcount;
  checkpointed decide (checkpoint digest + ≤10k-event tail) holds
  p99 at 19–21 ms at every N — adopted as a design rule for the
  runner's ledger discipline from day one.
- Floor-saturation arithmetic (≤30 holders/hour at 120 s holds;
  ~75% useful fraction) as the planning formula §7.1 applies.
- Award timeouts ≈ 0 except churn (≤3.2%), where they are the
  protocol working, not failing.

**What this trial must newly measure about the framework:**

1. **Floor contention under real generation load.** Hold-time
   distribution for real Iris seed batches (not the sim's uniform
   120 s); the floor's useful fraction when generation, Mira
   scoring, and text-station calls share one card; whether Mira
   scoring's floor holds are short enough to interleave or long
   enough to need their own class.
2. **Lease behaviour when a station copy dies mid-job.** Inject
   the kill (a named trial case, not an accident): time from death
   to lease expiry (does it match the TTL?), fencing rejection of
   the dead copy's late artifact if it revives, re-award latency,
   and end-to-end yield cost of one death per run.
3. **Label-join correctness across stations in practice.** Audit
   a sample of run artifacts: recorded label vs join(inputs)
   recomputed from the ledger. The sim proved the algebra; join
   *implementation* bugs are exactly what a simulation cannot
   catch, and a single mislabelled hand-off invalidates the
   layer's claims for the run.
4. **decide() re-run cost through the real attention tools** —
   replacing stream A's modelled 2 µs/event with a measurement at
   trial ledger sizes.
5. **Award-expiry behaviour under real rose latency.** Stream A's
   probes were steady-state; first-call load walls (a station
   copy's first call after a model swap) could cause spurious R9
   expiries the sim never produced. Count them separately.
6. **Bid decay on a real paused queue.** Pause the run; observe
   whether queued jobs decay and archive visibly per R11 instead
   of resuming at full claim.

### 7.5 Contradictions flagged, not harmonised

1. **This section supersedes §2's framing.** The benchmark table
   classified the substrate "FOLD IN (substrate, not trial
   content)" and §5 mentioned the board in one subordinate clause.
   The Owner's scope addition makes the framework a measured
   layer; the §2 row is left as written so the change of posture
   is on the record, and this section governs.
2. **The market protocol's premise is heterogeneous executors;
   the trial's premise is identical copies.** AUCTION-PROTOCOL,
   following Gemp et al., holds that perfect competition among
   clones collapses (winner's profit → 0, nobody participates) and
   that the viable regime is imperfect competition among agents
   with different costs — R1/R4 bidding and learned valuation
   presuppose that heterogeneity. Between identical copies of one
   3B, per-copy bids and per-copy valuation carry no information.
   The trial therefore runs the market at station-class and
   escalation level only (R1/R4 rows, §7.2), and whether an
   assembly line needs a market *inside* a station at all is
   recorded as an open question this trial does not resolve. The
   timeout and label rules (R6, R7, R9–R11) do not depend on the
   price machinery and bind in full.
3. **The single-scorer hazard is R6's named failure, adopted
   knowingly.** R2 requires ≥2 eligible executors per class and R6
   names the one-executor eligible set "label-induced monopsony —
   a named hazard, not a quiet award." S4 has exactly one eligible
   scorer: Mira. Trial 1 does not design this away; it mitigates
   with the κ spot-check protocol and the Owner acceptance gate
   (OD-4) and records the hazard as carried. A second scorer is a
   trial-2 question, with trial 1's κ number as its evidence.
4. **The trial implements R9–R11 runner-side before phlow does.**
   Stream A is explicit: the market semantics (leases/decay in
   phlow-attention) are S3 work and do not exist in code yet. The
   §5 runner therefore implements award expiry, evidence leases,
   fencing, and decay itself, per the protocol text, ledgered in
   the run record. Consequence, stated plainly: **trial results
   measure the protocol's behaviour, not phlow's implementation
   of it**, and must not be cited as phlow validation. When S3
   lands, the runner's semantics are the conformance target, not
   the other way round.
