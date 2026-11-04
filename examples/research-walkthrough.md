# End-to-End Walkthrough: Discovering, Reviewing, and Updating a Research Direction

> This walkthrough traces how K Research handles an open-ended research request—from initial problem framing and first-principles method design, through parallel subagent review (`red-team` and `novelty-audit`), to a follow-on decisive test and belief update. Real papers are cited accurately at the mechanism level; the candidate proposals, review rounds, and experimental observations below are an illustrative project trace.

## What this example shows about K Research

| Characteristic | Typical one-shot LLM research prompt | How K Research works in this walkthrough |
|---|---|---|
| **Problem definition** | Lists generic "future work" gaps from survey introductions. | Identifies a shared assumption across competing methods and traces a concrete failure scenario (`opportunity-discovery`). |
| **Method development** | Combines three trending keywords into a named black-box module. | Designs the most direct mechanism from first principles, defines inputs and operations explicitly, and works through a concrete numerical trace (`hypothesis-development`). |
| **Handling prior work** | Claims novelty because no single paper combines all listed components. | Separates problem, mechanism, method, and boundary dimensions; refuses to bolt on defensive complexity merely to look different (`novelty-audit`). |
| **Quality control** | Self-critiques mildly or accepts every brainstormed candidate. | Dispatches independent `red-team` and `novelty-audit` subagents in parallel on the same frozen proposal; the parent agent rejects one candidate (`D-01`) and simplifies the other (`D-02`). |
| **Default stop point** | Dumps a 6-benchmark evaluation table before the method is even well-defined. | Ends direction discovery with a **Research Brief** (problem, method, worked example, closest-work comparison, and recommendation). Detailed experiment design waits until requested (`decisive-test-design`). |
| **Project artifacts** | Emits a new standalone report per prompt (`report_v1.md`, `audit_2.md`). | Updates one living project tree (`README.md`, `research/`, `papers/`) and appends traceable judgment shifts to `research/decisions.md` (`belief-update`). |

---

## 1. User request and living project layout

Suppose the researcher starts with the prompt from the repository README:

```text
Read <repo>/skills/discover-research-direction/SKILL.md and follow it
to explore research directions in efficient long-context inference.
```

After clarifying that the researcher cares about **multi-turn coding and debugging sessions on a single 24 GB GPU (where CPU KV-cache offloading is unavailable or latency-prohibitive)**, K Research maintains a single project tree following [Project Layout](../docs/PROJECT-LAYOUT.md):

```text
README.md
research/
  overview.md
  decisions.md
  directions/
    anchor-rematerialization/
      proposal.md
      related-work.md
      evaluation-plan.md      # created later, only when validation is requested
papers/
  index.md
  references.bib
  notes/
    zhang-2023-h2o.md
    li-2024-snapkv.md
    tang-2024-quest.md
    xiao-2024-infllm.md
  pdf/
    ...
.research/
  state/
  cache/
  scratch/
```

Skills update these files in place by research object rather than saving a report per skill invocation.

---

## 2. From literature synthesis to a concrete problem (`research/overview.md`)

Using `collect-paper`, `paper-analysis`, `field-synthesis`, and `opportunity-discovery`, the agent maps the relevant literature and isolates a specific failure mode rather than a vague topic gap.

### Excerpt from `research/overview.md`

```markdown
# Research Overview

- Project ID: `multi-turn-kv-eviction`
- Updated: `2026-11-04`

## Research question and scope

How can an autoregressive language model maintain multi-turn reasoning accuracy under a strict GPU KV-cache budget (no host-memory KV offloading) when early context spans become temporarily irrelevant for several turns and then become critical again? See `../papers/index.md` for the 18-paper corpus and search boundary.

## Field account

Existing long-context KV management under memory constraints splits into two lines:

1. **Permanent token eviction (`zhang-2023-h2o`, `li-2024-snapkv`):** Bounds GPU memory by permanently discarding KV states whose cumulative attention (`zhang-2023-h2o`, Sec. 3.2) or prompt-window observation attention (`li-2024-snapkv`, Sec. 3.1) falls below a threshold.
2. **Query-aware page or block selection (`tang-2024-quest`, `xiao-2024-infllm`):** Preserves all KV states in GPU pages (`tang-2024-quest`, Sec. 3) or offloaded CPU memory (`xiao-2024-infllm`, Sec. 3.2) and retrieves top-scoring blocks dynamically per query.

**Shared assumption and tension:** Permanent eviction methods assume that *attention weight during the current turn predicts utility in future turns*. Query-aware selection removes that assumption but requires retaining the full KV tensor across turns (in VRAM or over PCIe).

## Problems and candidate directions

### Problem: Cross-turn eviction blindness in strictly memory-bounded sessions

- **Setting:** Multi-turn coding or debugging sessions where total context exceeds the GPU KV budget $B$, and retaining or transferring full KV tensors from host RAM is excluded by hardware or latency constraints.
- **Concrete scenario:** In Turn 1, the user provides a 400-token stack trace (`Span 1`). In Turn 2, the agent inspects a 2,400-token configuration file (`Span 2`) to check environment variables; during Turn 2, `Span 1` receives near-zero attention and is permanently evicted under a 1,024-token budget. In Turn 3, the user asks: *"Now patch the line in the original traceback that threw `KeyError`."* The evicted traceback KV states are gone, causing the model to guess the line number and variable name.
- **Candidate directions considered:**
  1. `block-summary-gating` (`rejected`, see `decisions.md#d-01-reject-block-summary-gating`): Store a mean-pooled key-value summary vector per evicted block and train a lightweight uncertainty gate to decide when to retain blocks.
  2. `anchor-rematerialization` (`pursue`, see `directions/anchor-rematerialization/proposal.md`): Evict low-attention interior KV states from VRAM, retain two unpooled boundary anchor tokens per evicted span plus a byte-offset pointer into the already-buffered plaintext transcript, and selectively re-prefill at most $K$ re-activated spans when a future turn's query attends to their anchors.

## Current recommendation

**Pursue `anchor-rematerialization`** (`decisions.md#d-02-pursue-anchor-rematerialization`). It exploits an asymmetry specific to text-based sessions: the raw token IDs (~4 bytes/token) are already resident in host memory even when the multi-megabyte FP16 KV states must be evicted from VRAM.

## Next action

Resolve whether single-pass selective re-prefill at original Rotary Position Embedding (RoPE) indices preserves downstream attention fidelity without intermediate evicted context.
```

---

## 3. Parallel review and revision: how K Research filters and sharpens methods

When `hypothesis-development` develops candidate methods, it does **not** immediately accept them or pad them with extra modules to look novel. Selected candidates go through two independent subagent reviews in parallel—`red-team` and `novelty-audit`—followed by parent integration.

### Why Candidate 1 (`block-summary-gating`) was rejected instead of padded

An early sketch proposed keeping a mean-pooled KV vector for each evicted 64-token block and training an uncertainty-conditioned gate to blend summary vectors into attention.

- **`novelty-audit` finding:** Indexing block-level key summaries for dynamic query matching is already established by Quest (`tang-2024-quest`, Sec. 3.1, min/max page bounds) and InfLLM (`xiao-2024-infllm`, Sec. 3.2, representative block tokens). Where KV states are permanently evicted, a gate over a single summary vector cannot recover token-level details such as line numbers or variable names.
- **`red-team` finding (`fatal`):** In RoPE-based transformers, keys at positions $p_1 \dots p_{64}$ are rotated by position-dependent frequencies before caching. Mean-pooling post-RoPE keys across positions causes destructive phase interference, making the pooled vector's dot product with a future query unreliable.
- **Parent action:** A weak workflow would try to "save" the idea by adding a learned de-rotation MLP and a contrastive uncertainty loss. Following K Research's design rules, the parent rejects `block-summary-gating` (`D-01`) and focuses on Candidate 2.

### How Candidate 2 (`anchor-rematerialization`) was revised after parallel review

In the initial draft of `anchor-rematerialization`, each evicted contiguous span retained a single mean-pooled landmark key in VRAM and re-prefilled any span whose landmark score exceeded a threshold $\tau$.

1. **`red-team` subagent review:**
   - **Major objection 1 (RoPE phase mixing on landmarks):** Even if re-prefill uses plaintext tokens, using a mean-pooled key as the retrieval trigger suffers from RoPE phase cancellation unless keys are stored pre-RoPE or anchored to real unpooled tokens.
   - **Major objection 2 (Unbounded re-prefill latency):** Threshold-based triggering ($\text{score} > \tau$) can fire on many spans simultaneously, causing Turn 3 prefill latency to exceed full-cache eviction budgets.
   - **Major objection 3 (Causal gap during re-prefill):** Re-prefilling `Span 1` in isolation during Turn 3 omits KV states that preceded or followed it if those were also evicted.
2. **`novelty-audit` subagent review:**
   - Audited against H2O, SnapKV, Quest, and InfLLM (see `related-work.md` below). Classified as `plausible_unverified`: prior eviction methods drop tokens irreversibly, while page-selection methods keep the full KV cache in GPU/CPU memory. Selective re-prefill from host token IDs triggered by retained in-cache anchor tokens targets the strict-VRAM, no-KV-offload boundary.
3. **Parent revision (subtraction over complication):**
   - Replaced the mean-pooled landmark with **two unpooled real tokens kept in the KV cache at their original RoPE positions** (the span's initial header token and its highest-cumulative-attention medoid token). This requires zero auxiliary weights and preserves exact RoPE inner products.
   - Replaced threshold triggering with a **strict top-$K$ cap ($K \le 2$ spans, max 512 tokens re-prefilled per turn)** so worst-case latency is bounded.

### Excerpt from `research/directions/anchor-rematerialization/proposal.md`

```markdown
# Direction Proposal: Anchor-Triggered Span Rematerialization

- Direction / Hypothesis ID: `anchor-rematerialization` (`H-02`)
- Status: `testable`
- Review status: `subagent_parallel`

## Problem and setting

In multi-turn agent sessions under a hard GPU KV-cache ceiling $B$ (tokens), observation-window eviction (`li-2024-snapkv`) permanently deletes KV states from earlier turns whenever intermediate turns shift attention elsewhere. Unlike full-KV CPU offloading (`xiao-2024-infllm`), which transfers tens of megabytes of KV tensors over PCIe per turn, a text-based session already holds the raw token IDs of prior turns in host memory (~4 KB per 1,024 tokens). The bottleneck is detecting *which* evicted text span a new query needs and rematerializing its KV states within a bounded compute budget.

## Proposed method

- **Inputs:** Active GPU KV cache $\mathcal{C}$ with capacity $B$ tokens; host-memory token buffer $\mathcal{T}$ storing full turn token IDs and original position indices; new turn query tokens $Q_t$ of length $L_q$; rematerialization budget $K$ spans (at most $M_{\max}$ tokens total).
- **Step 1 (Span-grouped eviction with dual anchors):** When $|\mathcal{C}| + L_q > B$, partition low-attention historical tokens into contiguous semantic spans $S_i$ (bounded by turn/tool delimiters or fixed 128-token chunks). Instead of deleting $S_i$ completely, evict its interior KV states from $\mathcal{C}$ and retain two real token KV entries in $\mathcal{C}$ at their original position indices:
  1. $a_{i,\text{head}}$: the first non-delimiter token of $S_i$;
  2. $a_{i,\text{med}}$: the token in $S_i$ with the highest cumulative attention score prior to eviction.
  Attach a lightweight metadata record $(p_{\text{start}}, p_{\text{end}})$ pointing to $S_i$'s slice in the host token buffer $\mathcal{T}$.
- **Step 2 (Anchor activation check):** During the prefill of $Q_t$ at a designated retrieval layer $\ell^*$ (e.g., layer $\lfloor N_L / 2 \rfloor$), compute the maximum attention weight from $Q_t$ to the retained anchor pairs:
  $$s(S_i) = \max_{q \in Q_t,\, a \in \{a_{i,\text{head}},\, a_{i,\text{med}}\}} \text{Attn}_{\ell^*}(q, a).$$
- **Step 3 (Bounded selective re-prefill):** Select up to $K$ evicted spans with the highest $s(S_i)$ that exceed the median active-token attention score, subject to $\sum |S_i| \le M_{\max}$. Fetch their token IDs from $\mathcal{T}$, run a partial forward pass conditioned on preceding retained cache entries using their original RoPE position indices $p_{\text{start}} \dots p_{\text{end}}$, and splice the rematerialized KV states back into $\mathcal{C}$ before completing decoding for Turn $t$.

## Design rationale

- **Why keep two real anchor tokens instead of a pooled summary vector?** Retaining unpooled KV entries at their original RoPE positions avoids phase cancellation across positions (resolving the `red-team` RoPE objection) and requires no learned projection or changes to the attention kernel.
- **Why re-prefill from token IDs instead of offloading KV tensors to CPU?** Re-prefilling $M_{\max} = 256$ tokens on GPU takes a single batched matmul pass, avoiding PCIe bandwidth bottlenecks and multi-gigabyte host memory allocation across concurrent sessions.
- **Revisions from parallel review:** Dropped threshold-based triggering in favor of a hard top-$K$ cap ($K=2$, $M_{\max}=256$) to bound worst-case turn latency; retained original position indices during re-prefill to preserve relative RoPE distances.

## Worked example

Consider a KV budget of $B = 1{,}024$ tokens across 3 turns, partitioned into 256-token spans:

1. **Turn 1 (512 tokens):** User submits a 256-token Python traceback (`S1`, positions `0..255`, headed by `Traceback:` and centered on `KeyError: 'auth_token' at client.py:142`) and a 256-token helper file (`S2`, positions `256..511`). Cache occupancy: `512 / 1,024`.
2. **Turn 2 (+768 tokens -> total 1,280 > 1,024):** User pastes a 768-token YAML deployment config (`S3`, `S4`, `S5`, positions `512..1279`) and asks to validate port mappings.
   - **Standard SnapKV (`li-2024-snapkv`):** Scores tokens using the end of Turn 2's prompt. Because Turn 2 only asks about YAML ports, `S1` (the Python traceback) has near-zero attention and all 256 of its tokens are permanently evicted.
   - **Anchor-Rematerialization:** Evicts the 254 interior KV states of `S1`, keeping 2 anchor tokens (`Traceback` at pos `2` and `auth_token` at pos `189`) in GPU cache plus pointer `(0, 255)` into host token buffer $\mathcal{T}$. Cache occupancy stays within `1,024`.
3. **Turn 3 (+64 tokens):** User asks: *"Fix the `auth_token` KeyError from the initial crash."*
   - **Standard SnapKV:** Generates a response without `S1`, guessing the file and line number.
   - **Anchor-Rematerialization:** Query tokens `auth_token` and `KeyError` attend strongly to retained anchor `a_{1,\text{med}}` (`auth_token` at pos `189`) at layer $\ell^*$. Step 3 fetches the 256 token IDs of `S1` from $\mathcal{T}$, re-prefills positions `0..255` into $\mathcal{C}$ (evicting low-attention YAML span `S4` to make room), and decodes with `client.py:142` restored in context.

**Design question exposed by the trace:** If Turn 3 asks *"Fix that crash from Turn 1"* without repeating lexical tokens near `a_{1,\text{med}}`, does the header anchor `a_{1,\text{head}}` (`Traceback`) still receive enough attention at layer $\ell^*$ to trigger rematerialization?

## Closest known work and difference

Shares importance-based eviction with H2O (`zhang-2023-h2o`) and SnapKV (`li-2024-snapkv`), and shares block-level retrieval intuition with Quest (`tang-2024-quest`) and InfLLM (`xiao-2024-infllm`). Differs in **method** and **operating boundary**: prior eviction methods are irreversible, whereas Quest and InfLLM retain the full KV tensor in GPU or CPU memory. See `related-work.md` for the full comparison and search boundary.

## Expected outcome and contribution

Recovers multi-turn needle and debugging recall after intermediate distractor turns under a fixed GPU KV budget, without retaining offloaded KV tensors in host RAM and with bounded re-prefill overhead ($\le 256$ tokens/turn).

## Feasibility, open objections, and next question

- **Compute/resources:** Testable on a single 24 GB GPU with an open-weights 7B–8B model; no training required.
- **Open major objection (`red-team`):** Partial re-prefill of `S1` when preceding spans are evicted might shift deeper-layer KV representations compared to full-prefix prefill. **Probe:** Measure cosine similarity and task accuracy of selective re-prefill against an oracle that retains `S1` from Turn 1.
```

---

## 4. Source-backed novelty audit (`research/directions/anchor-rematerialization/related-work.md`)

Instead of a single intuition score, `novelty-audit` records a structured comparison across contribution dimensions, actively searches for counterevidence, and documents its search boundary.

### Excerpt from `research/directions/anchor-rematerialization/related-work.md`

```markdown
# Novelty Audit: Anchor-Triggered Span Rematerialization

- Direction / Hypothesis ID: `anchor-rematerialization` (`H-02`)
- Audit date: `2026-11-04`
- Outcome: `plausible_unverified`
- Confidence: `medium`

## Candidate and contribution claim

Addresses multi-turn context loss under strict GPU KV eviction (`problem` and `method` dimensions) by retaining two unpooled anchor tokens per evicted span in VRAM and selectively re-prefilling activated spans from host plaintext token IDs. See `proposal.md`.

## Closest prior work

| Paper | Overlapping claim or component | What prior work establishes | Candidate's difference and dimension | Locators (prior / candidate) | Residual uncertainty |
|---|---|---|---|---|---|
| `zhang-2023-h2o` (H2O, NeurIPS 2023) | Retains heavy-hitter tokens with high cumulative attention. | A small fraction of heavy-hitter tokens dominates attention within a single generation pass. | `method`, `boundary`: H2O eviction is permanent; candidate uses retained heavy-hitters as span anchors to trigger selective re-prefill from host token IDs across turns. | H2O Sec. 3.2, Alg. 1 / `proposal.md` Steps 1–3 | Whether a single medoid heavy-hitter per span suffices when cross-turn queries paraphrase earlier context. |
| `li-2024-snapkv` (SnapKV, 2024) | Uses an observation window at the end of the prompt to cluster and retain KV states. | Prompt-end queries accurately identify needed context for single-turn QA. | `problem`, `method`: SnapKV drops spans unused by the current prompt permanently; candidate makes observation-window eviction reversible via plaintext rematerialization. | SnapKV Sec. 3.1, Fig. 2 / `proposal.md` Worked Example | Overhead of splicing re-prefilled spans into clustered KV caches. |
| `tang-2024-quest` (Quest, ICML 2024) | Scores KV pages at query time using page-level key metadata. | Page-level min/max key bounds identify critical KV pages without attending to all tokens. | `boundary`, `method`: Quest keeps all KV pages in memory and masks attention; candidate permanently evicts interior KV states and re-prefills from token IDs using two unpooled anchor tokens. | Quest Sec. 3.1–3.2 / `proposal.md` Step 2 | Need to check whether Quest's min/max page summary can be adapted to trigger token-ID re-prefill. |
| `xiao-2024-infllm` (InfLLM, 2024) | Keeps representative tokens per block to retrieve context units across long sequences. | Representative tokens select relevant blocks from CPU-offloaded KV cache. | `method`, `boundary`: InfLLM stores and transfers full KV blocks from CPU RAM; candidate discards interior KV states completely and recomputes at most $K$ spans from raw token IDs on GPU. | InfLLM Sec. 3.2, Table 1 / `proposal.md` Steps 1 & 3 | Latency trade-off between PCIe KV transfer (InfLLM) and GPU token re-prefill at $M_{\max}=256$. |

## Counterevidence

- **Closest mechanism match:** `xiao-2024-infllm` (Sec. 3.2) already selects context blocks using representative high-attention tokens. If CPU RAM capacity and PCIe bandwidth are unconstrained, InfLLM solves cross-turn block recovery without recomputation. The candidate's contribution holds only in the **strictly memory-bounded / no-KV-offload regime** or where recomputing $\le 256$ tokens on GPU is faster than host-to-device KV transfer.

## Novelty judgment

Classified as `plausible_unverified`. The combination of permanent interior KV eviction, dual unpooled in-cache anchors, and bounded on-GPU token rematerialization is distinct from inspected permanent-eviction and KV-offloading papers, but adjacent systems work on KV recomputation and prefix caching must be checked before claiming a `substantiated` method difference.

## Search boundary and unknowns

| Source / database | Query family | Date range | Results inspected | Coverage notes or access limits |
|---|---|---|---|---|
| arXiv / Semantic Scholar | `("KV cache" OR "key-value cache") AND ("eviction" OR "rematerialization" OR "recomputation") AND ("multi-turn" OR "agent")` | 2022–2026-11 | 28 screened, 11 full-text | Forward citations of H2O, SnapKV, Quest, and InfLLM checked; systems venues (OSDI/SOSP) only partially covered. |

## Next action

Run the diagnostic test in `evaluation-plan.md` (when validation is requested) to verify whether partial span re-prefill without evicted intermediate KV states preserves downstream generation accuracy.
```

---

## 5. Default stop point and traceable decision log (`research/decisions.md`)

**By default, `discover-research-direction` stops here.** The researcher has a complete Research Brief (`research/overview.md`, `proposal.md`, and `related-work.md`) and can judge the problem, method, worked example, and literature position before investing in experiment boilerplate.

Every meaningful judgment made so far is recorded in `research/decisions.md` rather than lost in chat history.

### Excerpt from `research/decisions.md` (after direction discovery)

```markdown
# Research Decisions

## d-01-reject-block-summary-gating: Reject mean-pooled KV summary gating

- Date: `2026-11-04`
- Project: `multi-turn-kv-eviction`
- Decision: `reject`
- Affected artifacts: `research/overview.md`
- Supersedes: `none`

### Decision and rationale

Reject `block-summary-gating`. Parallel review showed that block-level key indexing is already established by `tang-2024-quest` and `xiao-2024-infllm`, while mean-pooling post-RoPE keys destroys phase alignment and cannot reconstruct fine-grained token values once interior KV states are evicted.

### Alternatives considered

Adding a learned de-rotation adapter over pooled keys was considered and rejected as defensive complexity that still fails to recover exact token literals (such as line numbers) needed in debugging tasks.

### Evidence that mattered

- `tang-2024-quest` (Sec. 3.1) and `xiao-2024-infllm` (Sec. 3.2) establish block/page key indexing (`direct`, `strong`).
- `red-team` RoPE phase-interference analysis on post-rotation key averaging.

### Reconsideration trigger

Revisit only if the target task requires coarse topic routing without recovering exact span tokens, and keys are pooled prior to RoPE rotation.

---

## d-02-pursue-anchor-rematerialization: Pursue dual-anchor token rematerialization

- Date: `2026-11-04`
- Project: `multi-turn-kv-eviction`
- Decision: `pursue`
- Affected artifacts: `research/overview.md`, `research/directions/anchor-rematerialization/proposal.md`, `research/directions/anchor-rematerialization/related-work.md`
- Supersedes: `none`

### Decision and rationale

Pursue `anchor-rematerialization` (`H-02`) after revising the trigger from a mean-pooled landmark to two unpooled in-cache anchor tokens ($a_{\text{head}}, a_{\text{med}}$) and capping rematerialization at $K=2$ spans ($M_{\max}=256$ tokens/turn).

### Alternatives considered

1. Full-KV CPU offloading (`xiao-2024-infllm`): rejected for the target single-GPU no-offload setting due to host memory footprint and PCIe transfer latency.
2. Irreversible observation-window eviction (`li-2024-snapkv`): fails when an earlier span is unused in Turn 2 but queried in Turn 3.

### Evidence that mattered

- `li-2024-snapkv` (Sec. 3.1) scores importance solely from the current prompt's observation window (`direct`, `strong`).
- Host plaintext token IDs require $\sim 10^3\times$ less memory than multi-layer FP16 KV tensors.

### Decision-relevant risks

1. Partial re-prefill of an early span without intermediate evicted KV states may degrade deeper-layer representations.
2. Paraphrased Turn 3 queries may miss the single medoid anchor $a_{\text{med}}$.

### Reconsideration trigger

Revise or stop if an oracle span-selection re-prefill fails to recover at least 85% of full-cache accuracy on multi-turn debugging traces, or if anchor recall falls below 70% at $K=2$.
```

---

## 6. Follow-on stages: `decisive-test-design` and `belief-update`

When the researcher decides to validate `anchor-rematerialization`, two follow-on skills handle experiment design and evidence integration.

### Stage 6A: Designing the smallest informative test (`decisive-test-design`)

Rather than proposing a week-long benchmark sweep, `decisive-test-design` creates `research/directions/anchor-rematerialization/evaluation-plan.md` to separate the two main failure risks in a single 2-GPU-hour run:

1. **Representation risk:** Does selective re-prefill of `Span 1` (without evicted intermediate spans) actually restore generation accuracy when the right span is chosen?
2. **Retrieval risk:** Do the two retained anchor tokens ($a_{\text{head}}, a_{\text{med}}$) actually fire when Turn 3 references `Span 1`?

#### Excerpt from `research/directions/anchor-rematerialization/evaluation-plan.md`

```markdown
# Evaluation Plan: Anchor-Triggered Span Rematerialization

- Direction / Hypothesis ID: `anchor-rematerialization` (`H-02`)
- Status: `completed`

## Decision question and expected outcome

Does selective re-prefill of at most $K=2$ spans (256 tokens) from host token IDs recover cross-turn debugging accuracy lost by observation-window eviction under a matched 1,024-token GPU KV budget, and is any residual gap caused by **re-prefill representation drift** or **anchor recall misses**?

## Minimal test setup

- **Dataset / setting:** 120 3-turn debugging traces (Turn 1: 256-token traceback + 256-token code snippet; Turn 2: 768-token unrelated config inspection; Turn 3: patch request targeting Turn 1's traceback). Half of Turn 3 prompts repeat the exact identifier from Turn 1 (`lexical-match`); half refer to it indirectly (`paraphrased`).
- **Model:** Llama-3.1-8B-Instruct, FP16, single 24 GB GPU.
- **Configurations compared at matched active KV budget $B = 1{,}024$:**
  1. `Full-Cache` (unconstrained 1,536-token cache; reference upper bound).
  2. `SnapKV-1024` (irreversible observation-window eviction at the end of Turn 2).
  3. `Anchor-Remat-K2` (proposed: dual anchors per evicted 128-token span, re-prefill top $K=2$ spans / max 256 tokens at layer $\ell^* = 16$).
  4. `Oracle-Remat-K2` (diagnostic control: identical selective re-prefill mechanism as `Anchor-Remat-K2`, but selects the ground-truth Turn 1 traceback spans).

## Controls and interpretability

All bounded methods (`SnapKV-1024`, `Anchor-Remat-K2`, `Oracle-Remat-K2`) enforce the same peak GPU KV cache size ($1{,}024$ tokens). Comparing `Oracle-Remat-K2` against `Full-Cache` isolates representation degradation from missing intermediate KV states; comparing `Anchor-Remat-K2` against `Oracle-Remat-K2` isolates anchor trigger recall.

## Measurements and decision rules

Primary metrics: Turn 3 exact line-and-exception patch accuracy (%), Span-1 recall@2 (%), and Turn 3 prefill latency (ms).

| Observed outcome | Interpretation | Next decision |
|---|---|---|
| `Oracle-Remat-K2` recovers $\ge 85\%$ of `Full-Cache` gap over `SnapKV-1024`, AND `Anchor-Remat-K2` recall@2 $\ge 80\%$ on both splits | Both selective re-prefill and dual-anchor retrieval work as designed. | `continue` to broader multi-turn agent benchmarks. |
| `Oracle-Remat-K2` recovers $\ge 85\%$ of gap, BUT `Anchor-Remat-K2` recall@2 drops below $70\%$ on `paraphrased` split | Selective re-prefill works without intermediate KV, but dual anchors miss non-lexical references. | `revise` anchor selection rule (`H-02`); do not change re-prefill mechanism. |
| `Oracle-Remat-K2` recovers $< 50\%$ of `Full-Cache` gap over `SnapKV-1024` | Re-prefilling spans without preceding evicted KV context breaks deeper-layer representations. | `stop` / `reject` isolated span re-prefill. |
```

### Stage 6B: Updating beliefs when mixed results arrive (`belief-update`)

Suppose the execution agent runs `evaluation-plan.md` and returns the results:
- `Full-Cache`: **88.3%** patch accuracy
- `SnapKV-1024`: **31.7%** patch accuracy (evicts Turn 1 traceback during Turn 2)
- `Oracle-Remat-K2`: **84.2%** patch accuracy (+18 ms prefill overhead)
- `Anchor-Remat-K2`: **81.7%** on `lexical-match` (recall@2 = **93%**), but **51.7%** on `paraphrased` (recall@2 = **58%**)

When `belief-update` processes this evidence:
1. It does **not** discard the direction or hide the failure on the `paraphrased` split.
2. It maps the result against the prediction matrix: `Oracle-Remat-K2` (84.2% vs. 88.3%) confirms that **selective re-prefill at original RoPE indices works without retaining intermediate KV states** (resolving the `red-team` causal-gap objection), while the drop on `paraphrased` traces pinpoints the exact failure in `Anchor-Remat-K2`: a single cumulative-attention medoid token $a_{\text{med}}$ is often a punctuation or formatting token rather than a semantic anchor when Turn 3 uses indirect phrasing.
3. It updates `proposal.md` in place (`Status: revised`) and appends `d-03` to `research/decisions.md`, linking back to `d-02`.

#### Appended entry in `research/decisions.md`

```markdown
## d-03-revise-anchor-selection-for-paraphrase: Revise anchor selection after diagnostic test

- Date: `2026-11-05`
- Project: `multi-turn-kv-eviction`
- Decision: `revise`
- Affected artifacts: `research/directions/anchor-rematerialization/proposal.md`, `research/directions/anchor-rematerialization/evaluation-plan.md`
- Supersedes: `#d-02-pursue-anchor-rematerialization`

### Decision and rationale

Keep the selective token-ID re-prefill mechanism (supported by `Oracle-Remat-K2` reaching 84.2% vs. 88.3% `Full-Cache` and 31.7% `SnapKV-1024`), but revise `H-02`'s anchor selection rule. On indirect/paraphrased Turn 3 queries, cumulative-attention medoids $a_{\text{med}}$ selected punctuation/delimiter tokens in 41% of spans, dropping recall@2 to 58%. Replace cumulative-attention medoid selection with **sink-excluded key-norm + delimiter-boundary anchors** (retaining the span's structural header token plus two non-punctuation tokens with the highest L2 key norm at layer $\ell^*$).

### Evidence that mattered

- `evaluation-plan.md` diagnostic run (`run-20261105-01`, 120 traces, Llama-3.1-8B-Instruct):
  - `Oracle-Remat-K2` accuracy 84.2% vs. `SnapKV-1024` 31.7% (`supports` selective re-prefill feasibility; `direct`, `strong`).
  - `Anchor-Remat-K2` recall@2 = 93.3% on `lexical-match` vs. 58.3% on `paraphrased` (`qualifies` dual-anchor trigger claim; `direct`, `strong`).

### Reconsideration trigger

If excluding attention-sink/punctuation tokens and retaining 3 anchors per span fails to raise `paraphrased` recall@2 above 80% at the same 1,024-token budget, stop pure in-cache token anchoring and evaluate lightweight pre-RoPE span-key indexing.
```
