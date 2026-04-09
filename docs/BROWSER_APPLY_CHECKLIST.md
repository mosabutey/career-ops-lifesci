# Browser Apply Validation Checklist

Use this checklist when validating browser-assisted application support on real sites.

## Pre-checks

- `npm run doctor`
- `node verify-pipeline.mjs`
- The correct resume variant exists in `output/`
- The role has an evaluation report in `reports/`
- The candidate has reviewed work authorization details in `config/profile.yml`

## Test scenarios

### 1. Open and inspect a job posting

- Open the job URL
- Confirm the title matches the evaluated role
- Confirm the posting is still active
- Confirm the apply flow can be reached

### 2. Read and classify visible questions

- Free-text questions are detected
- Dropdown and yes/no questions are detected
- Custom comboboxes and listboxes are detected as interactive controls, not ignored because there is no native `select`
- Checkbox and acknowledgment controls are detected
- Radio or pill-style choice groups are detected when present
- Repeated labels such as `Yes` and `No` are matched within the correct question group rather than globally
- Upload fields are detected
- Work authorization and sponsorship questions are surfaced clearly
- Similar labels such as `First Name` and `Preferred First Name` do not confuse field matching

### 3. Upload documents

- The correct resume or CV variant is selected
- Cover letter upload works when a cover letter exists
- The agent does not upload an unapproved file

### 4. Fill fields

- Generated answers match the role and report context
- Required fields are filled accurately
- Salary and sponsorship answers remain truthful
- Custom dropdowns can be set either by visible option click or keyboard fallback
- Checkbox state is verified after clicking
- Radio groups are selected within the correct question block
- Selected values persist after interaction
- The user can review all populated fields before submission

### 5. Multi-step and gated flows

- Step-based platforms such as Workday are recognized as multi-step flows
- Account-creation or sign-in gates are identified before the agent goes further
- The agent stops at account-creation boundaries unless the user explicitly wants help proceeding

### 6. Safety boundary

- The agent stops before final submit
- The final review remains with the user
- No attempt is made to bypass captcha, login friction, or platform safeguards

### 7. Broken or stale links

- 404 or error-page application URLs are detected early
- Redirects to a generic jobs index are not mistaken for valid application forms
- The workflow falls back to re-finding the live posting rather than filling the wrong page

## Validation notes from live tests

Observed on real ATS pages:
- Greenhouse forms may contain overlapping labels such as `First Name` and `Preferred First Name`, so exact selectors are safer than loose label matches.
- Greenhouse commonly uses custom combobox widgets for country, sponsorship, relocation, and similar questions; they are not always native dropdowns.
- Keyboard fallback (`ArrowDown`, `Enter`) can work when a Greenhouse option list is not exposed cleanly for clicking.
- Checkbox acknowledgments can appear alongside custom question blocks and should be validated after clicking.
- Workday may expose the job posting first and only reveal the application structure after clicking `Apply` and, in some cases, `Apply Manually`.
- Some Workday flows reach a create-account/sign-in gate before the full question set is available.
- Some public ATS links are stale and may return 404 or redirect to a generic jobs page, so liveness and page identity should be rechecked before filling.

## Current proof status

Proven on live forms:
- Standard text fields
- Resume upload
- Some custom Greenhouse combobox interactions
- Checkbox acknowledgment interaction
- Native `select` controls
- Radio-group interaction
- Checkbox-group interaction
- Detection of Workday multi-step application structure

Observed but not yet fully proven across all platforms:
- Deep Workday question pages after account creation
- Every custom-dropdown variant on Greenhouse
- Complex captcha- or login-heavy flows

## Notes to record

After each validation run, note:
- employer / platform
- what worked
- what broke
- which fields were hard to detect
- which control types were proven vs only observed
- whether uploads succeeded
- whether sponsorship questions were handled correctly

Use those notes to improve `modes/apply.md`, scanner targeting, and future platform-specific guidance.
