# Unit 2 — Frameworks as quality practice

**Budget: ~5 hrs 15 min.** Five tasks, two artifacts. Take whatever calendar it takes.

**Theme:** NIST's AI Risk Management Framework is the common vocabulary of this field, and about 70% of it is a management system you have already run. This unit is about finding the other 30% — the parts where AI genuinely breaks quality practice rather than extending it. Then three concepts that have no QMS equivalent at all.

**Order matters.** Read the framework, then the concepts, then the system card — the card is where you see the concepts in production. Write the artifacts last.

---

## Task 1 — NIST AI RMF 1.0, read as a delta (90 min)

Free PDF, NIST AI 100-1. Read it once end to end, not slowly.

The four functions and their obvious counterparts:

| RMF function | What it covers | Your existing name for it |
|---|---|---|
| **GOVERN** | policies, accountability, risk tolerance, culture — cross-cutting | ISO 9001 clause 5 leadership, quality policy, the quality manual |
| **MAP** | context, system categorisation, risk identification | clause 4 context, design inputs, FMEA scoping |
| **MEASURE** | analyse, assess, benchmark, monitor | test and inspection, measurement system analysis, metrics |
| **MANAGE** | prioritise, respond, recover, communicate | CAPA, risk treatment, nonconformance handling |

Do not stop at that table — it is the easy half. **As you read, keep a running list of every point where the analogy fails.** That list is the unit's real output. Five places to look especially hard:

1. **The object is stochastic.** In a QMS you measure conformance to a specification. Here there is often no specification, only a distribution of outputs. What does "defect" mean when the same input legitimately produces different outputs?
2. **The harmed party is not your customer.** Quality management measures conformance to requirements set by whoever is buying. The AI RMF centres harm to people who never bought anything, cannot raise a complaint with you, and may not know the system exists. Your candidates are exactly this.
3. **Risk is socio-technical, not a property of the artifact.** The RMF is explicit that the same system carries different risk in different contexts of use. A QMS mostly treats the product as the unit of assessment.
4. **The trustworthiness characteristics.** Valid and reliable · safe · secure and resilient · accountable and transparent · explainable and interpretable · privacy-enhanced · fair with harmful bias managed. Map each to QMS practice and notice which two or three have no counterpart whatsoever.
5. **There is no certificate.** The RMF is voluntary, has no conformity assessment and no auditor. Coming from an ISO world, sit with what that changes about how it gets adopted — and why ISO 42001 exists alongside it.

---

## Task 2 — NIST AI 600-1, Generative AI Profile (45 min)

Free. This is the one that maps onto LLM applications specifically, and it is short.

Twelve risk categories. The ones that land on your screening tool: **confabulation** (a plausible, fluent, wrong rationale for a score), **harmful bias and homogenisation**, **data privacy**, **information integrity**, and **value chain and component integration** — which is the formal name for the risk you already identified when you noticed the model provider's deletion commitment is unenforceable from your side.

As you read, note which of the twelve your unit 1 known gaps already cover. You will find you reached several without the framework.

---

## Task 3 — Three concepts with no QMS equivalent (75 min)

These are the genuinely new ideas in this phase. Budget the time properly; they are not reading, they are thinking.

### 3a. Fairness metrics are mathematically incompatible (~35 min)

The result (Kleinberg et al., Chouldechova, around 2016–17): you cannot simultaneously have **calibration within groups**, **equal false positive rates**, and **equal false negative rates** — unless base rates are identical across groups, or your predictor is perfect. Neither will ever be true.

Work it through on your own screening tool. Suppose two groups of candidates with different base rates of succeeding in the role:

- If your scorer is **calibrated** — a score of 0.8 means roughly an 80% success probability for everyone — then false negative rates *will* differ between groups. Some group gets more qualified people wrongly rejected.
- If you **equalise false negative rates** so no group is disproportionately wrongly rejected, you break calibration. The same score now means different things for different people.

You must choose. There is no configuration that satisfies both.

**Why this is the most important idea in the unit:** the choice is a value judgment, not a technical one. No amount of engineering resolves it. Which means it cannot be made by a data scientist tuning a threshold — it has to be made deliberately, by a named accountable role, and written down with reasons.

That is precisely the Head of Talent Acquisition you named in unit 1. The impossibility result is *why* fairness needs an accountable owner.

### 3b. Disparate treatment vs disparate impact (~20 min)

- **Treatment** — using the protected characteristic itself. Direct, intentional, and the easy one to avoid.
- **Impact** — a facially neutral process producing disproportionate adverse outcomes for a protected group. No intent required.

Your scrubbing of name, age, ethnicity and region addresses **treatment**. It does nothing about **impact**, and impact is where the legal exposure actually sits.

This is the correction to unit 1's gap 3, properly nailed. Re-identification and proxy discrimination are different problems: one is about knowing *who* someone is, the other about inferring *what group* they belong to. Graduation year does not identify you. It estimates your age. The model never needs your identity to disadvantage you.

Different harm, different regime, different control. Minimisation fixes the first. Only outcome testing fixes the second.

### 3c. Automation bias (~20 min)

The tendency to over-rely on automated output and under-weight contradictory evidence, including your own direct observation. Related failure modes: automation complacency (reduced monitoring over time) and confirmation bias on the automated result.

You found this empirically in unit 1 without the vocabulary: the delivery driver who followed routing onto a tidal causeway against visible physical reality, and the officers who deferred to a risk score that said low when the situation said otherwise.

Now put it on your own system. A recruiter opening a ranked list has already been told what to think before reading a single CV. Ask the uncomfortable question: what would have to be true for that recruiter to move candidate 40 into the shortlist? If the answer is "nothing realistic", the oversight step is decorative — and that is unit 1's known gap 2, now with a name.

---

## Task 4 — One system card, read properly (45 min)

Pick a recent frontier-model system card (Anthropic, OpenAI and Google DeepMind all publish them). One, read properly — not three skimmed.

You are not reading it for the model. You are reading it as **an assurance document** written by people with resources, to see what a serious safety argument looks like on paper. Extract five things:

1. What did they actually test, and how do they describe coverage?
2. Where do they state a **limitation** rather than a result? How is it worded?
3. How is red-teaming reported — who did it, what access, what scope?
4. What is claimed as **residual risk**, and what is the argument for accepting it?
5. What is conspicuously absent?

That last one is the valuable question and the one your background equips you to ask. You have read vendor test reports for eighteen years.

---

## Artifacts

### 1. RMF → QMS delta table
Three columns: **familiar** (same practice, new noun) · **modified** (recognisable but changed, and how) · **new** (no counterpart in quality practice). Cover the four functions and the seven trustworthiness characteristics. One page.

This is the single most useful page you will write in Phase 2, for two reasons: it tells you where to spend your remaining study time, and it is the basis of the interview answer only you can give — "here is what AI governance borrows from quality management, and here is precisely where the analogy breaks."

### 2. Concept glossary
Six terms maximum, in your own words, each with a one-line note on how it applies to the screening tool. Candidates: calibration · disparate impact · automation bias · confabulation · distribution shift · residual risk.

**In your own words matters.** Unit 1's known gap 1 was close to a transcription of my sentence; gaps 2 and 4 were yours and were better. The glossary is only worth writing if it is yours.

---

## Not in this unit

Do not start the EU AI Act. That is unit 5, and you have a head start there from the training you delivered — no need to spend it early.

**Optional, if you want the monthly post out of the way:** unit 1's closeout contains two publishable pieces. The stronger one is the affected-persons argument — institutions have reputations, people have lives, and a log that records "trust was lost" has lost the person. Roughly 600 words, and almost nobody in this field writes about it.
