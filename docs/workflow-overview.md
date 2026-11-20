# Workflow overview

```mermaid
flowchart LR
    A[Run manually] --> B[1. Fictional<br/>refit requests]
    B --> C[2. Normalize and check<br/>missing details]
    C --> D[3. Categorize<br/>keyword rules]
    D --> E[4. Project summary<br/>and checklist]
    E --> F{Complete<br/>intake?}
    F -- yes --> G[5a. Draft status<br/>update]
    F -- no --> H[5b. Draft request<br/>for missing details]
    G --> I[Human review gate<br/>PENDING_HUMAN_REVIEW]
    H --> I
    I --> J[Review queue<br/>read this output]
```

## What each step adds

| Step | Adds to the record |
|---|---|
| 1 | The raw made-up request |
| 2 | `request` (tidied), `missing_fields`, `is_complete` |
| 3 | `classification`: project types with matched words, urgency with reasons |
| 4 | `project_summary` and `next_steps` (each with an owner role) |
| 5a / 5b | `draft_status_update` |
| Gate | `approval`: `PENDING_HUMAN_REVIEW`, `message_sent: false` |
| Last | One tidy record, with a one-line `summary` on top |

## What it never does

Cost estimates, vendor selection, timeline promises, approval of work, and sending messages. The final record lists these under `not_done_by_this_workflow`.

## Where to change the rules

- Required details: node 2.
- Project types, keywords and urgency words: node 3 (the lists at the top).
- Checklist steps: node 4.
- Draft wording: nodes 5a and 5b.
