# resume-generator

A Copilot-powered workflow for generating tailored, ATS-friendly resumes for specific job postings, using VS Code agent skills.

## What this is

This repo contains the **tooling** for tailoring resumes — agent skills — not anyone's personal resume data. Personal files (your base resume, profile context, generated resume drafts) are kept locally and excluded from version control by convention.

## How it works

- [`.agents/skills/resume-create`](.agents/skills/resume-create) — the `/resume-create` skill. Given a job description, it reads your base resume and confirmed profile facts, runs a guided clarification Q&A to fill gaps, then generates a final tailored resume.
- [`.agents/skills/grill-with-docs`](.agents/skills/grill-with-docs) — drives the clarification/interview step and keeps `CONTEXT.md` in sync with confirmed facts.
- [`.agents/skills/tailored-resume-generator`](.agents/skills/tailored-resume-generator) — generates the final tailored resume from the job description, base resume, and clarification answers.
- [`.agents/skills/documentation-writer`](.agents/skills/documentation-writer) — general-purpose documentation skill used when writing/updating docs in this repo.
- [`skills-lock.json`](skills-lock.json) — lock file tracking the source/version of installed skills.

## Setup

1. Clone this repo and open it in VS Code with GitHub Copilot enabled.
2. Add your own personal files at the repo root (all ignored by `.gitignore` automatically):
   - `resume.md` — your base resume (source of truth: history, stack, seniority, results).
   - `CONTEXT.md` — confirmed facts, positioning, and gap-mitigation notes reused across resumes (see the "Resume Tailoring Profile" structure the prompt expects).
3. **Naming convention:** any personal resume file you create (base resume, tailored drafts, exported PDFs, job postings, etc.) must start with the `resume.` prefix, e.g. `resume.acme.backend-engineer.md`. The `.gitignore` ignores everything matching `/resume.*` at the repo root, so following this convention keeps personal data out of git automatically.

## Usage

1. In VS Code Copilot Chat, run the `/resume-create` skill.
2. Paste the full job description (and company/title if not obvious from it).
3. Answer the one-at-a-time clarification questions the assistant asks.
4. Receive the tailored resume plus a fit summary and follow-up suggestions.
5. Save the result using the `resume.` prefix naming convention above.

## Repo hygiene

`.gitignore` excludes:
- `/resume.*` — any personal resume/profile/job-posting file following the naming convention above
- `/CONTEXT.md` — your personal confirmed-facts profile

Everything else in this repo is generic tooling meant to be shared/forked.
