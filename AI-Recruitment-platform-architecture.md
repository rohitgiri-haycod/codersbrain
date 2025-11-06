# AI-Powered Recruitment Platform - Architecture & Flowchart Guide

**Project:** Recruitment Collaboration & Candidate Management Platform  
**Client:** CodersBrain  
**Developer:** HayCod Solutions  
**Date:** 29 October 2025

---

## Table of Contents
1. [System Architecture Overview](#system-architecture-overview)
2. [Role-Based Dashboard Architecture](#role-based-dashboard-architecture)
3. [Onboarding & KYC Workflow](#onboarding--kyc-workflow)
4. [Job Description Management Flow](#job-description-management-flow)
5. [Candidate Profile & Data Privacy Flow](#candidate-profile--data-privacy-flow)
6. [Recruitment Pipeline Flow](#recruitment-pipeline-flow)
7. [Commission & Payment Flow](#commission--payment-flow)
8. [Review & Rating System Flow](#review--rating-system-flow)
9. [Referral System Flow](#referral-system-flow)
10. [AI Automation Flow (Optional)](#ai-automation-flow-optional)
11. [Security & Access Control Architecture](#security--access-control-architecture)
12. [Technical Architecture](#technical-architecture)
13. [Data Flow Diagrams](#data-flow-diagrams)

---

## 1. System Architecture Overview

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                     AI-POWERED RECRUITMENT PLATFORM                          │
│                            (Multi-Role System)                               │
└─────────────────────────────────────────────────────────────────────────────┘
                                      │
                    ┌─────────────────┼─────────────────┐
                    │                 │                  │
                    ▼                 ▼                  ▼
        ┌──────────────────┐  ┌──────────────┐  ┌──────────────┐
        │  CODERSBRAIN     │  │   VENDORS    │  │   CLIENTS    │
        │  ADMIN PANEL     │  │   PORTAL     │  │   PORTAL     │
        │                  │  │              │  │              │
        │  • Super Admin   │  │  • Agency    │  │  • Employer  │
        │  • Manager       │  │  • Recruiter │  │  • HR Team   │
        │  • HR           │  │              │  │              │
        └──────────────────┘  └──────────────┘  └──────────────┘
                    │                 │                  │
                    └─────────────────┼─────────────────┘
                                      │
                                      ▼
                         ┌─────────────────────────┐
                         │  CANDIDATES/FREELANCERS │
                         │       PORTAL            │
                         │                         │
                         │  • Full-time            │
                         │  • Freelancer           │
                         │  • Part-time            │
                         │  • Contract             │
                         └─────────────────────────┘
```

### Key Components:
- **4 Main User Types**: CodersBrain Admin (3 roles), Vendors, Clients, Candidates
- **Unified Platform**: Single codebase with role-based access
- **Data Isolation**: Vendor candidate data strictly controlled
- **AI Layer**: Optional automation for all processes
- **Security Layer**: RBAC, encryption, audit logging

---

## 2. Role-Based Dashboard Architecture

### 2.1 CodersBrain Admin Panel Hierarchy

```
                    ┌───────────────────────────┐
                    │      SUPER ADMIN          │
                    │  • System Configuration   │
                    │  • User Management        │
                    │  • Commission Setup       │
                    │  • KYC Approval           │
                    │  • AI Feature Toggle      │
                    │  • Financial Reports      │
                    └─────────────┬─────────────┘
                                  │
                    ┌─────────────┼─────────────┐
                    │                           │
          ┌─────────▼─────────┐     ┌─────────▼──────────┐
          │     MANAGER       │     │        HR          │
          │  • JD Management  │     │  • Screening       │
          │  • Vendor Assign  │     │  • Interviews      │
          │  • Candidate View │     │  • Onboarding      │
          │  • Client Coord   │     │  • Documentation   │
          │  • Analytics      │     │  • Compliance      │
          └───────────────────┘     └────────────────────┘
```

### 2.2 Dashboard Access Matrix

| Feature                          | Super Admin | Manager | HR | Vendor | Client | Candidate |
|----------------------------------|-------------|---------|-----|--------|--------|-----------|
| User Management                  | ✅          | ❌      | ❌  | ❌     | ❌     | ❌        |
| KYC Approval                     | ✅          | ✅      | ❌  | ❌     | ❌     | ❌        |
| Commission Config                | ✅          | ❌      | ❌  | ❌     | ❌     | ❌        |
| JD Create/Edit                   | ✅          | ✅      | ❌  | ❌     | ✅     | ❌        |
| JD Assignment                    | ✅          | ✅      | ❌  | ❌     | ❌     | ❌        |
| View All Candidates              | ✅          | ✅      | ✅  | ❌*    | ❌*    | ❌        |
| Upload Candidates                | ❌          | ❌      | ❌  | ✅     | ❌     | ❌        |
| Candidate Screening              | ✅          | ✅      | ✅  | ❌     | ❌     | ❌        |
| Interview Scheduling             | ✅          | ✅      | ✅  | ❌     | ✅     | ✅        |
| Offer Management                 | ✅          | ✅      | ✅  | ❌     | ✅     | ✅        |
| Commission Tracking              | ✅          | ✅      | ❌  | ✅     | ❌     | ❌        |
| Review/Rating                    | ✅          | ✅      | ✅  | ✅     | ✅     | ✅        |

*Vendors see only their own candidates; Clients see only shortlisted candidates

---

## 3. Onboarding & KYC Workflow

### 3.1 Registration Flow Diagram

```
                         ┌──────────────────────┐
                         │   Landing Page       │
                         │  Choose Role:        │
                         │  ┌────────────────┐  │
                         │  │ □ Vendor       │  │
                         │  │ □ Client       │  │
                         │  │ □ Candidate    │  │
                         │  │ □ Freelancer   │  │
                         │  └────────────────┘  │
                         └──────────┬───────────┘
                                    │
                         ┌──────────▼───────────┐
                         │  Basic Registration  │
                         │  • Email (OTP)       │
                         │  • Mobile (OTP)      │
                         │  • Password          │
                         │  • Basic Info        │
                         └──────────┬───────────┘
                                    │
                    ┌───────────────┼───────────────┐
                    │               │               │
           ┌────────▼────────┐     │      ┌────────▼────────┐
           │  VENDOR KYC     │     │      │  CLIENT KYC     │
           │  • Agency Docs  │     │      │  • Company Docs │
           │  • GST/PAN      │     │      │  • GST/PAN      │
           │  • Bank Details │     │      │  • Authorized   │
           │  • Domain       │     │      │    Signatory    │
           └────────┬────────┘     │      └────────┬────────┘
                    │               │               │
                    │      ┌────────▼────────┐      │
                    │      │  CANDIDATE KYC  │      │
                    │      │  (Optional)     │      │
                    │      │  • ID Proof     │      │
                    │      │  • Resume       │      │
                    │      │  • Certificates │      │
                    │      └────────┬────────┘      │
                    │               │               │
                    └───────────────┼───────────────┘
                                    │
                         ┌──────────▼───────────┐
                         │  PENDING APPROVAL    │
                         │  Status Dashboard    │
                         │  • Email Sent        │
                         │  • SMS Sent          │
                         └──────────┬───────────┘
                                    │
                         ┌──────────▼───────────┐
                         │  ADMIN REVIEW        │
                         │  • Document Check    │
                         │  • Background Verify │
                         │  • Approve/Reject    │
                         └──────────┬───────────┘
                                    │
                    ┌───────────────┼───────────────┐
                    │                               │
           ┌────────▼────────┐             ┌───────▼────────┐
           │    APPROVED     │             │    REJECTED    │
           │  Full Access    │             │  Resubmit KYC  │
           │  Notification   │             │  Reason Given  │
           └─────────────────┘             └────────────────┘
```

### 3.2 KYC Document Requirements

**Vendor/Agency:**
- GST Certificate (Mandatory)
- PAN Card (Mandatory)
- Business Registration Certificate (Mandatory)
- Agency Domain Verification (Mandatory)
- Bank Account Details (Mandatory)
- Owner ID Proof (Mandatory)
- Office Address Proof (Optional)
- Past Client References (Optional)

**Client/Employer:**
- Company Registration (Mandatory)
- GST Certificate (Mandatory)
- PAN Card (Mandatory)
- Authorized Signatory ID (Mandatory)
- Company Email Domain (Mandatory)
- Bank Details (Mandatory)
- Office Address Proof (Optional)

**Candidate/Freelancer:**
- Government ID (Before Placement)
- Educational Certificates (Before Placement)
- Resume (Mandatory)
- Bank Details (Before Payout)

---

## 4. Job Description Management Flow

### 4.1 JD Creation to Assignment Flow

```
┌─────────────────────────────────────────────────────────────────────┐
│                    JD MANAGEMENT WORKFLOW                            │
└─────────────────────────────────────────────────────────────────────┘

CLIENT SIDE                    CODERSBRAIN SIDE               VENDOR SIDE
─────────────                  ────────────────               ───────────

┌─────────────┐
│ Create JD   │                                                       
│ • Title     │                                                       
│ • Skills    │                                                       
│ • Budget    │                                                       
│ • Duration  │                                                       
└──────┬──────┘                                                       
       │                                                              
       │ Submit                                                       
       ▼                                                              
┌─────────────┐                ┌──────────────┐                       
│ JD Submitted│───────────────>│ Notification │                       
│ (Pending)   │                │ to Manager   │                       
└─────────────┘                └──────┬───────┘                       
                                      │                               
                              ┌───────▼────────┐                      
                              │ Manager Review │                      
                              │ • Edit JD      │                      
                              │ • Add Notes    │                      
                              │ • Set Priority │                      
                              │ • Config ₹     │                      
                              └───────┬────────┘                      
                                      │                               
                   ┌──────────────────┼──────────────────┐            
                   │                  │                  │            
                   ▼                  ▼                  ▼            
          ┌────────────────┐  ┌────────────────┐ ┌────────────────┐ 
          │ Manual Assign  │  │  AI Suggest    │ │  Bulk Assign   │ 
          │ Select Vendor  │  │  (OPTIONAL)    │ │  Multiple JDs  │ 
          └────────┬───────┘  └────────┬───────┘ └────────┬───────┘ 
                   │                   │                   │         
                   └───────────────────┼───────────────────┘         
                                       │                             
                                       │                             
                                       ▼                    ┌────────────────┐
                                 ┌──────────┐              │ JD Assigned    │
                                 │ Assigned │─────────────>│ Notification   │
                                 └──────────┘              │ • Email        │
                                                          │ • SMS          │
                                                          │ • In-app       │
                                                          └────────┬───────┘
                                                                   │
                                                          ┌────────▼───────┐
                                                          │ Vendor Accept/ │
                                                          │ Decline JD     │
                                                          └────────┬───────┘
                                                                   │
                                                   ┌───────────────┼───────────────┐
                                                   │                               │
                                          ┌────────▼────────┐             ┌───────▼────────┐
                                          │   ACCEPTED      │             │    DECLINED    │
                                          │ Start Sourcing  │             │  Reason Given  │
                                          └─────────────────┘             │  Re-assign     │
                                                                          └────────────────┘
```

### 4.2 Bulk JD Operations

**Client Bulk Upload:**
```
Excel/CSV Template → Validate → Upload → Manager Review → Assign
```

**CodersBrain Bulk Assignment:**
```
Select Multiple JDs → Select Multiple Vendors → AI Suggest Match → Confirm → Notify All
```

---

## 5. Candidate Profile & Data Privacy Flow

### 5.1 Candidate Data Flow with Privacy Controls

```
VENDOR PRIVATE DATABASE              CODERSBRAIN ACCESS           CLIENT ACCESS
───────────────────────              ──────────────────           ─────────────

┌─────────────────────┐
│ Vendor Uploads      │
│ Candidate Profiles  │
│                     │
│ ┌─────────────────┐ │
│ │ Candidate A     │ │──────┐
│ │ • Resume        │ │      │
│ │ • Skills        │ │      │
│ │ • Experience    │ │      │                                     
│ └─────────────────┘ │      │     
│                     │      │     
│ ┌─────────────────┐ │      │     
│ │ Candidate B     │ │      │     
│ └─────────────────┘ │      │     
│                     │      │     
│ ┌─────────────────┐ │      │     
│ │ Candidate C     │ │      │     
│ └─────────────────┘ │      │     
└─────────────────────┘      │     
         │                   │     
         │                   │     
         │ Explicit Share    │     
         │ Action Required   │     
         ▼                   │     
┌─────────────────────┐      │                                    
│ "Share with         │      │                                    
│  CodersBrain"       │      │                                    
│  Button Clicked     │      │                                    
└──────────┬──────────┘      │                                    
           │                 │                                    
           │ Complete        │ No Access                          
           │ Profile         │ Until Shared                       
           │ Transferred     │                                    
           ▼                 ▼                                    
                    ┌─────────────────────┐
                    │ CodersBrain Database│
                    │                     │
                    │ ┌─────────────────┐ │
                    │ │ Shared Profile  │ │
                    │ │ • Full Data     │ │
                    │ │ • All Docs      │ │
                    │ │ • Audit Log     │ │
                    │ └─────────────────┘ │
                    │                     │
                    │ Direct Candidates   │
                    │ ┌─────────────────┐ │
                    │ │ Candidate X     │ │
                    │ │ • Full Access   │ │
                    │ └─────────────────┘ │
                    └──────────┬──────────┘
                               │
                               │ Manager
                               │ Shortlisting
                               ▼
                    ┌─────────────────────┐
                    │ Shortlisted for     │
                    │ Client Review       │
                    └──────────┬──────────┘
                               │
                               │ Complete
                               │ Profile Sent
                               ▼
                                        ┌─────────────────────┐
                                        │ Client Dashboard    │
                                        │                     │
                                        │ ┌─────────────────┐ │
                                        │ │ Shortlisted     │ │
                                        │ │ Profiles Only   │ │
                                        │ │ • Full Data     │ │
                                        │ │ • Review Access │ │
                                        │ └─────────────────┘ │
                                        └─────────────────────┘
```

### 5.2 Data Privacy Rules

| Data Access Type           | Vendor | CodersBrain | Client | Audit Logged |
|----------------------------|--------|-------------|--------|--------------|
| Vendor's Own Candidates    | ✅ Full| ❌ None*    | ❌ None| ✅ Yes       |
| Shared Candidates          | ✅ Full| ✅ Full     | ❌ None| ✅ Yes       |
| Shortlisted Candidates     | ✅ Full| ✅ Full     | ✅ Full| ✅ Yes       |
| Direct Registered Candidates| ❌ None| ✅ Full     | ❌ None| ✅ Yes       |

*Until vendor explicitly shares

### 5.3 Complete Profile Data Structure

```
CANDIDATE COMPLETE PROFILE (Shared as Single Unit)
───────────────────────────────────────────────────

┌──────────────────────────────────────────────────────────┐
│                   PERSONAL INFORMATION                    │
│  • Full Name                • Date of Birth               │
│  • Email                    • Phone Number                │
│  • Current Location         • Permanent Address           │
│  • LinkedIn Profile         • GitHub Profile              │
│  • Portfolio Website        • Professional Photo          │
└──────────────────────────────────────────────────────────┘
┌──────────────────────────────────────────────────────────┐
│                   PROFESSIONAL DETAILS                    │
│  • Current Job Title        • Years of Experience         │
│  • Current Company          • Current Salary              │
│  • Notice Period            • Expected Salary             │
│  • Work Authorization       • Relocation Willingness      │
│  • Preferred Locations      • Work Preferences            │
└──────────────────────────────────────────────────────────┘
┌──────────────────────────────────────────────────────────┐
│                     SKILLS & EXPERTISE                    │
│  • Technical Skills (with proficiency levels)             │
│  • Soft Skills              • Certifications              │
│  • Tools & Technologies     • Languages                   │
│  • Industry Experience      • Domain Expertise            │
└──────────────────────────────────────────────────────────┘
┌──────────────────────────────────────────────────────────┐
│                    WORK EXPERIENCE                        │
│  Company 1                                                │
│  • Job Title                • Duration                    │
│  • Responsibilities         • Achievements                │
│  • Technologies Used        • Team Size                   │
│                                                           │
│  Company 2...                                             │
└──────────────────────────────────────────────────────────┘
┌──────────────────────────────────────────────────────────┐
│                      EDUCATION                            │
│  • Degrees/Diplomas         • Institutions                │
│  • Graduation Year          • GPA/Percentage              │
│  • Specializations          • Achievements                │
└──────────────────────────────────────────────────────────┘
┌──────────────────────────────────────────────────────────┐
│                   PROJECTS & PORTFOLIO                    │
│  Project 1                                                │
│  • Description              • Technologies                │
│  • Role                     • Duration                    │
│  • Outcomes/Metrics         • Links/Demos                 │
└──────────────────────────────────────────────────────────┘
┌──────────────────────────────────────────────────────────┐
│             SCREENING & ASSESSMENT RESULTS                │
│  • Resume Score             • Skill Assessment Scores     │
│  • Technical Test Results   • Behavioral Assessment       │
│  • AI Evaluation (Optional) • Internal Notes              │
└──────────────────────────────────────────────────────────┘
┌──────────────────────────────────────────────────────────┐
│                   DOCUMENTS & UPLOADS                     │
│  • Resume/CV (PDF)          • Cover Letter                │
│  • Certificates             • ID Proofs (KYC)             │
│  • Educational Docs         • Experience Letters          │
│  • Portfolio Files          • References                  │
└──────────────────────────────────────────────────────────┘
┌──────────────────────────────────────────────────────────┐
│                 AVAILABILITY & PREFERENCES                │
│  • Immediate/Notice Period  • Full-time/Part-time         │
│  • Remote/Hybrid/Onsite     • Salary Expectations         │
│  • Preferred Industries     • Company Size Preference     │
│  • Work Schedule            • Benefits Expected           │
└──────────────────────────────────────────────────────────┘
┌──────────────────────────────────────────────────────────┐
│              REVIEWS & RATINGS (if any)                   │
│  • Previous Client Ratings  • Interviewer Feedback        │
│  • Performance Reviews      • Recommendations             │
└──────────────────────────────────────────────────────────┘
```

---

## 6. Recruitment Pipeline Flow

### 6.1 Complete Pipeline Stages

```
STAGE 1              STAGE 2           STAGE 3           STAGE 4
JD Posted         Sourcing         Screening       Shortlisting
─────────         ────────         ─────────       ────────────
Client            Vendors          CodersBrain     CodersBrain
Creates JD    ──> Upload       ──> HR/Manager  ──> Manager
              CodersBrain          Reviews             Selects
              Assigns to           Candidates          Top
              Vendors                                  Candidates
                                                       
                   │                                       │
                   │                                       │
                   ▼                                       ▼

STAGE 5              STAGE 6           STAGE 7           STAGE 8
Client Review     Interview        Offer            Onboarding
─────────────     ─────────        ─────            ──────────
Client            Client/CB        Client           Client/CB
Reviews       ──> Schedules    ──> Generates    ──> HR Process
Profiles          Interviews       Offer            Documents
Requests                           Letter           Joining
Interviews                                          
```

### 6.2 Detailed Stage Flow with Access Control

```
┌──────────────────────────────────────────────────────────────────────┐
│                     STAGE 1: JD POSTING                               │
│  Access: Client (Create), CodersBrain Manager (Edit, Assign)         │
│  Actions: Post JD → Manager Reviews → Edits → Assigns to Vendors     │
│  AI (Optional): Suggest best vendors based on JD requirements         │
└───────────────────────────────┬──────────────────────────────────────┘
                                │
┌───────────────────────────────▼──────────────────────────────────────┐
│                     STAGE 2: SOURCING                                 │
│  Access: Vendors (Upload), CodersBrain (View All)                    │
│  Actions: Vendor Searches → Uploads Candidates → Shares with CB      │
│           Direct Candidates Register → Auto Added to CB Database     │
│  AI (Optional): Suggest matching candidates from database             │
└───────────────────────────────┬──────────────────────────────────────┘
                                │
┌───────────────────────────────▼──────────────────────────────────────┐
│                     STAGE 3: SCREENING                                │
│  Access: CodersBrain HR, Manager                                      │
│  Actions: Review Resumes → Conduct Initial Screening → Score         │
│           Run Skills Assessment → Mark Pass/Fail                      │
│  AI (Optional):                                                       │
│    - Auto resume parsing and skill extraction                         │
│    - Relevance scoring against JD                                     │
│    - Red flag detection (gaps, frequent changes)                      │
│    - Automated initial screening score                                │
│  Output: Screened candidates with pass/fail status                    │
└───────────────────────────────┬──────────────────────────────────────┘
                                │
┌───────────────────────────────▼──────────────────────────────────────┐
│                     STAGE 4: SHORTLISTING                             │
│  Access: CodersBrain Manager                                          │
│  Actions: Review Screened Candidates → Compare → Select Top 10-15    │
│           Add Internal Notes → Forward to Client                      │
│  AI (Optional):                                                       │
│    - ML-based candidate ranking                                       │
│    - Predictive success scoring                                       │
│    - Automated top-N selection                                        │
│    - Bias-free evaluation                                             │
│  Output: Shortlisted candidates sent to client                        │
└───────────────────────────────┬──────────────────────────────────────┘
                                │
┌───────────────────────────────▼──────────────────────────────────────┐
│                     STAGE 5: CLIENT REVIEW                            │
│  Access: Client (Full), CodersBrain Manager (Read-Only)              │
│  Actions: Review Complete Profiles → Request Interviews → Reject     │
│  AI (Optional): Suggest best candidates based on company preferences  │
│  Output: Interview requested candidates                               │
└───────────────────────────────┬──────────────────────────────────────┘
                                │
┌───────────────────────────────▼──────────────────────────────────────┐
│                     STAGE 6: INTERVIEW                                │
│  Access: Client, CodersBrain HR (Schedule), Candidate                │
│  Actions: Schedule Interview → Send Calendar Invites → Conduct       │
│           Submit Feedback → Rate Candidate → Decision                 │
│  Note: Video call feature REMOVED (use external tools)                │
│  Output: Interview feedback and hiring decision                       │
└───────────────────────────────┬──────────────────────────────────────┘
                                │
┌───────────────────────────────▼──────────────────────────────────────┐
│                     STAGE 7: OFFER                                    │
│  Access: Client (Create), CodersBrain Manager (View), Candidate      │
│  Actions: Generate Offer Letter → Negotiate → Candidate Accept/Reject│
│           Finalize Terms → Sign Documents                             │
│  Triggers: Commission calculation starts                              │
│  Output: Accepted offer, signed documents                             │
└───────────────────────────────┬──────────────────────────────────────┘
                                │
┌───────────────────────────────▼──────────────────────────────────────┐
│                     STAGE 8: ONBOARDING                               │
│  Access: Client HR, CodersBrain HR, Candidate                        │
│  Actions: Submit Documents → Background Verification → Joining Date  │
│           Onboarding Tasks → First Day → Probation Completion         │
│  Triggers: Commission payment after probation                         │
│  AI (Optional):                                                       │
│    - Auto checklist generation                                        │
│    - Smart reminders for pending items                                │
│    - Document verification automation                                 │
│  Output: Successfully onboarded candidate, commission processed       │
└───────────────────────────────────────────────────────────────────────┘
```

---

## 7. Commission & Payment Flow

### 7.1 Commission Configuration & Calculation

```
SUPER ADMIN PANEL
─────────────────
┌─────────────────────────────────────────────────────────────┐
│          COMMISSION CONFIGURATION                            │
│                                                              │
│  Commission Models:                                          │
│  ┌───────────────────────────────────────────────────────┐  │
│  │ □ Percentage of First Month Salary: [__]%            │  │
│  │ □ Fixed Fee per Placement: ₹ [_______]               │  │
│  │ □ Tiered Based on Role Level:                        │  │
│  │   • Junior: [__]%  • Mid-Level: [__]%                │  │
│  │   • Senior: [__]%  • Executive: [__]%                │  │
│  │ □ Performance Bonus: [__]% (if candidate completes)  │  │
│  │   probation with rating > 4 stars                    │  │
│  └───────────────────────────────────────────────────────┘  │
│                                                              │
│  Job Category Specific Rates:                                │
│  • IT/Software: [__]%                                        │
│  • Finance/Accounting: [__]%                                 │
│  • Sales/Marketing: [__]%                                    │
│  • Operations: [__]%                                         │
│  • Others: [__]%                                             │
│                                                              │
│  Vendor Specific Rates (Override):                           │
│  • Vendor A: [__]% (Premium Partner)                         │
│  • Vendor B: [__]% (New Partner)                             │
│                                                              │
│  Referral Commission:                                         │
│  • Candidate Referral: ₹ [_____] per successful placement   │
│  • Vendor Referral: [__]% of commission from referred vendor│
│  • Client Referral: [__]% for first year placements         │
└─────────────────────────────────────────────────────────────┘
```

### 7.2 Commission Lifecycle Flow

```
OFFER ACCEPTED                 JOINING                    PROBATION
(Day 0)                        (Day 1)                    (Day 90)
─────────────                  ───────                    ─────────
    │                              │                          │
    │ Commission Calculated        │ Commission Accrued       │ Commission
    │ and Logged                   │ Invoice Generated        │ Payment Released
    ▼                              ▼                          ▼
┌──────────────┐             ┌──────────────┐         ┌──────────────┐
│ Commission   │             │ Accrued      │         │ Payment      │
│ Record       │             │ Commission   │         │ Processing   │
│ Created      │  ────────>  │ Waiting for  │  ────>  │ Initiated    │
│              │             │ Confirmation │         │              │
│ Amount: ₹X   │             │              │         │ • Bank Txn   │
│ Vendor: A    │             │ Status:      │         │ • TDS        │
│ Status:      │             │ Pending      │         │ • Invoice    │
│ Pending      │             │              │         │              │
└──────────────┘             └──────────────┘         └──────┬───────┘
                                                             │
                                                             │
                                                             ▼
                                                     ┌──────────────┐
                                                     │ PAID         │
                                                     │ • Email Sent │
                                                     │ • SMS Sent   │
                                                     │ • Dashboard  │
                                                     │   Updated    │
                                                     └──────────────┘
```

### 7.3 Vendor Commission Dashboard

```
╔══════════════════════════════════════════════════════════════════╗
║                    VENDOR COMMISSION DASHBOARD                    ║
╠══════════════════════════════════════════════════════════════════╣
║                                                                   ║
║  Total Earnings:  ₹ 2,45,000                                     ║
║  Pending:         ₹   65,000  (3 candidates in probation)        ║
║  Paid:            ₹ 1,80,000  (8 successful placements)          ║
║                                                                   ║
║  ┌──────────────────────────────────────────────────────────┐   ║
║  │  Recent Commission Activity                               │   ║
║  ├──────────────────────────────────────────────────────────┤   ║
║  │ Candidate         JD Title        Amount   Status  Date   │   ║
║  ├──────────────────────────────────────────────────────────┤   ║
║  │ John Doe          Sr Developer    ₹18,000  PAID    01-Oct│   ║
║  │ Jane Smith        Data Analyst    ₹15,000  Pending 15-Oct│   ║
║  │ Mike Johnson      QA Engineer     ₹12,000  Accrued 20-Oct│   ║
║  └──────────────────────────────────────────────────────────┘   ║
║                                                                   ║
║  ┌──────────────────────────────────────────────────────────┐   ║
║  │  Payment History                    [Download Invoice]    │   ║
║  ├──────────────────────────────────────────────────────────┤   ║
║  │ Oct 2025    ₹ 45,000  [View Invoice] [Download]          │   ║
║  │ Sep 2025    ₹ 38,000  [View Invoice] [Download]          │   ║
║  │ Aug 2025    ₹ 52,000  [View Invoice] [Download]          │   ║
║  └──────────────────────────────────────────────────────────┘   ║
╚══════════════════════════════════════════════════════════════════╝
```

---

## 8. Review & Rating System Flow

### 8.1 Vendor Rating Flow

```
PLACEMENT COMPLETED
───────────────────
         │
         ├──────────────────────────────────┐
         │                                  │
         ▼                                  ▼
┌─────────────────────┐          ┌──────────────────────┐
│ CodersBrain Manager │          │ Client               │
│ Rates Vendor        │          │ Rates Vendor         │
│                     │          │                      │
│ Criteria:           │          │ Criteria:            │
│ • Candidate Quality │          │ • Candidate Quality  │
│ • Response Time     │          │ • Professionalism    │
│ • Professionalism   │          │ • Communication      │
│ • Communication     │          │ • Would Recommend?   │
│ • Overall (1-5⭐)  │          │ • Overall (1-5⭐)    │
│                     │          │                      │
│ Written Feedback    │          │ Written Feedback     │
└──────────┬──────────┘          └──────────┬───────────┘
           │                                │
           └────────────┬───────────────────┘
                        │
                        ▼
              ┌──────────────────┐
              │ Rating Aggregated│
              │                  │
              │ Average: 4.5⭐   │
              │ Total Reviews: 12│
              │                  │
              │ Breakdown:       │
              │ Quality:    4.7  │
              │ Response:   4.5  │
              │ Profession: 4.3  │
              │ Communic:   4.6  │
              └────────┬─────────┘
                       │
                       ▼
              ┌────────────────────┐
              │ Vendor Dashboard   │
              │ Rating Displayed   │
              │                    │
              │ Impact:            │
              │ • Profile Ranking  │
              │ • Job Priority     │
              │ • Trust Badge      │
              └────────────────────┘
```

### 8.2 Candidate Rating Flow

```
INTERVIEW/PLACEMENT COMPLETED
──────────────────────────────
         │
         ├──────────────────────────────────┐
         │                                  │
         ▼                                  ▼
┌─────────────────────┐          ┌──────────────────────┐
│ CodersBrain HR      │          │ Client               │
│ Rates Candidate     │          │ Rates Candidate      │
│                     │          │                      │
│ Criteria:           │          │ Criteria:            │
│ • Tech Skills       │          │ • Tech Skills        │
│ • Communication     │          │ • Cultural Fit       │
│ • Professionalism   │          │ • Performance        │
│ • Overall (1-5⭐)  │          │ • Would Hire Again?  │
│                     │          │ • Overall (1-5⭐)    │
│ Internal Notes      │          │                      │
└──────────┬──────────┘          │ Public Feedback      │
           │                     └──────────┬───────────┘
           │                                │
           └────────────┬───────────────────┘
                        │
                        ▼
              ┌──────────────────┐
              │ Rating Aggregated│
              │                  │
              │ Average: 4.3⭐   │
              │ Total Reviews: 5 │
              │                  │
              │ Visible to:      │
              │ • Candidate      │
              │ • CodersBrain    │
              │ • Future Clients │
              │   (Optional)     │
              └────────┬─────────┘
                       │
                       ▼
              ┌────────────────────┐
              │ Candidate Profile  │
              │ Rating Displayed   │
              │                    │
              │ Impact:            │
              │ • Profile Ranking  │
              │ • Job Matching     │
              │ • Visibility       │
              └────────────────────┘
```

---

## 9. Referral System Flow

### 9.1 Candidate Referral Flow

```
REGISTERED CANDIDATE
────────────────────
         │
         │ Generates Unique
         │ Referral Code
         ▼
┌─────────────────────┐
│ Referral Dashboard  │
│                     │
│ Your Code: ABC123   │
│ [Copy] [Share]      │
│                     │
│ Earnings: ₹ 5,000   │
│ Referrals: 3        │
│ Successful: 2       │
└──────────┬──────────┘
           │
           │ Shares code with
           │ Friend/Colleague
           ▼
┌─────────────────────┐
│ New Candidate       │
│ Registration        │
│                     │
│ Referral Code?      │
│ [ABC123__________]  │
│                     │
│ [Continue]          │
└──────────┬──────────┘
           │
           │ Code Validated
           │ Link Established
           ▼
┌─────────────────────┐
│ New Candidate       │
│ Completes Profile   │
│ Gets Placed         │
└──────────┬──────────┘
           │
           │ After Probation
           │ Completion
           ▼
┌─────────────────────┐
│ Referrer Earns      │
│ ₹ 2,500 Bonus       │
│                     │
│ Notification Sent   │
│ Amount Credited     │
└─────────────────────┘
```

### 9.2 Vendor Referral Flow

```
REGISTERED VENDOR
─────────────────
         │
         │ Refers New
         │ Client/Vendor
         ▼
┌─────────────────────┐
│ Referral Dashboard  │
│                     │
│ Refer Client        │
│ Refer Vendor        │
│                     │
│ Lifetime Earnings   │
│ from Referrals:     │
│ ₹ 45,000            │
└──────────┬──────────┘
           │
           │ Shares referral
           │ with new party
           ▼
┌─────────────────────┐
│ New Client/Vendor   │
│ Registration        │
│                     │
│ Referred by:        │
│ Vendor XYZ          │
└──────────┬──────────┘
           │
           │ KYC Approved
           │ First Placement
           ▼
┌─────────────────────┐
│ Referrer Earns      │
│ Commission %        │
│                     │
│ Lifetime Benefit:   │
│ X% of all           │
│ placements by       │
│ referred party      │
└─────────────────────┘
```

---

## 10. AI Automation Flow (Optional)

### 10.1 AI Feature Toggle System

```
SUPER ADMIN PANEL
─────────────────
┌──────────────────────────────────────────────────────────┐
│              AI FEATURES CONFIGURATION                    │
│                                                           │
│  ┌────────────────────────────────────────────────────┐  │
│  │ Feature                    Status      Confidence  │  │
│  ├────────────────────────────────────────────────────┤  │
│  │ Auto Job Assignment        [ON]  OFF   [75%___]   │  │
│  │ Auto Candidate Matching    [ON]  OFF   [80%___]   │  │
│  │ Auto Resume Screening       ON  [OFF]  [70%___]   │  │
│  │ Auto Shortlisting          [ON]  OFF   [85%___]   │  │
│  │ Smart Notifications        [ON]  OFF   [90%___]   │  │
│  │ Workflow Automation        [ON]  OFF   [75%___]   │  │
│  │ AI Analytics & Insights    [ON]  OFF   [80%___]   │  │
│  └────────────────────────────────────────────────────┘  │
│                                                           │
│  Fallback Behavior:                                       │
│  ☑ Fallback to Manual if AI confidence < threshold       │
│  ☑ Show AI reasoning for decisions                        │
│  ☑ Allow human override for all AI decisions             │
│  ☑ Log all AI decisions for audit                        │
│                                                           │
│  [Save Configuration]                                     │
└──────────────────────────────────────────────────────────┘
```

### 10.2 AI-Powered Job Assignment Flow

```
WITHOUT AI (Manual)                WITH AI (Optional)
───────────────────                ──────────────────

Manager receives JD           Manager receives JD
         │                              │
         ▼                              ▼
Manually reviews                ┌──────────────────┐
vendors' profiles               │ AI Analysis      │
         │                      │ • Vendor Specs   │
         ▼                      │ • Past Success   │
Selects vendors                 │ • Capacity       │
based on memory                 │ • Performance    │
         │                      └────────┬─────────┘
         ▼                               │
Assigns to 2-3 vendors                   ▼
         │                      ┌──────────────────┐
         │                      │ AI Suggests      │
         │                      │ Top 5 Vendors    │
         │                      │ with Scores:     │
         │                      │                  │
         │                      │ 1. Vendor A: 92% │
         │                      │ 2. Vendor B: 88% │
         │                      │ 3. Vendor C: 85% │
         │                      └────────┬─────────┘
         │                               │
         │                               ▼
         │                      ┌──────────────────┐
         │                      │ Manager Reviews  │
         │                      │ AI Suggestions   │
         │                      │                  │
         │                      │ [Accept All]     │
         │                      │ [Modify]         │
         │                      │ [Manual Select]  │
         │                      └────────┬─────────┘
         │                               │
         └───────────────────┬───────────┘
                             │
                             ▼
                  ┌──────────────────┐
                  │ JD Assigned      │
                  │ Notifications    │
                  │ Sent             │
                  └──────────────────┘

Time Saved: ~30 minutes per JD
Accuracy: Improved by AI learning from past placements
```

### 10.3 AI-Powered Candidate Matching Flow

```
VENDOR UPLOADS CANDIDATE
────────────────────────
         │
         ▼
┌─────────────────────────────────────────┐
│ AI Resume Parser                         │
│ • Extracts: Skills, Experience, Education│
│ • Identifies: Tech Stack, Domain         │
│ • Calculates: Years of Experience        │
│ • Detects: Career Trajectory             │
└──────────────────┬──────────────────────┘
                   │
                   ▼
┌─────────────────────────────────────────┐
│ AI Matching Engine                       │
│ • Compares with Open JDs                 │
│ • Scores Relevance (0-100%)              │
│ • Considers: Skills, Experience, Location│
│ • Analyzes: Salary Fit, Availability     │
└──────────────────┬──────────────────────┘
                   │
                   ▼
┌─────────────────────────────────────────┐
│ AI Match Results                         │
│                                          │
│ Top 3 Matching JDs:                      │
│ 1. Senior Developer @ Company A - 95%    │
│    ✓ 8/10 skills match                   │
│    ✓ 5 years exp (req: 5+)               │
│    ✓ Same location                       │
│    ⚠ Salary slightly above budget        │
│                                          │
│ 2. Tech Lead @ Company B - 88%           │
│    ✓ 7/10 skills match                   │
│    ✓ 7 years exp (req: 5+)               │
│    ⚠ Remote (preference: hybrid)         │
│                                          │
│ 3. Engineer @ Company C - 82%            │
│    ✓ 6/8 skills match                    │
│    ✓ 4 years exp (req: 3-5)              │
│    ✓ Perfect salary fit                  │
│                                          │
│ [Auto-Apply] [Review] [Ignore]           │
└──────────────────────────────────────────┘
```

### 10.4 AI Transparency & Control

```
AI DECISION SCREEN
──────────────────
┌────────────────────────────────────────────────────────┐
│  AI Recommendation: Shortlist Candidate John Doe        │
│                                                         │
│  Confidence Score: 85%  [Confidence Bar: ████████▒▒]   │
│                                                         │
│  Reasoning:                                             │
│  ✓ Skills match: 9/10 required skills present          │
│  ✓ Experience: 5 years (requirement: 3-5 years)        │
│  ✓ Education: Master's degree in relevant field        │
│  ✓ Location: Same city as job                          │
│  ⚠ Notice period: 60 days (preferred: 30 days)         │
│  ⚠ Current salary: 10% higher than budget              │
│                                                         │
│  Similar successful placements: 12                      │
│  • 10 candidates with similar profile hired            │
│  • Average performance rating: 4.3/5                   │
│                                                         │
│  Manager Actions:                                       │
│  [✓ Accept AI Recommendation]                          │
│  [✗ Reject with Reason]                                │
│  [👁 Review Manually]                                   │
│  [📝 Provide Feedback to AI]                           │
└────────────────────────────────────────────────────────┘
```

---

## 11. Security & Access Control Architecture

### 11.1 Role-Based Access Control (RBAC) Matrix

```
FEATURE ACCESS MATRIX
─────────────────────────────────────────────────────────────────

                          │ Super │ Mgr │ HR │ Vendor│Client│Candidate
Feature                   │ Admin │     │    │       │      │
──────────────────────────┼───────┼─────┼────┼───────┼──────┼─────────
System Config             │  ✅   │  ❌ │ ❌ │  ❌   │  ❌  │   ❌
User Management           │  ✅   │  ❌ │ ❌ │  ❌   │  ❌  │   ❌
KYC Approval              │  ✅   │  ✅ │ ❌ │  ❌   │  ❌  │   ❌
Commission Config         │  ✅   │  ❌ │ ❌ │  ❌   │  ❌  │   ❌
AI Feature Toggle         │  ✅   │  ❌ │ ❌ │  ❌   │  ❌  │   ❌
JD Create                 │  ✅   │  ✅ │ ❌ │  ❌   │  ✅  │   ❌
JD Edit                   │  ✅   │  ✅ │ ❌ │  ❌   │  ✅* │   ❌
JD Assignment             │  ✅   │  ✅ │ ❌ │  ❌   │  ❌  │   ❌
Upload Candidates         │  ❌   │  ❌ │ ❌ │  ✅   │  ❌  │   ❌
View All Candidates       │  ✅   │  ✅ │ ✅ │  ❌** │  ❌**│   ❌
View Own Candidates       │  N/A  │ N/A │N/A │  ✅   │  N/A │   ✅
Share Candidates          │  ❌   │  ❌ │ ❌ │  ✅   │  ❌  │   ❌
Candidate Screening       │  ✅   │  ✅ │ ✅ │  ❌   │  ❌  │   ❌
Candidate Shortlisting    │  ✅   │  ✅ │ ❌ │  ❌   │  ❌  │   ❌
Interview Scheduling      │  ✅   │  ✅ │ ✅ │  ❌   │  ✅  │   ✅
Interview Feedback        │  ✅   │  ✅ │ ✅ │  ❌   │  ✅  │   ❌
Offer Creation            │  ✅   │  ✅ │ ✅ │  ❌   │  ✅  │   ❌
Offer Accept/Reject       │  ❌   │  ❌ │ ❌ │  ❌   │  ❌  │   ✅
Commission Tracking       │  ✅   │  ✅ │ ❌ │  ✅   │  ❌  │   ❌
Commission Payment        │  ✅   │  ❌ │ ❌ │  ❌   │  ❌  │   ❌
Review Vendors            │  ✅   │  ✅ │ ✅ │  ❌   │  ✅  │   ❌
Review Candidates         │  ✅   │  ✅ │ ✅ │  ❌   │  ✅  │   ❌
View Reviews              │  ✅   │  ✅ │ ✅ │  ✅   │  ✅  │   ✅
Referral System           │  ✅   │  ✅ │ ✅ │  ✅   │  ✅  │   ✅
Analytics Dashboard       │  ✅   │  ✅ │ ✅ │  ✅*** │ ✅***│  ✅***
Audit Logs                │  ✅   │  ❌ │ ❌ │  ❌   │  ❌  │   ❌

* Client can only edit own JDs
** Can view only shared/shortlisted candidates
*** Limited to own data only
```

### 11.2 Data Encryption & Security Layers

```
┌─────────────────────────────────────────────────────────────────┐
│                    SECURITY ARCHITECTURE                         │
└─────────────────────────────────────────────────────────────────┘

LAYER 1: NETWORK SECURITY
──────────────────────────
┌─────────────────────────────────────────────────────────────────┐
│ • AWS WAF (Web Application Firewall)                             │
│ • DDoS Protection (AWS Shield Advanced)                          │
│ • VPC (Virtual Private Cloud) with Private Subnets              │
│ • Security Groups & Network ACLs                                 │
│ • IP Whitelisting for Admin Panel (Optional)                    │
└─────────────────────────────────────────────────────────────────┘

LAYER 2: APPLICATION SECURITY
──────────────────────────────
┌─────────────────────────────────────────────────────────────────┐
│ • TLS 1.3 Encryption (All Communications)                        │
│ • JWT with Refresh Tokens (Authentication)                       │
│ • RBAC (Role-Based Access Control)                               │
│ • Input Validation & Sanitization (Joi)                          │
│ • CSRF Protection (Anti-CSRF Tokens)                             │
│ • XSS Protection (CSP Headers)                                   │
│ • SQL Injection Prevention (Parameterized Queries)               │
│ • Rate Limiting (1000 req/hour per user)                         │
│ • Session Timeout (30 minutes inactivity)                        │
└─────────────────────────────────────────────────────────────────┘

LAYER 3: DATA SECURITY
──────────────────────
┌─────────────────────────────────────────────────────────────────┐
│ • Encryption at Rest: AES-256                                    │
│ • Encryption in Transit: TLS 1.3                                 │
│ • PII Masking for Unauthorized Users                             │
│ • Data Isolation (Vendor Candidate DB)                           │
│ • Audit Logging (All Access & Modifications)                     │
│ • Secure File Storage (S3 with Encryption)                       │
│ • Database Encryption (PostgreSQL/MongoDB)                       │
│ • Secret Management (AWS Secrets Manager)                        │
└─────────────────────────────────────────────────────────────────┘

LAYER 4: AUTHENTICATION & AUTHORIZATION
────────────────────────────────────────
┌─────────────────────────────────────────────────────────────────┐
│ • Multi-Factor Authentication (MFA) for Admin (Mandatory)        │
│ • Password Hashing (bcrypt with salt)                            │
│ • Password Policy (8+ chars, complexity requirements)            │
│ • Account Lockout (5 failed attempts)                            │
│ • Session Management (Redis with expiry)                         │
│ • OAuth 2.0 Integration (Optional SSO)                           │
│ • Granular Permissions (15+ predefined roles)                    │
└─────────────────────────────────────────────────────────────────┘

LAYER 5: COMPLIANCE & MONITORING
─────────────────────────────────
┌─────────────────────────────────────────────────────────────────┐
│ • GDPR Compliance (Right to be forgotten, Data portability)     │
│ • SOC 2 Type II Compliance (Annual audits)                       │
│ • Regular Penetration Testing (Quarterly)                        │
│ • Vulnerability Scanning (Weekly automated)                      │
│ • Security Incident Response Plan (24/7 monitoring)              │
│ • Audit Trail (All actions logged with timestamp & user)         │
│ • Compliance Reports (Automated generation)                      │
└─────────────────────────────────────────────────────────────────┘
```

### 11.3 Audit Logging System

```
AUDIT LOG ENTRY EXAMPLE
───────────────────────

{
  "timestamp": "2025-10-29T14:35:22Z",
  "event_type": "CANDIDATE_PROFILE_SHARED",
  "user_id": "vendor_123",
  "user_role": "VENDOR",
  "action": "SHARE_CANDIDATE",
  "resource_type": "CANDIDATE_PROFILE",
  "resource_id": "candidate_456",
  "details": {
    "shared_with": "codersbrain_manager_789",
    "jd_id": "jd_101",
    "profile_fields_shared": [
      "personal_info",
      "work_experience",
      "education",
      "skills",
      "documents",
      "assessments"
    ]
  },
  "ip_address": "203.0.113.42",
  "user_agent": "Mozilla/5.0...",
  "session_id": "sess_xyz789",
  "result": "SUCCESS"
}
```

---

## 12. Technical Architecture

### 12.1 High-Level System Architecture

```
┌───────────────────────────────────────────────────────────────────────────┐
│                              CLIENT LAYER                                  │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐  │
│  │   Admin      │  │   Vendor     │  │   Client     │  │  Candidate   │  │
│  │  Dashboard   │  │  Dashboard   │  │  Dashboard   │  │  Dashboard   │  │
│  │  (React)     │  │  (React)     │  │  (React)     │  │  (React)     │  │
│  └──────┬───────┘  └──────┬───────┘  └──────┬───────┘  └──────┬───────┘  │
└─────────┼───────────────────┼───────────────────┼───────────────────┼──────┘
          │                   │                   │                   │
          └───────────────────┴───────────────────┴───────────────────┘
                                      │
┌─────────────────────────────────────┼─────────────────────────────────────┐
│                               API GATEWAY                                  │
│                          (Load Balancer + WAF)                             │
└─────────────────────────────────────┬─────────────────────────────────────┘
                                      │
┌─────────────────────────────────────┼─────────────────────────────────────┐
│                           APPLICATION LAYER                                │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐  │
│  │   Auth       │  │  User        │  │  JD          │  │  Candidate   │  │
│  │  Service     │  │  Service     │  │  Service     │  │  Service     │  │
│  │  (Node.js)   │  │  (Node.js)   │  │  (Node.js)   │  │  (Node.js)   │  │
│  └──────┬───────┘  └──────┬───────┘  └──────┬───────┘  └──────┬───────┘  │
│         │                  │                  │                  │         │
│  ┌──────┴───────┐  ┌──────┴───────┐  ┌──────┴───────┐  ┌──────┴───────┐  │
│  │ Commission   │  │  Review      │  │  Referral    │  │  Notification│  │
│  │  Service     │  │  Service     │  │  Service     │  │  Service     │  │
│  │  (Node.js)   │  │  (Node.js)   │  │  (Node.js)   │  │  (Node.js)   │  │
│  └──────┬───────┘  └──────┬───────┘  └──────┬───────┘  └──────┬───────┘  │
└─────────┼───────────────────┼───────────────────┼───────────────────┼──────┘
          │                   │                   │                   │
┌─────────┼───────────────────┼───────────────────┼───────────────────┼──────┐
│                              DATA LAYER                                    │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐  │
│  │  PostgreSQL  │  │   MongoDB    │  │     Redis    │  │ Elasticsearch│  │
│  │  (Primary)   │  │  (Documents) │  │   (Cache)    │  │   (Search)   │  │
│  └──────────────┘  └──────────────┘  └──────────────┘  └──────────────┘  │
│                                                                            │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐                    │
│  │   AWS S3     │  │  RabbitMQ    │  │  AWS SES/SNS │                    │
│  │  (Files)     │  │  (Queue)     │  │  (Email/SMS) │                    │
│  └──────────────┘  └──────────────┘  └──────────────┘                    │
└────────────────────────────────────────────────────────────────────────────┘
                                      │
┌─────────────────────────────────────┼─────────────────────────────────────┐
│                        AI/ML LAYER (OPTIONAL)                              │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐  │
│  │  Resume      │  │  Matching    │  │  Scoring     │  │  Analytics   │  │
│  │  Parser      │  │  Engine      │  │  Engine      │  │  Engine      │  │
│  │  (Python)    │  │  (Python)    │  │  (Python)    │  │  (Python)    │  │
│  └──────────────┘  └──────────────┘  └──────────────┘  └──────────────┘  │
└────────────────────────────────────────────────────────────────────────────┘
```

### 12.2 Database Schema Overview

```
┌────────────────────────────────────────────────────────────────────┐
│                         POSTGRESQL SCHEMA                          │
└────────────────────────────────────────────────────────────────────┘

USERS TABLE
───────────
- id (PK)
- email (unique)
- mobile (unique)
- password_hash
- role (ENUM: super_admin, manager, hr, vendor, client, candidate)
- status (ENUM: pending, approved, rejected, suspended)
- created_at
- updated_at

USER_PROFILES TABLE
───────────────────
- id (PK)
- user_id (FK -> users.id)
- full_name
- company_name (for vendors/clients)
- profile_data (JSONB) -- role-specific data
- kyc_status
- kyc_documents (JSONB)
- created_at
- updated_at

JOB_DESCRIPTIONS TABLE
──────────────────────
- id (PK)
- client_id (FK -> users.id)
- title
- description (TEXT)
- requirements (JSONB)
- budget_min
- budget_max
- location
- job_type (ENUM: fulltime, parttime, contract, freelance)
- commission_rate
- status (ENUM: draft, active, assigned, closed)
- created_by (FK -> users.id)
- updated_by (FK -> users.id)
- created_at
- updated_at

JD_ASSIGNMENTS TABLE
────────────────────
- id (PK)
- jd_id (FK -> job_descriptions.id)
- vendor_id (FK -> users.id)
- assigned_by (FK -> users.id)
- assigned_at
- status (ENUM: assigned, accepted, declined, completed)
- ai_confidence_score (if AI used)

CANDIDATES TABLE
────────────────
- id (PK)
- vendor_id (FK -> users.id) -- NULL if direct registration
- user_id (FK -> users.id) -- if candidate registers directly
- profile_data (JSONB) -- complete profile structure
- resume_url
- status (ENUM: active, placed, inactive)
- visibility (ENUM: private, shared, public)
- created_at
- updated_at

CANDIDATE_SHARES TABLE
──────────────────────
- id (PK)
- candidate_id (FK -> candidates.id)
- shared_by (FK -> users.id) -- vendor
- shared_with (FK -> users.id) -- codersbrain manager
- jd_id (FK -> job_descriptions.id)
- shared_at
- profile_snapshot (JSONB) -- copy of profile at share time

PIPELINE_STAGES TABLE
─────────────────────
- id (PK)
- candidate_id (FK -> candidates.id)
- jd_id (FK -> job_descriptions.id)
- current_stage (ENUM: sourced, screened, shortlisted, interview, offer, onboarding)
- stage_data (JSONB) -- stage-specific info
- updated_by (FK -> users.id)
- updated_at

INTERVIEWS TABLE
────────────────
- id (PK)
- candidate_id (FK -> candidates.id)
- jd_id (FK -> job_descriptions.id)
- scheduled_at
- scheduled_by (FK -> users.id)
- status (ENUM: scheduled, completed, cancelled, rescheduled)
- feedback (TEXT)
- rating
- created_at
- updated_at

OFFERS TABLE
────────────
- id (PK)
- candidate_id (FK -> candidates.id)
- jd_id (FK -> job_descriptions.id)
- client_id (FK -> users.id)
- offer_details (JSONB)
- status (ENUM: draft, sent, accepted, rejected, withdrawn)
- sent_at
- responded_at
- created_at
- updated_at

COMMISSIONS TABLE
─────────────────
- id (PK)
- vendor_id (FK -> users.id)
- candidate_id (FK -> candidates.id)
- jd_id (FK -> job_descriptions.id)
- amount
- status (ENUM: pending, accrued, paid, disputed)
- payment_date
- invoice_url
- created_at
- updated_at

REVIEWS TABLE
─────────────
- id (PK)
- reviewer_id (FK -> users.id)
- reviewee_id (FK -> users.id)
- reviewee_type (ENUM: vendor, candidate)
- rating
- criteria_ratings (JSONB)
- feedback (TEXT)
- jd_id (FK -> job_descriptions.id) -- optional, context
- created_at

REFERRALS TABLE
───────────────
- id (PK)
- referrer_id (FK -> users.id)
- referee_id (FK -> users.id) -- newly registered user
- referral_code
- referral_type (ENUM: candidate, vendor, client)
- status (ENUM: pending, successful, failed)
- reward_amount
- reward_paid
- created_at

AUDIT_LOGS TABLE
────────────────
- id (PK)
- user_id (FK -> users.id)
- action
- resource_type
- resource_id
- details (JSONB)
- ip_address
- user_agent
- created_at
```

---

## 13. Data Flow Diagrams

### 13.1 End-to-End Recruitment Flow

```
CLIENT                CODERSBRAIN           VENDOR              CANDIDATE
──────                ───────────           ──────              ─────────

 [1]                                                                
 │ Post JD                                                          
 │────────────────────>│                                            
 │                     │[2]                                         
 │                     │ Review & Edit JD                           
 │                     │                                            
 │                     │[3] Assign to Vendor                        
 │                     │────────────────────>│                      
 │                     │                     │[4]                   
 │                     │                     │ Search & Upload      
 │                     │                     │ Candidates           
 │                     │                     │                      
 │                     │      [5] Share      │                      
 │                     │<────────────────────│                      
 │                     │      Profiles       │                      
 │                     │                     │                      
 │                     │[6] Screen           │                      
 │                     │ & Shortlist         │                      
 │                     │                     │         [6a]         
 │                     │                     │         Direct       
 │                     │<────────────────────────────Register       
 │                     │                     │                      
 │      [7] Send       │                     │                      
 │<────────────────────│                     │                      
 │   Shortlisted       │                     │                      
 │   Profiles          │                     │                      
 │                     │                     │                      
 │[8] Request          │                     │                      
 │ Interviews          │                     │                      
 │────────────────────>│─────────[9]────────────────────────────>  
 │                     │     Schedule                         │    
 │                     │     Interview                        │    
 │                     │                                      │    
 │        [10] Conduct Interview                             │    
 │<──────────────────────────────────────────────────────────┘    
 │                     │                                            
 │[11] Submit          │                                            
 │ Feedback            │                                            
 │────────────────────>│                                            
 │                     │                                            
 │[12] Generate        │                                            
 │ Offer               │                     │                      
 │────────────────────>│─────────[13]────────────────────────────> 
 │                     │     Send Offer                       │    
 │                     │                                      │    
 │                     │        [14] Accept/Reject           │    
 │                     │<─────────────────────────────────────┘    
 │                     │                                            
 │                     │[15] Commission                             
 │                     │     Calculated                             
 │                     │─────────────────────>│                     
 │                     │                                            
 │[16] Onboarding      │                                            
 │ Process             │                                            
 │────────────────────>│                                            
 │                     │                                            
 │                     │[17] Commission                             
 │                     │     Payment                                
 │                     │─────────────────────>│                     
 │                     │     (After                                 
 │                     │      Probation)                            
```

### 13.2 Data Privacy & Access Flow

```
DATA FLOW WITH ACCESS CONTROL
──────────────────────────────

VENDOR UPLOADS CANDIDATE PROFILE
─────────────────────────────────
         │
         ├───> Stored in Vendor's Private DB
         │     • Access: Vendor Only
         │     • Encryption: AES-256
         │     • Audit: Logged
         │
         ├───> Vendor Clicks "Share for JD#123"
         │     • Trigger: Explicit Action
         │     • Validation: Complete Profile Check
         │     • Audit: Logged (who, when, what)
         │
         ├───> Profile Copied to Shared DB
         │     • Access: CodersBrain Manager
         │     • Full Profile: All Fields
         │     • Original: Still in Vendor DB
         │     • Audit: Logged
         │
         ├───> Manager Reviews & Shortlists
         │     • Action: Screening & Scoring
         │     • Access: Full Read/Write
         │     • Audit: All Actions Logged
         │
         ├───> Shortlisted Profile Sent to Client
         │     • Access: Client (for this JD only)
         │     • Full Profile: All Fields Visible
         │     • Restriction: No Download Restrictions
         │     • Audit: Client Access Logged
         │
         └───> Client Reviews Profile
               • Action: Interview Request
               • Access: Read Only (no edit)
               • Audit: All Views Logged

DIRECT CANDIDATE REGISTRATION
──────────────────────────────
         │
         ├───> Stored in CodersBrain DB
         │     • Access: CodersBrain Manager/HR
         │     • Encryption: AES-256
         │     • Privacy: Candidate Controls Visibility
         │
         ├───> Candidate Applies to JD
         │     • Trigger: Candidate Action
         │     • Access: Profile Shared with Manager
         │     • Audit: Application Logged
         │
         └───> Same Flow as Vendor-Shared Candidates
```

---

## SUMMARY: Platform Flow in Simple Terms

1. **Registration & Onboarding**
   - Users choose role: Vendor/Client/Candidate/Freelancer
   - Complete KYC (documents, verification)
   - Admin approves after verification
   - Full platform access granted

2. **Job Posting & Assignment**
   - Client posts job requirements
   - CodersBrain Manager reviews and edits
   - Manager assigns to vendors (manual or AI-suggested)
   - Vendors receive notifications and accept

3. **Candidate Sourcing**
   - Vendors upload candidate profiles (bulk or individual)
   - Profiles stored in vendor's private database
   - Vendor explicitly shares relevant profiles with CodersBrain
   - Direct candidates can also register on platform

4. **Screening & Shortlisting**
   - CodersBrain HR/Manager screens candidates
   - AI optionally assists with resume parsing and scoring
   - Manager shortlists top candidates
   - Complete profiles sent to client

5. **Client Review & Interview**
   - Client reviews shortlisted candidates
   - Requests interviews for selected candidates
   - Interviews scheduled (no video call in platform)
   - Client submits feedback and ratings

6. **Offer & Onboarding**
   - Client generates offer letter
   - Candidate accepts/rejects
   - Commission calculated for vendor
   - Onboarding process initiated
   - Commission paid after probation

7. **Reviews & Ratings**
   - Client rates vendor and candidate
   - CodersBrain rates vendor and candidate
   - Ratings impact future job assignments
   - Reviews visible on dashboards

8. **Commission & Referrals**
   - Commission configured by admin
   - Calculated automatically on placement
   - Paid after probation completion
   - Referral rewards for successful referrals

9. **AI Automation (Optional)**
   - All AI features can be toggled on/off
   - AI suggests vendors for jobs
   - AI matches candidates to jobs
   - AI assists in screening and scoring
   - Human oversight always available

10. **Security & Privacy**
    - Role-based access control (RBAC)
    - Data encryption at rest and in transit
    - Vendor candidate data strictly private
    - Audit logs for all actions
    - GDPR and SOC 2 compliant

---

**END OF ARCHITECTURE & FLOWCHART GUIDE**

This document provides a comprehensive understanding of the AI-Powered Recruitment Platform architecture, workflows, and data flows. All processes are designed with industry-standard security, data privacy, and user experience in mind.

For technical implementation details, refer to the Technical Specification Document and API Documentation.

**Next Steps:**
1. Review and approve architecture
2. Begin Week 1 development (Project Setup)
3. Set up development environment
4. Initialize database schema
5. Create base authentication system

**Contact:**
- HayCod Solutions: Rohit Giri (rohit.giri@haycod.com, +91 86605 11585)
- CodersBrain: Sonu Gupta (sk@codersbrain.com, +91 83107 23070)
