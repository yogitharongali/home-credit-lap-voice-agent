# Home Credit LAP Voice Agent

A system prompt for an AI voice agent that calls existing Home Credit customers, presents a pre-approved Loan Against Property (LAP) offer of up to Rs. 75 lakh, and runs a preliminary eligibility check before handing qualified leads to a senior loan expert.

Built for the SalesAgents AI Prompt Engineer assignment and tested on Retell AI.

## Call flow

1. Greeting and identity verification (busy customers get a callback time)
2. Offer presentation
3. Eligibility checklist (7 data points)
4. Immediate disqualification, loan-transfer routing, or amount-cap handling
5. Handoff to a senior loan expert

## Eligibility rules

| # | Data point | Eligible | Not eligible |
|---|-----------|----------|--------------|
| 1 | Property type | Residential, Commercial, Industrial | Agricultural |
| 2 | Ownership | Sole, Joint | None |
| 3 | Original documents | Available | Not available |
| 4 | Loan amount | Up to Rs. 75,00,000 | Above cap: explain limit, offer the maximum |
| 5 | Occupation and income | Salaried or Self-employed, income via Bank | Income in Cash |
| 6 | Market value | Any estimate (no minimum) | None |
| 7 | Tenure | 3 to 15 years | Below 3 or above 15 |

Special routing: an existing loan on the property or a request to reduce EMI sends the customer to a loan-transfer specialist and ends the call.

## Design approach

The prompt follows one loop on every turn: **extract, validate, update state, ask the next missing question.**

- **State tracking:** every fact the customer volunteers is captured, so no question is asked twice.
- **First-missing-question rule:** the agent always asks the earliest unanswered item.
- **Handoff gate:** handoff happens only when all 7 items are answered and every rule is met.
- **Natural speech:** handles fillers, corrections, interruptions, multiple answers in one sentence and Indian number formats.
- **No invented facts:** interest rates, fees and timelines are always deferred to the senior loan expert.

## Repository contents
