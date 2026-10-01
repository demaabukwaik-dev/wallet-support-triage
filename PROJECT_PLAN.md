# Project Plan: Wallet Support Triage

## Workflow

### Agent flow

```mermaid
flowchart TD
    A[Customer submits form] --> B{Input valid?}
    B -- no --> B1[Show error, no ticket]
    B -- yes --> C[Masking]
    C --> D[Security prompt]
    D --> E[Classification prompt]
    E --> F{Python policy}
    F -- invalid output --> ESC[escalate]
    F -- sensitive data --> ESC
    F -- security flag --> ESC
    F -- multiple issues --> ESC
    F -- other --> ESC
    F -- refund not issued --> ESC
    F -- missing, followup_count = 0 --> ASK[ask_for_info]
    F -- missing, followup_count = 1 --> ESC
    F -- complete --> DR[draft_response]
    DR --> DC{Draft safety check}
    DC -- fails --> ESC
    DC -- passes --> S
    ESC --> S[Save / update ticket]
    ASK --> S
    S --> Q{New ticket?}
    Q -- yes --> M[Send acknowledgement email]
    Q -- no --> END[Done]
    M --> AK[Update ack_sent]
    ASK -. customer replies .-> C
```

---

### Ticket lifecycle

```mermaid
flowchart LR
    START([Agent decision]) -- ask_for_info --> W[Waiting for Info]
    START -- draft_response --> PR[Pending Review]
    START -- escalate --> ESC[Escalated]
    W -- customer replies, flow re-runs --> PR
    W -- customer replies, flow re-runs --> ESC
    W -- no reply + close_note --> CL[Closed]
    PR -- approve / edit / reject + own reply --> CL
    PR -- reject + close_note --> CL
    PR -- reject, needs follow-up --> ESC
    ESC -- staff resolves --> CL
    ESC -- staff closes + close_note --> CL
```

---

| Action | Status |
|---|---|
| ask_for_info | Waiting for Info |
| draft_response | Pending Review |
| escalate | Escalated |