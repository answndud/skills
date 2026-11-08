---
name: grilling
description: Pressure-test an unsettled product or design decision through an interactive interview. Use for explicit requests to uncover hidden assumptions and trade-offs.
---

# Grilling

Help the user discover the decisions that could change their design. Make a recommendation when the evidence supports one and leave consequential choices with the user.

## Before asking

- Use the conversation and relevant repository evidence to distinguish observed facts, confirmed decisions, proposed assumptions, and open choices. Check what you can verify directly before asking the user.
- Sketch the decision tree privately. Identify the outcome, the decisions that could redirect the design, and which questions depend on their answers.

## Interview

- Ask the question with the greatest downstream impact first. Ask one question when its answer determines the rest. Group independent questions when the user can answer them together.
- Pressure-test consequential assumptions with a concrete counterexample, failure scenario, or viable alternative. Explain what the answer would change. Add realistic options and a recommended default with its main trade-off when they help the user decide. Leave room for a counterproposal.
- Carry answers forward and reopen a settled decision only when new evidence reveals a material conflict. Treat an unambiguous “추천대로” as acceptance of the recommendations it refers to. Flag any material ambiguity before treating a recommendation as confirmed.
- Continue while an open choice could materially change the outcome, scope, or behavior. Mark low-impact unknowns as assumptions or defer them. Honor a request to stop or proceed and identify any unresolved decision that still blocks the requested next step.

## Close the interview

Summarize the goal, confirmed decisions and why they matter, and remaining open choices. Include a concrete success example when it clarifies the result. An interview request authorizes the interview and its summary. Switch to specification or implementation when the user requests it, using the confirmed decisions without asking for blanket reconfirmation.
