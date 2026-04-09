# ATS Apply Playbook

Use this guide when running `apply` mode against real applicant tracking systems. It summarizes the platform-specific behavior observed during live validation and gives the local agent a safer default strategy for each ATS family.

## Why this exists

Application platforms do not behave the same way:
- some use native `select` elements
- some use custom combobox and listbox widgets
- some gate the real application behind account creation
- some rename the call to action so it is not literally `Apply`

Treating all ATS platforms the same leads to brittle browser automation. This playbook keeps `apply` mode practical and platform-aware.

## Greenhouse

### Proven live behavior

- posting and form can be reachable on the same page
- text fields work
- file upload works
- many screening questions use custom `combobox` + `listbox` widgets instead of native `select`
- checkbox acknowledgments can appear alongside custom question blocks

### Representative findings

- overlapping labels can exist, such as `First Name` and `Preferred First Name`
- sponsorship and authorization questions may be custom comboboxes
- some comboboxes respond better to keyboard fallback than direct option clicking

### Best strategy

1. verify the job page is still active
2. prefer exact label or field ID targeting
3. treat dropdown-like questions as custom widgets first, not native `select`
4. if option clicking is unreliable, try keyboard fallback:
   - focus field
   - type query
   - `ArrowDown`
   - `Enter`
5. verify the selected value persisted after every choice

### Known risk

Not every Greenhouse combobox variant exposes options the same way, so value verification is mandatory.

## Lever

### Proven live behavior

- `/apply` pages are directly reachable on live postings
- text fields work
- file upload works
- native `select` controls work
- grouped radio questions work
- grouped checkbox questions work

### Representative findings

- some forms contain large self-ID sections with many radios and checkboxes
- repeated labels such as `Yes` and `No` can appear multiple times

### Best strategy

1. target radios and checkboxes within the surrounding question block
2. do not click a global `Yes` or `No` label without scoping it first
3. use native `select` handling when present
4. verify checked state after each interaction

### Known risk

Global label matching is brittle on long Lever forms with repeated response options.

## Workday

### Proven live behavior

- live postings can be opened
- `Apply` can lead into a true multi-step application state
- the step structure may be visible before deeper progression
- a create-account or sign-in step can appear before the actual question pages

### Representative findings

- Workday commonly exposes a gated flow such as:
  - `Create Account/Sign In`
  - `My Information`
  - `My Experience`
  - `Application Questions`
  - `Voluntary Disclosures`
  - `Self Identify`
  - `Review`

### Best strategy

1. detect whether the page is still just a posting or has entered the application flow
2. record visible step names when available
3. stop at account-creation or sign-in boundaries unless the user explicitly wants help proceeding
4. tell the user clearly that deeper progression may require a real applicant account

### Known risk

Deeper Workday proof usually requires creating or using a real employer-system account. That should remain an explicit user decision.

## SmartRecruiters

### Proven live behavior

- live postings can be opened
- expired postings are detectable
- the primary CTA may be labeled `I'm interested` rather than `Apply`

### Representative findings

- the `I'm interested` CTA can hand off to a one-click application surface
- in this environment, that one-click surface may render as a blank or JS-heavy handoff page rather than an immediately inspectable form

### Best strategy

1. do not assume the CTA says `Apply`
2. look for alternate intent labels such as `I'm interested`
3. verify whether the handoff page actually renders usable controls before proceeding
4. if the one-click surface is blank or inaccessible, fall back to telling the user what happened and preserve the current page context

### Known risk

SmartRecruiters may rely on rendering or handoff behavior that is less transparent in automated browser sessions than Greenhouse or Lever.

## Cross-platform rules

- verify the page is live before filling
- upload only approved files
- prefer exact selectors over fuzzy matches
- scope repeated labels to the correct question group
- verify persisted values after interactions
- stop before final submission
- stop at account-creation boundaries unless the user explicitly wants help proceeding

## Current live proof summary

High-confidence control types:
- text inputs
- file uploads
- native `select` controls
- grouped radio questions
- grouped checkbox questions
- some custom combobox/listbox questions

High-confidence workflow capabilities:
- stale-link detection
- grouped-question scoping
- multi-step Workday flow detection

Still not fully proven:
- deep Workday question pages after account creation
- every custom-dropdown variant on Greenhouse
- captcha-heavy or login-heavy flows
