# Agentic AI Saksham — Non-Engineering Session

A mentor handbook for delivering the **Agentic AI Saksham** course to a non-engineering audience. This document lists the topics to be covered, the order to teach them in, and the setup steps for this repository.

## Who this is for

Non-engineering learners with little to no coding background. The course is tool-first and hands-on: learners *use* AI products (ChatGPT, Claude, NotebookLM, n8n, Google AI Studio) rather than write code. Mentors should favor live demos, guided practice, and analogies over technical jargon.

## Course Structure

The course has three modules, taught in sequence. Each module builds on the platform/skill introduced in the one before it.

### Module 1 — Prompt Engineering (in ChatGPT)

Teach learners how to talk to an AI model effectively. All exercises in this module are done in ChatGPT.

| Topic | What to cover |
|---|---|
| Zero-Shot Prompting | Asking the model to do a task with no examples given. Show how wording and clarity alone drive output quality. |
| Few-Shot Prompting | Giving the model 2–3 examples of the desired input/output before asking it to do the real task. Show how examples steer format and tone. |
| Chain of Thought Prompting | Asking the model to reason step-by-step before answering. Useful for math, logic, and multi-step decisions. |
| Role-Based Prompting | Assigning the model a persona/role (e.g., "You are a career counselor") to shape tone, expertise, and perspective in its answers. |

**Mentor notes:**
- Run each technique on the *same* sample question so learners can directly compare outputs.
- End the module with a short exercise where learners pick the right technique for a given problem.

### Module 2 — Claude

Move learners from ChatGPT to Claude, highlighting Claude's project- and artifact-based workflow.

| Topic | What to cover |
|---|---|
| Claude Projects | Organizing related conversations, uploading reference files/knowledge, and setting project-level instructions. |
| Claude Skills | What skills are, how they extend Claude's capabilities for a task, and when to invoke one. |
| Claude Artifacts | Generating standalone outputs (documents, pages, visuals) that can be viewed, edited, and shared separately from the chat. |

**Mentor notes:**
- Have learners recreate one of their Module 1 prompting exercises inside a Claude Project to show continuity of context.
- Demonstrate at least one Artifact end-to-end (create → preview → share).

### Module 3 — Applied AI Tools

Introduce tools that apply AI beyond chat: research, automation, and multimodal generation.

| Topic | What to cover |
|---|---|
| NotebookLM | Uploading source documents and using AI to summarize, generate study guides, and answer grounded questions from those sources. |
| n8n | No-code workflow automation; connecting triggers and actions into an automated pipeline. Use the sample workflow included in this repo (see below). |
| Google AI Studio | Exploring Google's model playground — prompting, and multimodal (text/image) experimentation. |

**Mentor notes:**
- For n8n, walk through the included **`Resume Screening Agent.json`** workflow: import it into n8n, explain each node, and run it live so learners see an end-to-end automated agent.
- Keep the Google AI Studio segment exploratory — the goal is familiarity, not depth.

## Repository Contents

- `README.md` — this handbook.
- `Resume Screening Agent.json` — sample n8n workflow used in Module 3 to demonstrate a working automation/agent. Import it via n8n's **Workflows → Import from File** option.

## Setting Up This Repository (for mentors)

Steps to initialize this folder as a Git repository and publish it (e.g., to GitHub) so it can be shared with other mentors:

1. **Initialize Git** in this folder:
   ```
   git init
   ```
2. **Stage the course files**:
   ```
   git add README.md "Resume Screening Agent.json"
   ```
3. **Commit**:
   ```
   git commit -m "Initial commit: Agentic AI Saksham course handbook and n8n workflow"
   ```
4. **Create a remote repository** on GitHub (or your Git host of choice), then link it:
   ```
   git remote add origin <repository-url>
   ```
5. **Push**:
   ```
   git branch -M main
   git push -u origin main
   ```
6. **Keep it updated** — as new sample prompts, workflows, or slides are added for the course, repeat:
   ```
   git add <new-file>
   git commit -m "Describe what was added"
   git push
   ```

## Delivery Checklist

- [ ] Module 1: Zero-Shot demo
- [ ] Module 1: Few-Shot demo
- [ ] Module 1: Chain of Thought demo
- [ ] Module 1: Role-Based demo
- [ ] Module 2: Claude Projects walkthrough
- [ ] Module 2: Claude Skills walkthrough
- [ ] Module 2: Claude Artifacts walkthrough
- [ ] Module 3: NotebookLM walkthrough
- [ ] Module 3: n8n — import and run `Resume Screening Agent.json`
- [ ] Module 3: Google AI Studio walkthrough
