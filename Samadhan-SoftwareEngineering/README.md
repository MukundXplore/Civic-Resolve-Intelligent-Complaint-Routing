# Project Samadhan — Software Engineering Academic Deliverables

**Institution:** South Asian University  
**Department:** Department of Computer Science  
**Course:** Software Engineering (Academic Year 2025–2026)  
**Project:** Project Samadhan — Civic Resolve: Intelligent Complaint Routing  
**Repository Branch:** `Samadhan-SoftwareEngineering`

---

## 🏛️ Executive Summary

Project Samadhan (formerly Civic Resolve) is an intelligent campus maintenance grievance management and automated routing system developed following an iterative **Evolutionary Prototyping** Software Development Life Cycle (SDLC).

This directory contains the primary academic Software Engineering deliverables submitted for formal capstone evaluation, comprehensive IEEE 830 documentation, system analysis models, Capstone pitch presentation, and the synchronized evaluation speaking script.

---

## 📂 Deliverables Catalog

| Document / Artifact | Format | Scope & Description | SDLC Phase Alignment |
| :--- | :---: | :--- | :--- |
| **[Samadhan - CivicResolve - SE Documentation.pdf](Samadhan%20-%20CivicResolve%20-%20SE%20Documentation.pdf)** | PDF (118 pages) | Master Software Engineering documentation covering problem discovery, IEEE 830 SRS, dual-label state machine, architectural compliance review, comprehensive QA test cases, Requirements Traceability Matrix (RTM), change management log, and release readiness. | Phases 1 – 9 |
| **[Diagrams.pdf](Diagrams.pdf)** | PDF (10 pages) | Complete architectural and system analysis visual model catalog: Use Case, UML Class Diagram, Sequence Diagrams, Activity/Workflow Models, State Transition Diagram, and Database ER Schema. | Phases 4 & 5 |
| **[Project Samadhan - Pitch.pdf](Project%20Samadhan%20-%20Pitch.pdf)** | PDF (18 slides) | Capstone defense and product evaluation presentation deck mapping out the end-to-end engineering journey, running "leaking-pipe" test case, technical defense, and V2 roadmap. | Phase 10 |
| **[5_Minute_Slidewise_Script.docx](5_Minute_Slidewise_Script.docx)** | DOCX (30 paragraphs) | Timed, synchronized 5-minute defense script (4 presenters, 18 slides) maintaining rigorous technical accuracy without claiming unverified production deployment. | Phase 10 |

---

## 👥 Engineering Team & Role Governance

The project followed a disciplined team division across the complete Software Development Life Cycle:

| Presenter / Contributor | Engineering Role | Assigned Lifecycle Stages | Primary Deliverables & Focus |
| :--- | :--- | :--- | :--- |
| **Mukund Prasad** | Product Lead & Requirements Engineer | Problem Discovery, Requirements (SRS), UX/UI Design | Problem root-cause analysis, dual-label state machine (`wing` vs `true_wing`), multi-portal UI/UX system, student/faculty workflows. |
| **Farhan Akhlaq** | ML Engineer & Data Architect | Analysis, Machine Learning, NLP Inference Pipeline | TF-IDF vectorization, Multinomial Naive Bayes classifier, heuristic length validation, spam/uncertainty boundary thresholds. |
| **Karthik Baurai** | Systems Architect & QA Lead | System Architecture, Implementation, QA & Verification | Monolithic Flask-MySQL architecture, UML design, formal test plans, Requirements Traceability Matrix (RTM), verification status. |
| **Misbah Ul Islam** | DevOps Lead & Release Manager | Backend Integration, Change Management, Release Packaging | MySQL session authentication (`auth.py`), database migration scripts, configuration management, change control, deployment defense. |

---

## 🔄 SDLC Phase Mapping & Methodology

The engineering process adhered to a two-iteration **Evolutionary Prototyping** model:

```
[Iteration 1: Apr–May 2026]
Problem Discovery ➔ Initial Flask/ML Prototype ➔ Peer & Symposium Evaluation (May 25)
                                    │
                                    ▼
[Iteration 2: Jun–Nov 2026]
Engineering Restructure ➔ IEEE SRS Formalization ➔ Architectural Review & Hardening ➔ QA & Verification ➔ Release Packaging
```

### 10-Phase Lifecycle Execution:
1. **Problem Discovery & Root Cause Analysis:** Identified campus maintenance delays, untracked paper registers, and high manual misrouting rates.
2. **Product Discovery & Stakeholder Modeling:** Formalized three actor archetypes: Citizens (Students/Faculty), Maintenance Staff, and Administrators.
3. **Requirements Engineering (SRS):** Authored formal IEEE 830 functional and non-functional requirements. Specified deterministic triage rules.
4. **System Analysis & Modeling:** Created UML Class, Sequence, State, and Activity diagrams captured in `Diagrams.pdf`.
5. **Software Architecture:** Established lightweight Flask monolith with MySQL persistence, Jinja2 dynamic rendering, and scikit-learn inference.
6. **Implementation & Compliance Review:** Integrated `app.py`, blueprint authentication `auth.py`, and database access layers with credential security.
7. **Testing, QA & Traceability:** Developed comprehensive test cases across input validation, RBAC boundaries, classifier uncertainty, and SQL state integrity.
8. **Change Management:** Evaluated post-symposium feedback challenging ML routing necessity; introduced deterministic spam and confidence thresholds.
9. **Release Readiness:** Formulated formal release validation criteria, configuration checklists, and clear prototype vs production boundary.
10. **Product Pitch & Technical Demonstration:** Prepared 18-slide evaluation deck and synchronized 5-minute technical defense script.

---

## ⏱️ 5-Minute Technical Defense Script Summary

| Speaker | Section & Time | Slides | Narrative Focus |
| :--- | :--- | :---: | :--- |
| **Mukund Prasad** | **Problem & Product Discovery** (1:20) | 1–5 | Introduction to Samadhan; traditional register bottleneck; 3 users 1 workflow; natural language complaint intake; iterative development history. |
| **Farhan Akhlaq** | **Requirements, Analysis & Design** (1:05) | 6–9 | IEEE SRS scope; complaint lifecycle (`Pending` ➔ `In Progress` ➔ `Resolved`); TF-IDF + Multinomial Naive Bayes routing; leaking-pipe running example; defensive UI. |
| **Karthik Baurai** | **Architecture, Implementation & QA** (1:10) | 10–13 | Monolithic Flask-MySQL architecture; ticket processing workflow; end-to-end routing execution; testing philosophy and verified execution results. |
| **Misbah Ul Islam** | **Change, Release & Product Pitch** (1:25) | 14–18 | Handling stakeholder feedback; prototype vs production readiness; team lifecycle contributions; Version 2 roadmap; closing product pitch: *"Describe. Route. Resolve."* |

---

## ⚙️ Verification & Academic Integrity Notice

- **Prototype Status:** Project Samadhan is a fully functional, verified academic prototype running against local MySQL and development servers. It is not currently deployed to live institutional production infrastructure.
- **Testing Results:** Test cases documented in the SRS distinguish between planned verification suites and verified manual execution logs.
- **Model Boundaries:** Model inference metrics reflect offline validation splits on synthesized datasets; real-world edge cases are safely handled by the `General` triage queue.
