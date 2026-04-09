# Setup Guide

## Prerequisites

- an AI coding tool such as Claude Code, Codex, or OpenCode
- Node.js 18+
- Playwright Chromium for PDF generation
- optional: Go for the dashboard

## Quick Start

### 1. Clone and install

```bash
git clone https://github.com/mosabutey/career-ops-lifesci.git
cd career-ops-lifesci
npm install
npx playwright install chromium
npm run doctor
```

### 2. Configure your profile

```bash
cp config/profile.example.yml config/profile.yml
cp templates/portals.example.yml portals.yml
```

Edit `config/profile.yml` with:
- your identity
- your career stage
- your primary role packs
- your narrative and proof themes
- your markets and constraints

### 3. Add your source materials

Create `cv.md` in the project root.

Optional but strongly recommended:
- `article-digest.md` for proof points, publications, projects, awards, or case studies
- `modes/_profile.md` for your translation library and track-specific positioning

### 4. Open your AI tool

```bash
claude
# or: codex
# or: opencode
```

Then ask the tool to personalize the system. Examples:
- "Set this up for medical affairs and life sciences consulting"
- "Build an internship-friendly version for graduate students"
- "Make health-tech my secondary track"

### 5. Start using it

You can:
- paste a JD or URL to evaluate it
- run `/career-ops scan`
- run `/career-ops pdf`
- run `/career-ops patterns`
- run `/career-ops batch`

## Local PC capabilities

When the repo is open in a compatible local agent environment, the agent can:
- run repo scripts and validations
- open job sites and inspect live postings
- generate tailored documents locally
- assist with browser-based application forms
- upload resume or cover letter files when paths are known
- fill visible fields and stop before final submission

The user remains the final reviewer and submitter of all real applications.

For boundaries and operating expectations, see [docs/LOCAL_AGENT_GUIDE.md](LOCAL_AGENT_GUIDE.md).
For real-site validation of browser assistance, see [docs/BROWSER_APPLY_CHECKLIST.md](BROWSER_APPLY_CHECKLIST.md).

## Validate setup

```bash
npm run doctor
node cv-sync-check.mjs
node verify-pipeline.mjs
node analyze-patterns.mjs
```

## Optional dashboard

```bash
cd dashboard
go build -o career-dashboard .
./career-dashboard --path ..
```
