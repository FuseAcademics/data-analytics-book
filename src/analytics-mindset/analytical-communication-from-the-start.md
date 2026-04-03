# Analytical Communication from the Start

Analytical work does not begin with code, queries, or charts. It begins with communication. Before an analyst touches data, they need a clear understanding of the business problem, the decision at stake, the audience, the timeline, and the format of the final output.

Strong analysts communicate early, not just at the end. They reduce ambiguity, prevent wasted effort, and align stakeholders before the analysis becomes expensive to change. In practice, many analytics failures are not caused by weak technical work, but by poorly framed requests, mismatched expectations, or unclear deliverables.

This chapter focuses on how to communicate analytically from the start of a project: writing problem statements, creating analysis briefs, setting expectations, choosing the right outputs, and avoiding common communication failures.

---

## Why communication starts before analysis

Many requests arrive in vague form:

* “Can you look into churn?”
* “We need a dashboard for sales.”
* “Why are conversions down?”
* “Can you analyze customer behavior?”

These are not yet analysis plans. They are starting points. If an analyst accepts them at face value, several problems often follow:

* the wrong question gets answered
* the analysis becomes too broad
* stakeholders expect a result the data cannot support
* time is spent building outputs nobody uses
* the final work is technically correct but operationally irrelevant

Early communication solves this by turning informal requests into shared understanding.

Good early communication helps answer questions such as:

* What decision will this analysis support?
* Who is the primary audience?
* What exactly is in scope and out of scope?
* What level of confidence or rigor is needed?
* What constraints exist around time, data, tools, or privacy?
* What form should the result take?

The goal is not to create bureaucracy. The goal is to reduce rework and increase relevance.

---

## Writing problem statements

A problem statement is a concise description of what needs to be understood or decided. It should be specific enough to guide analysis, but broad enough to allow investigation.

A weak problem statement usually describes a topic. A strong problem statement describes a decision context.

### Weak problem statements

* Analyze customer churn.
* Build a retention report.
* Investigate website traffic.
* Review pricing performance.

These are vague because they do not clarify why the work matters, what question is being answered, or what action may follow.

### Strong problem statements

* Identify the main drivers of increased customer churn among first-year subscribers in the last two quarters, so the retention team can prioritize interventions for the next renewal cycle.
* Determine whether the recent drop in website conversion rate is concentrated in specific traffic sources, devices, or landing pages, in order to guide immediate optimization work.
* Evaluate whether the current discounting strategy improves total gross profit or only increases low-margin sales, to support pricing decisions for next quarter.

These statements are better because they include:

* the business issue
* the relevant population or time period
* the intended decision or action
* the reason the analysis matters

### A practical structure for problem statements

A useful template is:

**We need to understand `[issue or question]` for `[segment/process/time period]` so that `[stakeholder/team]` can `[decision or action]`.**

Examples:

* We need to understand why repeat purchase rates declined among new customers acquired through paid social in Q1 so that the growth team can decide whether to adjust acquisition targeting.
* We need to understand whether support ticket backlog is driven by volume growth, staffing gaps, or process delays so that operations can allocate resources appropriately.

### What a problem statement should include

A good problem statement usually clarifies:

* **Business context**: What is happening?
* **Analytical focus**: What needs to be measured, compared, explained, or predicted?
* **Scope**: Which business unit, product, market, customer segment, or time period?
* **Decision relevance**: What will someone do with the answer?

### What to avoid

Avoid problem statements that are:

* **solution-first**: “Build a dashboard” instead of clarifying the need
* **metric-only**: “Track DAU” without saying why
* **too broad**: “Analyze all customer behavior”
* **causal without basis**: “Prove the campaign caused growth” when the data only supports descriptive analysis

A problem statement should not promise more than the analysis can realistically deliver.

---

## Creating analysis briefs

An analysis brief is a short working document that aligns analyst and stakeholder before the work proceeds too far. It does not need to be long. In many cases, one page is enough. What matters is that it captures the key assumptions and reduces ambiguity.

Think of the analysis brief as the operational version of the problem statement.

### Purpose of an analysis brief

An analysis brief helps:

* confirm what question is being answered
* document scope and constraints
* define success
* identify required inputs and dependencies
* establish timelines and deliverables
* create a shared reference point if confusion arises later

It is especially useful when:

* multiple stakeholders are involved
* the request is high-impact or politically sensitive
* the work may take more than a few hours
* data access or definitions are uncertain
* the output will be widely distributed

### Core elements of an analysis brief

A practical analysis brief often includes the following sections.

#### 1. Background

Briefly describe the business context.

Example:

> Conversion rate declined by 12% month over month after the new onboarding flow was launched. Product leadership wants to understand whether the decline is broad-based or concentrated in specific user cohorts.

#### 2. Objective

State the analytical goal clearly.

Example:

> Assess where the conversion decline occurred, quantify the magnitude by segment, and identify the most plausible contributing factors visible in available behavioral and funnel data.

#### 3. Business decision

Explain what decision the work is meant to support.

Example:

> The product team will use the results to decide whether to roll back parts of onboarding, prioritize UX fixes, or run follow-up experiments.

#### 4. Key questions

List the questions the analysis should answer.

Example:

* When did the decline begin?
* Which funnel stage changed the most?
* Is the decline concentrated by device, geography, traffic source, or user type?
* Did downstream activation metrics change as well?
* Are there instrumentation or data-quality concerns?

#### 5. Scope

Clarify what is included and excluded.

Example:

**In scope**

* New users only
* Last 90 days
* Web onboarding funnel
* Device and acquisition channel breakdowns

**Out of scope**

* Mobile app onboarding
* Long-term retention effects
* Changes outside onboarding flow

#### 6. Data sources

List expected data sources and any uncertainties.

Example:

* product event logs
* signup and activation tables
* campaign attribution data
* experiment assignment logs

Potential risks:

* event naming changes during rollout
* incomplete source attribution for some sessions

#### 7. Assumptions and definitions

Capture important working definitions.

Example:

* Conversion is defined as account creation followed by successful setup completion within 24 hours.
* New user means first recorded signup.
* Traffic source uses last non-direct attribution.

#### 8. Deliverable

Specify what form the output should take.

Example:

> A short memo with charts and recommendations for the product leadership meeting on Friday.

#### 9. Timeline

State key dates.

Example:

* Initial readout: Wednesday afternoon
* Final deliverable: Friday 10:00 AM
* Stakeholder review: Thursday end of day

#### 10. Success criteria

Explain what a useful result looks like.

Example:

> Stakeholders should leave with a clear understanding of where the decline occurred, what likely caused it, what remains uncertain, and what next action is recommended.

---

## Example analysis brief

Below is a compact example of what an analysis brief may look like.

## Analysis Brief: Subscription Churn Review

**Background**
Monthly churn increased from 3.8% to 5.1% over the past two billing cycles, especially among annual plan customers.

**Objective**
Identify the main drivers of the churn increase and determine whether the change is associated with pricing, product engagement, service issues, or customer mix.

**Decision to support**
The retention team will use the findings to decide whether to prioritize pricing adjustments, lifecycle interventions, or support improvements.

**Key questions**

* Which customer segments account for most of the increase?
* Did churn rise uniformly or in specific cohorts?
* Did engagement decline before churn?
* Were there recent pricing, product, or service changes that align with the timing?
* Are there measurable differences between churned and retained users?

**Scope**

* Last 12 months
* Paid subscribers only
* Annual and monthly plans
* Primary markets: US, UK, Canada

**Out of scope**

* Free users
* Long-term lifetime value modeling
* Forecasting future churn

**Data sources**

* subscription billing data
* product usage logs
* customer support tickets
* NPS survey responses

**Definitions**

* Churn = subscription cancellation or non-renewal
* Active user = at least one product session in the last 30 days

**Deliverable**

* 2-page memo with exhibits
* optional appendix notebook for technical details

**Timeline**

* Draft findings by Tuesday
* Final memo by Thursday noon

**Success criteria**

* Findings identify the major sources of churn increase
* Recommendations are specific and operationally actionable
* Uncertainties and limitations are explicitly stated

---

## Defining stakeholder expectations

Stakeholder expectation management is one of the most important analyst skills. It is also one of the most underdeveloped. Analysts often assume that if they produce careful work, the rest will take care of itself. In reality, many projects fail because expectations were never aligned.

Expectation-setting means making explicit what the analysis will do, what it will not do, how long it will take, how definitive it can be, and what form it will take.

### Expectations to define early

#### 1. The question being answered

Different stakeholders may believe they asked the same question when they did not.

For example:

* one stakeholder wants a root-cause analysis
* another wants a performance summary
* another wants a recommendation for action

These are related but distinct tasks. Clarify which one is primary.

#### 2. The level of rigor required

Not every project requires the same standard of evidence.

Examples:

* A same-day business readout may tolerate directional analysis.
* A pricing decision affecting revenue may require more robust validation.
* A board-facing report may need careful definition review and reconciliation.

Say explicitly whether the result will be:

* exploratory
* directional
* production-grade
* decision-critical

#### 3. The timeline

Stakeholders often ask for fast answers without recognizing the tradeoffs. Analysts should state what is feasible within the requested timeframe.

A useful framing is:

* what can be delivered quickly
* what deeper work would require more time
* what assumptions are being made to move fast

#### 4. Data limitations

Stakeholders may assume the data exists, is clean, and measures exactly what they care about. Often it does not.

Set expectations around:

* missing data
* lagged data
* inconsistent definitions
* instrumentation gaps
* limited history
* inability to infer causality

Do this early, not as a surprise at the end.

#### 5. What “done” looks like

Completion should be defined jointly.

Examples:

* a dashboard with agreed metrics and filters
* a memo with findings and recommendation
* a slide deck for executive review
* a notebook for peer analysts
* a one-time answer to a narrow question

Without a clear definition of done, scope creep is almost guaranteed.

### Useful expectation-setting language

Analysts often benefit from using direct, disciplined language such as:

* “This analysis can quantify the pattern, but not definitively prove cause.”
* “We can provide a directional answer by tomorrow, with a more robust cut next week.”
* “The current data supports channel-level breakdowns, but not reliable customer-level attribution.”
* “To keep this scoped, I will focus on the top three drivers rather than every contributing factor.”
* “The output will be a decision memo, not a monitoring dashboard.”

This kind of language protects quality while remaining collaborative.

---

## Choosing outputs: dashboard, memo, presentation, notebook, report

A common communication mistake is choosing the output before understanding the use case. Different outputs serve different purposes. The best analysts select formats based on audience, decision context, frequency of use, and required depth.

The question is not “What can I build?” but “What does this audience need to act?”

---

## Dashboard

A dashboard is best for ongoing monitoring, repeated reference, and metric visibility across time.

### Best used when

* stakeholders need recurring access to the same metrics
* the goal is monitoring, not deep explanation
* users want to self-serve simple slicing and filtering
* the business process depends on routine tracking

### Strengths

* scalable for repeated use
* good for trend monitoring
* useful across teams
* supports operational visibility

### Limitations

* weak for nuance, context, and recommendations
* often encourages passive observation instead of action
* can become cluttered if used to answer every question
* not ideal for one-time root-cause investigations

### Use a dashboard when

* the metrics are stable
* the audience needs frequent access
* the main need is visibility

### Avoid relying on a dashboard when

* the real need is interpretation
* the issue is novel or ambiguous
* the audience needs a clear recommendation more than self-service charts

---

## Memo

A memo is often the most effective format for analytical communication because it forces clarity. It is good for explaining findings, tradeoffs, implications, and recommendations.

### Best used when

* the analysis supports a decision
* context and reasoning matter
* the audience needs interpretation, not just charts
* the output is relatively short and focused

### Strengths

* encourages structured thinking
* makes assumptions explicit
* supports recommendations
* easier to read asynchronously than a slide deck

### Limitations

* less suited for live presentations
* not ideal for recurring monitoring
* requires stronger writing discipline

### Use a memo when

* you need to answer “What happened, why, what matters, and what should we do?”

For many business analyses, a memo is the best primary output.

---

## Presentation

A presentation is appropriate when the analysis will be discussed live, especially with executive or cross-functional audiences.

### Best used when

* the findings need verbal walkthrough
* stakeholder alignment is needed in a meeting
* the audience is senior and time-constrained
* persuasion and sequencing matter

### Strengths

* effective for storytelling in meetings
* supports emphasis and framing
* can focus attention on key messages

### Limitations

* often oversimplifies technical detail
* can hide assumptions unless carefully designed
* usually requires accompanying notes or appendix for rigor

### Use a presentation when

* the primary communication moment is a meeting
* the audience needs a curated narrative

A strong presentation usually pairs well with a backup appendix or memo.

---

## Notebook

A notebook is useful for technical transparency, reproducibility, and analyst-to-analyst collaboration.

### Best used when

* the audience is technical
* the analysis may need replication or extension
* code, logic, and intermediate steps matter
* the notebook is part of an exploratory or research workflow

### Strengths

* transparent and reproducible
* combines code, output, and commentary
* useful for peer review

### Limitations

* poorly suited for non-technical stakeholders
* easy to confuse detail with communication
* often too raw to serve as the main business deliverable

### Use a notebook when

* you need a working analytical artifact
* the audience cares about method and traceability

A notebook is often a supporting artifact, not the final communication product.

---

## Report

A report is a more formal document, often longer and more comprehensive than a memo.

### Best used when

* the work requires detailed documentation
* the analysis must serve as a reference
* multiple sections, methods, and appendices are needed
* the audience includes audit, compliance, research, or formal governance groups

### Strengths

* thorough and durable
* suitable for archival use
* can include methodology, caveats, and detail

### Limitations

* time-consuming to produce
* often under-read
* can become verbose if not carefully structured

### Use a report when

* completeness and formality matter more than speed

---

## Choosing the right output

A simple way to choose is to ask:

### Who is the audience?

* executives may prefer memo or presentation
* operators may prefer dashboard
* analysts may prefer notebook plus memo
* governance teams may prefer report

### Is this recurring or one-time?

* recurring need: dashboard
* one-time decision: memo or presentation
* technical handoff: notebook
* formal documentation: report

### Is the main need monitoring or explanation?

* monitoring: dashboard
* explanation: memo or report
* persuasion in meeting: presentation
* reproducibility: notebook

### Does the audience need recommendation or exploration?

* recommendation: memo or presentation
* exploration and method: notebook
* broad reference and detail: report

In many real projects, the right answer is a combination:

* dashboard for monitoring + memo for interpretation
* presentation for meeting + appendix notebook for technical depth
* report for archive + executive summary memo for decision-makers

The key is intentionality.

---

## Common communication failures

Analytics communication often breaks down in familiar ways. Recognizing these patterns helps prevent them.

### 1. Accepting vague requests without clarification

When analysts start too quickly, they often answer the wrong question efficiently.

Example:
A stakeholder asks for a dashboard, but actually needs a one-time decision memo about a recent drop in performance.

**Fix:** clarify the decision, audience, and use case before committing to format.

---

### 2. Confusing the request with the need

Stakeholders often describe a desired output, not the underlying problem.

Example:
“Can you build a dashboard for cancellations?” may really mean:
“We are worried churn is increasing and need to know why.”

**Fix:** ask what action the stakeholder wants to take after seeing the output.

---

### 3. Failing to define terms

Words like active user, conversion, retention, churn, qualified lead, and revenue often have multiple meanings.

**Fix:** document working definitions early and repeat them in the final deliverable.

---

### 4. Overpromising certainty

Analysts sometimes imply that data can establish definitive cause when it only shows association or pattern.

**Fix:** be precise about what the analysis can and cannot support.

Examples:

* “This coincides with the rollout, but does not prove the rollout caused the decline.”
* “This model predicts risk, but it does not explain all underlying causes.”

---

### 5. Choosing the wrong deliverable

A sophisticated dashboard may be built when stakeholders needed three clear recommendations. A long report may be written when a short presentation would have sufficed.

**Fix:** choose the output based on use, not preference.

---

### 6. Mixing exploration with final communication

Exploratory analysis is messy by nature. Final communication should not be. Dumping raw notebook output or every explored chart into a stakeholder readout creates noise.

**Fix:** separate working analysis from decision communication. Curate the final output.

---

### 7. Hiding limitations until the end

Waiting until the final presentation to mention missing data, broken instrumentation, or definition uncertainty damages trust.

**Fix:** surface limitations early and update stakeholders as new constraints are discovered.

---

### 8. Letting scope expand silently

An initial question about churn becomes churn plus retention plus pricing plus onboarding plus forecasting.

**Fix:** restate scope explicitly when new requests appear. Distinguish between current scope and future work.

---

### 9. Reporting numbers without interpretation

Stakeholders rarely need numbers alone. They need meaning.

Bad communication:

* “Conversion is down 8%.”

Better communication:

* “Conversion is down 8%, mostly from mobile paid traffic after the landing page change, which suggests the issue is concentrated rather than site-wide.”

**Fix:** connect results to context, implications, and action.

---

### 10. Ignoring audience sophistication

The same content cannot be delivered identically to executives, operators, data scientists, and finance partners.

**Fix:** adapt depth, terminology, and emphasis to the audience.

---

## Practical workflow for early analytical communication

A disciplined early communication workflow often looks like this:

### Step 1: Restate the request in business terms

Translate the initial request into a provisional problem statement.

Example:

> You want to understand whether the recent conversion decline is broad-based or concentrated in specific parts of the funnel, so the product team can decide what to fix first.

### Step 2: Clarify the decision

Ask internally: what decision depends on this?

Even if you do not ask the stakeholder directly, your work should infer and surface the decision context.

### Step 3: Draft a brief

Write a short brief with objective, scope, key questions, assumptions, data sources, deliverable, and timeline.

### Step 4: Align on output

Do not default to a dashboard. Choose the format that matches the use case.

### Step 5: Surface constraints early

Flag missing data, ambiguous definitions, or timeline tradeoffs before deep work begins.

### Step 6: Reconfirm before final delivery

Before polishing the final output, verify that the analysis still matches stakeholder need. Sometimes the question shifts as new information emerges.

---

## A reusable template

Below is a lightweight template that can be adapted for many analysis requests.

## Analysis Setup Template

**Problem statement**
What business issue or decision is this analysis intended to support?

**Objective**
What specifically should the analysis determine, quantify, compare, explain, or predict?

**Primary audience**
Who will use the result?

**Decision to support**
What action will be taken based on the findings?

**Key questions**

* Question 1
* Question 2
* Question 3

**Scope**

* Included:
* Excluded:

**Definitions and assumptions**

* Definition 1
* Definition 2
* Assumption 1

**Data sources**

* Source 1
* Source 2
* Known risks or limitations

**Deliverable**

* dashboard, memo, presentation, notebook, report, or combination

**Timeline**

* draft date
* final date

**Success criteria**

* What does a useful outcome look like?

---

## Key takeaways

Analytical communication begins before analysis begins. The most effective analysts do not wait until the final presentation to communicate. They frame the problem, align expectations, define scope, select the right deliverable, and surface risks early.

A few principles matter most:

* write problem statements around decisions, not just topics
* use short analysis briefs to create alignment
* define expectations about scope, rigor, timeline, and limitations
* choose outputs based on audience and use case
* prevent common communication failures through explicit, early clarification

Technical skill makes analysis possible. Communication makes it useful.

---

## Practice prompts

1. Rewrite the following vague request as a strong problem statement:
   “Can you analyze customer retention?”

2. Draft a one-page analysis brief for this request:
   “We saw a sales drop after the pricing change. Leadership wants an answer by Friday.”

3. For each scenario below, choose the best output and explain why:

   * weekly operational KPI review
   * one-time root cause analysis for executive decision
   * technical handoff to another analyst
   * formal documentation for audit purposes

4. List three examples of communication failures you have seen or can imagine in analytics projects, and describe how to prevent them.

5. Take a recent business question and separate:

   * the stakeholder’s request
   * the actual need
   * the decision to support
   * the best final deliverable
