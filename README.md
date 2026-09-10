# voyagexp-project-agile-practice-exam
VoyageXP Project - Certification Practice Exams Practice Website

A Job Hackers (TJH) × Chingu VoyageXP project — an open-source quiz engine that helps community members practice for Scrum Master and Product Owner certification exams.

## Table of Contents

* [Overview](#bookmark=id.62s850jrxybt)  
* [About This Project](#bookmark=id.wfs3ivczfwdl)  
* [General Instructions](#bookmark=id.rqxt1p59sxam)  
* [Roles & Responsibilities](#bookmark=id.1a8n859jbvuv)  
* [Glossary](#bookmark=id.q3vb91aje)  
* [Requirements & Specifications](#bookmark=id.6ypc7qxp4yyf)  
  * [1\. Question Bank & Content Management](#bookmark=id.2jm8dirr2uxr)  
  * [2\. Question Editor (Admin)](#bookmark=id.k26uivj4rkdi)  
  * [3\. User Accounts & Answer Journal](#bookmark=id.z8a9x2ewez66)  
  * [4\. Exam Presenter (Test-Taking UI)](#bookmark=id.kwup1hw1hff2)  
  * [5\. Reporting & Analytics](#bookmark=id.5ij83g50pu8b)  
  * [6\. UX Design Requirements](#bookmark=id.vh3xxme0194j)  
  * [7\. Technical Requirements](#bookmark=id.rhyhet2ez9ot)  
  * [8\. Non-Functional Requirements](#bookmark=id.837t0d9xx07w)  
* [MVP vs. Stretch Goals](#bookmark=id.fum4ui4ti4qg)  
* [Suggested Development Milestones](#bookmark=id.xsv6vg48hmxj)  
* [Content Sourcing & Vetting Workflow](#bookmark=id.oxqon99s5yrp)  
* [Ownership, IP & Governance](#bookmark=id.r9avc3nqmso0)  
* [Working Agreement](#bookmark=id.d0r6l2jjdhr2)  
* [Acknowledgements](#bookmark=id.iz5gclr9nqpr)  
* [About Chingu](#bookmark=id.2zlh5ob6kdu)

## Overview

This project builds a **question-rendering system**: it stores exam questions in a database, presents them to a user in a defined order, captures the user's answers, evaluates them, and gives the user feedback while persisting their results over time.

The initial use case is helping people prepare for Scrum Master and Product Owner certification exams offered by [scrum.org](http://scrum.org) and [scrumalliance.org](http://scrumalliance.org) — effectively a modern, actively maintained successor to sites like the [mlapshin.com Scrum quizzes](https://mlapshin.com/index.php/scrum-quizzes/).

Although the first release targets Scrum certifications, the engine itself must be built as a **general-purpose question-review tool** so it can be reused for other exams and subject areas in the future.

## About This Project

The Job Hackers (TJH) is partnering with Chingu to build this application through one or more Chingu VoyageXP sessions. Unlike most VoyageXP projects, which produce a demo, **this is a real product** that TJH will deploy, maintain, and use with its community going forward. TJH will own the deployed instance and will provide and approve the exam questions; Chingu provides the initial codebase and VoyageXP teams to build it.

Because this proposal is expected to span more than one VoyageXP, treat the specifications below as the full target scope, and the [MVP vs. Stretch Goals](#bookmark=id.fum4ui4ti4qg) and [Suggested Development Milestones](#bookmark=id.xsv6vg48hmxj) sections as guidance for what a single team/VoyageXP should realistically aim to finish. **It is far better to fully and correctly implement a smaller slice of this scope than to partially implement all of it.**

## General Instructions

This project is designed to be worked on by a **team**: a Product Owner, a Scrum Master, a UI/UX Designer, and 3–5 Web Developers. Your team should thoroughly read and understand the requirements below, and manage the work using Scrum/Agile practices (sprints, backlog, standups, retros, etc.), consistent with the [Chingu VoyageXP Handbook](https://github.com/chingu-voyages/Handbook/blob/main/docs/guides/voyage/voyage.md#voyage-guide) if you are working within a VoyageXP.

A few things to keep in mind:

* **Scope discipline matters.** Read [MVP vs. Stretch Goals](#bookmark=id.fum4ui4ti4qg) before writing your backlog, and agree as a team on what "done" looks like for your VoyageXP before you start building.  
* **This is a real, maintained product**, not a disposable demo. Favor clean, documented, extensible code over quick hacks — a future team will build on top of what you deliver.  
* **No plagiarized or copyrighted exam content.** Questions must be reworded/original recollections vetted by a Subject Matter Expert (SME), never copied verbatim from a paid or copyrighted source. Build the duplicate/flagging tooling described below to help enforce this.  
* **The deliverable must be deployable**, not just running locally. See [Technical Requirements](#bookmark=id.rhyhet2ez9ot) for the container and hosting expectations.  
* Your team's GitHub repo must contain a well-written `README.md` describing what your team built, how to run it, and a link to the deployed version, along with any acceptance criteria you defined for stretch items you implemented.  
* This app is being developed under the AGPL and the README must contain a copy of this license.

## Roles & Responsibilities

| Role | Primary Responsibilities on This Project |
| :---- | :---- |
| **Product Owner** | Own and prioritize the backlog against the [Requirements & Specifications](#bookmark=id.6ypc7qxp4yyf); translate the business goals below into user stories and acceptance criteria; decide what's in/out of scope for the current VoyageXP; be the voice of TJH and end users (exam takers, Question Managers, admins) for the team. |
| **Scrum Master** | Facilitate ceremonies (planning, standups, review, retro); track and remove blockers; keep the team aligned with the [Working Agreement](#bookmark=id.d0r6l2jjdhr2) and Chingu VoyageXP cadence; coordinate with Chingu leadership's Lean Coffee / Technical Roundtable sessions. |
| **UI/UX Designer** | Produce wireframes and a design system covering, at minimum, the exam-taking screen, the question editor/admin screens, the results & answer-journal screens, and account/auth screens (see [UX Design Requirements](#bookmark=id.vh3xxme0194j)); ensure accessible, responsive design. |
| **Web Developers (3–5)** | Implement the functional and technical requirements below, split across frontend, backend, and database work as the team agrees; write tests; produce deployment documentation. |

## Glossary

* **TJH** — The Job Hackers, the organization sponsoring and owning this product.  
* **Chingu** — The organization running the VoyageXP program that provides the development team(s) for this project.  
* **VoyageXP** — A 10-week, Agile, team-based project sprint run by Chingu.  
* **SME** — Subject Matter Expert; a person qualified to write or approve exam questions and answer keys for a given certification.  
* **Questions Manager** — A non-technical team/role responsible for the content of the question bank for a given certification.  
* **PSM / PSPO** — Professional Scrum Master / Professional Scrum Product Owner certifications from scrum.org.  
* **CSM / CSPO** — Certified ScrumMaster / Certified Scrum Product Owner certifications from Scrum Alliance.

## Requirements and Specifications

The application has four user-facing/back-office capabilities (Question Bank, Question Editor, User Accounts & Journal, and the Exam Presenter), plus reporting, UX, and technical requirements that cut across all of them.

### 1\. Question Bank & Content Management

- [ ] Questions are stored in a database (PostgreSQL recommended) with, at minimum: question text, certification/category, answer type, correct answer(s)/answer key, status (draft / pending review / approved / rejected / flagged), submitted-by, approved-by, and timestamps.  
- [ ] Questions are organized by **certification/category** (e.g., scrum.org PSM, scrum.org PSPO, Scrum Alliance CSM, Scrum Alliance CSPO) so a user can pick which practice exam to take.  
- [ ] The schema must support at least three answer types:  
      - [ ] **Multiple choice** — one or more correct options out of a set of choices.  
      - [ ] **Short answer** — free-text answer, optionally graded with **fuzzy matching** (e.g., Postgres trigram/fuzzy-match extensions, or a graph DB such as Neo4j) to tolerate minor misspellings.  
      - [ ] **Essay** — free-text answer graded against a structured "key," written in a defined markup format (Markdown recommended) where required terms are marked in *italics* and AI-evaluated concepts are marked in **bold**. (See [Stretch Goals](#bookmark=id.fum4ui4ti4qg) — AI-assisted essay grading is not required for MVP.)  
- [ ] The system must support **user-submitted questions**: any registered user can propose a question, which enters a "pending" state until an SME/admin approves, edits, or rejects it.  
- [ ] Approved questions only are eligible to be served in a practice exam.  
- [ ] The system must detect and flag likely **duplicate submissions** (e.g., near-identical question text) to reduce redundant review work and reduce IP-theft risk.  
- [ ] No copyrighted/plagiarized question content is permitted; the submission and review flow must make it easy for an SME to reject content on this basis.

### 2\. Question Editor (Admin)

- [ ] Admin-only screen(s) to review pending/flagged questions and **approve, edit, or reject** them.  
- [ ] Admins can create, edit, and retire questions directly.  
- [ ] Admins can grant or revoke **admin (Questions Manager) privileges** for other users.  
- [ ] Admins can **remove or block** problematic users.  
- [ ] Admins can **edit a user's recorded answer** after the fact (e.g., when a short-answer or essay response was ambiguous and needs manual correction/regrading).  
- [ ] (Stretch) Admins can import a **purchased/licensed question bank** in bulk.

### 3\. User Accounts & Answer Journal

- [ ] Users can register and authenticate (exact auth method — e.g., email/password vs. OAuth — is a team decision; document it).  
- [ ] Each user has a persistent **journal** of every practice test/question attempted, their answer(s), whether they were correct, and the date/time.  
- [ ] Users can review their history and see progress over time (e.g., score trend across attempts for a given certification).  
- [ ] There is **no limit** on how many times a user may retake a practice exam.  
- [ ] (Future scope, not MVP) Support for admin-configurable limits on the number of attempts for a given practice test.

### 4\. Exam Presenter (Test-Taking UI)

- [ ] User selects a certification/category before starting a practice exam.  
- [ ] Questions are presented to the user in **random order**, and are pulled at random from the approved pool for that category, so repeat attempts don't just replay the same sequence.  
- [ ] The presenter records each answer as it is submitted and persists it to the user's journal.  
- [ ] Each answer is evaluated automatically where possible (multiple choice always; short answer via fuzzy matching if enabled; essay via AI grading if implemented).  
- [ ] At the end of the exam, the user is shown **overall results** (score, and a review of which questions were right/wrong) — per the source proposal, exam results are provided at the end of the test rather than in the middle of it.  
- [ ] The exam flow, question bank, and evaluation logic should be written generically enough to support future non-Scrum question sets without a redesign.

### 5\. Reporting & Analytics

- [ ] Admin-facing reports covering, at minimum: question-level stats (e.g., how often each question is answered incorrectly), user trends (e.g., attempts over time, average scores by category), and pending-review queue size.  
- [ ] Reports should be usable by TJH's Questions Managers to identify weak or confusing questions that may need editing.

### 6\. UX Design Requirements

- [ ] Wireframes are needed, at minimum, for: sign-up/login, category selection, the exam-taking screen (including the on-screen presentation of each answer type), the end-of-exam results screen, the user's answer journal/history, and the admin question-editor screens.  
- [ ] The interface must be usable by non-technical exam takers as well as by SMEs/admins reviewing content — these are meaningfully different personas and may warrant distinct navigation/IA.  
- [ ] Design should follow standard [UI design principles](https://www.justinmind.com/ui-design/principles) and be responsive (usable on both desktop and mobile).  
- [ ] Every screen should include a clear way to navigate back to the category selection / home, and a way to reach the user's own journal/history.

### 7\. Technical Requirements

- [ ] **Language:** TypeScript (recommended).  
- [ ] **Database:** PostgreSQL (recommended); a graph database such as Neo4j is an acceptable alternative if it better serves fuzzy short-answer matching.  
- [ ] **Deployment artifact:** the application must be delivered as a **Docker container**.  
- [ ] **Hosting:** the container must be deployable to a host of TJH's choosing (i.e., don't hard-code assumptions that tie the app to one hosting provider); document the URL-routing requirements for whoever hosts it.  
- [ ] The implementation must be **compatible with Chingu VoyageXP capabilities** (i.e., buildable and testable within the tooling/timeframe available to a VoyageXP team).  
- [ ] Include deployment documentation sufficient for TJH to review and approve a production deployment, and technical documentation sufficient for Chingu leadership to review the implementation.

### 8\. Non-Functional Requirements

- [ ] **Open source:** the full codebase, documentation, and configuration must be delivered as open source and handed over to TJH as the IP owner.  
- [ ] **Extensibility:** the data model and presenter should not hard-code "Scrum" anywhere it doesn't have to — new certifications/categories and new question types should be addable without a rewrite.  
- [ ] **Data integrity:** no user should be able to see the correct answer to a question before submitting their own answer.  
- [ ] **Accessibility:** screens should be usable via keyboard and with screen readers where practical (proper labels/roles on interactive elements).  
- [ ] **Quality over completeness:** whatever subset of this scope a VoyageXP team implements must be fully working and deployable — partial/broken features are worse than a smaller, complete feature set.

## MVP vs. Stretch Goals

Given the size of the full proposal, agree with your Product Owner on scope before sprint planning. A reasonable MVP is:

**MVP (must-have for a usable first release)**

- [ ] Question bank schema supporting multiple-choice and short-answer questions, categorized by certification.  
- [ ] User-submitted questions with an SME/admin approval workflow (approve/edit/reject).  
- [ ] Admin question editor with the ability to grant/revoke admin rights and remove/block users.  
- [ ] User registration/login and a persistent answer journal.  
- [ ] Exam presenter: category selection → randomized questions → answer capture → automatic grading for multiple choice → end-of-exam results screen.  
- [ ] Unlimited retakes.  
- [ ] Basic admin reporting (question/user stats).  
- [ ] Deployed via Docker to a publicly reachable URL.  
- [ ] Responsive, accessible UI covering all screens above.

**Stretch Goals**

- [ ] Short-answer fuzzy matching for grading.  
- [ ] Essay questions with a Markdown-defined answer key and AI-assisted grading.  
- [ ] Duplicate-question detection/flagging.  
- [ ] Bulk import of a purchased/licensed question bank.  
- [ ] Admin-configurable retry limits per exam.  
- [ ] Advanced analytics dashboards (trends, guess distributions, etc.).  
- [ ] Support for a second, non-Scrum certification/category as a proof of the engine's extensibility.

## Suggested Development Milestones

The source proposal calls out two concrete milestones that make good sprint/VoyageXP-sized targets if you need to split the MVP further:

1. **Administrative Capability** — the question editor: admins can review, edit, and approve/reject submitted questions; view basic analytics; and grant/revoke admin rights or remove problematic users.  
2. **User Accounts and Answer Journal** — user registration and a persistent record of each user's answers and attempts.

Build the exam presenter (category selection, randomized delivery, grading, results) alongside whichever of these your team tackles first — a question bank and admin tooling with no way to actually take an exam isn't a usable release, and neither is an exam presenter with no vetted questions to serve.

## Content Sourcing & Vetting Workflow

Exam questions come primarily from volunteers and instructors recalling questions from real exams, plus other sources as available. Every submitted question must be **vetted by an SME** before it can be served to users. The application must support this workflow end-to-end:

1. A user (or Questions Manager) submits a question and answer.  
2. The question enters a **pending** state, invisible to the general exam pool.  
3. An SME/admin reviews it: approve as-is, edit and approve, or reject.  
4. The system flags likely duplicates for the reviewer, and rejects/withholds anything that appears to be copied from a copyrighted source.  
5. Only approved questions are eligible for random selection in a practice exam.

## Ownership, IP & Governance

* TJH owns the deployed product instance, including hosting and ongoing maintenance, and provides/approves the exam content.  
* Chingu provides the initial codebase repository and the VoyageXP team(s) that build it; the codebase is Open Source throughout.  
* After the VoyageXP(s) working on this project conclude, TJH receives the full codebase, documentation, and configuration, with each VoyageXP's work cloned into the ongoing repo.  
* Any question content must be free of copyright/IP issues — see [Content Sourcing & Vetting Workflow](#bookmark=id.oxqon99s5yrp).

## Working Agreement

* TJH and Chingu leadership define requirements, resources, and developmental components together using Scrum principles; all collaboration terms are agreed to by both organizations' admin teams.  
* Cross-organization check-in meetings occur weekly or bi-weekly (exact cadence set once the sprint length is defined), separate from the VoyageXP team's own Scrum ceremonies.  
* Status updates from these check-ins are presented to both the TJH Board and Chingu leadership.  
* Within a VoyageXP, the team follows standard Chingu Scrum ceremonies (see the [VoyageXP Handbook](https://github.com/chingu-voyages/Handbook/blob/main/docs/guides/voyage/voyage.md#voyage-guide)) and has access to Chingu's Lean Coffee and Technical Roundtable sessions for support.

## Acknowledgements

This specification is adapted from *"[The Job Hackers/Chingu Certification Practice Exams Practice Website](https://docs.google.com/document/d/1n5avojtQRx-MjeSKoFT96SXocAdRbBc24BIsuMmpnZs/edit?pli=1&tab=t.0#heading=h.2gazcsgmxkub)"* proposal (v0.02) by Nathan Syfrig, The Job Hackers Chingu Champion, reorganized into an actionable requirements document for a VoyageXP build team.

## About Chingu

Chingu provides "VoyageXP" — a ten-week job-simulation where Developers (web developers, UI/UX designers), Scrum Masters, and Product Owners practice their roles by building a real application against a defined set of requirements, following Agile processes, with support from Chingu's Lean Coffee and Technical Roundtable sessions and mentoring by our Agile Leadership Team..  
