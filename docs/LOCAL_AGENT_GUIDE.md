# Local Agent Guide

Career-Ops LifeSci is designed to be operated locally by an AI agent running on the user's machine through tools such as Codex, Claude Code, or OpenCode.

This document explains what the agent can do, what it should not do, and where human review remains mandatory.

## What the local agent can do

With the repo open locally, the agent can:
- read and edit repo files
- personalize `config/profile.yml`, `modes/_profile.md`, `cv.md`, `article-digest.md`, and `portals.yml`
- run local Node scripts such as:
  - `npm run doctor`
  - `node verify-pipeline.mjs`
  - `node merge-tracker.mjs`
  - `node analyze-patterns.mjs`
- open job sites and evaluate live postings when browser automation is available
- generate ATS-safe resumes, CVs, and cover letters
- inspect job application forms and generate tailored responses
- upload approved resume or cover letter files when the path is known
- fill visible application fields for the user to review
- maintain tracker and report files without breaking the data contract

## What the local agent should not do

The agent should not:
- auto-submit applications without human review
- fabricate qualifications, metrics, publications, or work authorization
- bypass captchas, account protections, or platform safeguards
- ignore explicit employer restrictions such as sponsorship, citizenship, or clearance requirements
- spam low-fit applications or outreach messages
- modify user-layer files in ways that overwrite true personal information without the user's instruction

## Human-review boundary

The user must remain the final reviewer for:
- resume and cover letter content
- application answers
- uploaded files
- sponsorship or work-authorization disclosures
- the final submit action on an application

The agent may prepare, draft, upload, and fill. The user decides whether the final application is actually sent.

## Browser-assisted applications

When browser automation is available, a well-configured local agent may:
- open a company careers page
- navigate into the specific job posting
- open the application flow
- read visible questions and form structure
- choose the best-fit document variant
- upload that document
- fill visible fields from approved source material

The agent should then stop and present the application for review before final submission.

For platform-specific browser guidance, see [docs/ATS_APPLY_PLAYBOOK.md](ATS_APPLY_PLAYBOOK.md).

## Practical limits

Real-world application sites vary widely. Depending on the site, the agent may encounter:
- logins
- captcha or anti-bot screens
- multi-step workflows
- embedded widgets
- inaccessible custom components
- upload restrictions
- region-specific compliance questions

If the agent cannot safely or clearly interact with the site, it should fall back to:
- reading the visible page
- generating copy-paste-ready answers
- telling the user exactly what remains to do manually

## Best practices

- Keep source-of-truth documents current before applying.
- Generate the role-specific resume before opening the application form.
- Prefer evaluating a role before filling the form.
- Use the patterns mode regularly so the system learns from outcomes.
- Treat the repo as a quality system, not a mass-submission engine.
