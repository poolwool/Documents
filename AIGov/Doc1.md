# Week 1 — Foundations: What Actually Goes Wrong

**Time budget: 2 hrs 30 min.** Five tasks. Two deliverables at the end.

**Theme of the week:** before any framework, build a mental library of real AI failures. Governance people who skip this write policies that look correct and catch nothing. By Sunday you should be able to say, from memory, five distinct ways an AI system harms someone and which layer of the stack each failure lived in.

---

## Task 1 — Set up your working folder (15 min)

Create a folder, put it under git, keep it private for now. Plain markdown, no tools to learn, no subscription, and the whole thing is yours on disk.

```
ai-governance/
  00-log.md              # one entry per session: date, what you did, time spent
  01-incidents/
  02-case-study/
  03-deliverables/
```

`00-log.md` matters more than it looks. At 2–3 hrs a week, a study habit dies quietly and you don't notice for a month. One line per session is enough to notice.

---

## Task 2 — Apply to BlueDot (20 min)

Go to **bluedot.org** and apply to the **AGI Strategy** course (free / pay-what-you-want). It's the prerequisite for their Frontier AI Governance course, which is the one you actually want.

Cohorts are small and run in intakes, so the wait is real — applying now means it lands mid-plan rather than after. The part-time format is roughly 5 hrs/week for 5 weeks, which is above your normal budget; treat that stretch as a planned exception when your cohort comes up.

In the application, the "why" field matters. Say you're moving into AI governance from a technical background and want the strategic picture before the regulatory detail. That's true and it's exactly who they take.

---

## Task 3 — Download the AIGP Body of Knowledge (20 min)

From the IAPP site, download the **AIGP Body of Knowledge v2.1** (effective February 2026). It's free and you don't need to register for the exam to get it.

Don't study it. Read the domain headings and sub-topics once, then save it. You now have the field's own definition of what an AI governance professional is supposed to know — use it as a checklist you tick off against this plan, and as the basis for your month-5 decision on whether to pay for the exam.

While you're there: note which domains make you think "no idea what that is." Those are your gaps, and they're more useful to know now than later.

---

## Task 4 — Incident study (75 min) ⭐ the core of the week

Open the **AI Incident Database** (incidentdatabase.ai) and the **AIAAIC repository**. Work through **12 incidents**. Pick a spread — hiring, credit, healthcare, content moderation, facial recognition, chatbots, autonomous systems, generative AI.

For each, one row in `01-incidents/incident-log.md`:

| # | Incident | Sector | Who was harmed | Harm type | Failure layer | Would documentation have caught it? |
|---|---|---|---|---|---|---|

**Harm type** — pick from: physical, financial, discrimination, privacy, dignity/psychological, information integrity, loss of opportunity, erosion of autonomy.

**Failure layer** — this is the column that teaches you the most. Pick one:
- **Data** — the training data encoded the problem
- **Model** — the model itself was inaccurate, miscalibrated, or brittle
- **Product** — the system worked as built, but the design put it somewhere it shouldn't have been, or gave users no way to contest it
- **Deployment** — right system, wrong context, wrong population, or no monitoring after launch

**Last column** — be honest. Some failures were genuinely unforeseeable. Most weren't. Noticing which is which is the actual skill, because it's what separates governance that reduces harm from governance that produces paperwork.

Timebox strictly: ~6 minutes per incident. You're building pattern recognition, not writing case studies.

Then write **five lines** at the bottom of the file: the patterns you noticed. Not a summary — patterns. Things like "nobody was monitoring after launch" or "the affected people had no way to know a model was involved."

---

## Task 5 — Lock the case study (20 min)

You asked me to pick. Here's the call, and the reasoning, because you should be able to defend it.

### Primary case study: an AI-assisted candidate screening tool

**The scenario:** a mid-sized Indian IT services company builds an internal tool that ingests CVs, scores candidates against a job description, and ranks them for recruiters. It uses a third-party LLM API for parsing and scoring. It's used for the company's own hiring in India, and the company is now planning to offer it as a product to European and US clients.

**Why this one and not your own app:** a to-do planner is a fine place to *practice building guardrails* — and we'll use it for exactly that in Phase 3 — but it makes a weak governance case study. It doesn't make consequential decisions about people, so most of the interesting obligations never attach, and you'd learn the frameworks by reading them rather than by being forced to apply them.

The screening tool, by contrast, lights up nearly everything you need to learn:
- **Annex III high-risk** under the EU AI Act (employment and worker management) — so the full Art. 9–15 requirements apply, with a December 2027 deadline
- The **provider vs deployer** distinction becomes concrete and confusing, in a useful way: the company is a deployer when it uses the tool on its own hiring, and a provider when it sells it to European clients. Different obligations, same system. Most people get this wrong, and it's a standard interview question.
- **DPDP Act** obligations on candidate personal data, consent, retention, and grievance redressal
- **Colorado's AI law** treats employment decisions as high-risk too, with rules landing January 2027 — so the same system has to be argued under a US regime with a different structure
- Real, well-documented **fairness** problems with real public incidents behind them
- A **third-party model provider** in the chain, which is the value-chain risk that both NIST's GenAI Profile and ISO 42001 care about
- A genuine **human oversight** design question: what does meaningful oversight look like when a recruiter sees a ranked list?

It's hypothetical, which is a feature — you can publish everything, there's no employer NDA, and writing impact assessments for specified hypothetical systems is literally how ISO 42005 training works.

**Your task now:** write `02-case-study/system-description.md`, one page. Cover: purpose, users, affected persons, inputs, outputs, what decision the output influences, where the personal data comes from, what goes to the third-party model provider, retention, and who inside the company owns it. Invent the details — but invent them *specifically*. "Candidate data" is useless; "name, contact details, employment history, education, and a free-text cover letter, retained 24 months" is something you can reason about.

---

## Deliverables by end of week

1. `01-incidents/incident-log.md` — 12 rows plus five pattern lines
2. `02-case-study/system-description.md` — one page, specific

Paste both here when they're done and I'll review them: where the failure-layer calls are off, and where the system description is too vague to support a risk assessment. The second one is where most people's first attempt falls apart, and it's better to find that out in week 1 than in week 12.

---

## Optional, only if you have extra time

Skim the **NIST AI Risk Management Framework 1.0** — just the four functions (Govern, Map, Measure, Manage) and what each is for. Twenty minutes. It's week 2's starting point and a light skim now makes that week easier.

**Do not** start on the EU AI Act yet.
