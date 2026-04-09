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
- Upload fields are detected
- Work authorization and sponsorship questions are surfaced clearly

### 3. Upload documents

- The correct resume or CV variant is selected
- Cover letter upload works when a cover letter exists
- The agent does not upload an unapproved file

### 4. Fill fields

- Generated answers match the role and report context
- Required fields are filled accurately
- Salary and sponsorship answers remain truthful
- The user can review all populated fields before submission

### 5. Safety boundary

- The agent stops before final submit
- The final review remains with the user
- No attempt is made to bypass captcha, login friction, or platform safeguards

## Notes to record

After each validation run, note:
- employer / platform
- what worked
- what broke
- which fields were hard to detect
- whether uploads succeeded
- whether sponsorship questions were handled correctly

Use those notes to improve `modes/apply.md`, scanner targeting, and future platform-specific guidance.
