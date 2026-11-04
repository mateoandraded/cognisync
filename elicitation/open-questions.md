# Open questions for the client

Values the team **proposed** to make user stories measurable. They are not confirmed until the client accepts them. Work items that depend on a question carry the tag `needs-client-validation`.

Close a question by filling in **Decision** and **Date**, updating the affected work items, and removing the tag where nothing else is pending. Bring this list to the meeting where the client signs the conformity act (*acta de conformidad*) for the SRS.

| ID | Question | Team proposal | Affects | Decision | Date |
|---|---|---|---|---|---|
| OQ-01 | Account lockout after failed sign-ins? | Lock for 15 min after 5 consecutive failures | US-01 | | |
| OQ-02 | Idle-session timeout? | 30 min without activity → next action requires sign-in; note being edited is kept as draft | US-02 | | |
| OQ-03 | Which patient fields are "basic demographics" and which are required? | Required: first names, last names, date of birth, sex, phone, reason for consultation | US-05 | | |
| OQ-04 | Can a therapist see another therapist's patients or notes? | No — each therapist sees only their own patients | US-06, US-19 | | |
| OQ-05 | Default appointment duration? | 50 min, editable per appointment | US-09 | | |
| OQ-06 | What counts as "high dropout risk"? | 2 consecutive cancellations/no-shows, **or** ≥ 40 % of appointments missed in the last 60 days with ≥ 3 appointments in that window | US-11 | | |
| OQ-07 | Maximum length of a typed note? | 5,000 characters | US-12 | | |
| OQ-08 | Voice dictation limits and audio retention? | Recordings up to 10 min; a 5-min recording transcribed in ≤ 60 s; audio deleted once transcribed | US-13 | | |
| OQ-09 | Photos per note? | Up to 5 JPG/PNG images, 10 MB each | US-14 | | |
| OQ-10 | Can an approved note be edited? | No — approved notes are immutable; corrections are dated addenda | US-17 | | |
| OQ-11 | How long is the "brief summary" of the previous session? | ≤ 5 lines | US-18 | | |
| OQ-12 | Symptom catalog and intensity scale? | Closed catalog agreed with the client; intensity 1–10 | US-20, US-21, US-22 | | |
| OQ-13 | Default time range of evolution charts? | Last 3 months | US-22 | | |
| OQ-14 | Does "mobile" mean a responsive web app/PWA or a native app? CR-12 says "100% responsive", CONOPS v1.0 describes a mobile app component. | Responsive web app installable as a PWA | All `mobile` items | **Both**: a web application (computers) and a mobile application (phones and tablets), with the feature split of CONOPS v1.0 §4.2, which the `web`/`mobile` tags on Boards already follow. CR-12 (responsive design) still applies to the web application. Confirmed by the team as the approved CONOPS scope. | 2026-10-26 |
| OQ-15 | Is a patient's informed consent required before their notes are processed by an external AI service? Ecuador's LOPDP treats health data as a special category. | Record consent on the patient record; block AI processing without it | US-05, AI items | | |
| OQ-16 | Who may read the access audit log, and how long is it kept? | Clinic Administrator only; retained ≥ 5 years | Audit item | | |
| OQ-17 | AI provider terms: the client names OpenAI. Is a no-training / data-processing agreement required? Are names removed before sending text? | Send text without patient identifiers; use an API tier that does not train on inputs | AI items | | |
| OQ-18 | Does the Clinic Administrator have any access to clinical content? | No — administrators see therapist and patient *lists* only (CONOPS §3.1.1) | US-03/04, admin items | | |
| OQ-19 | Is bibliographic cross-reference (CR-10) in scope for this project? | Out of scope for SE I/II; kept as a `future` item | US-23 | | |
| OQ-20 | May the team publish the transcription of the client requirements and the elicitation evidence in a public repository (course requirement)? | Yes, without signatures or personal documents | Repository | | |
| OQ-21 | How long may the therapist wait for AI structuring before it counts as failed? Needed to meet the 3-minute target. | Result within 20 s for up to 5,000 characters; treated as failed after 30 s | US-15, US-16 | | |
| OQ-22 | Search response time? | ≤ 1 s with 500 patients per therapist | US-06 | | |
| OQ-23 | Password policy and recovery? | Minimum 10 characters; single-use reset link valid for 30 min | US-24 | | |
| OQ-24 | Which technology for the mobile application? CR-14 and CR-15 fix only the web client (`apps/web`, React + TypeScript). | React Native with Expo (TypeScript) in `apps/mobile`, sharing the API types and the `httpClient.ts` wrapper with `apps/web` | CR-14, all `mobile` items, SRS §2.4 | | |
| OQ-25 | How long may the introduction of a new therapist to the system take? | A demonstration of at most 15 min, after which the therapist creates a record and approves a note without help | NFR-04 | | |
| OQ-26 | What availability does the clinic need, and in which hours? | ≥ 99 % between 07:00 and 21:00, Monday to Saturday, Ecuador time | NFR-10, CR-13 | | |
| OQ-27 | How much data may be lost after a failure, and how fast must the service return? | Daily backups; at most 24 h of data lost; service restored within 4 h | NFR-12 | | |
| OQ-28 | How many people will use the system at the same time? | 20 concurrent users; screens load in ≤ 2 s | NFR-08 | | |
| OQ-29 | Which phone and tablet systems must the mobile application support? | Android 10 or later and iOS 15 or later | NFR-21 | | |
