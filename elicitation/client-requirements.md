# Client requirements (CR)

English transcription of **"CogniSync – Requerimientos"**, written and electronically signed (FirmaEC) by Ing. Fabrizzio Ontaneda. Each requirement gets a stable ID (`CR-xx`) so user stories, the SRS and tests can trace back to it.

The signed original is kept outside this repository (it is mirrored publicly). Where wording is ambiguous, the original Spanish is quoted.

> Status: transcription by the team, 2026-10-26. Confirm with the client that publishing this content in the public mirror is acceptable — see [open questions](open-questions.md).

## 1. Vision

CogniSync is a SaaS system for the end-to-end management of mental-health clinics. Its goal is to drastically reduce therapists' administrative load through efficient digitization, AI automation of clinical notes (SOAP/DAP), and predictive analysis of patient evolution.

## 2. Functional requirements

| ID | Module | Name | Requirement |
|---|---|---|---|
| CR-01 | Authentication & authorization | Role management | The system must support role-based access control (RBAC) with at least two levels: *Administrator/Clinic* and *Therapist/User*. |
| CR-02 | Authentication & authorization | Secure authentication | The system must allow secure sign-in, issuing JWT tokens handled by the frontend authentication service. |
| CR-03 | Patients & scheduling | Digital record | The therapist must be able to create, read, update and archive patient profiles, including basic demographics and consultation history. |
| CR-04 | Patients & scheduling | Dropout alert | The system must analyze the patient's attendance and cancellation history and show a visual alert on the dashboard when there is a high risk of therapy dropout. |
| CR-05 | Clinical notes (core) | Capture flexibility | The system must allow post-session clinical notes to be recorded through (a) manual text input (quick summary), (b) voice dictation (audio-to-text transcription), (c) image upload (OCR to extract text from handwritten notebook notes). |
| CR-06 | Clinical notes (core) | Automatic structuring | The system must process raw notes or transcriptions with AI to structure them into standardized clinical formats (e.g., SOAP or DAP notes). |
| CR-07 | Clinical notes (core) | Context memory | The system must show a brief summary or "starting point" of the previous session when a new note is started for the same patient. |
| CR-08 | Analysis & evolution (AI) | Symptom extraction | The AI engine must identify, extract and automatically tag key symptoms (e.g., insomnia, panic attacks, ideation) mentioned in clinical notes. |
| CR-09 | Analysis & evolution (AI) | Longitudinal heat maps | The system must generate visual charts (heat maps or trend lines) showing the intensity and frequency of the patient's symptoms over time. |
| CR-10 | Analysis & evolution (AI) | Bibliographic cross-reference (**future**) | The system will let the professional consult therapy manuals and cross-reference them with the patient's symptoms to suggest intervention plans. |

## 3. Non-functional requirements

| ID | Category | Requirement |
|---|---|---|
| CR-11 | Privacy & security | Database identifiers for users, patients and notes must be non-enumerable (UUIDs) to prevent record enumeration (original: «inyectables u ofuscados (UUIDs)»). All connections must be encrypted (HTTPS). |
| CR-12 | Usability (UX/UI) | The interface must be minimalist and intuitive, ensuring post-session data entry takes **no more than 3 minutes per patient**. 100% responsive design for PC, tablets and phones. |
| CR-13 | Availability | The web system must be hosted on a VPS. |

## 4. Technical and architecture requirements

| ID | Topic | Requirement |
|---|---|---|
| CR-14 | Hybrid monorepo | Clear separation of the client (`apps/web`) and the API services (`apps/api`) in one repository. |
| CR-15 | Web frontend | React with TypeScript, styled with Tailwind CSS. Backend communication standardized through an `httpClient.ts` wrapper for end-to-end type safety. |
| CR-16 | Backend | Built entirely with FastAPI (Python): heavy business logic, orchestration of asynchronous calls to the OpenAI API (ChatGPT), JWT authentication and data persistence. |
| CR-17 | Relational database | PostgreSQL running natively on the server (port **5433** to avoid conflicts with existing Docker containers). Main tables: `roles`, `users`, `patients`, `clinical_notes`. Accessed from FastAPI through an ORM (e.g., SQLAlchemy) with schema migrations. |
| CR-18 | Deployment | Ubuntu VPS. Nginx as web server and reverse proxy handling SSL certificates and routing (`/api/*` → FastAPI, everything else → React static files). React served directly by Nginx. FastAPI runs as a native systemd service (Gunicorn with Uvicorn workers). |

## Traceability notes

- CR-14…CR-18 are **design constraints**, not user stories (they describe *how*, not user value).
- CR-11 and CR-12 apply to every story through the Definition of Done.
- The client document has no requirement for **appointments** or **note history**, yet CR-04 and CR-07 depend on them. The team covers these with gap stories; see Azure Boards, tag `gap`.
