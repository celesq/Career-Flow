<p align="center">
  <img src="assets/careerflow-banner.svg" alt="CareerFlow — from application chaos to your next best move" width="100%" />
</p>

<p align="center">
  <a href="#the-problem">The problem</a> ·
  <a href="#the-experience">The experience</a> ·
  <a href="#product-flows">Product flows</a> ·
  <a href="#ai-with-human-in-the-loop">AI + HITL</a> ·
  <a href="#architecture-proposal">Architecture</a> ·
  <a href="#roadmap">Roadmap</a>
</p>

<p align="center">
  <img alt="Project stage: UX design and MVP planning" src="https://img.shields.io/badge/stage-UX%20design%20%26%20MVP%20planning-5765E8?style=for-the-badge" />
  <img alt="Product category: Career technology" src="https://img.shields.io/badge/product-career%20tech-0D9488?style=for-the-badge" />
  <img alt="AI approach: Human-in-the-loop" src="https://img.shields.io/badge/AI-human--in--the--loop-8B5CF6?style=for-the-badge" />
</p>

<h1 align="center">CareerFlow</h1>
<p align="center"><strong>Every application has a next step. Now you can see it.</strong></p>
<p align="center">
  A candidate-first workspace for tracking job applications, preparing for interviews,
  and staying ahead of deadlines — without losing the details between emails, calendars, and spreadsheets.
</p>

> [!IMPORTANT]
> **Project status:** CareerFlow is currently presented here as a **product and UX concept with a proposed MVP**. The diagrams, screen layouts, architecture, and AI interactions below describe the intended experience; they are **not claims that these features are already implemented**.

---

## The problem

Searching for internships and graduate roles rarely means managing *one* application. It means dealing with overlapping hiring processes, assessments, recruiter replies, interviews in different time zones, and deadlines that live in different places.

Most trackers tell you **where you applied**. CareerFlow is designed to tell you **what you should do next**.

| The friction | CareerFlow's proposed answer |
| :-- | :-- |
| Application details are scattered across inboxes and tabs | One record per application, with links, notes, tasks, and history |
| Deadlines appear in different messages and time zones | A unified, timezone-aware list of upcoming actions |
| Pipeline spreadsheets become stale | An editable visual recruitment pipeline |
| Recruiter conversations are hard to reconstruct | A chronological activity timeline for each company |
| Manual updates take time | Optional AI-assisted extraction, **reviewed before saving** |

### The product promise

**Capture → Prioritize → Act → Remember.**

```mermaid
flowchart LR
    A["Capture<br/>an opportunity"] --> B["Track<br/>its stage"]
    B --> C["Prioritize<br/>the next action"]
    C --> D["Act<br/>before the deadline"]
    D --> E["Preserve<br/>the history"]
    E -.->|New event| B
    classDef primary fill:#1d2454,stroke:#6c74ef,color:#fff,stroke-width:1.5px;
    classDef secondary fill:#e9f9f6,stroke:#00a88e,color:#123f3a,stroke-width:1.5px;
    class A,B,C primary;
    class D,E secondary;
```

---

## Designed for real applicants

<table>
<tr>
<td width="50%" valign="top">

### 🎓 Alexandra — Internship applicant

A university student juggling several internship applications, coding assessments, and interview invitations.

**Needs:** A fast way to add an application, spot urgent deadlines, and get to the right assessment link.

**Key question:** *“What do I need to do today?”*

</td>
<td width="50%" valign="top">

### 💼 Andrei — Graduate job seeker

A recent graduate comparing junior opportunities across companies, locations, and hiring processes.

**Needs:** An accurate history of recruiter interactions, a clear interview schedule, and space for decision notes.

**Key question:** *“What happened last, and what happens next?”*

</td>
</tr>
</table>

These are **design personas**, not actual user accounts or research participants.

---

## The experience

### One workspace. Three complementary views.

| **01 — Today** | **02 — Pipeline** | **03 — Timeline** |
| :-- | :-- | :-- |
| Your action-first home screen | Your visual recruitment overview | Your record of what happened |
| Overdue items, upcoming assessments, interview preparation, follow-ups | Drag or move applications through hiring stages | Recruiter conversations, status changes, notes, links, and decisions |
| **Optimized for urgency** | **Optimized for overview** | **Optimized for context** |

### An illustrative first screen

*Conceptual wireframe — not a screenshot of a running application.*

```text
┌──────────────────────────────────────────────────────────────────────────┐
│  CAREERFLOW                                       + Add application      │
├────────────────┬─────────────────────────────────────────────────────────┤
│                │  Good morning. Here's what matters.                   │
│  ● Today       │                                                         │
│    Pipeline    │  03 Needs attention  ·  17 Active  ·  02 Interviews     │
│    Calendar    │                                                         │
│    Applications│  NEEDS ATTENTION                                        │
│                │  ┌─────────────────────────────────────────────────┐    │
│                │  │ Orbit Labs        Submit coding assessment     │    │
│                │  │ Backend Intern     Tomorrow · 18:00            │    │
│                │  └─────────────────────────────────────────────────┘    │
│                │  ┌─────────────────────────────────────────────────┐    │
│                │  │ Northstar         Prepare for technical round  │    │
│                │  │ SWE Graduate       Tuesday · 11:30 CET         │    │
│                │  └─────────────────────────────────────────────────┘    │
│                │                                                         │
│                │  UPCOMING                      PIPELINE SNAPSHOT        │
│                │  Thu · HR screen               Applied         7        │
│                │  Fri · Assessment              Assessment      4        │
│                │                                Interview       6        │
└────────────────┴─────────────────────────────────────────────────────────┘
```

### Interaction principles

- **Action-first, not spreadsheet-first.** The most relevant next step is easier to see than the full history.
- **Progressive disclosure.** A quick overview opens into detailed application information when needed.
- **Fast manual capture.** Company, role, URL, and stage are enough to create an application; the rest can come later.
- **Honest states.** Distinguish *recruitment stage* from *task status*. An application can be in `Interview` while its preparation task is still `To do`.
- **Clear time semantics.** Show event time zones, flag missing hours, and never silently invent a deadline.
- **User control by default.** Assistive AI can suggest changes; the candidate decides whether they are stored.

---

## Product flows

### 1. The candidate's daily loop

```mermaid
flowchart TD
    A["Open CareerFlow"] --> B["View Needs Attention"]
    B --> C{"What needs attention?"}
    C -->|"Deadline approaching"| D["Open the related application"]
    C -->|"Interview scheduled"| E["Review details and notes"]
    C -->|"No urgent action"| F["Browse pipeline"]
    D --> G["Complete or reschedule task"]
    E --> G
    F --> H["Update application stage"]
    G --> I["Record activity in timeline"]
    H --> I
    I --> J["Recalculate next actions"]
    J --> B
    classDef action fill:#eaf3ff,stroke:#4787ec,color:#123053;
    classDef done fill:#dff9ef,stroke:#13a779,color:#124735;
    class D,E,F,G,H action;
    class I,J done;
```

### 2. Recruitment pipeline — stages are not tasks

```mermaid
stateDiagram-v2
    [*] --> Saved
    Saved --> Applied: Submit application
    Applied --> Assessment: Test invitation
    Applied --> Interview: Direct interview
    Assessment --> Interview: Advance
    Interview --> Interview: Another round
    Interview --> Offer: Offer received
    Offer --> Accepted: Accept
    Offer --> Declined: Decline
    Applied --> Rejected: Process ends
    Assessment --> Rejected: Process ends
    Interview --> Rejected: Process ends
    Saved --> Closed: Archive
    Applied --> Closed: Withdraw
    Rejected --> [*]
    Accepted --> [*]
    Declined --> [*]
    Closed --> [*]
```

> A hiring *stage* describes where the application stands. An *action item* describes what the candidate must do. The two are deliberately modeled separately.

### 3. From recruiter update to completed task

```mermaid
sequenceDiagram
    autonumber
    actor Candidate
    participant UI as CareerFlow
    participant App as Application record
    participant Tasks as Task list
    Candidate->>UI: Open an application
    UI->>App: Load current stage and history
    App-->>UI: Stage, activity, links, notes
    Candidate->>UI: Add assessment deadline
    UI->>Tasks: Create action item
    Tasks-->>UI: Deadline and status saved
    UI-->>Candidate: Show item in Needs Attention
    Candidate->>UI: Mark assessment complete
    UI->>Tasks: Complete action item
    UI->>App: Append activity event
    UI-->>Candidate: Updated timeline and next actions
```

---

## AI with Human-in-the-Loop

### Useful assistance. No silent edits.

The proposed AI feature is designed to reduce repetitive typing, **not** to take control of the job search.

A candidate could **paste a recruiter email** or **upload a selected document**. CareerFlow would suggest structured data — company, role, hiring stage, interview time, assessment deadline, and a possible next action. Before anything is saved, the candidate sees the **source, proposed changes, and editable fields**.

```mermaid
flowchart TD
    A["User-selected email text or file"] --> B["AI extracts candidate fields"]
    B --> C["Validate dates, time zones and context"]
    C --> D["Show source-backed proposed changes"]
    D --> E{"Human review"}
    E -->|"Approve"| F["Commit confirmed fields"]
    E -->|"Edit"| G["Correct values in review form"]
    G --> E
    E -->|"Reject"| H["Discard draft; change nothing"]
    F --> I["Update task and application history"]
    classDef ai fill:#f0e9ff,stroke:#8a61d7,color:#422576;
    classDef human fill:#e5f5ff,stroke:#2687c0,color:#134664;
    classDef success fill:#def9e9,stroke:#20a56e,color:#0b5132;
    classDef reject fill:#fff0f0,stroke:#d85e5e,color:#742626;
    class B,C,D ai;
    class E,G human;
    class F,I success;
    class H reject;
```

#### An example of the proposed review experience

| Field | Current value | AI suggestion | Candidate decision |
| :-- | :-- | :-- | :-- |
| Stage | Applied | Assessment | Approve / edit / reject |
| Next action | — | Complete coding test | Approve / edit / reject |
| Deadline | — | Fri, 17:00 CET | Approve / edit / reject |
| Source | — | Selected recruiter email | Inspect excerpt |

**The trust contract**

1. **Nothing is committed before confirmation.** Parsing is not permission to modify application data.
2. **Provenance stays visible.** The user can inspect where a suggested date or stage came from.
3. **Uncertainty is surfaced.** If an email says “Friday” without an unambiguous date or time zone, the system asks rather than guessing.
4. **Edits are reversible.** Application changes belong in an auditable timeline; undo is a product goal.
5. **External actions require separate approval.** Sending emails, scheduling on external calendars, or acting in third-party services are **not autonomous MVP features**.
6. **No inbox access is required for the initial AI concept.** User-selected text or a file is enough to test the interaction.

---

## Architecture proposal

A deliberately small architecture suits a two-person student project. A React UI with a repository/service layer and **local persistence or a mock API** is enough to validate the core experience. A backend or hosted database can be added when needed; external integrations are not prerequisites for the first usable version.

```mermaid
flowchart TB
    subgraph UI["Presentation layer · proposed"]
        Today["Today / Needs Attention"]
        Pipe["Pipeline"]
        Detail["Application details / Timeline"]
        Cal["Calendar"]
        Review["AI review dialog · optional"]
    end
    subgraph Logic["Domain and application logic"]
        AppService["Application service"]
        TaskService["Task & deadline service"]
        EventService["Activity history"]
        ProposalService["AI proposal / approval logic"]
    end
    subgraph Data["Persistence · choose for MVP"]
        Repo["Repository abstraction"]
        Local["Local storage / mock API"]
        API["Backend API · future option"]
    end
    subgraph Opt["Optional AI adapter"]
        Extract["Text / document extraction"]
    end
    Today --> TaskService
    Pipe --> AppService
    Detail --> AppService
    Detail --> EventService
    Cal --> TaskService
    Review --> ProposalService
    AppService --> Repo
    TaskService --> Repo
    EventService --> Repo
    ProposalService --> Repo
    ProposalService -. "suggestion only" .-> Extract
    Repo --> Local
    Repo -. "later" .-> API
    classDef optional fill:#f6eeff,stroke:#a78bfa,color:#51318a;
    class Extract,Review,ProposalService,API optional;
```

### Candidate domain model

```mermaid
erDiagram
    APPLICATION ||--o{ ACTION_ITEM : has
    APPLICATION ||--o{ ACTIVITY_EVENT : records
    APPLICATION ||--o{ RESOURCE : references
    APPLICATION {
        string id
        string company
        string role
        string stage
        string location
        string job_url
    }
    ACTION_ITEM {
        string id
        string application_id
        string title
        datetime due_at
        string timezone
        string status
    }
    ACTIVITY_EVENT {
        string id
        string application_id
        datetime occurred_at
        string event_type
        string note
    }
    RESOURCE {
        string id
        string application_id
        string label
        string url
        string kind
    }
```

> **Design proposal, not an existing database schema.** An AI extraction draft should remain separate from the saved application until the user approves it.

---

## MVP scope

The core product should remain useful even if the AI layer is never enabled.

| Capability | Priority | Proposed release |
| :-- | :--: | :-- |
| Add, edit, and archive job applications | **P0** | MVP |
| Recruitment stages and pipeline view | **P0** | MVP |
| Next action and due date per application | **P0** | MVP |
| Needs Attention dashboard | **P0** | MVP |
| Application detail view with activity timeline | **P0** | MVP |
| Interview and deadline overview | **P0** | MVP |
| Filters, notes, links, and timezone handling | **P1** | MVP if time allows |
| Paste text → AI suggestion → review → save | **P2** | Optional extension |
| Gmail/Outlook connection and inbox synchronization | **Later** | Post-MVP |
| Two-way calendar synchronization | **Later** | Post-MVP |
| Advanced analytics and offer comparison | **Later** | Post-MVP |

### Non-goals for the first release

No automatic job applications, autonomous recruiter messages, invisible AI database updates, scraping-dependent workflows, or complex email-account permissions. These add substantial reliability and privacy costs without being necessary to validate CareerFlow's core value.

---

## Roadmap

This is a **proposed delivery sequence** for a 13-week university project, not a completed milestone history.

```mermaid
flowchart LR
    A["01<br/>Discover<br/>Personas & needs"] --> B["02<br/>Design<br/>Flows & Figma prototype"]
    B --> C["03<br/>Build<br/>Core application"]
    C --> D["04<br/>Validate<br/>Usability tests"]
    D --> E["05<br/>Polish<br/>Accessibility & demo"]
    E -. "If capacity remains" .-> F["06<br/>Explore<br/>AI + HITL"]
    classDef core fill:#eaf2ff,stroke:#5b79da,color:#1e3975,stroke-width:1.5px;
    classDef optional fill:#f4eaff,stroke:#9069ca,color:#4e2f78,stroke-dasharray:4 3;
    class A,B,C,D,E core;
    class F optional;
```

<details>
<summary><strong>Suggested milestone checklist</strong></summary>

- [ ] Interview potential users; refine the two personas and user stories.
- [ ] Map navigation, information architecture, empty states, and error states.
- [ ] Build an interactive Figma prototype and run initial usability tests.
- [ ] Implement application records and manual add/edit flows.
- [ ] Implement pipeline, action items, and activity timeline.
- [ ] Implement urgency sorting and a compact calendar overview.
- [ ] Run task-based usability sessions and address the biggest issues.
- [ ] Improve keyboard support, responsive layouts, and validation messages.
- [ ] If feasible, prototype AI extraction with explicit approval and rejection.

</details>

---

## UX validation plan

Design decisions should be tested against observable behavior, not just visual preference.

| User task | Proposed success criterion |
| :-- | :-- |
| Add a new application | Candidate completes the flow in **≤ 60 seconds** |
| Find the most urgent pending task | Correct item identified in **≤ 10 seconds** |
| Update an application's stage | Completed in **≤ 3 interactions** |
| Recall the last recruiter interaction | Candidate locates the relevant timeline event without consulting email |
| Review an AI-generated change | Candidate can inspect, correct, approve, or discard it before any data is saved |

*These are design targets for future testing, **not measured product results**.*

### Accessibility and reliability considerations

- Clear text labels alongside color-coded stages; color alone must not communicate status.
- Keyboard navigation and visible focus states for critical actions.
- Legible countdowns and explicit time zones for deadlines.
- Useful empty, loading, error, and undo states.
- Mobile-friendly capture, with desktop-friendly multi-application views.
- Explicit consent and careful handling of recruitment emails and personal data.

---

## Development status & setup

CareerFlow is documented here as a **design-led product concept**. Once the repository contains an executable application, this section should describe the actual framework, prerequisites, installation commands, environment variables, and run/test scripts. No unverified setup commands are included here.

The architecture is intentionally flexible: **React is a proposed frontend option**, not a claim about the current codebase.

---

## Team

Built as a Human–Computer Interaction (IOC/HCI) university project by:

- **Rareș-Andrei Celescu**
- **Matei-Ovidiu Tudose**

**University POLITEHNICA of Bucharest · Faculty of Automatic Control and Computers · Group 342C4**

---

<p align="center">
  <strong>Less tracking. More progress.</strong><br/>
  <sub>CareerFlow — make the next move obvious.</sub>
</p>
