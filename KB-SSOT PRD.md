# PRD: Virima Knowledge Platform (SSOT)

**Owner (PM):** Mamatha Naganna (Director, Product Management)

**Workstream leads:**

* **Docs/Content Ops:** Vignesh, GopiChand
* **UX/UI:** Sourav
* **AI/Knowledge Engineering:** Neeraj
* **Support:** Balaji
* **Engineering:** LNR

**Status:** Draft v1.1

---

## Table of Contents

1. [Background and Problem Statement](#1-background-and-problem-statement)
2. [Goals and Non-goals](#2-goals-and-non-goals)
3. [Definitions (Shared Vocabulary)](#3-definitions-shared-vocabulary)
4. [Personas and User Needs](#4-personas-and-user-needs)
5. [User Journeys (Platform-level)](#5-user-journeys-platform-level)
6. [Success Metrics (KPIs)](#6-success-metrics-kpis)
7. [Scope and Requirements](#7-scope-and-requirements)
8. [Knowledge Object Model (v1)](#8-knowledge-object-model-v1)
9. [Experience Requirements (UX/UI)](#9-experience-requirements-uxui)
10. [AI Assistant Requirements](#10-ai-assistant-requirements)
11. [Context Bundles and Privacy Rules](#11-context-bundles-and-privacy-rules)
12. [Governance and Operating Model](#12-governance-and-operating-model)
13. [Implementation Plan (30/60/90)](#13-implementation-plan-306090)
14. [Risks and Mitigations](#14-risks-and-mitigations)
15. [Open Questions](#15-open-questions-resolve-in-week-1)
16. [User Stories and Acceptance Criteria](#16-user-stories-and-acceptance-criteria)
17. [Content Migration Strategy](#17-content-migration-strategy)
18. [Integration Requirements](#18-integration-requirements)
19. [Accessibility Requirements](#19-accessibility-requirements)
20. [Non-Functional Requirements](#20-non-functional-requirements)
21. [Appendix: RACI](#21-appendix-raci-starter)

---

## 1) Background and problem statement

Virima is a **platform** with multiple suites/apps. Today, product knowledge exists across multiple locations and formats (docs, internal notes, support macros, release notes, in-product tips), leading to:

* inconsistent or duplicate answers
* slower user time-to-value
* higher support ticket volume and longer time-to-resolution
* low trust in content freshness
* AI assistance risk (hallucinations) due to fragmented, ungoverned sources

We need a **state-of-the-art Knowledge Platform** that becomes a **Single Source of Truth (SSOT)** and is consumable via web KB, in-product help, and AI (grounded answers with citations), while supporting four user personas.

---

## 2) Goals and non-goals

### 2.1 Goals

1. Establish a **platform-level SSOT** for Virima knowledge that all suites/apps consume.
2. Deliver **persona-based help experiences**:

   * Persona A: "Nudge user" (actionable playbooks)
   * Persona B: "Support-first user" (guided flows + fast escalation)
   * Persona C: "Reader/power learner" (deep docs + tutorials)
   * **Persona D: "Partner/Implementer"** (training and enablement materials derived from SSOT)
3. Enable **AI assistance** that is:

   * grounded in canonical knowledge objects
   * citation-backed
   * measurable and safe (escalation when uncertain)
4. Implement **governance + lifecycle** so knowledge stays accurate as the platform changes.
5. Ensure partner-facing enablement assets (training decks, runbooks, labs) are **generated/derived from SSOT**, minimizing drift.

### 2.2 Non-goals (v1)

* Migrating/re-writing every legacy document before MVP
* Fine-tuning a proprietary model as the primary approach (start with RAG)
* Creating a full video academy as a prerequisite
* Designing app-specific help systems (platform pattern + components only)

---

## 3) Definitions (shared vocabulary)

### 3.1 Single source of truth (SSOT)

One authoritative source where the current, correct knowledge lives; all publishing surfaces either **link to it** or are **generated from it**.

### 3.2 Canonical knowledge objects

The smallest "unit of truth" treated as authoritative, e.g., a Task, Troubleshooting guide, Concept, Reference, Policy/Permissions, or Change note.

### 3.3 Canonical objects + ownership

Each canonical object has a clearly recorded **owner** (team/role) accountable for correctness and review cadence; duplicates are eliminated via redirects/links.

### 3.4 Context bundle

A package of user/session context attached to a support request to reduce back-and-forth (e.g., page, error codes, role, version).

### 3.5 Privacy rules for context bundles

Rules for what data may be collected/attached/stored/visible, with tiering, consent, masking, access control, and retention limits.

### 3.6 RAG (Retrieval-Augmented Generation)

AI retrieves relevant canonical knowledge objects and generates an answer grounded in those sources, typically with citations.

---

## 4) Personas and user needs

### Persona A: "Nudge user"

* Will act with small guidance.
* Needs short, reliable, step-by-step playbooks with verification and pitfalls.

### Persona B: "Support-first user"

* Avoids reading; wants fast resolution.
* Needs guided flows/decision trees + one-click escalation with context.

### Persona C: "Reader/power learner"

* Reads deep docs/tutorials.
* Needs structured documentation, navigation, conceptual clarity, and references.

### Persona D: "Partner/Implementer"

* Needs to **learn, deliver, and support** Virima for customers (implementations, onboarding, basic troubleshooting).
* Requires **consistent training assets** that match the product and can be reused across partner onboarding and delivery.

**Experience requirements (Partner):**

* Role-based learning paths (Sales/Presales, Implementation, Support)
* Training decks + speaker notes, demo scripts, labs, and checklists
* Partner FAQ and troubleshooting runbooks
* Certification/assessment readiness materials (optional in v1)
* Clear versioning and "what changed" alerts when the platform updates

---

## 5) User journeys (platform-level)

We intentionally focus on **platform journeys**, not suite/app journeys.

**Examples of platform journeys (initial candidates):**

* Identity & Access: users/roles/permissions
* Navigation & Global Search
* Core Data Model: key entities and relationships
* Integrations & Connectivity: connectors, credential patterns
* Automation & Workflows: triggers, rules, approvals
* Reporting & Exports: reports/dashboards
* Administration: configuration, environment
* Troubleshooting & Diagnostics: error codes/logs

**MVP selection principle:** start with the journeys that drive the highest support volume or onboarding friction.

---

## 6) Success metrics (KPIs)

Track baseline → target over 90 days (targets finalized during Phase 0).

### 6.1 Self-serve & Support

| Metric | Baseline | Target (90 days) | Measurement Method |
|--------|----------|------------------|-------------------|
| Ticket volume reduction (top categories) | TBD | -30% | Ticketing system analytics |
| Time-to-resolution | TBD | -25% | Ticketing system analytics |
| First-contact resolution | TBD | +15% | Support team metrics |

### 6.2 Findability

| Metric | Baseline | Target (90 days) | Measurement Method |
|--------|----------|------------------|-------------------|
| Search success rate | TBD | 80%+ | KB analytics |
| Zero-result rate | TBD | <10% | KB analytics |
| Pogo-sticking rate | TBD | <20% | KB analytics (click-back within 30s) |

### 6.3 In-product help

| Metric | Baseline | Target (90 days) | Measurement Method |
|--------|----------|------------------|-------------------|
| Help-open → task-complete conversion | TBD | 60%+ | In-app analytics |
| Helpfulness feedback score | TBD | 4.0+ / 5.0 | User feedback widget |

### 6.4 AI assistant

| Metric | Baseline | Target (90 days) | Measurement Method |
|--------|----------|------------------|-------------------|
| Usefulness score (thumbs up rate) | N/A | 75%+ | AI feedback widget |
| Escalation correctness rate | N/A | 90%+ | Manual review sampling |
| Citation coverage | N/A | 95%+ | Automated audit |
| Hallucination rate (on supported topics) | N/A | <5% | Golden Questions evaluation |

### 6.5 Content health

| Metric | Baseline | Target (90 days) | Measurement Method |
|--------|----------|------------------|-------------------|
| % objects reviewed within SLA | TBD | 90%+ | Content management system |
| Duplicate/conflicting objects count | TBD | <5 | Governance council audit |

### 6.6 Partner enablement

| Metric | Baseline | Target (90 days) | Measurement Method |
|--------|----------|------------------|-------------------|
| Partner onboarding time (days to "delivery-ready") | TBD | -40% | Partner program tracking |
| Partner certification pass rate | N/A | 80%+ | LMS/assessment system |
| Partner-generated support escalations | TBD | -25% | Ticketing system |
| Partner training satisfaction score | TBD | 4.2+ / 5.0 | Post-training survey |

### 6.7 Analytics Dashboard Requirements

The analytics dashboard shall display:

* Real-time and historical views of all KPIs above
* Drill-down by platform domain, object type, and persona
* Trend visualization (daily/weekly/monthly)
* Exportable reports (CSV, PDF)
* Alert thresholds for KPI degradation
* Attribution tracking for self-service deflection

---

## 7) Scope and requirements

### 7.1 In scope (v1)

1. **Canonical repository** for knowledge objects
2. **Knowledge Object Model v1** (types, templates, required metadata)
3. **Publishing pipeline** to:

   * Web KB
   * In-product help surfaces
   * AI retrieval index
   * Support linking/macro references
   * **Partner enablement surface** (Partner Portal / LMS / enablement hub) where applicable
4. **Help Surface System** (platform UX patterns + reusable components)
5. **AI retrieval with citations** for the MVP object set
6. **Analytics + feedback loop** across KB/help/AI/escalation
7. **Governance operating model** (owners, review SLAs, council)
8. **Derived partner training assets** (minimum set) generated from SSOT for MVP topics:

   * training deck outline (with speaker notes)
   * demo script(s)
   * implementation checklist(s)
   * partner FAQ/runbook for top issues

### 7.2 Out of scope (v1)

* bespoke per-app help UI patterns
* non-cited AI answers
* unlimited diagnostics collection without consent
* full video academy
* multi-language/localization (future roadmap)

---

## 8) Knowledge Object Model (v1)

### 8.1 Object types

| Type | Purpose | Primary Persona |
|------|---------|-----------------|
| Concept | Explain what something is and why it matters | C, D |
| Task/How-to | Step-by-step instructions to accomplish a goal | A, B, C, D |
| Troubleshooting | Diagnose and resolve issues | A, B, D |
| Reference | Technical specifications, API docs, field definitions | C, D |
| Policy/Permissions | Access control, security policies, compliance | C, D |
| Change note | What changed in a release and impact | A, B, C, D |

### 8.2 Required metadata (minimum)

| Field | Description | Required |
|-------|-------------|----------|
| Object ID | Stable unique identifier (e.g., KB-001234) | Yes |
| Title | Clear, descriptive title (max 100 chars) | Yes |
| Type | One of: Concept, Task, Troubleshooting, Reference, Policy, Change note | Yes |
| Platform domain | Taxonomy category (e.g., Identity & Access, Integrations) | Yes |
| Persona fit | One or more: A, B, C, D | Yes |
| Audience tag(s) | One or more: End User, Admin, Support Agent, Partner | Yes |
| Prerequisites | Required role/permissions/modules/environment | Yes (if applicable) |
| Applies to | Cloud/On-prem, version range | Yes |
| Owner | Team/role accountable for accuracy | Yes |
| Last reviewed date | Date of last review | Yes |
| Review SLA | Review cadence (e.g., 90/180 days) | Yes |
| Status | Verified / Draft / Deprecated | Yes |
| Related objects | Links to related KB objects | No |
| Keywords/tags | Search optimization terms | No |
| Difficulty level | Beginner / Intermediate / Advanced | No |

### 8.3 Templates (must-use)

**Task/How-to**

* Outcome statement
* When to use
* Prerequisites
* Steps (numbered, with screenshots where helpful)
* Verification (how to confirm success)
* Common pitfalls
* Next best actions

**Troubleshooting**

* Symptoms (user-observable)
* Likely causes (ranked by frequency)
* Diagnostics steps
* Fixes (least risky first)
* Escalation criteria + required attachments

**Concept**

* Definition
* Why it matters
* How it works (high level)
* Key terms
* Related tasks

**Reference**

* Overview
* Field/parameter definitions (table format)
* Valid values/constraints
* Examples
* Related APIs/objects

**Policy/Permissions**

* Policy statement
* Scope (who/what is affected)
* Requirements/constraints
* Exceptions
* Enforcement mechanism

**Change note**

* Version/release
* Change summary
* Impact (who is affected, what changes)
* Action required (if any)
* Rollback/mitigation (if applicable)

### 8.4 Object lifecycle states

| Status | Description | AI Behavior |
|--------|-------------|-------------|
| Draft | In progress, not published | Not indexed for AI retrieval |
| Verified | Reviewed and approved | Indexed and cited normally |
| Stale | Past review SLA | Indexed with freshness warning |
| Deprecated | No longer valid | Not indexed; redirects to replacement |

### 8.5 Versioning requirements

* System shall maintain version history for each object
* System shall allow comparison between any two versions
* System shall support rollback to previous version
* System shall display "what changed" summary between versions
* System shall notify subscribers when objects they follow are updated

---

## 9) Experience requirements (UX/UI)

### 9.1 Help surfaces (platform standard)

| Surface | Trigger | Content Priority |
|---------|---------|------------------|
| **Global Help** | Persistent icon/menu | Search, popular topics, AI assistant |
| **Context Help** | ? icon on pages/components | Relevant tasks for current context |
| **Error Help** | Error state/message | Troubleshooting for specific error |
| **Onboarding Help** | First-time user detection | Getting started, key concepts |

### 9.2 Search and navigation

**Search requirements:**

* Full-text search across all object fields
* Filters: domain, object type, persona, audience, status
* Auto-complete with top suggestions (as-you-type)
* Synonym handling (e.g., "login" = "sign in" = "authenticate")
* Spelling correction / "Did you mean?"
* Related content suggestions on results page
* Recent searches (per user)
* Clear "last reviewed" indicator on results

**Navigation requirements:**

* Hierarchical navigation by platform domain
* Breadcrumb navigation on all pages
* "On this page" table of contents for long articles
* Previous/Next navigation within related content
* Quick links to related objects

### 9.3 Persona handling

| Persona | Default Experience |
|---------|-------------------|
| Persona A | Short playbooks first; collapsible details |
| Persona B | Guided flow first; prominent escalation button |
| Persona C | Full documentation with navigation; show all sections |
| Persona D | Learning path view; progress tracking; assessments |

### 9.4 Feedback mechanisms

* **Article-level feedback:** "Was this helpful?" (Yes/No) + optional comment
* **AI answer feedback:** Thumbs up/down + optional correction
* **Search feedback:** "Did you find what you were looking for?" after 60 seconds
* **Escalation feedback:** Post-resolution survey on support quality

---

## 10) AI assistant requirements

### 10.1 Principles

* Must cite canonical objects/sections
* Must follow permissions/access controls
* Must escalate when confidence is low or risk is high
* Must log outcomes for evaluation
* Must provide feedback mechanism (thumbs up/down)

### 10.2 Answer policy

| Scenario | AI Behavior |
|----------|-------------|
| Canonical object exists, high confidence | Provide answer with citation(s) |
| Canonical object exists, low confidence | Provide answer with citation(s) + "Verify with support if needed" |
| No canonical object exists | "I don't have information on this topic. [Escalate to support]" + capture topic for backlog |
| Content is stale (past review SLA) | Provide answer with warning: "This information may be outdated" + suggest escalation |
| High-risk action (destructive, security-sensitive) | Provide answer + explicit warning + recommend verification |
| Out of scope (competitor, pricing, legal) | "I can only help with Virima product questions. [Contact Sales/Legal]" |

### 10.3 Fallback behavior

When RAG retrieval fails or returns no results:

1. Acknowledge limitation: "I couldn't find specific documentation on this topic."
2. Suggest alternatives: related topics, broader search terms
3. Offer escalation: "Would you like to create a support request?"
4. Log the query for content gap analysis

### 10.4 Feedback collection

* Every AI response includes thumbs up/down buttons
* Thumbs down triggers optional correction input
* Feedback is logged with query, response, and context
* Weekly review of negative feedback for improvement

### 10.5 Rate limiting and abuse prevention

* Maximum 50 queries per user per hour
* Maximum 500 queries per tenant per hour
* Repeated identical queries throttled after 5 attempts
* Abusive content detection with automatic block

### 10.6 Evaluation

* Build **Golden Questions** set from real tickets (minimum 100 questions)
* Score dimensions:
  - Correctness: Is the answer factually accurate?
  - Citation accuracy: Are citations relevant and correct?
  - Completeness: Does the answer fully address the question?
  - Safety: Did it correctly escalate risky/uncertain scenarios?
* Weekly evaluation against Golden Questions set
* Monthly refresh of Golden Questions based on new tickets

---

## 11) Context bundles and privacy rules

### 11.1 Context bundle tiers

**Tier 0 (always attach; low-risk):**

* page/screen identifier
* feature/module area
* timestamp/timezone
* version/build
* workflow step
* error code and sanitized error message

**Tier 1 (default attach; must sanitize):**

* user ID (internal)
* tenant/account ID
* non-sensitive configuration flags

**Tier 2 (opt-in only; explicit consent + preview):**

* logs/diagnostics
* screenshots
* payload samples
* exports

**Never attach:**

* passwords
* tokens/private keys
* SNMP community strings
* raw secrets
* PII beyond user ID (names, emails, addresses)

### 11.2 Privacy controls

* data minimization
* explicit consent for Tier 2
* automatic masking/redaction
* access control (role-based visibility)
* retention and deletion policy (90 days default, configurable)
* purpose limitation (support vs training)

---

## 12) Governance and operating model

### 12.1 Roles

* Program Owner: Mamatha
* Docs/Content Ops: Vignesh, GopiChand
* UX: Sourav
* AI: Neeraj
* Support: Balaji
* Eng: LNR

### 12.2 Rituals

* Weekly execution standup (30 min)
* Monthly KPI review (45 min)
* Knowledge Council (biweekly/monthly): taxonomy + governance + deprecations

### 12.3 SLAs

| Object Type | Review Cadence | Grace Period | Action if Overdue |
|-------------|---------------|--------------|-------------------|
| Critical (Task, Troubleshooting) | 90 days | 14 days | Flag as stale, notify owner |
| Standard (Concept, Reference) | 180 days | 30 days | Flag as stale, notify owner |
| Change note | N/A (point-in-time) | N/A | Auto-archive after 1 year |

### 12.4 Definition of Done for product changes

* canonical objects updated/created
* metadata complete
* help hooks added where relevant
* AI can retrieve/cite
* analytics events updated
* partner training assets updated (if applicable)

---

## 13) Implementation plan (30/60/90)

### 0–30 days: Align + prove

* finalize charter + KPIs baseline
* taxonomy + object schema v1
* help surface UX patterns (wireframes)
* Golden Questions (top 50)
* publish "Golden 25" canonical objects for top platform journeys
* complete content audit of existing sources

### 31–60 days: MVP platform capability

* canonical repository + publishing pipeline
* web KB MVP + in-product entry points
* AI retrieval with citations for Golden 25
* escalation with context bundle + tiering
* analytics dashboard live
* feedback mechanisms implemented

### 61–90 days: Scale responsibly

* expand to 100 objects based on telemetry
* governance fully operational
* guided flows for Persona B (top 10)
* enforce DoD and release gate for selected teams
* partner training materials for MVP topics

---

## 14) Risks and mitigations

| Risk | Likelihood | Impact | Mitigation |
|------|------------|--------|------------|
| Duplication persists | Medium | High | Canonicalization rules + redirects + governance council |
| Stale content | High | High | Ownership + review SLAs + release DoD + automated alerts |
| AI hallucinations | Medium | High | Citations required + escalation policy + Golden Questions eval |
| Privacy violations | Low | Critical | Tiering + consent + redaction + retention + audit logging |
| Low adoption | Medium | Medium | In-product help hooks + support macros + measurement + training |
| Content migration delays | High | Medium | Prioritized migration + parallel operation + redirect strategy |
| Partner content drift | Medium | Medium | Single-source derivation + automated sync + version alerts |

---

## 15) Open questions (resolve in Week 1)

1. Canonical repository tooling choice and publishing pipeline
2. Final platform domain taxonomy and naming conventions
3. What data is permitted in context bundles per security/privacy
4. KPI targets (baseline → target) for 90 days
5. Which journeys are the "Golden 25" for MVP
6. Partner enablement surface decision (Partner Portal/LMS): where will partners access training, and what authentication/permissions apply?
7. Which partner role learning paths are in v1 (Presales vs Implementation vs Support)?

---

## 16) User Stories and Acceptance Criteria

### Epic 1: Knowledge Base (Web KB)

#### US-1.1: Search Knowledge Base

**As a** platform user  
**I want to** search the knowledge base using keywords  
**So that** I can find answers to my questions quickly

**Acceptance Criteria:**
- [ ] User can enter search query in search bar
- [ ] Search returns results within 2 seconds
- [ ] Results display title, snippet, object type, and last reviewed date
- [ ] Results are ranked by relevance
- [ ] User can filter results by domain, type, and persona
- [ ] Zero-result state shows suggestions and escalation option
- [ ] Search supports auto-complete with top 5 suggestions
- [ ] Search handles synonyms (configurable synonym dictionary)

#### US-1.2: Browse Knowledge Base by Category

**As a** platform user  
**I want to** browse the knowledge base by category  
**So that** I can explore topics in a structured way

**Acceptance Criteria:**
- [ ] User can navigate hierarchical taxonomy (domain → subtopic)
- [ ] Each category displays count of articles
- [ ] User can expand/collapse category tree
- [ ] Breadcrumb navigation shows current location
- [ ] "Popular in this category" section shows top 5 articles

#### US-1.3: View Knowledge Object

**As a** platform user  
**I want to** view a knowledge object with clear formatting  
**So that** I can understand and follow the content

**Acceptance Criteria:**
- [ ] Article displays title, type, last reviewed date, and owner
- [ ] Article displays content using appropriate template
- [ ] "On this page" navigation for long articles
- [ ] Related objects displayed in sidebar
- [ ] Print-friendly view available
- [ ] "Was this helpful?" feedback widget at bottom

#### US-1.4: Provide Article Feedback

**As a** platform user  
**I want to** provide feedback on whether an article was helpful  
**So that** the content team can improve quality

**Acceptance Criteria:**
- [ ] User can click "Yes" or "No" for helpfulness
- [ ] Optional comment field appears after vote
- [ ] Feedback is logged with article ID, user ID, and timestamp
- [ ] User sees "Thank you for your feedback" confirmation
- [ ] Duplicate votes from same user are prevented (one vote per article per user)

---

### Epic 2: In-Product Help

#### US-2.1: Access Context Help

**As a** platform user  
**I want to** access help relevant to my current page/feature  
**So that** I can get assistance without leaving my workflow

**Acceptance Criteria:**
- [ ] Help icon (?) is visible on all pages with help content
- [ ] Clicking icon opens help panel without page navigation
- [ ] Panel displays content relevant to current page context
- [ ] User can search within help panel
- [ ] User can close panel and return to workflow
- [ ] Panel remembers last state (open/closed) per session

#### US-2.2: Access Error Help

**As a** platform user  
**I want to** get help when I encounter an error  
**So that** I can resolve the issue quickly

**Acceptance Criteria:**
- [ ] Error messages include "Get help" link
- [ ] Link opens troubleshooting content for that error code
- [ ] If no specific content exists, generic troubleshooting + escalation offered
- [ ] Context bundle (Tier 0 + Tier 1) auto-attached to escalation

#### US-2.3: Escalate to Support

**As a** platform user  
**I want to** escalate to support when self-service doesn't help  
**So that** I can get human assistance

**Acceptance Criteria:**
- [ ] Escalation button visible on all help surfaces
- [ ] Context bundle auto-populated (per tier rules)
- [ ] User can review context before submitting
- [ ] User can add additional description
- [ ] Confirmation displayed with ticket number
- [ ] User can track ticket status from platform

---

### Epic 3: AI Assistant

#### US-3.1: Ask AI Assistant a Question

**As a** platform user  
**I want to** ask the AI assistant a question in natural language  
**So that** I can get a quick answer without searching

**Acceptance Criteria:**
- [ ] User can type question in chat interface
- [ ] AI responds within 5 seconds
- [ ] Response includes citation(s) to source articles
- [ ] Citations are clickable links to full articles
- [ ] User can ask follow-up questions in same session
- [ ] Conversation history maintained for session

#### US-3.2: Provide AI Feedback

**As a** platform user  
**I want to** provide feedback on AI responses  
**So that** the AI can improve over time

**Acceptance Criteria:**
- [ ] Thumbs up/down buttons on every AI response
- [ ] Thumbs down triggers optional correction input
- [ ] Feedback logged with query, response, rating, and context
- [ ] User sees confirmation after feedback

#### US-3.3: AI Escalation

**As a** platform user  
**I want the** AI to escalate to support when it can't help  
**So that** I don't waste time with unhelpful responses

**Acceptance Criteria:**
- [ ] AI offers escalation when confidence is low
- [ ] AI offers escalation when no content exists
- [ ] AI offers escalation for high-risk queries
- [ ] Escalation includes conversation history as context
- [ ] User can accept or decline escalation offer

---

### Epic 4: Content Management (Admin)

#### US-4.1: Create Knowledge Object

**As a** content author  
**I want to** create a new knowledge object using templates  
**So that** content is consistent and complete

**Acceptance Criteria:**
- [ ] Author can select object type (Concept, Task, etc.)
- [ ] Template pre-populates required sections
- [ ] All required metadata fields enforced
- [ ] Preview mode available before publishing
- [ ] Draft can be saved without publishing
- [ ] Submission triggers review workflow

#### US-4.2: Review and Approve Content

**As a** content reviewer  
**I want to** review and approve submitted content  
**So that** only accurate content is published

**Acceptance Criteria:**
- [ ] Reviewer receives notification of pending reviews
- [ ] Reviewer can view content with all metadata
- [ ] Reviewer can approve, reject, or request changes
- [ ] Comments can be added to rejection/change request
- [ ] Approval publishes content and updates AI index
- [ ] Audit trail maintained for all actions

#### US-4.3: Deprecate Content

**As a** content owner  
**I want to** deprecate outdated content  
**So that** users don't see stale information

**Acceptance Criteria:**
- [ ] Owner can mark object as deprecated
- [ ] Deprecated objects removed from AI index
- [ ] Deprecated objects show warning banner
- [ ] Owner can specify redirect to replacement object
- [ ] Deprecation logged in audit trail

#### US-4.4: Receive Stale Content Alerts

**As a** content owner  
**I want to** receive alerts when my content needs review  
**So that** I can keep content accurate

**Acceptance Criteria:**
- [ ] System sends email alert 14 days before review SLA
- [ ] System sends reminder at SLA date
- [ ] System flags overdue content in dashboard
- [ ] Owner can snooze alert for 7 days (max 2 snoozes)
- [ ] Escalation to manager if 30+ days overdue

---

### Epic 5: Partner Enablement

#### US-5.1: Access Partner Learning Path

**As a** partner implementer  
**I want to** follow a structured learning path  
**So that** I can become certified to deliver Virima

**Acceptance Criteria:**
- [ ] Partner can view available learning paths by role
- [ ] Learning path shows modules, estimated time, and progress
- [ ] Partner can mark modules as complete
- [ ] Progress is saved across sessions
- [ ] Completion triggers certification eligibility (if applicable)

#### US-5.2: Download Partner Training Materials

**As a** partner implementer  
**I want to** download training materials for offline use  
**So that** I can prepare for customer engagements

**Acceptance Criteria:**
- [ ] Partner can download training decks (PPTX)
- [ ] Partner can download checklists (PDF)
- [ ] Partner can download demo scripts (PDF)
- [ ] Downloads are watermarked with partner info
- [ ] Download activity is logged

#### US-5.3: View Partner FAQ

**As a** partner support person  
**I want to** access partner-specific FAQ and runbooks  
**So that** I can resolve common issues without escalating

**Acceptance Criteria:**
- [ ] Partner FAQ is accessible from partner portal
- [ ] FAQ is filterable by topic/category
- [ ] FAQ links to detailed troubleshooting articles
- [ ] Partner can escalate if FAQ doesn't help

---

### Epic 6: Analytics and Reporting

#### US-6.1: View KB Analytics Dashboard

**As a** content manager  
**I want to** view analytics on KB usage  
**So that** I can identify gaps and improvement opportunities

**Acceptance Criteria:**
- [ ] Dashboard shows search volume, success rate, zero-result queries
- [ ] Dashboard shows article views, feedback scores, pogo-sticking rate
- [ ] Dashboard shows trending topics and top articles
- [ ] Data can be filtered by date range, domain, persona
- [ ] Data can be exported to CSV

#### US-6.2: View AI Performance Dashboard

**As an** AI lead  
**I want to** view AI assistant performance metrics  
**So that** I can improve AI quality

**Acceptance Criteria:**
- [ ] Dashboard shows query volume, response time, feedback scores
- [ ] Dashboard shows escalation rate and correctness
- [ ] Dashboard shows citation coverage and hallucination rate
- [ ] Dashboard shows top queries without good answers (content gaps)
- [ ] Weekly Golden Questions evaluation results displayed

---

## 17) Content Migration Strategy

### 17.1 Content Audit

**Phase 0 (Days 1-15):** Complete audit of existing content sources

| Source | Owner | Est. Objects | Priority |
|--------|-------|--------------|----------|
| Confluence docs | Docs team | TBD | TBD |
| Support macros | Support team | TBD | TBD |
| In-product tips | UX team | TBD | TBD |
| Release notes | PM team | TBD | TBD |
| Internal runbooks | Engineering | TBD | TBD |

### 17.2 Prioritization Framework

Content migrated in order of:

1. **Support ticket volume:** Topics with highest ticket count
2. **Onboarding friction:** Topics blocking new user success
3. **Partner enablement:** Topics required for partner certification
4. **Freshness:** Recently updated content (more accurate)

### 17.3 Migration Process

1. **Identify:** Flag content for migration from source audit
2. **Assess:** Determine if content is accurate, complete, current
3. **Transform:** Convert to canonical template format
4. **Enrich:** Add required metadata
5. **Review:** Content owner validates accuracy
6. **Publish:** Publish to SSOT and AI index
7. **Redirect:** Create redirect from legacy source (if applicable)
8. **Deprecate:** Mark legacy source as deprecated

### 17.4 Parallel Operation

During migration period:

* Legacy sources remain accessible with "Moving to new KB" banner
* Banner links to new canonical object when available
* Search includes both legacy and new content with preference for new
* Analytics track usage of both to validate migration

### 17.5 Redirect Strategy

* Permanent redirects (301) from legacy URLs to new objects
* Redirect mapping maintained for 2 years
* Analytics track redirect usage to identify external links
* Broken link monitoring for unmapped legacy URLs

---

## 18) Integration Requirements

### 18.1 Platform Integrations

| System | Integration Type | Purpose |
|--------|-----------------|---------|
| Virima CMDB | Read | Context-aware help based on CI data |
| Virima Discovery | Read | Error codes and troubleshooting context |
| Virima Auth | SSO | Single sign-on for KB and partner portal |
| Virima Audit | Write | Log KB access and actions for compliance |

### 18.2 External Integrations

| System | Integration Type | Purpose |
|--------|-----------------|---------|
| Ticketing (ServiceNow, Jira SM) | Bidirectional | Escalation creation, ticket status sync |
| Slack/Teams | Notifications | Content update alerts, stale content reminders |
| LMS (if selected) | Content sync | Partner training content publication |

### 18.3 Integration Requirements

**Ticketing Integration:**
- [ ] Create ticket from KB/AI escalation with context bundle
- [ ] Link ticket to relevant KB articles
- [ ] Update ticket with resolution for feedback loop
- [ ] Sync ticket status back to platform for user visibility

**Collaboration Integration:**
- [ ] Notify content owners of pending reviews via Slack/Teams
- [ ] Alert on stale content approaching SLA
- [ ] Weekly digest of content health metrics

---

## 19) Accessibility Requirements

### 19.1 WCAG 2.1 AA Compliance

All KB and help surfaces shall meet WCAG 2.1 Level AA standards:

**Perceivable:**
- [ ] All images have descriptive alt text
- [ ] Color contrast ratio minimum 4.5:1 for text
- [ ] Content is readable without CSS
- [ ] Video/audio content has captions (when applicable)

**Operable:**
- [ ] All functionality accessible via keyboard
- [ ] No keyboard traps
- [ ] Skip navigation links available
- [ ] Focus indicators visible
- [ ] No time limits on reading content

**Understandable:**
- [ ] Language is clear and simple (8th grade reading level target)
- [ ] Consistent navigation across pages
- [ ] Error messages are clear and actionable
- [ ] Form labels are descriptive

**Robust:**
- [ ] Valid HTML markup
- [ ] Compatible with screen readers (JAWS, NVDA, VoiceOver)
- [ ] Compatible with browser zoom (up to 200%)

### 19.2 Testing Requirements

* Automated accessibility testing in CI/CD pipeline
* Manual screen reader testing for new features
* Keyboard-only navigation testing
* Color contrast validation for all new UI

---

## 20) Non-Functional Requirements

### 20.1 Performance

| Metric | Requirement |
|--------|-------------|
| KB page load time | < 2 seconds (P95) |
| Search response time | < 1 second (P95) |
| AI response time | < 5 seconds (P95) |
| Help panel open time | < 500ms |

### 20.2 Scalability

| Dimension | Requirement |
|-----------|-------------|
| Concurrent users | 10,000+ |
| Knowledge objects | 10,000+ |
| Search queries/minute | 1,000+ |
| AI queries/minute | 500+ |

### 20.3 Availability

| Metric | Requirement |
|--------|-------------|
| Uptime SLA | 99.9% |
| Planned maintenance window | Monthly, < 4 hours, with notice |
| Recovery Time Objective (RTO) | 4 hours |
| Recovery Point Objective (RPO) | 1 hour |

### 20.4 Security

| Requirement | Description |
|-------------|-------------|
| Authentication | SSO via Virima Auth (OIDC/SAML) |
| Authorization | Role-based access for admin functions |
| Data encryption | TLS 1.2+ in transit, AES-256 at rest |
| Audit logging | All content changes, access, and escalations logged |
| Data residency | Configurable by tenant (US, EU, APAC) |

---

## 21) Appendix: RACI (starter)

| Activity                       | PM  | Docs | UX  | AI  | Support | Eng |
| ------------------------------ | --- | ---- | --- | --- | ------- | --- |
| Charter + KPIs                 | A/R | C    | C   | C   | C       | C   |
| Taxonomy + schema              | A   | R    | C   | C   | C       | C   |
| Content ops + QA               | C   | A/R  | C   | C   | C       | C   |
| Help surfaces UX               | C   | C    | A/R | C   | C       | C   |
| AI retrieval + eval            | C   | C    | C   | A/R | C       | C   |
| Ticket taxonomy + feedback     | C   | C    | C   | C   | A/R     | C   |
| Instrumentation + release gate | C   | C    | C   | C   | C       | A/R |
| Content migration              | C   | A/R  | C   | C   | C       | C   |
| Partner enablement             | A   | R    | C   | C   | C       | C   |
| Accessibility compliance       | C   | C    | A/R | C   | C       | C   |
| Analytics dashboard            | C   | C    | C   | C   | C       | A/R |

Legend: R=Responsible, A=Accountable, C=Consulted

---

**End of Document**

