---
name: debugging
description: Investigate intermittent bugs, failures that are hard to reproduce, or bugs that persist after a fix attempt. Use a focused reproduction to distinguish plausible causes.
---

# Debugging

Identify the cause of the reported failure and show the evidence for it. Start with the smallest check that can distinguish a real failure from expected behavior.

1. Establish the expected and observed behavior and the conditions that matter. Reproduce the failure with a targeted test, minimal script, request, or trace. For intermittent failures, record the conditions and baseline failure frequency when practical.
2. Compare plausible causes by asking what observation would distinguish them. Run the cheapest discriminating check first. Change one relevant variable at a time and follow the evidence through the affected path.
3. If a fix is in scope, change the smallest surface that addresses the demonstrated cause. Remove temporary probes from the final diff and rerun the original signal and relevant regression checks. For intermittent failures, report how many attempts ran under comparable conditions and what happened.

For diagnosis-only requests, leave tracked source files unchanged. Report the cause and evidence or the leading hypotheses and next discriminating check. When the original signal cannot be reproduced or retested, state which part of the diagnosis or fix remains unverified.
