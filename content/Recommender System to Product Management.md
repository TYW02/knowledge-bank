---
title: Recommender System to Product Management
---
# Why use Recommender Systems ?
Brings **Values** to customer
- Find things that are more relevant
- Narrow down the set of choices
- Explore and discover more interesting spaces

Bring **Values** to providers
- Improve profit by providing relevant and accurate recommendations
- Increase customer retention
- Guide consuming behaviours

## Factors used to recommend content
User Activity: Likes, Shares, Comments
Content: Video, Audio, hashtag, effects
Auxiliary information: Gender, Country, Language
Social Information: Follower/followee, tags, linked to other accounts
Contextual Information: Location, Geographic, time


## Collaborative Filtering

"Wisdom of the crowd": Looks at ratings of like-minded users to recommend items
Analyze known preferences of groups of users to make predictions of unknown preferences for other users.

Basic Assumption:
User give ratings to a group of items
Users who had similar tastes in the past, will have similar tastes in the future.


# ML for Personalization & Insights in Banking and Finance

Recommendation: "What content should you show me and where?"
- With the goal of enabling customers to discover new products, services, and insight information, based on their profile and activity

Eligibility: "Can I have?"
- Whether a customer meets a set of criteria to receive a certain product

Suppressions: "Who can not have ?"
- Customers who cannot have

Audiences: "Which group am I in?"
- A subset of customers to which a particular communication, insights, nudge, marketing, campaign or promotion may be delivered.

Insights: "What do I do, want, or need ?"
- Help to make informed decisions about their finances


### Model Risk & Governance
Key Points
- Each governance review is unique and has subjective variations
- Model workflows often have complex and interlacing manual stages


## GenAI in the workflow
WHERE: Where to adapt LLMs, which roles that LLMs could play at different parts of the pipelines such as feature engineering, feature encoding, scoring/ranking function, pipeline controller
HOW: How to adapt LLMs, in which can be integrated into 2 phases:
	Training phase: Tune LLMs and NOT Tune LLMs (Whether to freeze parameters during training phase)
	Inference/Serving Phase: Infer with models (Whether to involve models during inference phase)


# From Product Management Perspective


## Where "Recommendations" show up in banking
"Next best action" in mobile app (Pay bill, set up alerts, start saving)
Personalized insights (Spending summaries, cash-flow forecasts, unusual activity)
Product/Content suggestions (Card features, budgeting tools, education modules)
Service routing (Which help article, chatbot path, or specialist to connect to)

## PM's Mission: Value + Trust
Goal: Improve customer outcomes and business outcomes without creating harm
Banking differs from media/e-commerce: Higher stakes, regulation, and expectations
PM work spans: Experience design, metrics, data, controls, rollout, monitoring
"Success" includes: Adoption + Satisfaction + Fewer complaints, not only clicks

## Pick a use case and define a goal
Examples:
- Help customer avoid fees / manage cash flow
- Help customers discover relevant features (alerts, savings rules)
- Help customer learn (financial education content)

Avoid vague goals like "increase engagement" without a user problem
Define user segment: Students, new-to-bank, paycheck-to-paycheck
Define the moment: Onboarding, Payday, after large purchase, after overdraft


## Guardrails
Suitability/Appropriateness: Don't recommend products/actions that are misaligned
Fairness: Avoid systematically disadvantaging protected or vulnerable groups
Transparency: "Why am I seeing this?" explanations in simple language
Privacy & Consent: Minimize sensitive data use, offer controls/opt-out where needed
Safety checks: Blocklist restricted content, escalation paths for high-risk signals


## KPI 
Examples:
- Reduced overdraft/fee incidence
- Increased successful bill payments on time
- Improved savings consistency

Input/behavior metrics: Feature adopting, completion rate, repeat usage
Trust metrics: Complaint rate, "Hide this" rate, customer satisfaction
Model proxy metrics (offline): Ranking quality as a secondary check

Some example metrics & KPI
- Management Monthly Recurring Revenue (MRR)
- Average Revenue per User (ARPU)
- Customer Lifetime Value (CLTV)
- Customer Acquisition Cost (CAC)
- Customer Retention Rate (CRR)
- Session Duration
- Number of Sessions per User
- Traffic


## Data & Instrumentation
Define events: Impression -> click -> action completed
Context captured: Channel (app/email), placement, time, device, customer state
Item catalog/taxonomy: What can be recommended
Data quality pitfalls in finance
- Delayed outcomes (Payment success later)
- Policy-driven exclusions (Eligibility rules)
- Feedback loops (Recommendation changes behavior, which changes training data)

## Roadmap
MVP (Minimum Viable Product)
- Rule-based or simple ranking + Strict eligibility filters
- A few recommendation types
- Basic tracking + manual review of content

v1:
- Personalized using behavioral/context features
- Better candidate generation (Segment-based, similarity, sequence signals)
- First experimentation framework with guardrails

Scale:
- Multi-surface consistency, real-time freshness where needed
- Automated monitoring, retraining cadence, model/version governance


## Experimentation
Hypothesis + Primary metric + Guardrails decided before launch

A/B test design considerations
- Seasonality (holiday, tuition cycle), small segments, long-term effects
- "Do no harm" thresholds (Complaints, fee increases, opt-out)

Evaluate by segment (new account vs established, student vs non-student)
Rollout plan: Limited launch -> Expand -> Rollback rules if guardrails trip

## Operating model: Who PMs partner with
Core team: PM + Design + Engineering + data + AI/ML

Plus critical partners in finance: Risk/compliance, legal, model governance, ops

Regular rituals:
- Weekly experiment/results review (including guardrails)
- Monthly quality + bias checks; quarterly model lifecycle review

Various meetings with stakeholders to hold things together.