# AI Business Saksham — Mentor Handbook

This handbook is your reference for running the AI Business Saksham program. It covers the schedule, what each segment is meant to achieve, what you're responsible for as a mentor, and how the hackathon runs. Read it end to end before day one, then keep it open during the program.

## Index

* [Program at a Glance](#program-at-a-glance)
* [Pre-Work, Before Day One](#pre-work-before-day-one)
* [Day 1, First Half — Hackathon Kickoff, Team Formation, Post Generator (n8n)](#day-1-first-half--hackathon-kickoff-team-formation-post-generator-n8n)
* [Day 1, Second Half — Post Generator (n8n), continued](#day-1-second-half--post-generator-n8n-continued)
* [Day 2, First Half — AI Studio, Post Uploader (n8n)](#day-2-first-half--ai-studio-post-uploader-n8n)
* [Day 2, Second Half — Hackathon Building Begins](#day-2-second-half--hackathon-building-begins)
* [Additional Content — Chatbot (n8n)](#additional-content--chatbot-n8n)
* [Day 3, First Half — Hackathon](#day-3-first-half--hackathon)
* [Day 3, Second Half — Evaluation, Presentation, Winner Declaration](#day-3-second-half--evaluation-presentation-winner-declaration)
* [Mentor Responsibilities, By Phase](#mentor-responsibilities-by-phase)
* [What "Done" Looks Like](#what-done-looks-like)
* [Reference Material](#reference-material)

## Program at a Glance

* Three days, each split into a first half and a second half.
* Icebreaker/LLM fundamentals, prompt engineering, and Claude (Projects, Artifacts, Skills, Connectors, Design) are no longer taught in person — they've moved to online pre-program sessions. In-person teaching now opens directly with the hackathon kickoff and n8n.
* This is a college-level competition: the current college cohort competes as teams, with winners declared on Day 3.
* Tool order: n8n for automation, Google AI Studio for frontend prototyping.
* Students continue building "Postly," the Instagram posting app they started in the online session, as their first hands-on build — Day 1 and Day 2's teaching sections walk through the same Postly workflows (post generator, post uploader) and the AI Studio frontend, in person.
* Teams register and sit together from Day 1 morning, and can start working on their build from Day 1 itself; formal open-ended hackathon building begins right after Day 2 First Half.
* Teaching-half mentor role: catch the moment a student falls behind and pull them back in before the gap widens.
* Hackathon mentor role: not teaching anymore, purely unblocking.

## Pre-Work, Before Day One

* Every student needs: a Gemini account, a Claude account, an n8n account (cloud or self-hosted), and Google AI Studio access with a Gemini API key generated.
* Icebreaker/LLM fundamentals, prompt engineering, and Claude (Projects, Artifacts, Skills, Connectors, Design) are covered in the online pre-program sessions, not in person — confirm students have completed those sessions alongside account setup.
* Send setup instructions at least three days out.
* Confirm completion the day before, not the morning of.
* Skipping this eats day one's teaching time on account creation and email verification instead of content.

## Day 1, First Half — Hackathon Kickoff, Team Formation, Post Generator (n8n)

**Hackathon kickoff**

* Introduce the hackathon: this is a college-level competition among the current cohort, with winners declared on Day 3.
* Students register their teams at hackathon.capabl.in and then sit together by team for the rest of the program.
* Explain that teams can start working on their build from Day 1 itself — the Postly workflows taught across Day 1 and Day 2 are their first hands-on progress toward the hackathon, not a separate exercise. Open-ended hackathon building (own problem statements) formally begins right after Day 2 First Half.

**Post Generator (n8n)**

* Continue "Postly," the Instagram posting app started in the online session: build the Instagram post generation agent in teams (workflow 1 of 2; see `Instagram Post Generation Agent.json`). Every team builds this exact workflow before improvising, so the room moves at one pace and you have a known state to debug against.
* Architecture: a chat trigger fans out to two parallel chains, both on Claude Haiku:

  * Instagram Post Writer: produces a hook line, short body, and hashtags as structured output.
  * Prompt Writer: converts the same input into a single visual text-to-image prompt under 25 words.
* The two outputs merge and feed an HTTP request to Clipdrop's text-to-image endpoint (free 100 credits on sign-up at clipdrop.co/apis).
* The generated image and post copy return together through a webhook response.
* **Before lunch:** share the first feedback form in the program's WhatsApp group. Students fill it out before leaving for the break.

## Day 1, Second Half — Post Generator (n8n), continued

* Continue the post generator build from the first half.
* Have students notice:

  * the structured output parser forces the caption into a fixed JSON shape
  * the prompt-writing chain is separate because a caption needs voice and tone, while an image prompt needs purely visual and physical description
* This build teaches the agent-with-structured-output pattern that day two's upload workflow and AI Studio segment both build on.
* Running ahead of schedule? Don't idle the room — pull day two's content forward. Once a team's generator works, let them start the Post Uploader build or open Google AI Studio early, rather than waiting for day two to begin.
* **End of day:** share the second feedback form in the WhatsApp group.

## Day 2, First Half — AI Studio, Post Uploader (n8n)

**AI Studio — connect the post generator to the website**

* Start the day in AI Studio: connect the post generator workflow's output to the Postly prototype frontend: https://ai.studio/apps/8c381cf1-3342-4e6c-82af-40a09468a484
* Use this app as the templated starting point for non-technical cohorts rather than a blank build.
* Keep the prompting flow tight: describe the adjustment, generate, review.
* This segment should produce something a team can point at and call "our app," even if rough.

**Post Uploader (n8n)**

* Build the second Instagram workflow: a webhook that receives the generated image and caption, converts them to a file, and pushes them live via the `upload-post.com` node (workflow 2 of 2, same JSON file as day one, second webhook).
* Prerequisite: an `upload-post.com` account with credentials configured in n8n, and a **professional** Instagram account linked there — a personal account will not work. Confirm this the day before, same as the pre-work accounts.
* Architecture: Webhook → Convert to File → Upload photos (upload-post.com node) → Send Success Message.
* Have students notice this is the same trigger-then-tool-call pattern from day one's workflows, just wired to a publish action instead of a response.
* Chain it to day one's output: the post generator's webhook response becomes this workflow's webhook input, so the two workflows together take a prompt all the way to a live Instagram post.
* Before the hackathon opens, run one live demo of the full chain: the post generator as the creation layer, the post uploader as the publish layer, the connected AI Studio app as the frontend layer.
* Protect this demo. It is the single most important moment on the schedule and the most likely to get cut under time pressure. Without it, teams leave the teaching halves having learned disconnected tools instead of one system.

## Day 2, Second Half — Hackathon Building Begins

* Hackathon building starts immediately after Day 2 First Half wraps — no separate kickoff block. Teams already registered and sat together on Day 1, so there's no re-forming to do here.
* Present the problem statements and judging criteria before teams branch off their own ideas.
* Assign each mentor to a fixed set of teams for the rest of the hackathon rather than floating freely, so students know exactly who to flag down.
* Walk teams through the build order before they start:

  1. Claude Design, for a frontend idea.
  2. n8n, for the AI workflow their product needs.
  3. Google AI Studio, to bring the design idea and the workflow together into one working product.
* Teams that jump straight to AI Studio without a design direction or a working n8n workflow tend to end up with a shell that doesn't do anything.
* **End of day:** share the feedback form in the WhatsApp group (one form per day from here on, at end of day only).

## Day 3, First Half — Hackathon

* Students continue building through the same order: Claude Design, then n8n, then AI Studio.
* Run mentor rotations at fixed intervals, for example every ninety minutes, checking in with assigned teams rather than waiting to be approached. Many students won't ask for help even when they need it.
* If a team is stuck, check which of the three stages they're actually on:

  * design idea but no workflow → send them back to n8n before AI Studio
  * jumped to AI Studio with neither → pull them back to design first

## Day 3, Second Half — Evaluation, Presentation, Winner Declaration

* Run evaluation against the judging criteria set at kickoff.
* Shortlist the top 5 teams to present to the full room and judging panel.
* Keep each presentation slot short and enforce the time limit; the last team deserves the same attention as the first.
* Declare the top 3 winners to close the program.
* Distribute certificates.
* **End of day:** share the final feedback form in the WhatsApp group as part of program close-out.

## Additional Content — Chatbot (n8n)

* Use this only as filler: if a cohort finishes the Post Generator, Post Uploader, and AI Studio segments with time to spare, or a student needs extra content beyond the core two workflows, teach the customer support chatbot (`customer chatbot.json`) as a third example of connecting a messaging app to an LLM through n8n.
* Architecture: a Telegram trigger feeds an AI Agent node (Claude Haiku via AWS Bedrock) with a buffer window memory attached, so the bot holds context across a conversation.
* The agent replies through a Telegram send-message tool rather than returning plain text. Emphasize this: the model doesn't respond automatically, it has to call a tool to send anything back.
* Have students notice the system prompt defines:

  * scope (what the bot can help with)
  * escalation rules (when to hand off instead of guessing)
  * Telegram-specific formatting constraints (no headers or tables, short messages, plain text over markdown)
  * a hard rule against inventing policy or pricing facts not in the prompt or knowledge base
* Framing for students: this is the general pattern for wiring any messaging app (Telegram, WhatsApp, Slack) to an AI agent in n8n — a trigger from the messaging platform, an AI Agent node with memory, and a reply tool back to that same platform. The Instagram workflows swap the messaging trigger/tool for a webhook and a publish action, but the trigger → agent → tool-call shape is identical.
* Do not let this crowd out the core Day 1/Day 2 workflows — it's a bonus pattern, not a required build.

## Mentor Responsibilities, By Phase

**Teaching halves**

* Watch for the student who's gone quiet, not just the one asking questions. The quiet one is usually the one who's lost.
* Walk the room during hands-on segments instead of standing at the front.

**Hackathon**

* Not delivering content, purely removing blockers.
* n8n: expect credential and webhook authentication failures. Keep a working reference workflow open on your own machine to compare against a stuck student's setup.
* Claude: expect Connector authentication issues and confusion over which surface fits a task. Redirect anything students want to hand in or show toward Artifacts.
* AI Studio: expect students to over-scope their frontend ambition. Help them cut scope, not add features.

## What "Done" Looks Like

* A working product built in the taught order: a frontend idea shaped in Claude Design, an AI workflow built in n8n, and both brought together into one functioning product in Google AI Studio.
* Not acceptable: three disconnected pieces (a design mockup nobody used, a workflow nothing calls, a bare AI Studio shell).
* If a team is trending toward disconnected pieces during day three's first half, intervene and help them re-scope toward something that actually connects before evaluation begins.

## Reference Material

* The workshop presentation this program: https://docs.google.com/presentation/d/1Cuz-rFOxWD0lsvlPH8OceX-s7fMNEQf01INOxcYOWnw/edit?usp=sharing

