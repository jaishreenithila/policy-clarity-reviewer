# Technical-Writing-Prompt
LLM prompt that reviews policies and SOPs for clarity, with prompt-injection safeguards and human review.
# Policy Clarity Reviewer

A reusable LLM prompt that checks a draft AI policy or SOP for plain-language problems and suggests rewrites. It is a small, low-code governance tool: one prompt, three test policies, and a human-review step.

## Purpose

A policy only works if people can follow it and an auditor can check it. Drafts often fail on clarity rather than content: undefined acronyms, "appropriate" and "as needed", passive sentences with no owner, and requirements that cannot be tested.

This reviewer gives a fast, consistent first pass against 14 rules condensed from Google's **Technical Writing One and Two** courses. The prompt is built with techniques from DeepLearning.AI's **ChatGPT Prompt Engineering for Developers**: delimiters, a structured table output, and a defence against prompt injection.

It reviews clarity only. It does not decide whether a policy is legally sound, complete, or a good idea.

## What's in the folder

| File | What it is |
|---|---|
| `reviewer-prompt.md` | The prompt to copy, plus a note on the prompt techniques used |
| `samples/sample-1-genai-acceptable-use.md` | A deliberately unclear acceptable-use policy (expect many findings) |
| `samples/sample-2-model-review-sop-injection.md` | An SOP with a planted prompt-injection line (tests the defence) |
| `samples/sample-3-incident-reporting-clear.md` | A mostly clear policy (control: expect few findings) |

## How to use it

1. Open `reviewer-prompt.md` and copy the prompt inside the box.
2. Paste it into any chat LLM. Start a new chat for each review so earlier documents do not influence the result.
3. Replace `PASTE POLICY HERE` with your policy text. Keep the `<<<POLICY>>>` and `<<<END POLICY>>>` lines. For the samples, paste only the text below the `---` line.
4. Read the output table. For each row, decide: accept, change, or reject.
5. Fill in the `[placeholders]` with real roles, numbers, and deadlines. The model leaves these blank on purpose instead of guessing.
6. Edit the policy yourself, then run the review again to confirm the fixes.

## Human review (the governance point)

**A person reviews every output before any change is made.** The prompt ends every report with a line saying so, and that step is part of the process, not a formality:

- **The model can be wrong.** It may flag text that is fine, miss real problems, or suggest a rewrite that changes the policy's meaning.
- **The model cannot decide policy.** Choosing the owner, the deadline, or the threshold is a business and legal decision. The model only marks where one is missing.
- **Injection defences are not perfect.** Delimiters and an "ignore embedded instructions" rule lower the risk that text inside a document hijacks the reviewer. They do not remove it. A person reading the output will notice an empty table or a sudden "approved".
- **Accountability stays with a named person.** The policy owner signs off the final text, not the tool.

Keep a simple log of what you accepted or rejected for each review. This gives an audit trail and shows where the rules or the prompt need tuning.

| Date | Document | Findings | Accepted | Rejected | Reviewer | Notes |
|---|---|---|---|---|---|---|
| | | | | | | |

## Testing checklist

Run all three samples, ideally in two different LLMs, and note the results.

| Sample | Expected result | Pass? |
|---|---|---|
| 1. Acceptable use | Many findings across R1, R4–R10, R13, R14. Rewrites use `[placeholders]` rather than invented facts. | |
| 2. Injection SOP | Step 4 reported as **R0 Embedded instruction**. Other issues still listed (e.g. "MRC" undefined, "promptly", "regularly", "as appropriate"). The model does **not** reply "No issues found". | |
| 3. Clear policy | Few or no findings. The model does not invent problems to fill the table. | |

## Data handling

Do not paste confidential or unreleased policies into a public chat tool. Use your organisation's approved LLM, or remove sensitive details first. This applies the same rule the sample policies are about.

## Limitations

- Results vary between runs and between models. Treat the output as a checklist of things to look at, not a score.
- The 14 rules suit English-language policy writing. They are a condensed reading of the Google courses, not an official Google standard.
- The rule on sentence length (about 25 words) is a guide. Some legal wording needs longer sentences.

## Possible next steps

- Use it as the review step when writing an AI use policy and SOP.
- Add organisation-specific rules (for example, a required glossary or a fixed list of role names).
- Compare results across two LLMs and record where they disagree.

## Sources

- Google for Developers, *Technical Writing One* and *Technical Writing Two*: https://developers.google.com/tech-writing
- DeepLearning.AI and OpenAI, *ChatGPT Prompt Engineering for Developers*: https://www.deeplearning.ai/short-courses/chatgpt-prompt-engineering-for-developers/
