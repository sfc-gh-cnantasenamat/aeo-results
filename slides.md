---
# AEO Benchmark: Results

## V4 — 9 models, 840 questions, 4 deployment configurations

---
# The Punchline

We tested **8 frontier models** (plus GLM 5.2) on **840 Snowflake developer questions**, scored by a panel of **5 LLM judges**, under 4 deployment configurations: **Baseline**, **Citation** (C), **Agentic** (A), and **Citation + Agentic** (C+A).

**The result is the same for every single model:** the **C+A** configuration wins.

**Best baseline (bare model):** as low as 41.8% on answer quality.

**Best configuration (`gpt-5.5` with Citation + Agentic):** **84.1%** answer quality, 79.9% must-have fact pass rate.

Averaged across all 8 models, moving from Baseline to C+A lifted answer quality **+26.5 points** and must-have fact pass rate **+22.6 points** — with no change to model weights or training. The only difference was how each model was deployed.

```
  Answer Quality (8-model average)
  Baseline (bare)   49.5% ███████████████████████░░░░░░░░░░░░░░░░
  Citation + Agentic 76.0% ████████████████████████████████████░░░
```

What deployment changes made this happen? Keep reading.

---
# The Benchmark at a Glance

```
  840 questions   32 Snowflake product categories × 4 question types
  9 models        opus 4.6/4.7/4.8 · sonnet 4.5/4.6/5 · gpt 5.4/5.5 · glm 5.2
  4 configs       Baseline · Citation (C) · Agentic (A) · Citation+Agentic (C+A)
  5 judges        per response, scored independently, averaged
  6 scores        Correctness, Completeness, Recency, Citation, Recommendation
                  (1-10 each) + Must-Have fact pass rate (5 facts per question)
  composite       (avg total + must-have×10) / 60 × 100
```

**Agentic (A)** = the model answers through Cortex Code, with tools (doc search, SQL, web) instead of a single direct completion call. **Citation (C)** = the question is appended with an instruction to cite official `docs.snowflake.com`. **C+A** applies both.

Every one of the 33 runs is soundness-verified: 840/840 responses contain a real answer body (no truncated planning stubs).

---
# Full Leaderboard (33 runs)

```
+----+-----------------------+--------+---------+-------+
| #  | Model                 | Config | Score % | MH %  |
+----+-----------------------+--------+---------+-------+
|  1 | openai-gpt-5.5        |  C+A   |  84.1%  | 79.9% |
|  2 | claude-opus-4-8       |  C+A   |  82.1%  | 79.0% |
|  3 | claude-sonnet-5       |  C+A   |  81.5%  | 76.9% |
|  4 | claude-sonnet-4-6     |  C+A   |  79.5%  | 74.9% |
|  5 | claude-opus-4-7       |  C+A   |  75.2%  | 69.9% |
|  6 | claude-opus-4-8       |   A    |  73.5%  | 78.2% |
|  7 | claude-opus-4-6       |  C+A   |  72.3%  | 68.2% |
|  8 | claude-sonnet-4-5     |  C+A   |  72.0%  | 67.5% |
|  9 | openai-gpt-5.5        |   A    |  70.2%  | 77.5% |
| 10 | claude-sonnet-5       |   A    |  69.4%  | 73.6% |
| 11 | claude-sonnet-4-6     |   A    |  66.0%  | 69.7% |
| 12 | claude-opus-4-7       |   C    |  65.4%  | 54.8% |
| 13 | glm-5.2               |   A    |  64.4%  | 65.3% |
| 14 | openai-gpt-5.5        |   C    |  63.1%  | 47.1% |
| 15 | claude-sonnet-5       |   C    |  61.3%  | 48.4% |
| 16 | openai-gpt-5.4        |  C+A   |  61.0%  | 50.3% |
| 17 | claude-opus-4-7       |   A    |  60.3%  | 61.7% |
| 18 | openai-gpt-5.4        |   C    |  60.2%  | 44.0% |
| 19 | claude-opus-4-6       |   C    |  59.9%  | 48.7% |
| 20 | claude-sonnet-4-5     |   A    |  59.6%  | 60.6% |
| 21 | claude-opus-4-7       |  base  |  58.9%  | 60.9% |
| 22 | claude-opus-4-6       |   A    |  55.0%  | 56.6% |
| 23 | claude-opus-4-8       |   C    |  53.3%  | 43.9% |
| 24 | claude-sonnet-4-5     |   C    |  53.2%  | 42.1% |
| 25 | claude-sonnet-4-6     |   C    |  53.1%  | 42.0% |
| 26 | claude-opus-4-8       |  base  |  51.9%  | 50.3% |
| 27 | claude-opus-4-6       |  base  |  51.3%  | 51.4% |
| 28 | openai-gpt-5.4        |   A    |  51.3%  | 47.8% |
| 29 | claude-sonnet-5       |  base  |  50.8%  | 50.3% |
| 30 | openai-gpt-5.5        |  base  |  49.1%  | 45.7% |
| 31 | openai-gpt-5.4        |  base  |  47.0%  | 43.4% |
| 32 | claude-sonnet-4-6     |  base  |  45.1%  | 43.4% |
| 33 | claude-sonnet-4-5     |  base  |  41.8%  | 40.4% |
+----+-----------------------+--------+---------+-------+
```

The top 5 slots are all **C+A**. The bottom of the board is all **Baseline**. Configuration, not model choice, sorts this leaderboard.

---
# The Configuration Progression

## Averaged across all 8 full-factorial models

```
+----------+---------+-------+
| Config   | Score % | MH %  |
+----------+---------+-------+
| Baseline |  49.5%  | 48.2% |
| Citation |  58.7%  | 46.4% |
| Agentic  |  63.2%  | 65.7% |
| C + A    |  76.0%  | 70.8% |
+----------+---------+-------+
```

```
  Answer Quality Score
  Baseline  49.5% ███████████████████████░░░░░░░░░░░░░░░░
  Citation  58.7% ████████████████████████████░░░░░░░░░░░
  Agentic   63.2% ██████████████████████████████░░░░░░░░░
  C + A     76.0% ████████████████████████████████████░░░

  Must-Have Fact Pass Rate
  Baseline  48.2% ███████████████████████░░░░░░░░░░░░░░░░
  Citation  46.4% ██████████████████████░░░░░░░░░░░░░░░░░
  Agentic   65.7% ███████████████████████████████░░░░░░░░
  C + A     70.8% ██████████████████████████████████░░░░░
```

Note that **Citation alone lowers the must-have pass rate** (48.2% → 46.4%). Agentic is what moves facts.

---
# Main Effects

## Averaged across every paired comparison in the design

- **Agentic Tools (Cortex Code: doc search, SQL, web):** improved answer quality **+15.5 points** and must-have fact pass rate **+21.0 points**. It is the single most impactful lever, and the only one that materially improves *both* metrics.

- **Citation Instruction ("cite official Snowflake docs"):** improved answer quality **+11.0 points**, but moved must-have pass rate only **+1.6 points** — because without tools the model cites documentation it never actually read.

```
  Average Main Effect on Score (pp)
  Agentic   +15.5 ▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓
  Citation  +11.0 ▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓

  Average Main Effect on Must-Have (pp)
  Agentic   +21.0 ▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓
  Citation   +1.6 ▓▓▓
```

Citation tells the model *what to look for*. Agentic tools let it actually *find and verify* the answer. Together they compound.

---
# C + A Wins for Every Model

## The best configuration is identical across the board

```
+-----------------------+-------------+---------+
| Model                 | Best config | Score % |
+-----------------------+-------------+---------+
| openai-gpt-5.5        |    C + A    |  84.1%  |
| claude-opus-4-8       |    C + A    |  82.1%  |
| claude-sonnet-5       |    C + A    |  81.5%  |
| claude-sonnet-4-6     |    C + A    |  79.5%  |
| claude-opus-4-7       |    C + A    |  75.2%  |
| claude-opus-4-6       |    C + A    |  72.3%  |
| claude-sonnet-4-5     |    C + A    |  72.0%  |
| openai-gpt-5.4        |    C + A    |  61.0%  |
+-----------------------+-------------+---------+
```

8 models, 8 winners, one configuration. The deployment recipe generalizes — it is not a quirk of any single model.

---
# The Citation Dimension Tells the Story

## Per-dimension judge scores (1-10), Baseline vs C+A

```
+-----------------+----------+--------+--------+
| Dimension       | Baseline |  C+A   | Delta  |
+-----------------+----------+--------+--------+
| Correctness     |   6.1    |  7.7   | +1.6   |
| Completeness    |   5.3    |  7.2   | +1.9   |
| Recency         |   6.4    |  8.2   | +1.8   |
| Citation        |   1.5    |  7.9   | +6.4   |
| Recommendation  |   5.6    |  7.4   | +1.8   |
+-----------------+----------+--------+--------+
```

```
  Citation dimension (1-10)
  Baseline  1.5 ██████░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░
  C + A     7.9 ███████████████████████████████░░░░░░░░░
```

Bare models essentially **do not cite** (1.5/10). Add Citation + Agentic and citation quality jumps to 7.9/10 — the model now points to documentation it actually retrieved. Every other dimension improves too, but citation is the transformation.

---
# GLM 5.2: Agentic-Only

GLM 5.2 is not available through Snowflake's `CORTEX.COMPLETE` SQL function — it can only be reached through the agentic Cortex Code path. So GLM 5.2 has an **Agentic (A)** entry only; its Baseline / Citation / C+A configs cannot be produced without self-hosting a ~753B-parameter model.

- **`glm-5.2` (Agentic):** 64.4% score, 65.3% must-have — mid-pack among the agentic runs, ahead of several models' A configs.

It is included as an agentic-only reference point rather than a full factorial entry.

---
# Difficulty by Question Type

## Composite score averaged across all runs

```
+------------+---------+
| Type       | Score % |
+------------+---------+
| Explain    |  63.1%  |
| Debug      |  62.8%  |
| Compare    |  61.1%  |
| Implement  |  60.3%  |
+------------+---------+
```

The spread is narrow (~3 points). Conceptual **Explain** questions are easiest; **Implement** (write the code/SQL) is hardest — models are stronger at describing Snowflake than at producing exactly-correct syntax. The C+A lift applies across all four types.

---
# Key Takeaways

**1. Agentic tools are the single most impactful lever.** Across every model, giving the model Cortex Code (doc search, SQL, web) improved answer quality +15.5 points and must-have fact pass rate +21.0 points on average — the only lever that improves both.

**2. Citation + Agentic is the universal winner.** C+A was the top configuration for all 8 full-factorial models, peaking at 84.1% (`gpt-5.5`). The recipe generalizes across model families and sizes.

**3. Citation without tools is hollow.** The citation instruction lifted quality scores but barely moved the must-have fact rate (+1.6pp), because a bare model cites documentation it never read (citation dimension: 1.5/10 at baseline).

**4. Deployment beats model choice.** The gap between the worst and best configuration of a *single* model (often 25-35 points) dwarfs the gap between models at a *fixed* configuration. How you deploy a model matters more than which model you pick.

---
# Thank You

## AEO Benchmark — V4

- **840 Snowflake developer questions** across 32 product categories and 4 question types, each scored on 5 dimensions plus 5 required must-have facts
- **9 models × 4 deployment configurations** (Baseline, Citation, Agentic, Citation+Agentic) — 33 runs, all soundness-verified
- **5-model judge panel** scoring every response independently, averaged for robustness
- **Key result:** the Citation + Agentic configuration won for every model, topping out at 84.1% (`gpt-5.5`); agentic tool access was the biggest single lever (+15.5 score / +21.0 must-have)

*Open the methodology deck for the full experimental design.*
