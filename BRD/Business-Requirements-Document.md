[Business-Requirements-Document.md](https://github.com/user-attachments/files/27350971/Business-Requirements-Document.md)
# Business Requirements Document (BRD)
## FitRetain — Gym Member Retention System

---

| Field | Details |
|-------|---------|
| **Document Version** | 1.0 |
| **Date** | May 2026 |
| **Prepared By** | Business Analyst |
| **Review Status** | Approved for FRD Development |
| **Project Code** | FITRETAIN-2026 |

---

## 1. Executive Summary

FitRetain is a SaaS-based gym member retention system built to address one of the fitness industry's most expensive problems — member churn. Indian gyms spend ₹800–₹1,500 acquiring each new member, yet lose 40–60% of them within the first 90 days due to disengagement, poor follow-up, and zero visibility into at-risk behavior.

This document defines the business context, objectives, stakeholders, scope, and high-level requirements that FitRetain must fulfill. It serves as the foundation for all downstream product and technical documentation.

---

## 2. Business Context

### Industry Background
- India's gym and fitness market is valued at ₹4,500 crore and growing at 16.4% CAGR (KPMG, 2024).
- Over 2.5 lakh registered gyms operate across India, with 60% being independent or small-chain setups.
- Average gym revenue depends 70–80% on monthly membership renewals.
- Studies show that increasing member retention by just 5% can improve gym profits by 25–95%.

### Current Operational Reality
Most gyms today operate with:
- Paper registers or basic Excel sheets for attendance
- WhatsApp broadcasts for renewal reminders (no personalization)
- No system to identify which members are at risk before they cancel
- No structured exit interview or cancellation feedback process
- Trainers working in silos with no shared member engagement data

### The Core Problem
**Gyms are losing members silently.** By the time the owner notices a member hasn't renewed, the member has already mentally checked out weeks earlier — and no one intervened.

---

## 3. Problem Statement

Indian gyms face a structural retention crisis driven by three gaps:

**Gap 1 — Visibility Gap:** Gym owners and trainers have no real-time view of member engagement. A member can stop attending for 2–3 weeks with no one noticing until renewal is missed.

**Gap 2 — Action Gap:** Even when disengagement is noticed, there is no standardized process for outreach. Re-engagement attempts are inconsistent, untimely, and manual.

**Gap 3 — Intelligence Gap:** Gyms collect no exit data. They cannot identify patterns in why members leave, which trainers retain better, or which membership plans have higher churn — making improvement impossible.

**Measured Impact:**
- A gym with 300 members and ₹1,500/month average fee losing 50% annually loses ₹22.5 lakh/year in preventable churn.
- 68% of members who cancelled said they would have stayed if someone had reached out during disengagement (Fitness Industry Report India, 2023).

---

## 4. Business Objectives

| # | Objective | KPI | Baseline | Target | Timeline |
|---|-----------|-----|----------|--------|----------|
| BO-1 | Reduce early churn | 90-day dropout rate | 50% | < 25% | 6 months |
| BO-2 | Improve renewal rate | % of memberships renewed | 40% | 65% | 6 months |
| BO-3 | Automate re-engagement | % of outreach automated | ~0% | 80% | 3 months |
| BO-4 | Collect exit intelligence | % of exits with feedback | ~0% | 80% | 3 months |
| BO-5 | Increase member LTV | Avg. months per member | 4.2 months | 7+ months | 12 months |

---

## 5. Stakeholders

### Primary Stakeholders (Direct Users)

| Stakeholder | Role in System | Primary Need |
|-------------|---------------|--------------|
| Gym Member | End user of member portal | Track progress, get reminders, manage membership |
| Personal Trainer | Monitors assigned members | Flag disengaged members, log check-ins |
| Gym Admin / Reception | Manages day-to-day operations | Attendance, memberships, renewal follow-ups |
| Gym Owner | Strategic decision maker | Retention KPIs, revenue dashboard, churn reports |

### Secondary Stakeholders

| Stakeholder | Role | Concern |
|-------------|------|---------|
| FitRetain Platform Admin | System management | Gym onboarding, platform health |
| SMS/WhatsApp Gateway (e.g., MSG91) | Integration partner | Reliable notification delivery |
| Payment Gateway (Razorpay) | Integration partner | Membership fee collection |
| Gym Franchise HQ (for chains) | Multi-branch oversight | Cross-branch retention analytics |

---

## 6. Scope

### In Scope — Version 1.0

- Member registration, profile, and membership management
- Digital attendance tracking (QR code or manual check-in)
- Automated churn risk scoring based on attendance pattern
- Automated SMS/WhatsApp/email re-engagement campaigns
- Membership renewal reminders and online renewal payment
- Trainer dashboard for assigned member monitoring
- Admin dashboard with retention KPIs and renewal pipeline
- Exit/cancellation survey for members who do not renew
- Basic reporting: churn rate, attendance trends, renewal conversion

### Out of Scope — Version 1.0

- Diet and nutrition tracking
- Workout plan builder or exercise library
- Wearable device integration (Fitbit, Apple Watch)
- Live class or PT session booking
- Multi-location / franchise-level consolidated analytics (planned v2.0)
- E-commerce (supplements, merchandise)
- Mobile app (v1.0 is web-based; native app planned for v2.0)

---

## 7. High-Level Business Requirements

### BR-01 — Member Profile Management
The system must maintain a digital profile for every active and past member, including membership type, start date, renewal date, assigned trainer, attendance history, and goal preferences.

### BR-02 — Attendance Tracking
The system must record member attendance on each visit. Attendance can be logged via QR code scan at the gym gate or manually by reception staff. The system must calculate days since last visit in real time.

### BR-03 — Churn Risk Detection
The system must automatically flag members as "At Risk" when they have not attended for 7 or more consecutive days. Members inactive for 14+ days must be escalated to "High Risk." The flag must trigger an automated notification to the assigned trainer and gym admin.

### BR-04 — Automated Re-engagement Outreach
The system must send pre-configured re-engagement messages to at-risk members via SMS and/or WhatsApp. Message content, timing, and frequency must be configurable by the gym admin. A minimum of three touchpoints must be supported (Day 7, Day 14, Day 21 of inactivity).

### BR-05 — Membership Renewal Management
The system must send automated renewal reminders to members 30 days, 7 days, and 1 day before membership expiry. Members must be able to renew online. Gym admin must see all upcoming renewals in a pipeline view.

### BR-06 — Trainer Engagement Monitoring
Personal trainers must have a dashboard showing their assigned members' attendance frequency, last visit date, current risk status, and a log of any check-ins or notes they have added.

### BR-07 — Exit and Cancellation Feedback
When a member cancels or does not renew, the system must automatically send an exit survey (3–5 questions) via SMS/email. Survey responses must be stored and visible in the admin analytics dashboard.

### BR-08 — Admin Reporting and Analytics
Gym admin must be able to access monthly reports showing: total active members, churn rate, renewal rate, at-risk member count, trainer-wise retention performance, and revenue summary.

### BR-09 — Online Membership Renewal and Payment
Members must be able to renew their membership online via UPI, debit/credit card, or net banking. Receipts must be auto-generated and emailed. Admin must be able to track payment status.

### BR-10 — Role-Based Access Control
The system must enforce role-based access. Trainers see only their assigned members. Admin sees all members. Owner sees all members plus financial reports. Members see only their own data.

---

## 8. Assumptions

- Each gym has at least one staff member (admin/receptionist) managing the system daily.
- Members have a mobile number for notifications; email is optional.
- QR code scanners or a front-desk tablet will be available at gym entry points.
- Gym owners will configure messaging templates during onboarding.
- The system onboards one gym location per account in v1.0.

---

## 9. Constraints

- All member personal data must comply with India's Digital Personal Data Protection (DPDP) Act, 2023.
- The platform must be accessible on mobile browsers (responsive web design).
- Notification delivery must achieve 95%+ delivery rate.
- System must handle up to 5,000 member profiles per gym account.

---

## 10. Risks and Mitigations

| Risk | Likelihood | Impact | Mitigation Strategy |
|------|------------|--------|---------------------|
| Gym staff resistance to adoption | Medium | High | Provide training, simple UI, onboarding support |
| Low member portal engagement | Medium | Medium | Incentivize logins (streak badges, renewal discounts) |
| Notification opt-out by members | Low | Medium | Ensure opt-out mechanism; focus on value messaging |
| Inaccurate churn flag (false positives) | Medium | Low | Allow trainer to override/dismiss flag manually |
| Data entry errors in attendance | Medium | Medium | Prioritize QR-based auto check-in to reduce manual entry |

---

## 11. Success Criteria

The project will be considered successful at the 6-month post-launch review if:
- 90-day churn rate drops below 25%
- At least 80% of re-engagement campaigns are sent automatically without manual intervention
- Renewal rate reaches 60% or above
- Gym admin NPS score for the platform is 7 or above (out of 10)

---

*End of Business Requirements Document — FitRetain v1.0*
