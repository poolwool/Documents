# Unit 2 — The ideas behind AI risk

**Budget: ~5 hrs.** Part A is reading this page. Part B is five numbered things to do. Part C is two files to write.

**How this unit works:** Part A teaches you the ideas in plain language. Part B sends you to the real sources, which will go fast because you will already know what you are looking for. Do Part A first.

---
---

# PART A — The ideas

Read this section once. About 40 minutes. You are not taking notes yet.

---

## A1. What the NIST framework is, and why anyone cares

NIST AI RMF is a free document from the US standards body. It is voluntary. There is no certificate, no auditor, no penalty for ignoring it.

It matters anyway, because it is the shared language. When a customer asks "do you follow a recognised AI risk framework?", NIST is the answer that needs no explanation anywhere in the world. Other things map to it. Job adverts name it.

It has four parts:

| Part | What it means in practice |
|---|---|
| **GOVERN** | Who is in charge, what the rules are, what risk you are willing to accept |
| **MAP** | What is this system, who does it affect, what could go wrong |
| **MEASURE** | Test it. Get numbers. Keep watching after release |
| **MANAGE** | Decide what to fix first, fix it, handle it when something goes wrong |

That is it. Govern, Map, Measure, Manage. If it sounds like running a test programme, that is because it largely is.

**What you already know how to do.** You have spent eighteen years on test strategy, coverage, regression suites, defect triage by severity, root cause analysis and release sign-off. Every one of those has a direct equivalent here:

| Your work | Same thing, new name |
|---|---|
| Test strategy | Evaluation strategy |
| Test coverage — what we tested, what we skipped | Evaluation coverage |
| Regression suite | Re-testing after a model version changes |
| Severity triage on a defect | Severity of a harm |
| Root cause — was it code, config or environment? | Failure layer — data, model, product or deployment |
| Release sign-off | Risk acceptance |

You already did the root-cause one in unit 1. The "failure layer" column was root cause analysis with different words.

**So what is actually new?** Four things. They are the rest of Part A.

---

## A2. New thing 1: there is often no expected result

In testing, you compare what happened against what should have happened. The expected result is the foundation of everything.

With an AI system scoring CVs, there is frequently no single correct answer. What score *should* a particular CV get? Nobody knows. There is no spec to compare against.

Two consequences:

**You cannot write pass/fail for most inputs.** You can only look at patterns across many outputs. Is the average sensible? Do similar CVs get similar scores? Does the ranking match human judgement most of the time?

**Non-determinism is normal, not a bug.** You know this feeling already — a flaky test. Same input, different result, maddening to debug. An LLM is flaky by design. Ask it twice, get two slightly different answers. In testing you hunt flakiness down and kill it. Here you cannot. You have to measure around it: run things many times, look at the spread, decide how much variation is acceptable.

That decision — how much variation is acceptable — is a judgement someone has to make and write down. It is not discoverable by testing.

---

## A3. New thing 2: the person harmed is not your user

A software defect annoys your user. They raise a ticket. You fix it.

Your screening tool's defects land on job candidates. They are not your users. They cannot raise a ticket. They do not know the tool exists. They will never find out why they were rejected.

This is why this field talks constantly about "affected persons" — and why I kept pushing you on that column in unit 1. There is no feedback loop from the people being harmed. If you do not go looking for the harm deliberately, nobody will report it to you.

---

## A4. New thing 3: fairness forces a choice you cannot engineer away

This is the hardest idea in the unit. Take it slowly.

### First, calibration

A score is **calibrated** if it means what it says. If your tool gives 100 candidates a score of 0.8, and roughly 80 of them turn out to be good hires, the score is calibrated. 0.8 means 80%, consistently, for everybody.

That sounds like an obviously good property. Hold that thought.

### Now the problem

Imagine 1,000 candidates in two groups. Say Group B went to less prestigious universities, had more career breaks, or wrote in less fluent English — whatever the reason, their CVs *look* weaker to the model.

Suppose, in reality, 30% of Group A would succeed in the role and 15% of Group B would. (That gap usually reflects earlier unfairness — worse schools, fewer opportunities — but the model does not know or care why.)

**If your scores are calibrated,** Group B's scores sit lower on average. Set one threshold for everyone, and something follows automatically: a *qualified* Group B candidate is more likely to score below the line than a *qualified* Group A candidate.

| | Group A | Group B |
|---|---|---|
| Score of 0.8 means | 80% likely to succeed | 80% likely to succeed |
| Qualified people wrongly rejected | fewer | **more** |

So calibration is satisfied, and Group B bears more of the wrongful rejections.

### Can you fix it?

Yes — lower the threshold for Group B until both groups are wrongly rejected at the same rate.

But now a Group B candidate scoring 0.4 gets through and a Group A candidate scoring 0.4 does not. The score no longer means the same thing for everyone. **You have broken calibration.**

### The point

You can have scores that mean the same thing for everybody, **or** error rates that fall equally on everybody. Not both. This is proven mathematics, not a limitation of current technology. It holds unless the groups have identical success rates, or your model is perfect. Neither will ever happen.

**Why this matters more than anything else in the unit:** no engineer can resolve this. There is no better model, no cleverer threshold. Somebody has to choose which kind of fairness the company wants, and write down why.

That person is the Head of Talent Acquisition you named in unit 1. This is the reason that role has to exist. Not paperwork — an unavoidable decision that only an accountable human can make.

---

## A5. New thing 4: two kinds of discrimination, and you only fixed one

**Disparate treatment** — using someone's protected characteristic directly. Rejecting candidates for being over 40. Obvious, intentional, illegal.

**Disparate impact** — a process that looks neutral but produces worse outcomes for a protected group. No intent needed. Still illegal in most places.

Your system scrubs name, age, ethnicity and region before the CV reaches the model. That handles **treatment**. Nothing more.

What stays in the CV: the university, the graduation year, gaps in employment, how fluently the person writes. Graduation year does not tell the model who you are. It tells it roughly how old you are. Employment gaps correlate with parental leave. Fluency patterns correlate with nationality.

So the model can still disadvantage a group without ever knowing anyone's identity. **That is disparate impact, and it is where the legal risk actually sits.**

This is the correction to your unit 1 gap 3. You wrote that the leftover fields could be used to "derive PII profiling." Two separate problems were merged there:

- **Working out who someone is** → a privacy problem → fixed by removing data
- **Working out what group someone belongs to** → a discrimination problem → only found by testing outcomes, never fixed by removing data

Different problem, different law, different control. Removing fields does nothing for the second one. The only way to find it is to measure results across groups after the fact.

---

## A6. One more term: confabulation

An LLM producing a fluent, confident, completely wrong answer. Not lying — it has no concept of truth. It generates plausible text.

Relevant to you because the moment your tool explains *why* it gave a score, that explanation may be invented after the fact and have nothing to do with the actual scoring. A reviewer reads a convincing paragraph and trusts a number that the paragraph does not actually justify.

Keep that in mind when you get to unit 1's gap 4 about making scores explainable. The naive fix makes things worse.

---

## A7. And the thing you already found

**Automation bias** — people over-trust automated output and under-weight their own judgement, even when they can see the machine is wrong.

You found this in unit 1 without the name for it. The delivery driver who followed the route onto a tidal causeway. The officers who trusted a risk score that said "low" when the situation said otherwise.

Now apply it to your own tool. A recruiter opens a ranked list. They have been told what to think before they read a single CV. Ask yourself: **what would have to happen for that recruiter to pull candidate number 40 into the shortlist?** If the honest answer is "nothing realistic," then the review step is decoration.

That is your unit 1 gap 2, with a proper name.

---
---

# PART B — Now go to the sources

Five things. Roughly 3 hours 20 minutes total. These go fast because Part A told you what to look for.

### B1. Read NIST AI RMF 1.0 (75 min)
Free PDF, search "NIST AI 100-1". Read it start to finish without stopping to take notes.

**What you are looking for:** places where it describes something you do differently in test work, or something you have never done at all. Jot a line each time. Do not write notes on the parts that feel familiar — you already have those.

### B2. Read NIST AI 600-1, the Generative AI Profile (40 min)
Free, and short. Twelve risk categories for systems built on LLMs.

**What you are looking for:** which of the twelve your unit 1 known gaps already cover. You will find you got to several of them on your own. Note which ones.

### B3. Re-read your own unit 1 patterns (15 min)
Open your incident log. Read your five patterns against Part A.

Pattern 5 — periodic re-evaluation so new problems do not creep in — is the MEASURE and MANAGE functions. You wrote it from evidence before reading the framework. Note where else this happened.

### B4. Read one system card (45 min)
Pick one recent frontier-model system card (Anthropic, OpenAI and Google DeepMind all publish them). Just one, read properly.

You are not reading about the model. You are reading **somebody else's test report**, which is a document type you have assessed for eighteen years. Answer five questions:

1. What did they test, and how do they describe coverage?
2. Where do they admit a limitation instead of reporting a result?
3. How is red-teaming described — who, what access, what scope?
4. What risk do they accept, and what is their argument for accepting it?
5. **What is missing?**

Question 5 is the one your background makes you good at. Trust it.

### B5. Apply automation bias to your own tool (25 min)
Answer the question from A7 in writing: what would have to happen for a recruiter to promote candidate 40? Half a page. Be honest.

---
---

# PART C — Two files to write

### C1. `03-deliverables/testing-to-ai-delta.md`

One page, three lists:

- **Same as test work, different word** — e.g. test strategy → evaluation strategy
- **Similar but changed** — and say how it changed
- **Nothing like it in test work** — the genuinely new things

Use Part A as your starting material, add whatever B1 and B2 turned up.

**Why this page matters:** it tells you where to spend your remaining study time, and it becomes an interview answer nobody else can give — "here is what AI assurance borrows from software testing, and here is exactly where it stops working."

### C2. `03-deliverables/glossary.md`

Six terms, **in your own words**, each with one line on how it applies to the screening tool:

calibration · disparate impact · automation bias · confabulation · residual risk · non-determinism

Writing them in your own words is the whole point. If you copy my sentences, the file is worth nothing. Your unit 1 gaps 2 and 4 were yours, and they were better than my versions.

---

## Not in this unit

Do not start the EU AI Act. That is unit 5, and you already have a head start from the training you ran for your product team.

**If anything in Part A is still unclear, tell me which section and I will explain it differently.** A4 is the one people get stuck on, and getting stuck there is normal.
