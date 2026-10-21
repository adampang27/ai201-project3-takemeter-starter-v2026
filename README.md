# TakeMeter

> ### 👋 Start here
>
> **New to this repo? Read [RUNNING.md](RUNNING.md) first** — setup, the
> notebook, the baseline, and what to do when something breaks.
>
> Once `python test.py` passes:
>
> ```bash
> head -5 data/practice_labels.csv     # the shape your labels.csv needs
> ```
>
> Then open `takemeter.ipynb` **in this folder** — in VS Code, or with
> `jupyter notebook` if you prefer. Pick the kernel: the `.venv` inside this
> project. Run section 1, which reports the hardware you'll be training on.
> Everything else waits until you have data.
>
> Nothing to upload, nothing to connect, no accounts and no keys. The notebook
> runs on your machine and writes next to your code.
>
> **The rest of this file is your submission.** Fill it in as you go.

---

<!-- ─────────────────────────────────────────────────────────────────────────
     HOW TO USE THIS FILE

     Unit 5 asks for the first five sections. Unit 6 adds the five below them.

     Everything is pasted as TEXT. No screenshots, no images.

     ⚠️ The confusion matrix especially. The notebook prints one as a markdown
     table, ready to copy. A screenshot of a matrix earns nothing. Paste the
     table.
     ───────────────────────────────────────────────────────────────────────── -->

<!-- ═══════════════════════ UNIT 5 — THE BUILD ═══════════════════════ -->

## What This Does

This classifies public posts from [r/DeepThoughts](https://www.reddit.com/r/DeepThoughts/) as `reasoned` or `no_reasoning`. I chose this community because the posts include everyday casual opinions and broader philosophical discussions..

Three differences stood out in the posts:

- Some posts have a claim and give reasoning behind it, others just state a thought.
- Some posts use personal experiences, others use hypothetical situations.
- Some posts refer to famous philosophers or theories, others use everyday examples from their observations.

---

## Label Taxonomy

I chose this split because I can point to the part of a post that gives a reason. The examples below are from the linked posts.

### `reasoned`

**Definition:** A post that connects a claim to a reason, even if the reasoning is weak or incorrect.

**Example 1:** [A perfect system will stagnate, unless it's disrupted frequently.](https://www.reddit.com/r/DeepThoughts/comments/1x1wf6k/a_perfect_system_will_stagnate_unless_its/)

> To get a perfect system to generate growth, you must disrupt the system, and force it to adapt.
>
> Then, you get progression.

The post links disruption to adaptation and growth, so it gets `reasoned`.

**Example 2:** [I know what being deceased feels like, and as do you.](https://www.reddit.com/r/DeepThoughts/comments/1x2mcu1/i_know_what_being_deceased_feels_like_and_as_do/)

> You are your consciousness and therefore being nothing implies being unconscious. A dead person is not conscious.

The author uses a claim about consciousness to support a claim about death. That counts as reasoning even if the argument is wrong.

### `no_reasoning`

**Definition:** A post that states a claim or asks a question without giving a reason for a conclusion.

**Example 1:** [Between thinking and knowing, thinking is more important](https://www.reddit.com/r/DeepThoughts/comments/1x295et/between_thinking_and_knowing_thinking_is_more/)

> Between thinking and knowing, thinking is more important

This states which matters more without saying why, so it gets `no_reasoning`.

**Example 2:** [Our modern concept of "being in a rush" is entirely manufactured by technology rather than a natural human instinct.](https://www.reddit.com/r/DeepThoughts/comments/1x0tjdu/our_modern_concept_of_being_in_a_rush_is_entirely/)

> If our digital infrastructure, atomic clocks, and instant messaging suddenly vanished, how long would it take for society to unlearn the psychological anxiety of urgency? Would we naturally revert to a slower, cyclical rhythm dictated by nature, or has the artificial pressure of time been permanently hardwired into our collective psychology?

### The hardest boundary

**Which two labels:** `reasoned` and `no_reasoning`.

The post about being in a rush is the closest case. Its title says technology creates urgency, but the body only asks what would happen without it. I put it in `no_reasoning` because it doesn't give a reason for that claim.

**The decision rule:** If a post gives a reason for its claim, I use `reasoned`, even if the reasoning is weak or wrong. Otherwise, I use `no_reasoning`.

The eight test posts included circular arguments, claims backed only by authority, and hypothetical questions.

---

## The Dataset

The posts come from public [r/DeepThoughts](https://www.reddit.com/r/DeepThoughts/) feeds and linked threads. Each row keeps the title and full body.

Each post was labeled using the definitions above, then checked again. More unsupported claims and questions were collected to stay within the 70% limit. The source links and hard-case notes are in `note`.

The 20 independent cold labels are still pending.

| Label | Count | Share |
|---|---|---|
| `reasoned` | 140 | 70% |
| `no_reasoning` | 60 | 30% |
| Total | 200 | 100% |

Three cases were hard to place between `reasoned` and `no_reasoning`:

1. The [post about being in a rush](https://www.reddit.com/r/DeepThoughts/comments/1x0tjdu/our_modern_concept_of_being_in_a_rush_is_entirely/) blames technology in its title, but the body only asks questions. It gets `no_reasoning` because it never says why technology causes that feeling.

2. The [free-will post](https://www.reddit.com/r/DeepThoughts/comments/1x1e6rd/free_will_may_be_an_illusion_created_by_the/) is mostly questions, but connects decisions to genes, past experiences, and the environment. It gets `reasoned` because it uses that connection to question whether choices are free.

3. The [post blaming 90% of humanity's problems on self-interest](https://www.reddit.com/r/DeepThoughts/comments/1tiu39e/90_of_humanity_problems_is_caused_by_shortterm/) lists problems without explaining the connection. It gets `no_reasoning` because repeating the cause does not give a reason to believe it.

---

## The Training Run

<!-- Your starting model, your settings, and anything you changed and why. -->

**Base model:**

**Settings:** <!-- epochs, learning rate, batch size, seed -->

**Anything I changed from the defaults, and why:**

**Split sizes:** <!-- train / val / test, and per-label counts in the test
split. If a label had fewer than about 8 in test, say so — it explains a lot
of next unit's variance. -->



---

## How I Used AI

<!-- Two specific moments — what you asked, what came back, what you changed.

     ⚠️ Plus disclosure of any pre-labelling. If you had a model pre-label a
     batch and then read and corrected every one, say that. It's an allowed
     workflow and disclosing it costs you nothing. Not disclosing it is the
     problem. -->

**Moment 1**

- *What I asked for:*
- *What came back:*
- *What I changed:*

**Moment 2**

- *What I asked for:*
- *What came back:*
- *What I changed:*

**Pre-labelling disclosure:**

<!-- ═══════════════════════ UNIT 6 — THE TEST ═══════════════════════

     Don't fill these in during unit 5.
     ═══════════════════════════════════════════════════════════════════ -->

---

## Baseline vs. Trained

<!-- Both models on the same posts. `python baseline.py --trained results.json`
     prints this table for you. -->

| Measure | Baseline | Trained | Difference |
|---|---|---|---|
| Overall accuracy |  |  |  |
| Macro F1 |  |  |  |
| F1 — `label_one` |  |  |  |
| F1 — `label_two` |  |  |  |

**What I predicted before I looked:**
<!-- Milestone 1 asks you to write this BEFORE seeing the trained numbers. A
     prediction made afterwards isn't one. -->

**What the gap actually means:**
<!-- If the baseline matched your trained model, your fine-tuning added
     nothing — and that is a real finding, not a failure. Say it plainly. -->



---

## Run Log — Before

<!-- Five criteria across three seeds. The notebook's section 6 prints the
     spread table; the Target and Verdict columns are yours. -->

| Criterion | Target | Seed 42 | Seed 7 | Seed 2024 | Verdict |
|---|---|---|---|---|---|
| 1.  |  |  |  |  |  |
| 2.  |  |  |  |  |  |
| 3.  |  |  |  |  |  |
| 4.  |  |  |  |  |  |
| 5.  |  |  |  |  |  |

### Confusion matrix

<!-- ⚠️ TYPED AS A MARKDOWN TABLE. The notebook prints one ready to paste.
     An image of a matrix earns nothing. -->

| true \ predicted |  |  |  |
|---|---|---|---|
| **** |  |  |  |
| **** |  |  |  |
| **** |  |  |  |

**My biggest off-diagonal number, and what it means:**
<!-- Not "the model made mistakes" — WHICH boundary it didn't learn, and which
     direction. "7 real analysis posts were called hot_take and only 3 went the
     other way" is a direction, not just an error rate. -->



---

## Verdicts and Diagnoses

<!-- MET or MISSED against LAST UNIT's target. The target has to hold across
     all three seeds, not turn up sometimes. -->

| # | Criterion | Target | Verdict | How I decided |
|---|---|---|---|---|
| 1 |  |  |  |  |
| 2 |  |  |  |  |
| 3 |  |  |  |  |
| 4 |  |  |  |  |
| 5 |  |  |  |  |

**Diagnoses**

<!-- For each miss: the cause, and how you know. The four common causes are:
     too few examples for a label, a boundary you applied inconsistently, a
     genuinely hard label pair, and a task the model can't reach from this
     much data.

     ⚠️ Use your agreement report as evidence. It is the only instrument you
     have that can tell a LABELLING problem from a MODEL problem, and this
     section is graded on whether you used it that way. -->



---

## Agreement Report

<!-- Your rate against the staff set, and every disagreement adjudicated.

     Remember you labelled these 30 under the STAFF taxonomy in
     data/staff_taxonomy.md, not your own — so every argument below is made
     from those definitions and those decision rules. -->

**Agreement rate:** ___ / 30 = ___%

<!-- Nobody grades this number. A 60% who argues every disagreement from the
     stated rules beats a 95% who wrote "staff was right" nine times. Several
     of the 30 were chosen because they're genuinely ambiguous — you should be
     winning some of these. -->

**Disagreements**

<!-- Three lines each: the post, both labels, and who you think is right and
     why — grounded in the staff definitions you were both applying.

     Then sort each into one of three piles:
       (a) the rule covered it and I applied it loosely → a consistency problem
       (b) the rule genuinely doesn't say               → a gap in the definitions
       (c) the rule is ambiguous here and my reading is defensible → argue it.
           This is a legitimate win.

     Pile (a) is the one that matters most for your diagnosis: if you applied a
     written rule two different ways on 30 posts, that is direct evidence about
     what you did across your own 200. -->

**1.**
> *The post:*
>
> *Staff said / I said:*
>
> *My call, and why:*
>
> *Which pile:*

**2.**
> *The post:*
>
> *Staff said / I said:*
>
> *My call, and why:*
>
> *Which pile:*

**What the pattern in my disagreements tells me:**



---

## The Improvement

**What I changed:**

**Which diagnosis pointed at it:**

### Run Log — After

| Criterion | Target | Seed 42 | Seed 7 | Seed 2024 | Verdict |
|---|---|---|---|---|---|
| 1.  |  |  |  |  |  |
| 2.  |  |  |  |  |  |
| 3.  |  |  |  |  |  |
| 4.  |  |  |  |  |  |
| 5.  |  |  |  |  |  |

**Did it help, and how do I know:**

<!-- If it didn't, say so. Relabelling that didn't help is a genuinely
     interesting result and earns full credit. -->



---

## What's Still Broken

<!-- For each criterion still missed: what you'd do, and why you stopped. -->



**The gap between what I meant my labels to capture and what the model
learned:**
<!-- Two sentences. Your confusion matrix is the evidence. -->



<!-- ═════════════════════════════════════════════════════════════════════

     SUBMISSION CHECKLIST — unit 5

       [ ] criteria.md has five numbered criteria, each naming a NUMBER
       [ ] Each has a reason underneath tied to your data or taxonomy
       [ ] labels.csv: at least 150 rows, text/label/note, ONE file not split
       [ ] No label above 70%
       [ ] All five unit 5 sections have real content
       [ ] Label Taxonomy includes the decision rule for your hardest boundary
       [ ] The Dataset includes three hard cases
       [ ] results.json and test_split.csv committed (the notebook does this)
       [ ] At least four new commits
       [ ] Repository URL submitted — WRITE IT DOWN

     SUBMISSION CHECKLIST — unit 6

       [ ] Baseline vs. Trained table, with your prediction written beforehand
       [ ] Run Log — Before, five criteria across three seeds
       [ ] Confusion matrix TYPED AS A MARKDOWN TABLE
       [ ] A verdict on every criterion
       [ ] A diagnosis for every miss, using the agreement report as evidence
       [ ] Agreement Report with every disagreement adjudicated
       [ ] One improvement, with Run Log — After
       [ ] What's Still Broken
       [ ] results_three_seeds_before.json, results_three_seeds_after.json,
           baseline_results.json and
           agreement_results.json committed
       [ ] At least four new commits
       [ ] The SAME repository URL as last unit

     Do not delete and recreate this repository.
     ═════════════════════════════════════════════════════════════════════ -->

---

📖 **How to run this project: [RUNNING.md](RUNNING.md)**
