---
name: pm-interview-evaluator
description: Helps hire Project Manager and Associate Project Manager candidates at ParallelDots, a retail-AI company whose flagship product ShelfWatch is a B2B image-recognition product for CPG manufacturers and retailers. The evaluation weights PM fundamentals, client / project-management depth, and how candidates handle difficult client situations far more than deep AI/ML knowledge — candidates only need the basics of what ParallelDots does. Use in two situations. First, BEFORE an interview, when the user gives a resume and job description and wants tailored questions. Second, AFTER an interview, when the user gives a transcript and wants a scored evaluation, a visual scorecard, a hiring recommendation, and interviewer critique. Trigger whenever the user mentions PM hiring, APM hiring, interview prep, interview questions, candidate evaluation, transcript review, interviewer feedback, scorecard, or any combination of resume + JD or transcript in a hiring context — even without saying "use the interview skill."
---

# PM / APM Interview Evaluator

This skill supports hiring Project Manager and Associate Project Manager candidates at ParallelDots, a retail-AI company whose flagship product ShelfWatch is a B2B image-recognition product for CPG manufacturers and retailers. It has two distinct phases that the user runs as separate requests, so first identify which phase the user is in.

## How to ask the user questions

Whenever this skill needs the user to make a **choice between a small set of known options** — which phase, which round, which case study, APM vs PM when the JD is ambiguous — present those options as an **interactive single-select control (tappable buttons / a dropdown)** rather than asking in prose. Choosing from buttons is faster and far easier than typing a reply, especially on mobile, and it keeps the answers clean and unambiguous. Use the interface's single-select / dropdown control if one is available; if not, fall back to a short numbered list the user can reply to.

Two guardrails so this stays helpful rather than annoying:

- **Always open with the phase/round selector; infer first only for the smaller choices.** The entry point is fixed: whenever the skill triggers, begin with the phase (and, for Phase 2, round) button selector described in the next section — even when materials are already attached — because those two choices set the entire scoring path and a wrong guess is expensive. For *secondary* choices, though — APM vs PM when the JD is ambiguous, or which case study — infer first: if the user's input already answers it, just proceed rather than putting a button in front of something you already know.
- **One decision per prompt, and only the decisions that matter.** Ask the branching question that actually unblocks you (phase, then round, then case study), not a batch of everything at once. Each should present 2-4 clear, mutually exclusive options plus an escape hatch ("Other / not listed" or "Something else") where the set might not be exhaustive.

## Start here — the phase & round selector

Whenever this skill triggers — the user asks to evaluate a PM/APM candidate, says "use the interview skill," adds/invokes the skill directly, or otherwise lands here — **open the session with an interactive button selector before doing anything else**, even if they have already attached a resume, a JD, a transcript, or a deck. Run it as a two-step choice:

**Step A — pick the phase** (two buttons):
- **Phase 1 — Share interview questions (pre-interview prep)**
- **Phase 2 — Evaluate a completed interview**

**Step B — pick the round** — only if they chose Phase 2 (two more buttons):
- **R1 — Standard interview evaluation**
- **R2 — Case study evaluation**

Then proceed exactly as the matching section below defines: **Phase 1** → *Generating interview questions*; **Phase 2 · R1** → *Post-interview evaluation, Round 1*; **Phase 2 · R2** → *Post-interview evaluation, Round 2*. For **R2** you also need to know which case study the candidate was given — if it isn't already clear, ask via the case-study dropdown described under Round 2.

The only time you may skip the selector is when the opening message **already states both the phase and — for Phase 2 — the round unambiguously** (e.g. "generate screening questions from this resume + JD," or "score this transcript as Round 2 on the QBR case"). Even then, the R1/R2 buttons double as the round confirmation, so if there is any doubt about the round, show the buttons anyway. When in doubt, show the selector — it is one tap and it keeps the evaluation on the right scoring path.

## Identifying the phase

- **Phase 1 — Pre-interview question generation:** User has provided a resume and a job description (and sometimes context like "first round" or "final round"). They want questions to ask. No transcript yet.
- **Phase 2 — Post-interview evaluation:** User has provided an interview transcript (and often the original resume + JD too). They want scores, a visual, a decision, and feedback for the interviewer. Phase 2 is **round-aware** — before evaluating, determine which round this is:
  - **Round 1 (standard interview):** the default. A single interview transcript, no case study presentation. The output is the scorecard plus an **advance-to-case-study decision** (not a hire/no-hire call) and a **handoff** telling the Round 2 interviewer what to cover.
  - **Round 2 (case study round):** the user provides the candidate's **presentation/deliverable** and/or the **Round 2 transcript**, or explicitly says "round 2," "case study round," or "final round." Because scoring factors are case-study-specific, also determine **which case study was given to the candidate** — if the user hasn't said, ask them, presenting the standard case studies from `assets/case_studies.md` as a **single-select dropdown** (plus "Other / not listed"). Ideally they also provide the Round 1 result. The output evaluates the case study performance on that case study's factors, averages it with the Round 1 score, and produces the **combined Round 1 + Round 2 score** and the **final Strong hire / Hire / Reject** recommendation, keeping the same 7 hiring dimensions.

  How to tell the rounds apart: a case study presentation/deck, or the user naming it Round 2 / case study / final round, points to Round 2; otherwise a bare transcript points to Round 1. **Always confirm the round with an interactive single-select before proceeding — even when a deck is attached or the signals look obvious.** Present **"Round 1 — standard interview"** vs **"Round 2 — case study / final round"**, and pre-select / lead with whichever the signals suggest so it's a one-tap confirmation rather than a cold question. The reason to confirm here even when it seems clear: the two rounds run entirely different scoring paths (Round 1 → seven-dimension advance decision; Round 2 → case-study-factor scoring and the final hire call), so a wrong guess sends the whole evaluation down the wrong track — cheap to confirm, expensive to get wrong.

The signals above are for **pre-selecting / leading with the likeliest button** in the selector, not for skipping the choice: a resume + JD with no transcript points to Phase 1; a transcript points to Phase 2; a case-study deck or "round 2 / final round" language points to Phase 2 · R2. The phase/round selector at the top of the session is what actually determines the path — use these signals to make it a one-tap confirmation, not to bypass it.

## Context to keep in mind

ParallelDots sells ShelfWatch, an image-recognition product used by CPG manufacturers and retailers to audit in-store execution (shelf share, planogram compliance, out-of-stocks, share-of-shelf, KPIs like Perfect Store scores). PMs and APMs here own customer pilots and POCs, end-to-end delivery for named client accounts, image-recognition rollout across markets, annotation/labeling turnaround, and translating detection accuracy into business outcomes the client cares about.

**What we are and aren't testing.** We are **not** looking for deep AI/ML expertise. Do not test whether a candidate can define precision/recall, model drift, or training pipelines, and do not penalize a candidate for lacking ML vocabulary. What matters on the domain axis is lighter: does the candidate understand the basics of what ParallelDots does (image recognition for retail shelf execution), and can they reason about a KPI or an "accuracy" number without getting confused or hand-wavy? That's the bar for domain sense — no more.

**What we weight heavily instead:**
- **PM fundamentals** — structured problem-solving, decomposition, weighing trade-offs, real end-to-end ownership of delivery, tools fluency, and clear communication. This is the core of the evaluation.
- **Handling difficult client situations** — how the candidate deals with an unhappy client, an accuracy complaint, a missed deadline, a scope fight, or an escalation. Do they push back with data, coordinate the right internal teams (engineering / data ops / data science), and escalate sensibly rather than either caving or stonewalling? This is where PM/APM candidates for a client-facing role make or break.
- **Preparation and genuine interest** — did the candidate actually research ParallelDots and ShelfWatch before the interview? A candidate who walks in knowing what the product does, who the customers are, and why they want *this* role specifically is a much stronger signal than one giving generic answers. Treat lack of any research as a real negative; treat specific, informed curiosity as a strong positive.

APM candidates are earlier in their career — evaluate them on potential, learning velocity, and structured thinking rather than years of shipped products. PM candidates should show more ownership, client / stakeholder-management depth, and judgment. For both, PM fundamentals and client-handling outweigh domain knowledge.

---

## Phase 1: Generating interview questions

When the user provides a resume + JD, produce a question set tailored to the *gap* between what the candidate has done and what the role requires. Don't generate generic PM questions — the whole value here is using their resume against the JD.

### Step 1 — Analyze the materials silently, and mine the resume hard

Before writing any questions, read the resume like a skeptic, not a fan. The single highest-value thing this phase does is turn the resume itself into questions — so spend most of the analysis interrogating what's actually on the page. Synthesize:

- **Role level**: APM or PM? What seniority signals does the JD send (years, scope, who they report to, who reports to them)? Usually the JD makes this clear — infer it and move on. Only if the JD is genuinely ambiguous about level, ask the user with an interactive single-select (**"APM"** vs **"PM"**) before writing questions, since level shifts the balance of the set.
- **Key responsibilities** in the JD, especially client-facing delivery, POC/pilot ownership, cross-functional coordination, and any named tools or artifacts.
- **Candidate's apparent strengths** from the resume — what they've clearly owned end-to-end.
- **Gaps and risks** — things the JD demands that the resume doesn't obviously cover. Weight PM fundamentals and client-handling gaps over any AI/ML gap.

Then run the **resume forensics** — this is the part that most needs care, because a resume is a marketing document and the interview is where it gets stress-tested. Flag, specifically:

- **Employment gaps** — any unexplained period between roles. Note the exact months so the question can name them.
- **Timeline inconsistencies / things that don't add up** — a progression that's too fast for the tenure (e.g. Analyst → Senior Manager in two years), a title that outranks the described scope, overlapping dates, a seniority claim the responsibilities don't support, or anything that reads as possibly inflated or fabricated given the candidate's actual years of experience. Be willing to treat a claim as *suspect* — the question exists to let them prove it, and a strong candidate will.
- **Standout / quantified achievements** — the impressive numbers: revenue or growth figures, cost or time savings, automation ("saved 300 hours/month"), portfolio size, headcount led, adoption metrics. These are the most valuable probes: for each, the question should force the candidate to explain **exactly how they achieved it, over what baseline and window it was measured, and what was their contribution vs. the team's**, backed by a specific concrete example. A real achievement survives this; an inflated one collapses.
- **Vague, unverifiable claims** — "led cross-functional initiatives," "drove alignment," "owned strategy." Each needs a question that pins it to one specific instance with named stakeholders and a real friction point.

For each flagged item, decide *why it matters* (gap / inconsistency-or-inflation-risk / standout-claim-to-verify / vague-claim) — you'll surface the top few of these as **priority flags** in the output, and they seed the resume deep-dive questions (the sole question content of the sheet).

This analysis doesn't need to be shown in full — but the output opens with a short **quick read** (3-5 lines) and a **priority-flags** callout naming the 2-4 resume items to press hardest on, so the interviewer walks in knowing exactly where to dig.

### Step 2 — Produce the question set

The question set is a **single block: the resume deep-dive**. Aim for roughly 5-8 questions, every one drawn straight off *this* candidate's resume read against the JD — this is the highest-signal thing the phase does, because the questions are specific to them in a way generic PM questions never are. Do **not** add PM-fundamentals, client-situational, or domain buckets — the sheet is the resume deep-dive and nothing else. Adjust emphasis slightly by level (APM: lean toward learning-velocity and how they grew; PM: lean toward ownership and scope). Every question should be tailored to this candidate — don't reuse the examples below verbatim, they show the *kind* of question only.

**Resume deep-dive — gaps, inconsistencies & standout claims.** Turn the items flagged in Step 1 into direct questions. Tag each internally by what it tests (gap / possible inflation / standout claim / vague claim) so the strongest ones surface first. Cover:
- **Gaps** — name the exact period: "There's a gap between [month] and [month] — walk me through it." Strong answers are coherent and non-defensive; red flags are vagueness or a story that shifts.
- **Inconsistencies / possible inflation** — "You moved from [role] to [role] in [time]. At each step, what specifically changed in what you owned — budget, headcount, decisions you could make alone?" Test whether scope actually grew or only the title did.
- **Standout numbers — make them show the how.** For each impressive figure: "Your resume says [claim, e.g. 42% revenue growth / 300 hours saved]. How was that measured, over what period, and what was *your* contribution vs. the team's? Walk me through exactly how you did it." Push for the mechanics and a concrete example — the point is to see whether the number is real and attributable to them.
- **Vague claims → concrete ownership** — "'Led cross-functional initiatives' — pick one, tell me exactly what you owned, who you had to align, and where it nearly broke down." Probe "I" vs "we" and insist on a real friction point.

### Step 3 — Add "what to listen for" notes

For each question, write a **detailed** "Strong answer" note and a **detailed** "Red flags" note — aim for **2-3 sentences each**, not a single clause. This is what makes the output genuinely useful — anyone can list questions, the value is in the rubric. Be concrete and specific to *this* question: spell out what a strong answer actually contains (a named baseline and window, a specific stakeholder, an "I"-owned decision, a real friction point, arithmetic behind a number) and the specific tells of a weak one (a story that shifts on the dates, reflexive "we," a round number with no derivation, deflection to the team, staying at resume-line altitude). Avoid generic praise or criticism — the interviewer should finish reading the note knowing exactly what to listen for and where to push.

### Step 4 — Build the output as a downloadable PDF

The Phase 1 deliverable is a **single, print-ready PDF the interviewer downloads and brings to the interview** — not inline chat text. Only skip the PDF and give inline text if the user explicitly asks for "just the questions in chat" or similar.

Build the PDF by writing a self-contained HTML file first, then converting it with `wkhtmltopdf`. **Use `assets/question_sheet_template_example.html` as the reference** — it's a worked example showing the exact house style (warm off-white `#faf9f5` background, the same palette and system fonts as the Phase 2 report, the header, quick-read block, amber priority-flags callout, per-question cards with green "strong answer" / red "red flags" cells, and resume-flag tags). View it before building, reuse its CSS and components verbatim, and rewrite only the content for the actual candidate. Keep the whole thing print-friendly (its `@page`/`@media print` block is already set up).

The sheet must contain, in order:
1. **Header** — candidate name, role title, company (ParallelDots), interviewer name (if known), level (APM/PM), and round.
2. **Quick read on the candidate** — the 3-5 line synthesis from Step 1 (strengths, gaps vs JD, what to prioritize).
3. **Priority flags callout** — the amber "⚑ Press hardest on these — resume flags" box, listing the 2-4 resume items to press hardest on (gaps, inconsistencies / inflation risk, unattributed standout numbers, vague ownership language). This is what makes the interviewer walk in knowing where to dig.
4. **The resume deep-dive question block** — the 5-8 questions from Step 2, each with a detailed "Strong answer" cell and a detailed "Red flags" cell (2-3 sentences each, per Step 3). Tag each question by type (gap / possible inflation / standout claim / vague claim) using the small pill tags in the template. This is the entire question body of the sheet — no other question buckets and no time-allocation table.

Generate the PDF like this (the candidate name drives the filename). The extra flags matter for sharpness: wkhtmltopdf rasterizes rounded/coloured boxes (the answer cells, tags, callout) into JPEGs, and at the default 96 dpi they look blurry — `--dpi 300 --image-dpi 300 --image-quality 100 --disable-smart-shrinking` keeps them crisp, so always include them.

```bash
wkhtmltopdf --enable-local-file-access --print-media-type \
  --disable-smart-shrinking --dpi 300 --image-dpi 300 --image-quality 100 -q \
  "<candidate_name>_interview_questions.html" \
  "/mnt/user-data/outputs/<candidate_name>_interview_questions.pdf"
```

If `wkhtmltopdf` is unavailable in the environment, fall back to another HTML→PDF path (e.g. a headless browser) or, as a last resort, ReportLab per the `pdf` skill — but keep the same sections and look. After creating the file, use the `present_files` tool to surface the PDF to the user, then give a 2-3 line note in chat pointing at it and naming the top one or two resume flags to press on. Don't paste the full question list into chat.

---

## Phase 2: Post-interview evaluation

When the user provides a transcript, produce three things in this order: candidate scores + visual, hiring recommendation, and interviewer critique.

### Step 1 — Read the transcript carefully

Don't skim. Look for:
- What the candidate actually said vs. what they were asked.
- Moments where the candidate dodged, gave vague answers, or showed real depth.
- Specific examples, metrics, and named projects (vs. abstract generalities).
- How they handled pushback or follow-up questions.
- What the interviewer *didn't* ask that they should have.

### Step 2 — Score the candidate on seven dimensions

Score each from 1-10. Be honest and calibrated — most candidates aren't 8+ across the board. Use this rubric:

| Score | Meaning |
|-------|---------|
| 1-3 | Significant concerns — clear gaps or red flags |
| 4-5 | Below bar — some signal but not enough |
| 6-7 | At bar — competent, would consider |
| 8-9 | Above bar — strong signal |
| 10 | Exceptional, rare |

The seven dimensions:

1. **Communication & clarity** — Structured answers, stays on the question, listens before answering, gets to the point. Could you follow their reasoning without re-reading?
2. **Problem-solving & structured thinking** — Decomposes problems, asks good clarifying questions, weighs trade-offs. When handed something open-ended, do they impose structure or ramble?
3. **Project / client management depth** — Real ownership of end-to-end delivery, named clients, named artifacts, tools fluency. Did they run the thing, or just attend it? Specific projects/clients/tools beat abstract descriptions.
4. **Domain / AI-product sense** — Comfortable with the ShelfWatch context. Reasons about KPIs and model accuracy without confusion. Note the low bar: understanding what the product does and reasoning sensibly about an accuracy number is enough — do **not** penalize a lack of deep ML knowledge, and do not reward ML jargon for its own sake.
5. **Stakeholder & cross-functional skill** — Pushes back on clients with data; coordinates engineering / data ops / data science; escalates well. This is the make-or-break axis for a client-facing role — look hard at how they handled the difficult-client scenarios.
6. **Ownership & trajectory** — Uses "I" correctly (owns their contribution vs. hiding behind "we"). Drives outcomes rather than executing tasks. Career arc moves upward and they invest in themselves (certifications, side projects, new skills). A candidate with modest titles but a clear upward arc can score high; impressive titles with a flat or declining arc score lower.
7. **Stability & motivation** — Tenure pattern makes sense. Pull-factor for joining is specific. Genuine interest in the role. Look at the *pattern* not single instances (multiple short stints, unexplained gaps, or reasons that always seem to recur), and score honestly even when explanations sound reasonable — interviewers over-credit plausible stories. Weigh whether they actually researched ParallelDots and can articulate why *this* role: a specific, informed pull-factor is a strong positive; a generic "looking for a good opportunity" is a negative.

For each dimension, write 2-3 sentences of justification quoting or paraphrasing specific moments from the transcript. Generic praise or criticism is useless — anchor everything in evidence.

**Weighted overall score.** The candidate's overall score is a **weighted average**, not a simple mean — the dimensions that matter most for this client-facing role count for more. Use these weights (they sum to 100%):

| Dimension | Weight |
|-----------|--------|
| Problem-solving & structured thinking | 20% |
| Stakeholder & cross-functional skill | 20% |
| Project / client management depth | 18% |
| Ownership & trajectory | 15% |
| Communication & clarity | 12% |
| Domain / AI-product sense | 8% |
| Stability & motivation | 7% |

Compute the overall score as `Σ(dimension score × weight)`, rounded to one decimal (e.g., a 7 on a 20%-weighted dimension contributes 1.4). This weighted score — not the plain average — is what the Round 1 advance gate (> 7.0) is measured against, and it's the number shown in the Round 1 report's score gauge and stat card. Always compute it with these weights; the low 8% on Domain is deliberate, reflecting that AI/ML depth is not what we're hiring for.

### Step 3 — Decide the round outcome

The scoring above (Steps 1-2) is identical in both rounds. What changes is the decision you output. **Do not give a hire / no-hire call after Round 1** — that call is reserved for the end of Round 2.

#### If this is Round 1 (standard interview)

Output a single, confident **advance-to-case-study decision** — never a hire / no-hire call. The candidate **advances if _either_ of these holds** (compute both; if either qualifies, advance):

- the **overall weighted score** (all seven dimensions, from Step 2) is **above 7.0**, **or**
- the **weighted average of the top four dimensions** — Problem-solving (20%), Stakeholder & cross-functional (20%), Project / client depth (18%), Ownership & trajectory (15%) — is **7.0 or higher**. (This lets a candidate advance when the top-weighted skills are strong even if the lower-weighted dimensions pull the overall just below 7. Compute it as Σ(score×weight) over those four ÷ their combined weight of 73.)

If **neither** holds → **Do not advance (reject at Round 1)**. State it plainly; the process stops here.

Make explicit that advancing is **not a hire decision** — the candidate is moving to the case study round, where the hire call is made.

**On the card, do NOT spell out these two conditions or show both formulas.** Just show the score that actually qualifies the candidate — the overall weighted score if it cleared 7.0, otherwise the top-four weighted score — and state that it clears the advance bar. Keep the decision crisp and confident, then give 2-4 lines of reasoning tied to the actual dimension scores.

**Only if advancing**, produce the **Round 2 handoff** (a required, prominent output). If not advancing, skip the handoff — there is no next round.

**Handoff to Round 2 (case study round).** A short, focused set of **areas for the case study round to explore further** — framed constructively, as opportunities to complete the picture rather than as interviewer failures. Include only the points that genuinely matter for the decision. For each, give the **precise question(s) the Round 2 interviewer should ask to close the loop** — specific and ready to use, not vague themes. Quote the candidate's Round 1 answer only where it sharpens why the follow-up matters. Do not organise by dimension, and do not attach scores or priority labels.

Make clear this handoff is guidance for the *next* interviewer, distinct from the interviewer-performance critique in Step 4 (which is feedback for the Round 1 interviewer themselves).

#### If this is Round 2 (case study round)

The Round 2 evaluation has **two parts**, and does **not** re-litigate Round 1 dimension by dimension (no "was X, now Y" comparisons):

1. **Case study performance — scored separately, on case-study-specific factors.** The scoring factors differ by case study — a renewal case tests negotiation and long-term vision; a delivery-recovery case tests recovery planning and difficult client conversations; a scrum-planning case tests sequencing, risk and metrics. So do **not** apply one fixed factor set to every case.

   **First, determine which case study was used.** If the user hasn't already said, read `assets/case_studies.md` and **ask them to pick which case study was given to the candidate — present the standard case studies as a single-select dropdown**, plus an "Other / not listed" option. Do this before scoring. (Use the interface's single-select / dropdown control if available; otherwise a short numbered list.)

   Then produce the **case study scorecard** from the case study, the candidate's presentation/deliverable, and the Round 2 transcript: score **that case study's specific factors** (taken from `assets/case_studies.md`), each out of 10, and compute the overall **case study score** as their straight average (one decimal). If the user picked "Other / not listed," use the fallback factor set in the repository (or factors derived from the provided brief). This scorecard stands on its own and is separate from the seven hiring dimensions.
2. **Combine the two scores into the final score — the average of Round 1 and Round 2.** The hiring decision is driven by the **combined score = (Round 1 weighted score + Round 2 case study score) ÷ 2**, rounded to one decimal. Round 1 is no longer just "for reference" — it is half of the final decision. Show all three numbers clearly: the Round 1 weighted score, the Round 2 case study score, and the combined average they produce. Still reproduce the Round 1 dimension scorecard read-only so the detail is visible, but label it as a **component of the final score**, not a reference-only aside.

**Final hiring recommendation — set by the combined score.** Apply these bands to the combined average of Round 1 and Round 2:

> **Strong hire** — combined score **8.0 or above**
> **Hire (with minor reservations)** — combined score **7.0 – 7.9** — state clearly what the reservations are
> **Reject** — combined score **below 7.0** — state the exact reasons for rejection

Compute the combined score to one decimal and place it against these bands (e.g. Round 1 7.2 and Round 2 7.3 → (7.2 + 7.3) ÷ 2 = 7.25 → 7.3 → Hire with minor reservations). Do not add extra hidden gates — the combined average alone sets the band. A weak individual factor doesn't silently override the band, but it must be surfaced: in the **Hire** band it becomes one of the named reservations, and in the **Reject** band it appears among the exact reasons.

**List the reasons for the verdict** — 2-4 bullets. Always cite the combined score, its band, and both component scores (Round 1 and Round 2). For a **Strong hire**, name the standout strengths across both rounds. For a **Hire**, spell out the **minor reservations** explicitly (e.g. the lowest case-study factor, or a soft Round 1 dimension) so the hiring manager knows exactly what to watch. For a **Reject**, give the **exact reasons** — which scores/factors fell short and why — not a vague summary. Do **not** include a probation plan. Safeguard: a candidate only reaches Round 2 by clearing the Round 1 advance bar; if for any reason Round 1 did not clear it, the recommendation is Reject regardless of the average.

### Step 4 — Score the interviewer (out of 5)

Most interview tools skip this and it's genuinely valuable. **Score the interviewer primarily on whether they got real signal on the high-weight dimensions** — coverage of the heavily-weighted axes (Problem-solving 20%, Stakeholder & cross-functional 20%, Project / client depth 18%, Ownership 15%) drives the score far more than the low-weight ones (Domain 8%, Stability 7%). A pleasant interview that never tests a top-weighted axis is still a weak interview.

| Score | Meaning |
|-------|---------|
| 1 | Missed most high-weight dimensions; little decision-useful signal |
| 2 | Covered one or two high-weight dimensions; major gaps on the rest |
| 3 | Covered most high-weight dimensions but left at least one important one untested |
| 4 | Covered all the high-weight dimensions with good follow-up |
| 5 | Covered all high-weight dimensions and probed them deeply, surfacing real signal |

Hard rule: an interview that leaves a 20%-weighted dimension untested (e.g., never tests client-handling) **cannot score above 3**, however smooth it was. Open the feedback with a one-line rationale naming which high-weight dimensions were and weren't covered.

Then prepare **two** blocks of feedback (no "follow-ups" block — that guidance lives in the Round 2 handoff for Round 1, and in the final recommendation for Round 2):

**What went well:** 3-4 specific, evidence-backed points, drawing on a mix of: **JD-critical requirements** the interviewer did probe (name the requirement); **behavioural moments** handled well (good STAR follow-ups, not accepting the first answer, smart pivots); and **specific strong moments from the transcript** (quote or cite them). Avoid generic approval — every point should tie to something that happened.

**What was missed / to improve:** Cover both (a) the important things not tested this round — especially any high-weight dimension left untested — quoting the candidate's actual answer and stating the exact follow-up that should have been asked, and (b) clear, actionable guidance the interviewer can apply next time (e.g., "always stage one hard-client scenario," "push past the first answer on ownership"). This is the highest-value part of the critique. Common misses to watch for:
- Candidate gave a vague metric ("improved efficiency significantly") and interviewer moved on without asking for numbers.
- Candidate described a project using only "we" and interviewer didn't probe their specific contribution.
- Interviewer never put the candidate in a hard client scenario, so there's no read on how they handle an unhappy client, scope creep, or an escalation.
- Interviewer accepted a textbook answer without testing whether the candidate had actually lived the situation.
- Interviewer never checked whether the candidate had researched ParallelDots / ShelfWatch or why they want this role specifically.
- Interviewer didn't probe a JD-critical skill or tool at all (Excel, data quality, specific tools mentioned in the JD).

### Step 5 — Generate the full evaluation as a downloadable PDF report

The default output for Phase 2 — for **both Round 1 and Round 2** — is a single self-contained **PDF** the user can save, share, print, or attach to an ATS. Do NOT default to inline chat output for the full evaluation — the report belongs in a downloadable PDF. Inline chat output is acceptable only if the user explicitly says "just give me the summary in chat" or similar.

Build it by writing a self-contained HTML file first, then converting it to PDF with `wkhtmltopdf` (the same engine and flags as Phase 1). Write the PDF to `/mnt/user-data/outputs/<candidate_name>_Round<1|2>_evaluation.pdf`. The report should look polished and confident — this is a document a hiring manager will read and forward. Two layouts share the same house style but differ by round.

**Common to both rounds:**
1. **Header** — candidate name, role, company, interviewer name, and round clearly labelled ("Round 1 — Interview" or "Round 2 — Case study · Final").
2. **Summary stat cards** — three cards. First card is the round outcome (Round 1: the advance/reject decision; Round 2: the final recommendation). Second: the score (Round 1: the **weighted score** with the >7.0 advance gate; Round 2: the **combined score** — the R1+R2 average — with its band). Third card (Round 1: next step in one phrase; Round 2: the two component scores, e.g. "R1 7.2 · R2 7.3"). Do NOT put the interviewer rating here.
3. **Decision hero** — a prominent, visually strong banner near the top that reads as a confident verdict: a circular score gauge showing the headline score (Round 1: the **weighted score**; Round 2: the **combined R1+R2 average score**), coloured by band, next to a large verdict headline, a one-line rationale, and a small clarifying note. Green tint for advance/hire, red tint for reject/no-hire, amber for lean calls. This is the visual centrepiece — make it clean and self-assured, not busy.
4. **Interviewer Performance** — at the very end, in its own visually separated section: interviewer score /5 with name and round, a one-line rationale naming which high-weight dimensions were and weren't covered (the score is driven by high-weight coverage), then **two** accent-bordered blocks — green "What went well" (mixing JD-critical requirements probed, behavioural moments handled well, and specific transcript moments) and red "What was missed / to improve" (important things left untested plus actionable guidance for next time). Do **not** add a third "follow-ups to carry forward" block — it duplicates the Round 1 handoff.

**Round 1 layout (order):** Header → stat cards → **Decision hero (advance if overall weighted > 7.0 OR top-four weighted ≥ 7.0; otherwise reject)**, whose note states, without spelling out both conditions, the qualifying score and that this is *not* a hire decision → Strengths & Concerns (two-column, evidence-backed) → Candidate scorecard chart (7 dimensions, an **inline-SVG horizontal bar chart**, coloured by band: red 1-3, amber 4-5, blue 6-7, green 8-10) → per-dimension justification cards (all 7) → **Handoff to Round 2** (only when advancing; omit entirely on reject) → Interviewer Performance. The Handoff section opens with the brief line, then a short, constructively-framed list of areas for the case study round to explore further — each with the precise question(s) the Round 2 interviewer should ask to close the loop. No dimension groupings, no score or priority tags, no blunt "missed" language.

**Round 2 layout (order):** Header → stat cards → **Decision hero = final recommendation, with the score gauge showing the combined (R1+R2 average) score** (its note states the combined-score band rule: Strong hire ≥ 8.0, Hire 7.0–7.9, Reject < 7.0, and that the score is the average of Round 1 and Round 2) → **Section 1: Case study performance** — open with a labelled callout showing the case study brief the candidate was given, then the overall **case study score** in its own gauge, then a **"Performance against each metric" subsection**: for **each of that case study's specific factors** (from `assets/case_studies.md` — 5 to 7 factors depending on the case), a per-metric card with a band-coloured score box (out of 10) and a **detailed 2-3 sentence justification** of how the candidate performed on that metric — what they did well and where it fell short, anchored in specifics from their deliverable and the Round 2 transcript. These are detailed justifications, not one-liners. Name the selected case study in the section heading. This scorecard is separate from the seven hiring dimensions. → **Section 2: Round 1 score — a component of the final decision** — show **only** the Round 1 weighted score, the Round 2 case study score, and their combined average, as an explicit **`(Round 1 + Round 2) ÷ 2 = combined` calc block** so the averaging is transparent. **Do not reproduce the Round 1 dimension scorecard chart here** — its full seven-dimension breakdown lives in the Round 1 report; in Round 2 it feeds the decision as a single score. → **Why this recommendation** — a short bulleted rationale (2-4 points) for the Strong hire / Hire / Reject verdict, citing the **combined score and its band**, both component scores, and — for a Hire — the **named minor reservations**, or — for a Reject — the **exact reasons**. → Interviewer Performance. Do **not** include a probation plan. Do **not** render Round 1-vs-Round 2 deltas anywhere. Omit the Handoff section in Round 2.

Render the scorecard as an **inline-SVG horizontal bar chart** (one bar per dimension, coloured by band) — **not Chart.js**. The old Chart.js-from-CDN approach is removed: the PDF renderer can't reach a CDN or run modern JS, so a canvas chart would come out blank. The SVG chart is fully self-contained and prints crisply; `report_template_example.html` (Round 1) contains a worked SVG scorecard to copy. Note the bar scorecard appears in the **Round 1 report only** — the Round 2 report does not reproduce it (it uses SVG ring gauges for the hero and case-study score instead). Wherever the seven-dimension scorecard is shown (Round 1): the **scorecard chart labels each dimension with its weight** (e.g., "Problem-solving & structured thinking (20%)"); each **per-dimension justification card shows that dimension's weight** as a small muted badge next to the score; and the **justification cards are ordered from highest weight to lowest** — Problem-solving 20% → Stakeholder 20% → Project depth 18% → Ownership 15% → Communication 12% → Domain 8% → Stability 7% — so the most heavily-weighted dimensions read first.

Build the report as a single self-contained HTML file with embedded CSS — no external stylesheets, no JS, no CDN resources (it must render fully offline). Use a warm off-white background (`#faf9f5`), system fonts, generous whitespace, and the same color palette across all sections so it feels like one cohesive document. Two constraints matter for the PDF renderer (`wkhtmltopdf`, an older WebKit engine): **use flexbox, never CSS Grid** (grid silently collapses to a single stack — the templates already use flex for the stat cards, strengths/concerns columns, dimension cards, and case-study factor grid), and **charts/gauges must be inline SVG** (as above). Keep the `@media print` block and a `@media (max-width: 640px)` block.

Convert to PDF with the same fidelity flags as Phase 1 (the defaults produce blurry 96-dpi rasterised regions):

```bash
wkhtmltopdf --enable-local-file-access --print-media-type \
  --disable-smart-shrinking --dpi 300 --image-dpi 300 --image-quality 100 -q \
  "<candidate_name>_Round<1|2>_evaluation.html" \
  "/mnt/user-data/outputs/<candidate_name>_Round<1|2>_evaluation.pdf"
```

If `wkhtmltopdf` is unavailable, fall back to another HTML→PDF path (e.g. a headless browser) or, as a last resort, ReportLab per the `pdf` skill — but keep the same sections and look.

**Use the worked templates as the reference** — `assets/report_template_example.html` is a worked **Round 1** report and `assets/report_template_round2_example.html` is a worked **Round 2** report. Both show the exact house style (decision hero with SVG score gauge, stat cards, the inline-SVG scorecard, per-dimension cards, the interviewer section) and are already PDF-safe (flex layout, inline SVG, no Chart.js). View the matching one before building so the styling stays consistent, reuse its CSS and components verbatim, and rewrite only the content. The Round 2 template additionally shows the final-recommendation hero (combined-score gauge), the Case study performance section (case-brief callout, an overall case-study score gauge, and a detailed per-metric card for each factor), and the Section 2 combined-score calc block — no read-only Round 1 scorecard, no handoff, no Round 1 deltas.

After creating the PDF, use the `present_files` tool to surface it to the user.

### Step 6 — In-chat summary

Once the file is created, write a short summary in chat (3-5 lines). In **Round 1**: the advance/reject decision and the weighted score against the >7.0 gate, the strongest and weakest dimensions, and (if advancing) the single most important thing the case study must cover. In **Round 2**: the final verdict from the **combined R1+R2 average** and its band (Strong hire ≥ 8.0 / Hire 7.0–7.9 / Reject < 7.0), the two component scores and the combined number, and — for a Hire — the named minor reservations, or — for a Reject — the exact reasons. Then point to the report. Don't repeat the report's contents in chat.

---

## A note on tone

Be honest, not sycophantic. If a candidate did poorly, say so plainly with evidence. If an interviewer missed obvious things, point them out directly — they're asking for feedback to get better. Hedging or padding the evaluation reduces its value. At the same time, ground every criticism in something specific from the transcript, not a general feeling.
