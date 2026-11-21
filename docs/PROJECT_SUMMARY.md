# Go Booster: Project Summary

**Go Booster is an AI-assisted boutique acquisition and outreach copilot for Booster.** Booster delivers online
orders from a customer's nearest London boutique within the hour, starting in Central London.

## What it does
It takes each luxury or premium boutique in W1, SW1, WC and EC through five stages: **Find → Research → Check fit →
Contact → Email**. The result is a ranked, explainable shortlist with a personalised, fact-based email ready for a
human to review and send.

## Who it helps
Booster's partnerships and business-development team: the people who need to decide which boutique to approach next
and what to say, without spending hours per brand on repetitive research.

## Why it matters to Booster
Booster's supply side grows one boutique at a time, and every partnership starts with a relevant first message to
the right channel. Go Booster aims to make that process **consistent, comparable and trustworthy**:
- Prioritise on transparent criteria rather than gut feel.
- Keep verified facts separate from assumptions, so outreach never relies on invented claims.
- Make every email specific to the boutique's own published policies (for example its current delivery terms).

*Expected benefits (less repetitive research, better prioritisation, more relevant outreach) are hypotheses.
They have not been measured.*

## What is actually implemented
- A complete, self-contained web app (`index.html`) that runs offline in Chrome or Edge, with no server or API key.
- **10 real prospects** from public research on official brand websites, with source links, public contact routes
  and Unknowns marked. **27 fictional demo records**, clearly labelled.
- An explainable 100-point scoring model with live adjustable weights, confidence and missing-data reporting.
- FACT / ASSUMPTION / UNKNOWN tagged brand intelligence.
- Personalised first email and follow-up per real prospect: copy, download, open in your own mail app.
  Nothing is sent automatically.
- Search, filters, sorting, CSV/JSON export, pipeline stages and a schematic map.

## What is demonstrated
The live demo walks one real boutique (e.g. Drake's, 9 Savile Row) through all five stages in under three minutes.
It shows the facts with sources, the score breakdown, the public contact route and the personalised email.

## Future work
Live research agent with citations; automatic re-verification of facts; a shared CRM backend with authentication;
score calibration on real outcomes; integration with Booster's email system, still with human approval; real
delivery-zone mapping.
