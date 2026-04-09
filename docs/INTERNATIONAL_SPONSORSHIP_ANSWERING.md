# International Sponsorship Answering

Use this guide when the candidate is an international applicant and the ATS or recruiter asks about U.S. work authorization or sponsorship.

This repo's stance is simple:
- answer truthfully
- separate "authorized to work now" from "will require sponsorship now or in the future"
- do not collapse temporary work authorization into "sponsorship-free forever"
- do not give legal advice

This playbook is informed by Interstride's March 24, 2026 guidance on how international students should answer the standard U.S. sponsorship question.

Source:
- [Interstride: How to Answer: Will You Now or in the Future Require Sponsorship to Work In the U.S.](https://www.interstride.com/blog/how-to-answer-will-you-now-or-in-the-future-require-sponsorship-to-work-in-the-us/)

## The two questions to separate

Most ATS flows are really trying to learn two different things:

1. Can the candidate legally work in the U.S. right now for this role?
2. Will the candidate need employer sponsorship now or later to continue long-term U.S. employment?

Those are not the same question.

## Shared answering rules

- If the candidate can work now but will later need sponsorship, answer both parts truthfully.
- If the employer asks only one combined question, do not hide the future sponsorship need.
- If the profile says future sponsorship will be required, never answer `No` just because the candidate has temporary authorization today.
- If the role is internship-only and the candidate's authorization is internship-limited, say that clearly in free-text explanations.
- If the candidate may have a non-sponsorship path such as TN, do not assume it applies unless the profile explicitly says it does and the role is actually compatible.
- If timing is tight, include the real expiration month and year when helpful.

## Profile types the repo should support

Store one of these in `authorization.candidate_profile_type` when it fits:

- `f1_cpt_internship`
- `f1_opt_non_stem`
- `f1_opt_stem`
- `work_authorization_expiring_soon`
- `tn_eligible`
- `immediate_employer_sponsorship_required`
- `other`

## Profile-type answer map

### 1. `f1_cpt_internship`

Use when:
- the candidate is on F-1
- the role is an internship, co-op, externship, or other CPT-compatible position

Default ATS logic:
- `authorized_to_work_now`: yes, for qualifying CPT-authorized internship work
- `requires_immediate_sponsorship`: no
- `future_sponsorship_required`: yes, if the candidate wants long-term U.S. work after graduation

Short answer sample:
- "I am authorized to work for this internship through CPT. If I continue in the U.S. long term after graduation, I will require sponsorship in the future."

Use with care:
- do not reuse this wording for full-time post-grad roles unless the profile confirms that path

### 2. `f1_opt_non_stem`

Use when:
- the candidate can work now on OPT
- they do not have STEM extension eligibility

Default ATS logic:
- `authorized_to_work_now`: yes
- `requires_immediate_sponsorship`: no, while OPT remains active
- `future_sponsorship_required`: yes

Short answer sample:
- "I am currently authorized to work in the U.S. through OPT. I do not require immediate sponsorship, but I will require employer sponsorship in the future to continue long-term U.S. employment."

### 3. `f1_opt_stem`

Use when:
- the candidate is on STEM OPT or expects the STEM OPT extension path

Default ATS logic:
- `authorized_to_work_now`: yes
- `requires_immediate_sponsorship`: no
- `future_sponsorship_required`: yes

Short answer sample:
- "I am currently authorized to work in the U.S. through STEM OPT. There is no immediate sponsorship required during my current authorization period, but I will require employer sponsorship in the future for long-term U.S. employment."

Helpful free-text extension:
- "My current authorization does not require immediate employer sponsorship or filing cost during the active OPT period."

### 4. `work_authorization_expiring_soon`

Use when:
- the candidate can work now, but the authorization window is short enough that sponsorship may become an immediate hiring issue

Default ATS logic:
- `authorized_to_work_now`: yes, until the real expiration date
- `requires_immediate_sponsorship`: often yes for practical recruiting purposes
- `future_sponsorship_required`: yes

Short answer sample:
- "I am currently authorized to work in the U.S. through [month year]. If I continue beyond that point, I will require employer sponsorship."

Practical note:
- if the employer's start date is after the authorization end date, treat this as an immediate sponsorship case

### 5. `tn_eligible`

Use when:
- the candidate is a Canadian or Mexican citizen
- the role is actually compatible with TN classification
- the candidate wants the repo to treat TN as the likely path

Default ATS logic:
- `authorized_to_work_now`: profile-dependent
- `requires_immediate_sponsorship`: often no in standard ATS wording if TN is the intended path
- `future_sponsorship_required`: often no if the candidate expects to remain on TN-compatible work authorization

Short answer sample:
- "I am eligible to work in TN-qualifying roles and do not expect standard employment visa sponsorship for this path."

Use with care:
- do not use this template unless the profile explicitly instructs it
- tell the candidate to verify the role and legal pathway with counsel or their immigration advisor

### 6. `immediate_employer_sponsorship_required`

Use when:
- the candidate needs employer action now, not later
- examples may include expired or near-expired student authorization, a new H-1B/O-1 need, or another employer-dependent status

Default ATS logic:
- `authorized_to_work_now`: profile-dependent
- `requires_immediate_sponsorship`: yes
- `future_sponsorship_required`: yes

Short answer sample:
- "Yes. I will require employer sponsorship to work in the United States. I am happy to discuss the appropriate visa pathway based on the role."

## Standard ATS question handling

### "Are you legally authorized to work in the United States?"

Answer based on current truth, not future plans.

Examples:
- CPT internship candidate applying to a qualifying internship: `Yes`
- OPT/STEM OPT candidate within valid authorization: `Yes`
- candidate whose authorization already expired and who cannot start without sponsorship: do not auto-answer `Yes`

### "Will you now or in the future require sponsorship to work in the U.S.?"

Answer based on long-term truth.

Examples:
- CPT internship candidate who wants long-term U.S. employment: `Yes`
- OPT or STEM OPT candidate planning to stay in the U.S.: `Yes`
- TN-eligible candidate whose profile explicitly says TN path and no standard sponsorship expected: often `No`

### "Do you require immediate sponsorship?"

Answer based on whether the employer must act now for the candidate to start or continue lawfully.

Examples:
- active STEM OPT with runway left: usually `No`
- authorization expiring before the likely start date: usually `Yes`
- immediate H-1B/O-1 or other employer petition needed: `Yes`

## Free-text answer templates by use case

### Concise ATS note

- "I am currently authorized to work in the U.S. and do not require immediate sponsorship. I will require employer sponsorship in the future for long-term U.S. employment."

### Internship-specific note

- "I am authorized to work for this internship through CPT. If I continue in the U.S. after graduation, I will require sponsorship in the future."

### OPT timing note

- "I am currently authorized to work in the U.S. through [authorization basis] until [month year]. I do not require immediate sponsorship during that period, but I will require employer sponsorship afterward if I continue long term."

### Immediate sponsorship note

- "I will require employer sponsorship to work in the U.S. and can discuss the most appropriate pathway based on the role."

## Repo behavior this guide should drive

- `config/profile.yml` should capture the candidate's profile type, timing, and preferred truthful wording.
- `modes/apply.md` should use the profile type to answer ATS forms consistently.
- `modes/evaluate.md` should assess sponsorship fit without treating employer silence as an automatic rejection.
- docs and examples should show candidates how to encode their specific situation.

## Caution

This repo can help with truthful framing, but it is not a substitute for legal advice. If the answer depends on visa timing, employer type, cap-exempt status, TN eligibility, or another legal nuance, the candidate should confirm details with a school official, program sponsor, immigration attorney, or employer immigration team.
