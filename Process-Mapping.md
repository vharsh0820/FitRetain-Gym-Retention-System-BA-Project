[Process-Mapping-AS-IS-TO-BE.md](https://github.com/user-attachments/files/27351138/Process-Mapping-AS-IS-TO-BE.md)
# Process Mapping — AS-IS and TO-BE
## FitRetain — Gym Member Retention System

---

| Field | Details |
|-------|---------|
| **Document Version** | 1.0 |
| **Date** | May 2026 |
| **Prepared By** | Business Analyst |
| **Diagram Tool** | Draw.io (diagrams.net) |

---

## Purpose

This document describes the current (AS-IS) state of gym member retention processes and the improved (TO-BE) state enabled by FitRetain. It also provides a detailed guide on what each process diagram should include so you can build them accurately in Draw.io.

# PART 1 — AS-IS PROCESS (Current State)

## Overview

Today, most independent gyms in India manage member retention entirely through manual effort. There is no system to proactively detect disengagement. By the time an owner realises a member is gone, the opportunity to retain them has long passed.

---

## AS-IS Process 1: Member Joins the Gym

**Narrative:**
A new member walks into the gym, negotiates a plan with the owner, pays cash or via UPI, and their details are written in a physical register or a basic Excel sheet. No digital profile is created. No welcome message is sent. No membership card or portal access is provided.

**Steps:**
1. Prospect walks in / is referred.
2. Owner or staff verbally explains membership plans.
3. Member selects a plan and pays.
4. Staff writes name, phone, plan, and dates in a paper register or Excel.
5. Member starts visiting the gym.

**Pain Points:**
- Data is siloed (one register per gym, no backup).
- Member has no self-service access to their own information.
- No automated welcome or onboarding experience.
- Spelling errors, duplicate entries, and lost records are common.

---

## AS-IS Process 2: Attendance Tracking

**Narrative:**
Either staff verbally acknowledge a member's presence, or members sign in a biometric machine that only records entry time with no link to membership data.

**Steps:**
1. Member arrives at gym.
2. Member signs in a paper register or scans fingerprint on standalone biometric device.
3. No system connects attendance data to membership records or engagement scoring.
4. Trainer is unaware of how frequently members are attending.

**Pain Points:**
- Attendance data is completely disconnected from membership status.
- No visibility into "who hasn't come in 2 weeks."
- Trainers operate blind — no way to know if their assigned members are showing up.

---

## AS-IS Process 3: Member Disengagement (The Silent Dropout)

**Narrative:**
A member gradually reduces visits from 4x/week to 2x to 1x to zero — and no one notices in time. By week 3 or 4, the owner might remember to call, but the member has already mentally committed to leaving.

**Steps:**
1. Member begins missing sessions — no alert triggered.
2. Trainer may notice informally (if they happen to remember the member).
3. No structured outreach process — perhaps a generic WhatsApp broadcast is sent to all members.
4. Member stops coming altogether.
5. Owner calls the member at renewal time (1–2 months later) — far too late.
6. Member says "I'll think about it" or rejects the renewal.
7. Membership lapses. Owner moves on to finding a new member.

**Pain Points:**
- Zero proactive detection of at-risk behaviour.
- Outreach is reactive, not proactive.
- No personalised communication — only bulk WhatsApp messages.
- No record of whether any outreach was attempted or what the outcome was.

---

## AS-IS Process 4: Membership Renewal

**Narrative:**
The gym relies entirely on the member remembering to renew, or a receptionist manually checking expiry dates in a register and making phone calls — an inconsistent, time-intensive process.

**Steps:**
1. Receptionist manually scrolls through register or Excel to check expiry dates.
2. Receptionist calls members whose membership is expiring soon.
3. If the member picks up and agrees, they come in to pay (cash preferred).
4. If member doesn't pick up, a WhatsApp message may or may not be sent.
5. Many members lapse simply due to lack of a timely reminder.
6. No data is collected on why members choose not to renew.

**Pain Points:**
- Entirely manual and inconsistent.
- No centralised renewal pipeline or reminder system.
- No online payment option — member must physically visit.
- No exit data collected; the gym learns nothing from each churn.

---

---

# PART 2 — TO-BE PROCESS (Future State with FitRetain)

## Overview

FitRetain replaces every manual, reactive, and disconnected process with a structured, automated, and data-driven retention workflow. Each touchpoint is tracked, personalised, and measurable.

---

## TO-BE Process 1: Member Joins the Gym

**Steps:**
1. Staff (or member) fills the digital registration form on FitRetain.
2. System validates data, creates a unique Member ID, and sets membership expiry date automatically.
3. System sends a personalised welcome SMS to the member within 60 seconds.
4. Assigned trainer's dashboard is updated with the new member.
5. Member receives a QR code (via SMS link) for daily check-ins.

**Improvement:**
- 100% digital record — no paper, no data loss.
- Trainer is informed on Day 1.
- Member feels welcomed and onboarded professionally.

---

## TO-BE Process 2: Attendance Tracking

**Steps:**
1. Member arrives and scans QR code with their phone.
2. System logs attendance record instantly: Member ID + Timestamp.
3. "Last Visit Date" and "Days Since Last Visit" counters update in real time.
4. Churn risk scoring engine re-evaluates the member's risk level.
5. Trainer dashboard reflects the check-in; "At-Risk" badge is cleared if previously flagged.

**Improvement:**
- Zero manual effort — fully automated.
- Attendance is linked to membership and risk scoring.
- Trainers have real-time visibility into who is showing up.

---

## TO-BE Process 3: Proactive Churn Intervention

**Steps:**
1. Nightly risk engine scans all active members.
2. Member inactive 7 days → flagged "At Risk." Trainer notified. Day-7 message sent.
3. Member inactive 14 days → escalated "High Risk." Admin notified. Day-14 message sent.
4. Member inactive 21 days → "Critical." Owner notified. Day-21 final outreach sent. Manual task created for admin.
5. At each stage, personalised messages are sent via SMS/WhatsApp using the gym's custom templates.
6. If member checks in at any point → all flags cleared, campaign stopped.

**Improvement:**
- Intervention starts at Day 7, not Day 60.
- Every at-risk member receives 3 structured touchpoints before churning.
- Every action is logged — gym knows what was done and when.

---

## TO-BE Process 4: Membership Renewal

**Steps:**
1. System auto-sends renewal reminders at Day -30, -7, -1, and Day 0 (expiry day).
2. Each reminder contains a personalised renewal link.
3. Member clicks link → sees plan options → pays online (UPI / card).
4. On payment: membership extended, receipt emailed, admin dashboard updated in real time.
5. If not renewed by expiry → status auto-changes to Lapsed.
6. 24 hours after lapse → exit survey sent automatically.
7. Exit survey responses feed into admin analytics dashboard.

**Improvement:**
- Members can renew anytime, anywhere, without visiting the gym.
- Renewal rate expected to improve significantly due to timely, frictionless reminders.
- For the first time, the gym collects structured data on why members leave.

---

---

# PART 3 — DRAW.IO DIAGRAM GUIDE

Use this section as your reference when building diagrams in Draw.io (diagrams.net).

---

## Diagram 1: AS-IS Member Retention Flow

**Diagram Type:** Swimlane Flowchart (Cross-functional)

**Swimlanes (top to bottom):**
- Gym Member
- Reception / Staff
- Gym Owner / Trainer

**Shapes to Use:**
- Rounded rectangle = Process steps
- Diamond = Decision points
- Parallelogram = Data input/output
- Bold red border = Pain point step

**Key Nodes to Include:**
```
[Member Joins] → [Staff writes in register] → [Member starts visiting]
→ [Attendance via paper sign-in or biometric]
→ (Decision) Did member attend this week?
  → YES → [No action taken]
  → NO → [No alert triggered] → [Owner calls at renewal time]
→ (Decision) Does member renew?
  → YES → [Manual payment collected]
  → NO → [Member lost — no exit data] → END
```

**Pain Point Callouts (add sticky note shapes in red):**
- "No system detects absence"
- "Generic bulk WhatsApp, no personalisation"
- "No online payment option"
- "Zero exit data collected"

---

## Diagram 2: TO-BE Member Retention Flow

**Diagram Type:** Swimlane Flowchart (Cross-functional)

**Swimlanes (top to bottom):**
- Gym Member
- FitRetain System (Automated)
- Trainer
- Gym Admin / Owner

**Key Nodes to Include:**
```
[Member Registers on FitRetain] → [System creates profile + sends Welcome SMS]
→ [Member checks in via QR Code daily]
→ [System logs attendance + updates risk score nightly]
→ (Decision) DSLV >= 7?
  → NO → [Status: Engaged — no action]
  → YES → [Flag: At Risk] → [Notify Trainer] → [Send Day-7 Message]
    → (Decision) Member checks in?
      → YES → [Flag cleared — resume normal]
      → NO → (Decision) DSLV >= 14?
        → YES → [Escalate: High Risk] → [Notify Admin] → [Send Day-14 Message]
          → (Decision) DSLV >= 21?
            → YES → [Critical] → [Send Day-21 Message] → [Create manual follow-up task for Admin]
→ [System sends Renewal Reminders at -30, -7, -1 days]
→ (Decision) Member renews online?
  → YES → [Membership extended + Receipt sent] → END (success)
  → NO → [Status: Lapsed] → [Exit Survey sent after 24 hrs] → [Responses in Analytics]
```

**Improvement Callouts (add sticky note shapes in green):**
- "Intervention at Day 7, not Day 60"
- "Personalised automated messages"
- "Online renewal — no gym visit needed"
- "Exit data collected every time"

---

## Diagram 3: Churn Risk Engine — Decision Flow

**Diagram Type:** Standard Flowchart (single lane)

**Purpose:** Shows how the nightly batch job assigns risk levels.

**Key Nodes:**
```
START → [Run nightly at midnight]
→ [Fetch all Active members]
→ [Calculate DSLV for each member]
→ (Decision) DSLV < 7?
  → YES → [Set status: Engaged 🟢] → [No action] → [Next member]
  → NO → (Decision) DSLV 7–13?
    → YES → [Set status: At Risk 🟡] → [Notify Trainer] → [Queue Day-7 SMS]
    → NO → (Decision) DSLV 14–20?
      → YES → [Set status: High Risk 🔴] → [Notify Admin] → [Queue Day-14 SMS]
      → NO → [Set status: Critical ⚫] → [Notify Admin + Owner] → [Queue Day-21 SMS] → [Create follow-up task]
→ [Log risk change in member activity timeline]
→ (Decision) More members to process?
  → YES → [Next member]
  → NO → END
```

---

## Diagram 4: Membership Renewal Flow

**Diagram Type:** Swimlane Flowchart

**Swimlanes:**
- FitRetain System
- Gym Member
- Payment Gateway (Razorpay)
- Gym Admin

**Key Nodes:**
```
[System: Membership expiry in 30 days detected]
→ [Send SMS Reminder with renewal link]
→ [Member clicks link] → [Renewal page loads with plan options]
→ [Member selects plan and clicks Renew]
→ [Razorpay payment page]
→ (Decision) Payment success?
  → YES → [Membership extended] → [Receipt emailed] → [Admin dashboard updated] → END ✅
  → NO → [Show error + Retry button] → [Member retries or exits]
→ (Decision) Membership expires without renewal?
  → YES → [Status → Lapsed] → [24 hours later: Exit survey sent]
    → (Decision) Survey completed?
      → YES → [Responses logged in analytics]
      → NO → [Marked: No Response after 7 days]
```

---

## Draw.io Tips

| Element | Recommended Shape | Color |
|---------|------------------|-------|
| Process step | Rounded rectangle | Light blue (#DAE8FC) |
| Decision | Diamond | Light yellow (#FFF2CC) |
| Start / End | Oval | Dark green / Dark red |
| System automated action | Rectangle with double border | Light purple (#E1D5E7) |
| Pain point (AS-IS) | Sticky note | Red (#F8CECC) |
| Improvement (TO-BE) | Sticky note | Green (#D5E8D4) |
| Data store / log | Cylinder | Grey (#F5F5F5) |
| Swimlane header | Filled rectangle | Dark grey (#666666), white text |

**File naming for Draw.io exports:**
- `AS-IS-Retention-Flow.drawio`
- `TO-BE-Retention-Flow.drawio`
- `Churn-Risk-Engine-Flow.drawio`
- `Renewal-Flow.drawio`

Save `.drawio` files in the `/Process-Mapping/` folder alongside this document.

---

*End of Process Mapping Document — FitRetain v1.0*
