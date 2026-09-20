Get all the free resources of this video here below 👇

Eight prompting rules for the Claude 5 models, and the giveaway that goes with each one: templates, prompts, and two Claude skills. Every one is built straight from Anthropic's published guidance, with the source linked so you can check it yourself.

Templates and prompts: copy the block and paste it where you work. Skills: download the zip and drop the folder into `~/.claude/skills/`, or upload it to Claude under Settings → Capabilities. Then it just works.

## 1. Give it the whole job 📦

Stop feeding Claude step 1, then step 2, then step 3. Describe the job, the guardrails, and what done looks like, then let it run. The Claude 5 models are trained to take the full task and work it end to end.

### The Full Job Brief (Template)

One prompt that hands Claude the whole job. Four blanks: the job, the why, the guardrails, and what done means. Fill the brackets, delete what a given task does not need.

```
THE JOB
[What you want done, as an outcome, not as steps. One or two sentences.]

THE WHY
I'm working on [the larger task] for [who it's for]. They need [what the output enables].

THE GUARDRAILS
- Only touch [the scope]. Leave everything else alone.
- [Anything that must not change, be sent, or be deleted.]
- Make routine judgment calls yourself. Ask me only if the answer would change the whole result.

DONE MEANS
- [How we both know it's finished: the exit criteria.]
- Keep the deliverable to [size: sections, word count, or "as short as covers the substance"].
- When you finish, tell me where the result is and give me [3] short bullets on what you did. Nothing more.
```

- See a filled example
    
    ```
    THE JOB
    Update our monthly client report for August with the latest numbers and one clear recommendation.
    
    THE WHY
    I'm running the [client name] account for our agency. The client's CEO reads this to decide next month's budget, so it has to be skimmable and decision-ready.
    
    THE GUARDRAILS
    - Only update the August report file. Leave the rest of the client folder alone.
    - Keep the existing structure and branding exactly as they are.
    - Make routine judgment calls yourself. Ask me only if the numbers look wrong at the source.
    
    DONE MEANS
    - Every number traces to the analytics export in the data folder.
    - Under 300 words across the same 5 sections as July.
    - When you finish, tell me where the file is and give me 3 short bullets on what changed. Nothing more.
    ```
    
- Why each part is there
    - **The job as an outcome:** the Opus 5 guide says the model "performs best when given the complete task specification up front and left to run."
    - **The why:** the Fable 5 guide's own template. Models perform better when they understand intent.
    - **The guardrails and done-means caps:** the Opus 5 guide's task scope and verbosity guidance. Cap what it touches, how big the deliverable is, and how much it reports back.
    - Sources: Opus 5 prompting guide, Fable 5 prompting guide, Boris Cherny's YC interview

## 2. Let Claude interview you 🎤

You don't know what belongs in the brief, and that's fine. Have Claude ask you one question at a time before it starts, so the missing context comes out of your head instead of getting guessed at.

### Interview Me (Skill)

Say "interview me" before any big or fuzzy task. Claude asks you 5 to 7 questions, one at a time, prioritising the ones whose answer would change the plan, then writes the brief back and runs it. Based on the interview pattern in Anthropic's Fable 5 field guide.

<aside>
📔 **Download below 👇**

interview-me.zip

</aside>

- Read the SKILL.md
    
    ```markdown
    ---
    name: interview-me
    description: Interview the user one question at a time before starting a big or fuzzy task, then write the brief and execute it. Use when the user says "interview me", "brief me", "help me brief this", "I don't know where to start", or hands over a large task with obvious gaps in the request. Based on the interview pattern Anthropic recommends in the Claude Fable 5 field guide.
    ---
    
    # Interview Me
    
    Most briefs fail because the missing context is in the user's head and nobody asked for it. This skill pulls it out before any work starts, using the pattern Anthropic recommends: interview one question at a time, prioritising the questions whose answers would change the plan.
    
    Source: A field guide to Claude Fable 5 (https://claude.com/blog/a-field-guide-to-claude-fable-finding-your-unknowns).
    
    ## Process
    
    1. **Read before you ask.** Look at whatever is already available: the folder, the files the user mentioned, recent related work. Never ask a question you could answer yourself by reading. Questions you burned on discoverable facts are questions you cannot spend on real unknowns.
    
    2. **Interview, one question at a time.** Ask 5 to 7 questions maximum, one per turn, in plain language. Prioritise questions whose answer would change the shape of the work: the audience, the decision this output feeds, what already exists, what must not change. Push past vague answers: if the user says "make it better," ask what better looks like and how you would both know it happened.
    
    3. **Cover four things by the end of the interview:**
       - What already exists and where it lives.
       - The goal: what this output enables, and for whom.
       - Which decisions the user actually cares about. Everything they do not claim is your call.
       - What proof of done looks like: how they want the result verified before they see it.
    
    4. **Run a blind spot pass.** Before writing the brief, ask yourself one final question and share the answer: what has this interview not covered that could change the outcome? Name the unknown unknowns you can see.
    
    5. **Write the brief back.** Compile everything into one master brief with these parts: the job, the why (who it is for and what it enables), the guardrails (scope, what not to touch), and done-means (exit criteria, deliverable size, how to report back). Show it to the user.
    
    6. **On approval, execute the brief.** Check in only at decisions the user claimed in step 3.
    
    ## Rules
    
    - One question per turn. A wall of seven questions defeats the purpose.
    - Stop at 7 questions even if curiosity remains. Make reasonable calls on the small stuff yourself.
    - If the user starts rambling, let them. Reconstruct the ramble into answers and only ask about what it did not cover.
    - If the task is small and clear, say so and skip the interview. This skill is for work where a wrong start is expensive.
    ```
    

## 3. Say why, not just what 🎯

Claude 5 performs better when it knows the intent behind the ask. One sentence of context, who it's for and what it enables, beats a paragraph of instructions.

### The Why Sentence (Template)

Copied straight from Anthropic's Fable 5 docs. Put it at the top of any prompt, or keep it as THE WHY inside the Full Job Brief above.

```
I'm working on [the larger task] for [who it's for]. They need [what the output enables].
```

## 4. Stop telling it to double-check 🗑️

Claude 5 already verifies its own work. Every "check this twice" and "verify before responding" line you carried over from old prompts now makes it re-verify, which costs tokens and time and adds nothing.

### The Retired Instructions Checklist

Twelve lines to delete from your prompts, CLAUDE.md files, and skills today. Each one cites the Anthropic doc that retires it.

1. **"Double-check your answer" / "re-verify before responding."** Claude 5 verifies its own work; these lines compound with that behavior and add cost without improving results. (Opus 5 guide, self-correction section)
2. **"Include a final verification step for any non-trivial task" / "use a subagent to verify."** Quoted verbatim in the docs as instructions to remove: they cause over-verification. (Opus 5 guide, task scope section)
3. **"Think step by step."** Claude 5 models think adaptively on their own; manual chain-of-thought prompting is a fallback for older models, not a boost for these. (Best practices, thinking section)
4. **"CRITICAL: You MUST use [tool] when..."** The docs' own example of language to dial back: aggressive emphasis written for models that undertriggered now causes overtriggering. Replace with "Use [tool] when..." (Best practices, tool usage section)
5. **"If in doubt, use [tool]."** Named in the docs as an instruction that now causes overtriggering. (Best practices, overthinking section)
6. **"Only report high-severity issues" / "be conservative" in review prompts.** The model follows it literally and reports less. Ask for everything and filter afterwards instead. (Opus 5 guide, code review bullet)
7. **Bare "do not" formatting rules, like "do not use markdown."** Tell it what to do instead: "write in smoothly flowing prose paragraphs." (Best practices, format control section)
8. **Prefill hacks, like starting the assistant's answer with "Here is the summary:".** Prefills are unsupported on Claude 4.6 and later; use direct instructions or structured outputs. (Best practices, prefill migration section)
9. **Defensive patches written for an old model's mistakes, like "never state plan details, point users to the URL."** Newer models overfit to these and withhold information they actually have. If you cannot remember why a patch exists, it is a candidate. (Prompting Playbook workshop, and the context engineering post's core argument)
10. **"Do not think" / "do not reason" rules.** On Opus 5 these increase the chance of internal tags leaking into visible output. (Opus 5 guide, thinking-disabled section)
11. **"Explain your reasoning" as a standing line, on Fable 5 specifically.** Can trigger the reasoning_extraction refusal and silently reroute the request to Opus 4.8. Ask reasoning questions ad hoc instead. (Fable 5 guide, scaffolding section)
12. **Step-by-step task scripts: "first do 1, then 2, then 3, then 4."** Describe the task, the guardrails, and the exit criteria, then let it work. Over-specifying the path is, per Boris Cherny, the most common failure mode among experienced users. (YC interview: https://www.youtube.com/watch?v=qyPCVqFUyDo)
- Keep these
    
    Not everything is retired. Keep: project gotchas the model cannot discover on its own, hard rules where being wrong is expensive (deletes, sends, money, client-facing surfaces), a one-line role, XML-style tags to separate sections, and 3 to 5 examples when output format matters. These are all still recommended in the current best practices docs.
    
- Sources
    - Opus 5 guide
    - Fable 5 guide
    - Prompting best practices
    - The new rules of context engineering

## 5. Swap rules for reasons 🔁

Hard rules backfire on smart models. Tell Claude why the rule exists and it generalises. Give it a bare "never do X" and it either ignores it or overfits and breaks something else.

### Rule Rewriter (Skill)

Say "rewrite my rules" or "audit my CLAUDE.md". It inventories every instruction line, sorts it into retired, one-sided, bare prohibition, aggressive, obvious, or keep, then rewrites each into judgment plus the reason, or flags it for deletion. Shows you the review table before it touches anything.

<aside>
📔 **Download below 👇**

rule-rewriter.zip

</aside>

- Read the SKILL.md
    
    ```markdown
    ---
    name: rule-rewriter
    description: Audit a CLAUDE.md or skill file for rules written for older Claude models and rewrite them for the Claude 5 generation. Finds one-sided rules, bare prohibitions, retired instructions, and aggressive language, then rewrites each into judgment plus the reason, or flags it for deletion. Use when the user says "rewrite my rules", "audit my CLAUDE.md", "fix my claude md", "rule rewriter", "my skills feel too strict", or after upgrading to a Claude 5 model.
    ---
    
    # Rule Rewriter
    
    Claude 5 models follow judgment better than they follow rules. A bare "never do X" gets ignored or overfitted; "X breaks because [reason], so avoid it" generalizes. This skill audits an instruction file and rewrites it accordingly.
    
    Grounded in Anthropic's published guidance:
    - Rules to judgment: https://claude.com/blog/the-new-rules-of-context-engineering-for-claude-5-generation-models
    - Give the why: https://platform.claude.com/docs/en/build-with-claude/prompt-engineering/claude-prompting-best-practices
    - Remove verification instructions: https://platform.claude.com/docs/en/build-with-claude/prompt-engineering/prompting-claude-opus-5
    
    ## Process
    
    1. **Locate the target.** Default to the CLAUDE.md in the current working folder. If the user names a skill or another file, use that. If nothing is found, ask for the path and stop.
    
    2. **Inventory every instruction line.** Classify each into exactly one bucket:
       - **RETIRED**: instructions the model now does by itself. Delete candidates. Examples: "double-check your work", "verify before responding", "think step by step", "be thorough", "always re-read the file", "you are an expert...".
       - **ONE-SIDED**: rules that state a cost or a command without the counterweight, so the model overfits. Rewrite with both sides.
       - **BARE PROHIBITION**: "never / always / do not" lines with no reason. Rewrite as judgment plus the why.
       - **AGGRESSIVE**: "CRITICAL", "YOU MUST", all-caps emphasis written to fix undertriggering on old models. Soften to normal language; Claude 5 overtriggers on these.
       - **OBVIOUS**: anything the model can see by listing the file system or reading the repo. Delete candidates.
       - **KEEP AS HARD RULE**: places where being wrong is expensive. Safety, destructive or irreversible actions, client-facing sends, money, permissions. Do not soften these; a hard rule is correct here.
       - **KEEP AS GOTCHA**: non-obvious project facts the model cannot discover on its own. These are the most valuable lines in the file; leave them alone.
    
    3. **Rewrite.** For every RETIRED, ONE-SIDED, BARE PROHIBITION, AGGRESSIVE, and OBVIOUS line, produce the replacement (or deletion) using the patterns below.
    
    4. **Present before touching anything.** Output a three-column review: original line, proposed line (or DELETE), one-line reason with its bucket. End with the counts per bucket and the estimated line reduction. Apply changes only after the user approves, then edit the file.
    
    5. **Suggest the follow-up.** After applying, remind the user that `claude doctor` right-sizes overall CLAUDE.md and skill length, which this skill deliberately does not do.
    
    ## Rewrite patterns
    
    **Bare prohibition to judgment plus why** (Anthropic's own example):
    - Before: `NEVER use ellipses`
    - After: `Your response is read aloud by a text-to-speech engine, so never use ellipses since it cannot pronounce them.`
    
    **One-sided rule to both sides** (Anthropic's escalation example):
    - Before: `Avoid escalating to a specialist, it costs $8 per case.`
    - After: `Escalating costs $8, but a wrong answer costs a refund and the customer's trust. Escalate when you are not confident.`
    
    **Retired instruction to deletion**:
    - Before: `Before finishing, double-check every file you changed and verify your work.`
    - After: DELETE. Claude 5 verifies its own work; this line causes over-verification and wastes tokens.
    
    **Aggressive to normal**:
    - Before: `CRITICAL: You MUST use the search tool when the user asks about the codebase.`
    - After: `Use the search tool when the user asks about the codebase.`
    
    ## Rules for this skill itself
    
    - Never rewrite a line in the KEEP buckets to seem productive. Fewer, correct changes beat many cosmetic ones.
    - Preserve the file's voice and formatting conventions.
    - When unsure which bucket a line belongs to, put it in the review table with a question mark and let the user decide. Do not guess on safety-relevant lines.
    - This skill changes rule quality, not file structure. For a CLAUDE.md that is too long, route sections into folder-level instruction files instead (see the companion optimization framework).
    ```
    

## 6. Tell it where the job ends 🚧

Cap three things in every brief: what it may touch, how big the deliverable is, and how much it reports back. Otherwise a capable model keeps going.

### The Done Means Block (Template)

The exit-criteria half of the Full Job Brief, on its own so you can bolt it onto any prompt.

```
DONE MEANS
- [How we both know it's finished: the exit criteria.]
- Only touch [the scope]. Leave everything else alone.
- Keep the deliverable to [size: sections, word count, or "as short as covers the substance"].
- When you finish, tell me where the result is and give me [3] short bullets on what you did. Nothing more.
```

## 7. Make it prove it 🧾

Claude should show receipts, not claim progress. One instruction makes it audit every status line against something it actually did.

### Anthropic's Audit Prompt

Anthropic's own instruction, copied verbatim from the Fable 5 prompting guide. In their testing it "nearly eliminated fabricated status reports even on tasks designed to elicit them." We did not improve it. Do not improve it.

```
Before reporting progress, audit each claim against a tool result from this session. Only report work you can point to evidence for; if something is not yet verified, say so explicitly. Report outcomes faithfully: if tests fail, say so with the output; if a step was skipped, say that; when something is done and verified, state it plainly without hedging.
```

- Where to use it
    - Any task that runs longer than a few minutes.
    - Anything you will not review line by line yourself.
    - Inside skills that produce deliverables, so "done" always arrives with receipts.

## 8. Fix the voice once 🔧

Stop rewriting jargon-dense answers by hand. Set the voice once in the place Claude reads on every chat.

### The Plain English Voice Block

One block of text that stops the jargon essays. Assembled from Anthropic's own published instruction texts and tuned for business work. Paste it once in the home that matches how you use Claude.

```
Communicate in plain English.

Lead with the answer: your first sentence should tell me what happened or what you found. Supporting detail comes after, for when I want it.

Keep responses focused, brief, and concise. Keep disclaimers and caveats short, and spend most of the response on the main answer. When asked to explain something, give a high-level summary unless I specifically ask for depth.

Use the simplest everyday words that carry the idea. If a technical term is genuinely needed, define it in a few words the first time it appears. State each fact once.

Match the length of written documents to what the task needs: cover the substance, but do not pad with filler sections, redundant summaries, or boilerplate.
```

- Where to put it
    - **Claude Cowork (recommended): project instructions.** Open your project, paste the block into the project's instructions. Every chat in that project inherits it.
    - **Claude app, everywhere: Instructions for Claude.** Settings, then your profile's Instructions for Claude. Applies account-wide to every new chat.
    - **Claude Code: an output style.** Ask Claude Code: "Create an output style from the following text and switch to it," then paste the block. Docs: output styles
    - **On-demand companion: the /eli5 skill.** For a single confusing answer, Anthropic's team uses /eli5, which re-explains a topic as a visual one-pager. Free on the community plugin marketplace.
- Sources
    - "Keep responses focused, brief, and concise..." is the conciseness instruction in the Opus 5 guide.
    - "Lead with the outcome..." is the brevity instruction in the Fable 5 guide.
    - "Match the length of written documents to what the task needs..." is the deliverable-length instruction in the Opus 5 guide (same page).

## Bonus: Prompt Master, all 8 rules in one skill 🧠

Everything above, as a single skill you run instead of remembering the rules. It starts by interviewing you one question at a time, then writes a new prompt, rewrites an old one, or audits a whole CLAUDE.md or skill file. It strips the retired instructions, rebuilds the ask as a Full Job Brief, swaps bare rules for reasons, caps scope and report-back, and adds Anthropic's audit line on long runs. Every change it makes comes with the Anthropic source it is based on.

### Prompt Master (Skill)

Say "prompt master", "write me a prompt", "fix this prompt", or "audit my CLAUDE.md". It asks up to 7 questions, plays the brief back, then hands you one copyable prompt plus a five-line change log with sources. The other seven giveaways live inside it as reference files, so this one download replaces the lot.

<aside>
💡 **Download below 👇**

prompt-master.zip

</aside>

- Read the SKILL.md
    
    ```markdown
    ---
    name: prompt-master
    description: The one skill for prompting the Claude 5 models the way Anthropic says to. Starts by interviewing the user one question at a time, then writes a new prompt, rewrites an old one, or audits a whole CLAUDE.md, skill or project-instruction file, applying the rules from Anthropic's Opus 5 guide, Fable 5 guide, best practices page and context engineering post. Strips retired instructions, rebuilds the ask as a Full Job Brief (job, why, guardrails, done-means), swaps bare rules for reasons, caps scope, length and report-back, and adds Anthropic's audit line on long runs. Use when the user says "prompt master", "write me a prompt", "fix this prompt", "upgrade my prompt for Claude 5", "audit my CLAUDE.md", "rewrite my rules", "my skill feels too strict", "brief this for me", "help me brief this", "I don't know where to start", or pastes any prompt and asks why Claude over-does or under-does the task.
    ---
    
    # Prompt Master
    
    Turns what the user wants into a prompt, brief or instruction file written the way Anthropic says to prompt the Claude 5 generation. Always begins by asking. The rulebook with sources is `references/rulebook.md`; read it once per session, then work from the steps.
    
    ## Steps
    
    Track progress:
    
    ```
    Task Progress:
    - [ ] 1. Interview
    - [ ] 2. Strip what is retired
    - [ ] 3. Rebuild as a Full Job Brief (or audit the file)
    - [ ] 4. Rules to reasons
    - [ ] 5. Deliver with receipts
    ```
    
    ### 1. Interview
    Read what the user gave you first (the pasted prompt, the file, the folder). Then interview one question at a time following `references/interview.md`: never ask what you could read, prioritise questions whose answer changes the shape of the prompt, stop at 7. Skip to a single confirming question when the ask is already small and clear. By the end you know the input type (rough idea, existing prompt, or whole instruction file), the surface (Claude Cowork, Claude app, Claude Code, API), the run length (quick answer or long run), who the output is for, and what done looks like.
    
    ### 2. Strip what is retired
    For an existing prompt or file, check every line against `references/retired-instructions.md`; remove or replace what matches and record each change for step 5. For a rough idea, skip this step.
    
    ### 3. Rebuild as a Full Job Brief, or audit the file
    - **Rough idea or existing prompt:** write it in the four-part shape from `references/job-brief.md` (job, why, guardrails, done-means). For a long run, append the audit line verbatim from that file. Drop any part the task does not need; a three-line prompt is right for a three-line task.
    - **Whole instruction file (CLAUDE.md, skill, project instructions):** run the bucket audit in `references/file-audit.md`, produce the three-column review table, and wait for approval before editing anything.
    
    ### 4. Rules to reasons
    Re-read the draft or the proposed rewrites. Any hard rule without a reason gets the reason or gets cut, using `references/rules-to-reasons.md`. Keep hard rules only where being wrong is expensive. Say what to do instead of what not to do.
    
    ### 5. Deliver with receipts
    For a prompt: one copyable block, then a change log of at most five bullets, each naming the rule applied and its Anthropic source, taken from the source column of the reference file that drove the change (`rulebook.md` for the brief, `retired-instructions.md` for removals). For a file audit: the review table, counts per bucket, and the line reduction; apply on approval. If the user wants a standing voice or format, add the one-line install note for their surface from `references/voice-and-format.md`. Nothing else.
    
    ## Human checkpoints
    - Interview answers are the first checkpoint; play the brief back in one paragraph before writing if the task is large.
    - File audits never edit before the user approves the review table.
    - If the user asks for options, give 3 to 5 variants that each differ in one dimension (tighter scope, longer run, different audience, terser report-back, different surface) and let them pick.
    
    ## Self-improvement
    This skill is never finished. Improve it as you use it.
    - When the user corrects how a step was done, update the relevant reference file (or this SKILL.md) so the correction sticks. Do not just fix it for this run.
    - When a correction is a hard rule, add it here as a permanent rule with its reason.
    - When the user says a prompt or audit was genuinely good, save the input and output to `references/examples/` as a model for future runs.
    - When Anthropic updates the Opus 5, Fable 5 or best practices pages, update `references/rulebook.md` and re-check `references/retired-instructions.md` before changing anything else.
    - Keep the skill small while doing this: when you add something, cut anything that no longer changes behavior.
    
    ## Routing
    | Step | Reference |
    |------|-----------|
    | All steps, once per session | `references/rulebook.md` |
    | 1. Interview | `references/interview.md` |
    | 2. Strip what is retired | `references/retired-instructions.md` |
    | 3. Rebuild (prompt) | `references/job-brief.md` |
    | 3. Audit (whole file) | `references/file-audit.md` |
    | 4. Rules to reasons | `references/rules-to-reasons.md` |
    | 5. Standing voice or format | `references/voice-and-format.md` |
    | 3. Rebuild, when the input is an existing prompt: skim before drafting | `references/examples/client-report-rewrite.md` |
    
    ```
    

## Want the whole thing done for you? ⚙️

These giveaways are the prompting layer of the full system we run on the Claude stack. If you want the rest of it set up for you or your team, that happens inside the Accelerator.

<aside>
🚀 **Get it set up for you and your team inside my Accelerator: https://www.benai.co/accelerator**

</aside>

### Plus everything else inside the Accelerator

- 1:1 tech help from my team to adapt these skills to your business
- Weekly live Q&As with me and the team
- Full courses on Claude Code, Cowork and Design, n8n, and Relevance AI
- Playbooks for embedding AI into your operations, marketing, sales, and delivery
- A community of operators sharing what's working week to week

If you're serious about turning the Claude stack into real leverage in your business and work, the Accelerator is where the rest of it fits together.