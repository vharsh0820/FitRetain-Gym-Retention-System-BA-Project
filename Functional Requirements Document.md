[Functional-Requirements-Document.md](https://github.com/user-attachments/files/27351044/Functional-Requirements-Document.md)
# Functional Requirements Document (FRD)
## FitRetain — Gym Member Retention System

---

| Field | Details |
|-------|---------|
| **Document Version** | 1.0 |
| **Date** | May 2026 |
| **Prepared By** | Business Analyst |
| **Linked BRD** | BRD v1.0 — FitRetain |
| **Status** | Ready for Technical Review |

---

## Overview

This document breaks down each system feature into functional specifications: what inputs it accepts, how it processes them, and what outputs it produces. It is intended as the primary requirements handoff artifact to the product manager and engineering team.

---

## Feature Index

| Feature ID | Feature Name | Linked BR |
|------------|-------------|-----------|
| F-01 | Member Registration and Profile | BR-01 |
| F-02 | Attendance Tracking (QR + Manual) | BR-02 |
| F-03 | Churn Risk Scoring Engine | BR-03 |
| F-04 | Automated Re-engagement Campaigns | BR-04 |
| F-05 | Membership Renewal Reminders | BR-05 |
| F-06 | Trainer Dashboard | BR-06 |
| F-07 | Exit and Cancellation Survey | BR-07 |
| F-08 | Admin Analytics Dashboard | BR-08 |
| F-09 | Online Membership Renewal and Payment | BR-09 |
| F-10 | Role-Based Access Control | BR-10 |

---

## F-01 — Member Registration and Profile

**Description:**
Enables new members to be onboarded into the system by reception staff or self-registration, creating a persistent digital profile tied to their membership.

**Inputs:**
- Full name (mandatory)
- Mobile number (mandatory, unique)
- Date of birth (mandatory)
- Gender (mandatory)
- Membership plan selected (e.g., Monthly / Quarterly / Annual)
- Membership start date (mandatory)
- Assigned personal trainer (optional)
- Fitness goal (dropdown: Weight Loss / Muscle Gain / Endurance / General Fitness)
- Emergency contact number (optional)
- Profile photo (optional)

**Process:**
1. Reception staff or member accesses registration form.
2. System validates mobile number uniqueness (no duplicate accounts).
3. System assigns a unique Member ID (MBXXX format) upon submission.
4. System calculates membership expiry date based on plan duration + start date.
5. System sends welcome SMS to member: "Welcome to [Gym Name]! Your Member ID is MBXXX. Track your fitness journey on FitRetain."
6. Member profile is created with status: **Active**.
7. If a trainer is assigned, trainer's dashboard is updated with new member.

**Outputs:**
- Active member profile with Member ID
- Welcome SMS to member
- Trainer dashboard updated (if assigned)
- Member appears in admin's active member list

**Business Rules:**
- One mobile number = one member account.
- Membership expiry is auto-calculated: Monthly = 30 days, Quarterly = 90 days, Annual = 365 days.
- A member with an expired membership retains profile but status changes to **Lapsed**.

---

## F-02 — Attendance Tracking

**Description:**
Records each member visit digitally to enable accurate engagement monitoring and churn risk calculation.

**Inputs:**
- Member ID (via QR code scan or manual entry)
- Timestamp (auto-captured by system)
- Check-in method: QR Scan / Manual by Staff

**Process:**
1. Member scans QR code at gym entry using mobile camera, OR receptionist enters Member ID manually.
2. System validates Member ID.
3. System checks membership status — if **Expired**, check-in is blocked and alert shown: "Membership expired. Please renew to continue."
4. If **Active**, system logs attendance record: Member ID + Date + Time + Check-in method.
5. System updates "Last Visit Date" on member profile in real time.
6. System recalculates "Days Since Last Visit" counter and updates churn risk status if threshold is crossed.

**Outputs:**
- Attendance record logged in member history
- Last Visit Date updated on profile
- "Days Since Last Visit" counter refreshed
- If member was previously flagged as At-Risk and now checks in → risk flag auto-cleared

**Business Rules:**
- Only one attendance entry per member per calendar day.
- Attendance cannot be backdated by more than 1 day (admin override required for corrections).
- Members with Lapsed or Suspended status cannot check in.

---

## F-03 — Churn Risk Scoring Engine

**Description:**
An automated background engine that continuously monitors member attendance and assigns a risk score to flag disengaged members before they churn.

**Inputs (System-generated, no manual input):**
- Days Since Last Visit (from attendance records)
- Membership expiry date
- Historical attendance frequency (visits per week, rolling 4 weeks)
- Previous churn flag history

**Process:**
1. System runs risk scoring job every 24 hours at midnight.
2. For each active member, system calculates Days Since Last Visit (DSLV).
3. Risk Score is assigned based on the following logic:

| DSLV | Risk Level | Action Triggered |
|------|------------|-----------------|
| 0–6 days | 🟢 Engaged | No action |
| 7–13 days | 🟡 At Risk | Trainer notified; Day-7 re-engagement message sent |
| 14–20 days | 🔴 High Risk | Admin notified; Day-14 escalation message sent |
| 21+ days | ⚫ Critical | Admin + Owner notified; Day-21 final outreach sent |

4. Risk level is displayed on the member's profile card and on the admin/trainer dashboard.
5. System logs each risk level change in the member's activity timeline.
6. If a member checks in after being flagged, risk level resets to Engaged.

**Outputs:**
- Risk level badge updated on member profile
- Dashboard counts updated (e.g., "12 members At Risk today")
- Notifications dispatched to trainer / admin based on risk level
- Re-engagement campaign triggered (linked to F-04)

**Business Rules:**
- Trainers can manually dismiss an At-Risk flag for a member with a documented reason (e.g., "Member traveling — confirmed via WhatsApp").
- Members whose membership expires in ≤ 7 days are always shown in the renewal pipeline regardless of attendance.
- The engine does not run on members with Lapsed, Suspended, or Paused status.

---

## F-04 — Automated Re-engagement Campaigns

**Description:**
Sends pre-configured outreach messages to at-risk members at defined intervals to encourage them to return to the gym.

**Inputs:**
- Member risk level (from F-03)
- Member mobile number and name
- Gym admin's configured message templates
- Campaign trigger schedule (Day 7 / Day 14 / Day 21)

**Process:**
1. When churn risk engine (F-03) flags a member, it queues a campaign trigger.
2. System selects the message template mapped to the risk level (configurable by admin).
3. System personalizes message by injecting member's first name and gym name.
4. Message is dispatched via SMS and/or WhatsApp (based on admin's channel preference).
5. System logs: message sent, timestamp, channel, delivery status.
6. If member checks in after receiving a message, campaign sequence stops automatically.
7. If member does not respond after Day 21 message, system creates a manual follow-up task for gym admin.

**Default Message Templates (editable by admin):**

| Trigger | Sample Message |
|---------|---------------|
| Day 7 | "Hi [Name], we miss you at [Gym]! It's been a week — come back and crush your goals. Your trainer [Trainer Name] is looking forward to seeing you. 💪" |
| Day 14 | "Hey [Name], it's been 2 weeks since your last visit. Don't let your progress slip! Book a session this week and we'll make it worth it." |
| Day 21 | "Hi [Name], we'd love to have you back. Reply YES and we'll have your trainer call you today to plan your comeback session." |

**Outputs:**
- Message delivered to member (SMS/WhatsApp)
- Campaign log entry: member ID, trigger day, channel, status (Delivered / Failed / Opened)
- Admin dashboard shows campaign performance: messages sent, delivery rate, re-engagement rate

**Business Rules:**
- A member receives a maximum of 3 automated messages per inactive period.
- If a member explicitly opts out of messages, they are removed from all campaign queues immediately.
- Campaign messages are not sent between 10 PM and 8 AM.
- Admin can pause the campaign engine globally (e.g., during gym holidays).

---

## F-05 — Membership Renewal Reminders

**Description:**
Proactively notifies members of upcoming membership expiry and drives online renewals.

**Inputs:**
- Membership expiry date (from member profile)
- Member contact details
- Renewal plan options (from admin-configured plan catalog)

**Process:**
1. System runs a daily check for memberships expiring in the next 30 days.
2. Automated reminders sent at:
   - **30 days before expiry:** Friendly early reminder with renewal link.
   - **7 days before expiry:** Urgency nudge with plan options.
   - **1 day before expiry:** Final reminder with quick-pay link.
   - **Day of expiry:** "Your membership expires today — renew now to avoid interruption."
3. Member clicks renewal link → directed to self-service renewal page (F-09).
4. On successful renewal, membership expiry date is extended and confirmation SMS sent.
5. If not renewed by expiry date, membership status changes to **Lapsed** and member is removed from active list.

**Outputs:**
- Reminder messages at each configured touchpoint
- Renewal pipeline in admin dashboard showing: Member Name, Expiry Date, Reminder Status, Renewed (Yes/No)
- Status auto-updated to Lapsed on expiry date if not renewed

**Business Rules:**
- If a member renews early (e.g., 20 days before expiry), remaining days carry forward.
- A Lapsed member can be reactivated within 30 days without losing their profile history.
- Renewal reminder messages use the same opt-out mechanism as campaign messages.

---

## F-06 — Trainer Dashboard

**Description:**
Provides personal trainers with a focused view of their assigned members' engagement and risk status.

**Inputs:**
- Trainer login credentials
- Assigned member list (configured by admin)
- Member attendance data (read-only feed from F-02)
- Trainer check-in notes (text input, max 300 characters)

**Process:**
1. Trainer logs in and lands on their personal dashboard.
2. Dashboard displays assigned member cards, each showing:
   - Member name and photo
   - Last visit date and days since last visit
   - Current risk level (colour-coded: Green / Yellow / Red / Black)
   - Membership expiry date
3. Trainer can click any member card to view:
   - Full attendance history (last 90 days)
   - Goal set at registration
   - Notes log
4. Trainer can add a check-in note (e.g., "Spoke to member — traveling until June 15, will return").
5. Trainer can dismiss an At-Risk flag with a mandatory reason logged.
6. Dashboard shows alerts for: new at-risk flags, memberships expiring in ≤ 7 days.

**Outputs:**
- Real-time view of assigned member engagement status
- Notes logged with timestamp and trainer name
- Flag dismissals recorded with reason (visible to admin)

**Business Rules:**
- Trainers can only view their assigned members, not the full gym roster.
- Notes added by trainers are visible to admin but not to the member.
- Trainers cannot modify member profiles or financial data.

---

## F-07 — Exit and Cancellation Survey

**Description:**
Captures structured feedback from members who cancel or do not renew, building a data foundation for retention improvement.

**Inputs:**
- Trigger: Membership status changes to Lapsed or Cancelled
- Member mobile number and email

**Process:**
1. When a membership expires without renewal or is manually cancelled by admin, system waits 24 hours then sends exit survey via SMS link.
2. Survey contains 5 questions (mobile-optimised, < 2 minutes to complete):
   - Q1: Why did you stop coming? (Multiple choice: Schedule conflict / Cost / Achieved goal / Moved location / Dissatisfied with trainers / Other)
   - Q2: How satisfied were you overall? (1–5 stars)
   - Q3: Did your trainer help you achieve your goals? (Yes / Partially / No / I didn't have a trainer)
   - Q4: What would have made you stay? (Open text, optional)
   - Q5: Would you recommend [Gym Name] to a friend? (NPS: 0–10)
3. Responses are stored against the member record.
4. Survey expires after 7 days (no response = recorded as "No Response").

**Outputs:**
- Survey responses stored in member record
- Admin analytics dashboard aggregates:
   - Top reasons for cancellation
   - Average satisfaction score of exiting members
   - NPS score trend (monthly)
   - Trainer satisfaction scores

**Business Rules:**
- Survey is sent only once per membership period.
- Survey responses are anonymous in public-facing reports but linked to member ID internally for quality review.
- If member reactivates within 30 days, survey responses are retained in their history.

---

## F-08 — Admin Analytics Dashboard

**Description:**
Provides gym owners and admins with a real-time, visual summary of retention performance and operational health.

**Inputs:**
- All member, attendance, campaign, renewal, and survey data (system-generated)
- Date range filter (Today / This Week / This Month / Custom)

**Process:**
1. Admin logs in and lands on analytics home page.
2. Dashboard renders key metric tiles:
   - Total Active Members
   - Members At Risk (7–13 days inactive)
   - Members High Risk (14+ days inactive)
   - Memberships Expiring This Month
   - Renewal Rate (%) this month
   - Churn Rate (%) this month
3. Charts available:
   - Attendance trend (line chart — daily check-ins over 30 days)
   - Retention funnel (joined → active → renewed → churned)
   - Churn reason breakdown (pie chart from exit surveys)
   - Trainer-wise retention comparison (bar chart)
4. Renewal pipeline table: lists all members expiring in next 30 days with renewal status.
5. Admin can export any report to CSV or PDF.

**Outputs:**
- Real-time dashboard view
- Downloadable CSV/PDF reports
- Email-scheduled weekly report (optional, configurable)

**Business Rules:**
- Financial data (revenue) visible only to Owner role, not Admin or Trainer.
- Dashboard data refreshes every 15 minutes.
- Historical data retained for 24 months.

---

## F-09 — Online Membership Renewal and Payment

**Description:**
Allows members to renew their membership online without visiting the gym, reducing drop-off at renewal time.

**Inputs:**
- Member ID (auto-filled from login or reminder link)
- Selected renewal plan
- Payment method (UPI / Debit/Credit Card / Net Banking)

**Process:**
1. Member accesses renewal page via reminder link or member portal.
2. System displays current membership details and available renewal plans with pricing.
3. Member selects plan and clicks "Renew Now."
4. System redirects to Razorpay payment gateway.
5. On payment success:
   - Membership expiry date extended from current expiry (or today if already lapsed).
   - Payment receipt generated and emailed.
   - Member status updated to Active (if was Lapsed).
   - Admin notified of renewal.
6. On payment failure: member sees error message with retry option.

**Outputs:**
- Extended membership with updated expiry date
- Digital receipt via email and SMS
- Admin renewal log updated
- Member status set to Active

**Business Rules:**
- If a member renews before expiry, new period starts from current expiry date (days are not lost).
- Renewals made within 30 days of lapsing retain original profile and history.
- Partial payments are not supported — full plan fee must be paid.

---

## F-10 — Role-Based Access Control (RBAC)

**Description:**
Ensures each user type sees and can do only what their role permits, protecting member data and business-sensitive information.

**Roles and Permissions Matrix:**

| Feature / Data | Member | Trainer | Admin | Owner |
|----------------|--------|---------|-------|-------|
| View own profile | ✅ | — | ✅ | ✅ |
| View all member profiles | ❌ | Assigned only | ✅ | ✅ |
| Log attendance | ❌ | ❌ | ✅ | ✅ |
| Add trainer notes | ❌ | ✅ | ✅ | ✅ |
| Dismiss churn risk flag | ❌ | ✅ | ✅ | ✅ |
| Configure message templates | ❌ | ❌ | ✅ | ✅ |
| View retention analytics | ❌ | ❌ | ✅ | ✅ |
| View revenue reports | ❌ | ❌ | ❌ | ✅ |
| Manage gym settings | ❌ | ❌ | ✅ | ✅ |
| Manage staff accounts | ❌ | ❌ | ✅ | ✅ |

**Process:**
1. User logs in with credentials.
2. System identifies role from user record.
3. Navigation menus, data views, and action buttons are rendered based on role permissions.
4. Any direct URL access to unauthorized resources returns a 403 Forbidden response.

**Business Rules:**
- Roles are assigned by the Owner or Admin at account creation.
- A single user cannot hold multiple roles.
- Role changes take effect at next login.

---

*End of Functional Requirements Document — FitRetain v1.0*
