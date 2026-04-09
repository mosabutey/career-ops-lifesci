# Live Apply Validation Notes

This document records hands-on validation findings from real public application flows.

## Validated platforms

### Greenhouse

Representative live tests:
- Legend Biotech -- Medical Affairs Co-Op
- Cytokinetics -- Director, Regulatory Affairs CMC Europe

Observed:
- The application page was reachable
- The `Apply` flow stayed on the same page and exposed a full form
- Text fields could be filled
- Resume upload could be triggered
- Custom combobox-style questions were present in quantity, including country, sponsorship, relocation, and other screening questions
- A live sponsorship combobox was successfully driven with keyboard fallback on the Cytokinetics form
- A live checkbox acknowledgment was successfully marked on the Cytokinetics form
- The workflow stopped before submission

Important finding:
- Greenhouse may expose both `First Name` and `Preferred First Name`, so exact selectors are safer than broad label matching
- Greenhouse dropdowns are often not native `select` elements; they may behave as `combobox` + `listbox` controls instead
- Some comboboxes are easier to drive by keyboard than by clicking a visible option list
- Not every combobox variant behaved the same way across pages, so value verification after selection is important

### Lever

Representative live test:
- enGene -- Vice President, Medical Affairs

Observed:
- The `/apply` route was reachable
- Standard contact fields could be filled
- Resume upload worked
- Native `select` controls were filled successfully
- Radio groups were selected successfully when scoped to the surrounding question block
- Checkbox groups were selected successfully
- The workflow stopped before submission

Important finding:
- Lever can include many repeated `Yes`/`No` labels and large self-ID sections, so question-scoped selectors are safer than global label matching

### Workday

Representative live test:
- Montclair State University -- Procurement Systems Analyst

Observed:
- The posting page was reachable
- The `Apply` path could be opened
- The flow progressed into a real multi-step application state
- The step structure was visible before account creation, including `Create Account/Sign In`, `My Information`, `My Experience`, `Application Questions`, `Voluntary Disclosures`, `Self Identify`, and `Review`
- A checkbox-style account-creation acknowledgment was present on the create-account step

Important finding:
- Workday may require an account-creation or sign-in step before the deeper question pages are reachable, so this is a real workflow boundary the repo should respect

### SmartRecruiters

Representative live tests:
- AbbVie -- Pipeline Medical Science Liaison
- AbbVie -- Medical Science Liaison

Observed:
- expired postings are clearly detectable
- a live posting can expose a primary CTA labeled `I'm interested` instead of `Apply`
- following that CTA can hand off to a one-click SmartRecruiters surface

Important finding:
- in this environment, the SmartRecruiters one-click handoff did not expose an immediately inspectable form surface, so the repo should treat SmartRecruiters as a platform with CTA naming and rendering nuances rather than assuming Greenhouse-like behavior

## Failure cases observed

- A stale Lever job link returned a 404 page
- A Greenhouse job link redirected to a generic jobs error page instead of a valid application
- A sector-relevant Workday link for Sarepta returned a "page doesn't exist" error page
- Some Greenhouse question widgets exposed field IDs cleanly but did not always expose click-friendly option lists consistently
- A SmartRecruiters posting was expired, and a live SmartRecruiters one-click handoff rendered without accessible form controls in this environment

## Product implications

- Apply mode should verify the application page before filling
- Field selectors should be robust to overlapping labels
- Upload flows are realistic and worth supporting as a first-class capability
- Custom ATS controls should be handled as role-based widgets, not just native form elements
- Keyboard fallback is valuable for some combobox widgets
- Workday support should explicitly account for gated multi-step flows and account-creation boundaries
- SmartRecruiters support should look for alternate CTA text such as `I'm interested` and verify whether the application handoff actually renders usable controls
- Browser-assisted application support is viable, but must keep the user-review boundary intact

## Current confidence by control type

High confidence:
- text inputs
- file uploads
- stale-link detection
- Greenhouse custom-combobox handling in at least one live sponsorship flow
- checkbox interaction
- Workday multi-step flow detection

Medium confidence:
- broader Greenhouse combobox families across different employers
- Workday progression up to the account-creation gate

Not yet proven in live testing:
- deep Workday question pages after account creation
- final-submit handling, by design

## Workday boundary note

Going deeper than the create-account or sign-in gate on most live Workday applications would require creating or using a real applicant account on an employer system. That should remain an explicit user decision, not a default automation step. The repo should treat this as a documented handoff boundary unless the user clearly asks for help proceeding.
