[User-Stories-and-Acceptance-Criteria.md](https://github.com/user-attachments/files/27351101/User-Stories-and-Acceptance-Criteria.md)
# User Stories and Acceptance Criteria
## FitRetain — Gym Member Retention System

---

| Field | Details |
|-------|---------|
| **Document Version** | 1.0 |
| **Date** | May 2026 |
| **Prepared By** | Business Analyst |
| **Methodology** | Agile — Scrum |
| **Total Stories** | 15 |

---

## Story Format

> **As a** [role], **I want to** [action/feature], **so that** [business value/benefit].
>
> **Acceptance Criteria** use the **Given-When-Then** format.

---

## US-01 — Member Self-Registration

**Role:** Gym Member
**Priority:** High | **Sprint:** 1

> As a **new gym member**, I want to **register my profile on the FitRetain portal**, so that **I can digitally manage my membership and track my attendance**.

**Acceptance Criteria:**

**Scenario 1 — Successful Registration**
- **Given** I am a new member with a valid mobile number not already in the system
- **When** I submit the registration form with my name, mobile number, date of birth, and membership plan
- **Then** the system creates my profile with a unique Member ID, sets my membership status to Active, and sends me a welcome SMS within 60 seconds

**Scenario 2 — Duplicate Mobile Number**
- **Given** I enter a mobile number already linked to an existing account
- **When** I submit the registration form
- **Then** the system displays an error: "This mobile number is already registered. Please log in or contact the gym admin."

**Scenario 3 — Mandatory Field Missing**
- **Given** I leave the "Date of Birth" field empty
- **When** I click Submit
- **Then** the form highlights the missing field with a red border and displays "This field is required." Registration does not proceed.

---

## US-02 — Member Login via OTP

**Role:** Gym Member
**Priority:** High | **Sprint:** 1

> As a **registered gym member**, I want to **log in using my mobile number and OTP**, so that **I can securely access my profile without remembering a password**.

**Acceptance Criteria:**

**Scenario 1 — Successful OTP Login**
- **Given** I enter my registered mobile number and request an OTP
- **When** I receive and correctly enter the 6-digit OTP within 5 minutes
- **Then** I am logged in and redirected to my member dashboard

**Scenario 2 — OTP Expiry**
- **Given** I receive an OTP but do not use it within 5 minutes
- **When** I enter the expired OTP
- **Then** the system shows "OTP has expired. Please request a new one." and allows me to resend

**Scenario 3 — Wrong OTP (3 Attempts)**
- **Given** I enter an incorrect OTP three times consecutively
- **When** the third incorrect attempt is made
- **Then** the system locks OTP login for 15 minutes and displays "Too many failed attempts. Try again after 15 minutes."

---

## US-03 — QR Code Attendance Check-In

**Role:** Gym Member
**Priority:** High | **Sprint:** 1

> As a **gym member**, I want to **check in by scanning a QR code at the gym entrance**, so that **my attendance is recorded automatically without any manual effort**.

**Acceptance Criteria:**

**Scenario 1 — Successful Check-In**
- **Given** I am an active member with a valid membership
- **When** I scan the gym's QR code with my mobile camera
- **Then** the system logs my attendance with the current timestamp, updates my "Last Visit Date," and displays a confirmation screen: "Welcome back, [Name]! 💪 Checked in at 7:03 AM."

**Scenario 2 — Duplicate Check-In Same Day**
- **Given** I have already checked in today
- **When** I scan the QR code again on the same day
- **Then** the system displays "You've already checked in today. Enjoy your workout!" and does not create a duplicate attendance record.

**Scenario 3 — Expired Membership**
- **Given** my membership has expired
- **When** I scan the QR code
- **Then** the system blocks check-in and displays "Your membership expired on [Date]. Please renew to continue." with a "Renew Now" button.

---

## US-04 — View Attendance History

**Role:** Gym Member
**Priority:** Medium | **Sprint:** 2

> As a **gym member**, I want to **view my attendance history**, so that **I can track my consistency and stay motivated**.

**Acceptance Criteria:**

**Scenario 1 — View Monthly Attendance**
- **Given** I am logged in to the member portal
- **When** I navigate to "My Attendance" and select a month
- **Then** the system displays a calendar view with check-in days highlighted, total visits for that month, and a streak counter (consecutive days visited)

**Scenario 2 — No Attendance Data**
- **Given** I am a newly registered member with no check-ins yet
- **When** I visit the "My Attendance" section
- **Then** the system displays "No check-ins recorded yet. Visit the gym and scan the QR code to start tracking!"

---

## US-05 — Churn Risk Auto-Flagging

**Role:** System (Automated) / Gym Admin
**Priority:** High | **Sprint:** 2

> As a **gym admin**, I want the **system to automatically flag members who haven't visited in 7+ days**, so that **I can take proactive action before they churn**.

**Acceptance Criteria:**

**Scenario 1 — Member Flagged At Risk (7 Days)**
- **Given** a member has not checked in for 7 consecutive days
- **When** the nightly risk scoring engine runs
- **Then** the member's status changes to "At Risk" (yellow), the assigned trainer receives a dashboard notification, and an automated Day-7 re-engagement message is queued

**Scenario 2 — Member Escalated to High Risk (14 Days)**
- **Given** a member flagged At Risk has not checked in for 14 consecutive days
- **When** the nightly scoring engine runs
- **Then** the risk level escalates to "High Risk" (red), a Day-14 message is queued, and the gym admin receives an alert on their dashboard

**Scenario 3 — Risk Flag Auto-Cleared**
- **Given** a member is currently flagged "At Risk"
- **When** the member successfully checks in
- **Then** the risk flag is cleared, the member's status returns to "Engaged" (green), and any pending campaign messages for that trigger cycle are cancelled

---

## US-06 — Trainer Views At-Risk Members

**Role:** Personal Trainer
**Priority:** High | **Sprint:** 2

> As a **personal trainer**, I want to **see which of my assigned members are at risk of dropping out**, so that **I can personally reach out and bring them back**.

**Acceptance Criteria:**

**Scenario 1 — View At-Risk Member List**
- **Given** I am logged in as a trainer
- **When** I open my dashboard
- **Then** I see a list of my assigned members sorted by risk level (Critical → High Risk → At Risk → Engaged), with each card showing name, last visit date, days inactive, and membership expiry

**Scenario 2 — Dismiss Flag With Reason**
- **Given** a member on my list is flagged At Risk but has informed me they are traveling
- **When** I click "Dismiss Flag" and enter the reason "Member traveling — confirmed. Returns June 20"
- **Then** the flag is cleared for this cycle, my note is logged with timestamp, and admin can see the dismissal reason in the member's activity log

---

## US-07 — Automated Re-engagement Message

**Role:** System / Gym Admin
**Priority:** High | **Sprint:** 2

> As a **gym admin**, I want the **system to automatically send re-engagement messages to inactive members**, so that **my team doesn't have to manually chase every absent member**.

**Acceptance Criteria:**

**Scenario 1 — Day-7 Message Sent**
- **Given** a member has been inactive for exactly 7 days and has not opted out of messages
- **When** the campaign engine runs
- **Then** the system sends a personalized WhatsApp/SMS using the Day-7 template, logs the delivery status, and marks the campaign as "In Progress" on the admin dashboard

**Scenario 2 — Member Opts Out**
- **Given** a member replies "STOP" to a campaign message
- **When** the opt-out is received
- **Then** the member is added to the do-not-contact list, all pending campaign messages for that member are cancelled, and admin is notified

**Scenario 3 — Campaign Message Timing Rule**
- **Given** a message is queued for delivery
- **When** the scheduled send time falls between 10 PM and 8 AM
- **Then** the message is held and delivered at 8:00 AM the following morning

---

## US-08 — Membership Renewal Reminder

**Role:** Gym Member
**Priority:** High | **Sprint:** 3

> As a **gym member**, I want to **receive timely reminders before my membership expires**, so that **I don't accidentally lose access to the gym**.

**Acceptance Criteria:**

**Scenario 1 — 7-Day Reminder Sent**
- **Given** my membership expires in exactly 7 days
- **When** the daily reminder check runs
- **Then** I receive an SMS: "Hi [Name], your [Gym Name] membership expires in 7 days. Renew now: [link]"

**Scenario 2 — Member Renews After Reminder**
- **Given** I receive the renewal reminder
- **When** I click the link and complete payment
- **Then** my membership expiry date is extended, I receive a confirmation SMS with the new expiry date, and the renewal pipeline in the admin dashboard marks my status as "Renewed"

**Scenario 3 — No Renewal by Expiry**
- **Given** my membership expires today and I have not renewed
- **When** the end-of-day system job runs
- **Then** my status changes to "Lapsed," I am removed from the active member list, and I receive an SMS: "Your membership has expired. Renew within 30 days to keep your history."

---

## US-09 — Self-Service Online Renewal

**Role:** Gym Member
**Priority:** High | **Sprint:** 3

> As a **gym member**, I want to **renew my membership online via UPI or card**, so that **I don't have to visit the gym just to pay for a renewal**.

**Acceptance Criteria:**

**Scenario 1 — Successful Online Renewal**
- **Given** I click the renewal link in the reminder SMS
- **When** I select my plan and complete UPI payment successfully
- **Then** my membership is extended, my status updates to Active, I receive a digital receipt on email, and the admin's renewal dashboard reflects the update within 5 minutes

**Scenario 2 — Payment Failure**
- **Given** I attempt payment and my transaction fails
- **When** the payment gateway returns a failure status
- **Then** the system shows "Payment unsuccessful. Please try again." with a retry button; my membership status is unchanged

---

## US-10 — Admin Views Renewal Pipeline

**Role:** Gym Admin
**Priority:** Medium | **Sprint:** 3

> As a **gym admin**, I want to **see a list of all memberships expiring in the next 30 days**, so that **I can prioritize follow-ups and forecast monthly revenue**.

**Acceptance Criteria:**

**Scenario 1 — Renewal Pipeline View**
- **Given** I am logged in as admin and navigate to "Renewals"
- **When** the page loads
- **Then** I see a table of members with columns: Name, Expiry Date, Days Remaining, Plan, Renewal Status (Pending / Renewed / Lapsed), and Last Contact Date — sorted by soonest expiry

**Scenario 2 — Filter by Status**
- **Given** I want to focus only on members who have not yet renewed
- **When** I apply the filter "Status = Pending"
- **Then** the table updates to show only members with upcoming expiry who haven't renewed, and the count badge updates accordingly

---

## US-11 — Exit Survey Sent on Lapse

**Role:** System / Gym Owner
**Priority:** Medium | **Sprint:** 3

> As a **gym owner**, I want the **system to automatically send an exit survey when a member's membership lapses**, so that **I can understand why members leave and fix the root causes**.

**Acceptance Criteria:**

**Scenario 1 — Survey Sent After Lapse**
- **Given** a member's membership expires without renewal
- **When** 24 hours pass after the expiry date
- **Then** the system sends an SMS with a survey link: "Hi [Name], we're sad to see you go. Help us improve by answering 5 quick questions: [link]"

**Scenario 2 — Survey Completed**
- **Given** the member clicks the survey link and submits responses
- **When** the form is submitted
- **Then** responses are saved, the admin dashboard's "Exit Reasons" chart updates, and the member record shows "Survey Completed"

**Scenario 3 — Survey Expired Without Response**
- **Given** the survey link was sent 7 days ago and the member has not responded
- **When** 7 days elapse
- **Then** the survey link is deactivated and the member record shows "Survey: No Response"

---

## US-12 — Admin Configures Message Templates

**Role:** Gym Admin
**Priority:** Medium | **Sprint:** 2

> As a **gym admin**, I want to **customize the re-engagement and reminder message templates**, so that **the messages reflect my gym's brand and tone**.

**Acceptance Criteria:**

**Scenario 1 — Edit Template**
- **Given** I navigate to Settings > Message Templates
- **When** I edit the Day-7 re-engagement template and click Save
- **Then** the new template is saved, the preview reflects my changes, and all future Day-7 messages use the updated template

**Scenario 2 — Template Too Long**
- **Given** I type a message longer than 160 characters (SMS limit for single message)
- **When** I type beyond the limit
- **Then** the system shows a live character counter turning red and a warning: "Messages over 160 characters will be split into 2 SMS. This may increase cost."

---

## US-13 — Trainer Logs a Check-In Note

**Role:** Personal Trainer
**Priority:** Low | **Sprint:** 3

> As a **personal trainer**, I want to **log notes on a member's profile after a personal check-in**, so that **I have a record of conversations and the admin has context if they follow up too**.

**Acceptance Criteria:**

**Scenario 1 — Note Successfully Added**
- **Given** I open a member's profile on my trainer dashboard
- **When** I enter a note (max 300 characters) and click "Save Note"
- **Then** the note is saved with my name and the current timestamp, and appears in the member's activity log

**Scenario 2 — Note Exceeds Character Limit**
- **Given** I type more than 300 characters in the note field
- **When** I reach the limit
- **Then** the system stops accepting input and shows "300/300 characters used"

---

## US-14 — Owner Views Retention Analytics

**Role:** Gym Owner
**Priority:** High | **Sprint:** 4

> As a **gym owner**, I want to **view retention KPIs on a dashboard**, so that **I can track whether FitRetain is improving member retention and making a business impact**.

**Acceptance Criteria:**

**Scenario 1 — Dashboard Loads with Current Month Data**
- **Given** I am logged in as Owner and open the Analytics dashboard
- **When** the page loads
- **Then** I see the current month's: total active members, churn rate (%), renewal rate (%), number of at-risk members, and average member tenure in months — all with a comparison vs. last month (up/down arrows)

**Scenario 2 — Export Report**
- **Given** I want to share the monthly report with a business partner
- **When** I click "Export" and select PDF
- **Then** a formatted PDF report downloads to my device within 10 seconds

---

## US-15 — Admin Manually Marks Membership as Cancelled

**Role:** Gym Admin
**Priority:** Medium | **Sprint:** 2

> As a **gym admin**, I want to **manually cancel a member's membership when they request it in person**, so that **the system stays in sync with ground reality and the exit survey is triggered**.

**Acceptance Criteria:**

**Scenario 1 — Successful Manual Cancellation**
- **Given** a member has requested cancellation in person
- **When** I search for the member, select "Cancel Membership," confirm with reason (Relocating / Personal reasons / Financial / Other), and click Confirm
- **Then** the membership status updates to "Cancelled," the member is removed from active lists, and the exit survey is queued for sending after 24 hours

**Scenario 2 — Cancellation Confirmation Step**
- **Given** I click "Cancel Membership" accidentally
- **When** the confirmation dialog appears
- **Then** I must type the member's name to confirm before the action proceeds, preventing accidental cancellations

---

## Story Summary

| Story ID | Role | Feature Area | Priority |
|----------|------|--------------|----------|
| US-01 | Member | Registration | High |
| US-02 | Member | Login/Auth | High |
| US-03 | Member | Attendance | High |
| US-04 | Member | Attendance History | Medium |
| US-05 | System/Admin | Churn Risk Engine | High |
| US-06 | Trainer | Dashboard | High |
| US-07 | System/Admin | Re-engagement | High |
| US-08 | Member | Renewal Reminder | High |
| US-09 | Member | Online Renewal | High |
| US-10 | Admin | Renewal Pipeline | Medium |
| US-11 | System/Owner | Exit Survey | Medium |
| US-12 | Admin | Message Templates | Medium |
| US-13 | Trainer | Notes/Check-in | Low |
| US-14 | Owner | Analytics | High |
| US-15 | Admin | Manual Cancellation | Medium |

---

*End of User Stories Document — FitRetain v1.0*
