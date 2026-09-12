# AI Business Saksham — Mentor Handbook

This handbook is your reference for running the AI Business Saksham program. It covers the schedule, what each segment is meant to achieve, what you're responsible for as a mentor, and how the hackathon runs. Read it end to end before day one, then keep it open during the program.

## Index

- [Program at a Glance](#program-at-a-glance)
- [Pre-Work, Before Day One](#pre-work-before-day-one)
- [Day 1, First Half — Icebreaker, Prompt Engineering, Claude](#day-1-first-half--icebreaker-prompt-engineering-claude)
- [Day 1, Second Half — Chatbot (n8n)](#day-1-second-half--chatbot-n8n)
- [Day 2, First Half — Post Generator (n8n), AI Studio](#day-2-first-half--post-generator-n8n-ai-studio)
- [Day 2, Second Half — Hackathon Start](#day-2-second-half--hackathon-start)
- [Day 3, First Half — Hackathon](#day-3-first-half--hackathon)
- [Day 3, Second Half — Evaluation, Presentation, Winner Declaration](#day-3-second-half--evaluation-presentation-winner-declaration)
- [Mentor Responsibilities, By Phase](#mentor-responsibilities-by-phase)
- [What "Done" Looks Like](#what-done-looks-like)
- [Reference Material](#reference-material)

## Program at a Glance

- Three days, each split into a first half and a second half.
- Tool order: Gemini for prompt fundamentals, Claude for building and reasoning, n8n for automation, Google AI Studio for frontend prototyping.
- Hackathon runs from the second half of day two through day three.
- Each tool is introduced only after the one before it has given students something concrete to carry forward, so by the hackathon they've already seen the full pipeline work once, end to end.
- Teaching-half mentor role: catch the moment a student falls behind and pull them back in before the gap widens.
- Hackathon mentor role: not teaching anymore, purely unblocking.

## Pre-Work, Before Day One

- Every student needs: a Gemini account, a Claude account, an n8n account (cloud or self-hosted), and Google AI Studio access with a Gemini API key generated.
- Send setup instructions at least three days out.
- Confirm completion the day before, not the morning of.
- Skipping this eats day one's teaching time on account creation and email verification instead of content.

## Day 1, First Half — Icebreaker, Prompt Engineering, Claude

**Icebreaker into LLM fundamentals**
- Students form small circles.
- One student says a line built around a random word; the next continues the story; the third continues again.
- After the chain completes, connect it explicitly to how a language model works: each student only had the previous lines to go on, which is the context window; the story usually drifts by the third line, which is a live example of context loss and hallucination.
- Don't skip the explicit connection. The exercise alone is just a game.
- Optional framing line for this segment: an AI agent is a system that acts autonomously to pursue a goal by planning and executing steps. Introduce this early since it's the concept the whole program builds toward.
- Cover, at a business-student level: what a token is, why context windows have limits, why a model can sound confident while being wrong.
- Before moving to prompting, have each student pick one real topic or business process they want to work with for the rest of the day (their own business area, or a process they're familiar with). Everything they build from here on should use that same topic, so their work stays coherent instead of scattering across unrelated examples.

**Prompt Engineering** (on Gemini, to preserve Claude usage for later)
- Zero-shot: direct instruction, no examples. Good for quick summaries and definitions.
- Few-shot: one or more input-output examples so the model matches pattern and structure. Good for consistent, standardized outputs.
- Chain-of-thought: instruct the model to think step by step. Good for reasoning and multi-step problems; less necessary on newer models but still relevant for smaller or older ones.
- Role-based and context prompting: give the model a persona and a situation. Role sets the perspective, context sets the situation; together they set tone, style, and content.
- Multi-turn chat: ask the model to question you first, then confirm before giving a final answer.
- Negative prompting: state explicitly what not to do.
- Quality standards: ask for a response that would rank in the "top 5%" of a given profession, which forces the model to reason and self-check before answering.
- Prompt-by-AI: give the model your raw details and ask it to write the prompt for you.
- Add a short block on evaluating outputs: how to check whether a model's output is actually correct before acting on it. This matters more for a business cohort than a technical one, since they'll be shipping outputs into workflows and interfaces without an engineer checking behind them. Keep it to about fifteen minutes: show one confidently wrong output and have the group catch the error.

**Claude**
- Teach Projects, Artifacts, and Skills in depth, since these are what students use to produce hackathon deliverables.
  - Projects: a persistent workspace with context that carries across a conversation.
  - Artifacts: a way to produce a standalone output (document, mini-app, piece of content) that can be iterated on.
  - Skills: a way to package a reusable instruction set instead of re-explaining a task every time.
- Cover Connectors and Design as a fast pass, one quick example each, not a hands-on build for every student. Connector authentication in particular tends to eat time unpredictably when a whole room tries it at once.
- If running behind, compress Connectors and Design further first. Do not cut into Projects, Artifacts, or Skills.

## Day 1, Second Half — Chatbot (n8n)

- Build the customer support chatbot. Every student builds this exact workflow before improvising, so the room moves at one pace and you have a known state to debug against.
- Architecture: a Telegram trigger feeds an AI Agent node (Claude Haiku via AWS Bedrock) with a buffer window memory attached, so the bot holds context across a conversation.
- The agent replies through a Telegram send-message tool rather than returning plain text. Emphasize this: the model doesn't respond automatically, it has to call a tool to send anything back.
- Have students notice the system prompt defines:
  - scope (what the bot can help with)
  - escalation rules (when to hand off instead of guessing)
  - Telegram-specific formatting constraints (no headers or tables, short messages, plain text over markdown)
  - a hard rule against inventing policy or pricing facts not in the prompt or knowledge base
- This build teaches the agent-with-memory-and-tool pattern that the next day's workflow reuses.

## Day 2, First Half — Post Generator (n8n), AI Studio

**Post Generator (n8n)**
- Build the Instagram post generation agent.
- A chat trigger fans out to two parallel chains, both on Claude Haiku:
  - Instagram Post Writer: produces a hook line, short body, and hashtags as structured output.
  - Prompt Writer: converts the same input into a single visual text-to-image prompt under 25 words.
- The two outputs merge and feed an HTTP request to Clipdrop's text-to-image endpoint.
- The generated image and post copy return together through a webhook response.
- Have students notice:
  - the structured output parser forces the caption into a fixed JSON shape
  - the prompt-writing chain is separate because a caption needs voice and tone, while an image prompt needs purely visual and physical description

**AI Studio**
- Once the post generator works, connect its output to the prototype frontend: https://ai.studio/apps/8c381cf1-3342-4e6c-82af-40a09468a484
- Use this app as the templated starting point for non-technical cohorts rather than a blank build.
- Keep the prompting flow tight: describe the adjustment, generate, review.
- This segment should produce something a student can point at and call "my app," even if rough.
- Before the hackathon opens, run one live demo of the full chain: the Telegram chatbot pattern as the reasoning-and-memory layer, the Instagram post generator as the automation layer, the connected AI Studio app as the frontend layer.
- Protect this demo. It is the single most important moment on the schedule and the most likely to get cut under time pressure. Without it, students leave the teaching halves having learned three separate tools instead of one system.

## Day 2, Second Half — Hackathon Start

- Present the problem statements, explain judging criteria, form teams.
- Assign each mentor to a fixed set of teams for the rest of the hackathon rather than floating freely, so students know exactly who to flag down.
- Walk teams through the build order before they start:
  1. Claude Design, for a frontend idea.
  2. n8n, for the AI workflow their product needs.
  3. Google AI Studio, to bring the design idea and the workflow together into one working product.
- Teams that jump straight to AI Studio without a design direction or a working n8n workflow tend to end up with a shell that doesn't do anything.
- Hackathon building begins as soon as teams are formed.

## Day 3, First Half — Hackathon

- Students continue building through the same order: Claude Design, then n8n, then AI Studio.
- Run mentor rotations at fixed intervals, for example every ninety minutes, checking in with assigned teams rather than waiting to be approached. Many students won't ask for help even when they need it.
- If a team is stuck, check which of the three stages they're actually on:
  - design idea but no workflow → send them back to n8n before AI Studio
  - jumped to AI Studio with neither → pull them back to design first

## Day 3, Second Half — Evaluation, Presentation, Winner Declaration

- Run evaluation against the judging criteria set at kickoff.
- Shortlist the top 5 teams to present to the full room and judging panel.
- Keep each presentation slot short and enforce the time limit; the last team deserves the same attention as the first.
- Declare the top 3 winners to close the program.
- Distribute certificates and run a feedback form as part of program close-out.

## Mentor Responsibilities, By Phase

**Teaching halves**
- Watch for the student who's gone quiet, not just the one asking questions. The quiet one is usually the one who's lost.
- Walk the room during hands-on segments instead of standing at the front.

**Hackathon**
- Not delivering content, purely removing blockers.
- n8n: expect credential and webhook authentication failures. Keep a working reference workflow open on your own machine to compare against a stuck student's setup.
- Claude: expect Connector authentication issues and confusion over which surface fits a task. Redirect anything students want to hand in or show toward Artifacts.
- AI Studio: expect students to over-scope their frontend ambition. Help them cut scope, not add features.

## What "Done" Looks Like

- A working product built in the taught order: a frontend idea shaped in Claude Design, an AI workflow built in n8n, and both brought together into one functioning product in Google AI Studio.
- Not acceptable: three disconnected pieces (a design mockup nobody used, a workflow nothing calls, a bare AI Studio shell).
- If a team is trending toward disconnected pieces during day three's first half, intervene and help them re-scope toward something that actually connects before evaluation begins.

## Reference Material

- The workshop presentation this program: https://docs.google.com/presentation/d/10ozIRqPussYi9tZ_vNKOWe26VJCeJ-FZwUsdl_BXt1M/edit?usp=sharing