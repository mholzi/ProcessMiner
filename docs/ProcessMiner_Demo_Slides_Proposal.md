# ProcessMiner Demo Presentation - Slide Deck Proposal

**Audience:** Senior Decision Makers
**Duration:** 45 minutes
**Total Slides:** 14 slides (excluding backup)

---

## PHASE 1: THE BUSINESS PROBLEM (Slides 1-3)

---

### Slide 1: Title + The Challenge

**Title:** ProcessMiner
**Subtitle:** AI-Powered Process Transformation for Enterprise Banking

**Layout:** Split slide — title left, challenge right

**Right Panel — The Problem:**

```
┌─────────────────────────────────────────┐
│     "How long to document a single      │
│      process for transformation?"       │
│                                         │
│              4-6 WEEKS                  │
│           average per process           │
└─────────────────────────────────────────┘
```

**Three Pain Points (icons + short text):**
- 📄 Scattered, inconsistent documentation
- ⏰ SMEs too busy to write from scratch
- 🔄 Gap between business knowledge and IT specs

**Speaker Notes:**
> Open with the question. Let the room respond. Then reveal the typical answer and pain points. This establishes the problem in 60 seconds.

---

### Slide 2: The Solution — Flip the Burden

**Title:** What If AI Drafted and SMEs Validated?

**Layout:** Before/After comparison + KPIs

**Top Section — Comparison:**

| Traditional | ProcessMiner |
|-------------|--------------|
| SME writes from scratch | AI drafts, SME validates |
| 4-6 weeks per process | 30-minute sessions |
| Single document format | Multi-altitude outputs |
| Manual compliance mapping | Built-in regulatory frameworks |

**Bottom Section — Three KPIs:**

```
┌─────────────┐  ┌─────────────┐  ┌─────────────┐
│    70%+     │  │    90%+     │  │    80%+     │
│  REDUCTION  │  │ COMPLETENESS│  │  APPROVAL   │
│  in SME time│  │ without edit│  │  rate auto  │
└─────────────┘  └─────────────┘  └─────────────┘
```

**Speaker Notes:**
> Core insight: SMEs are excellent validators but poor writers. Flip the burden. These metrics are from pilot testing.

---

### Slide 3: The 6-Agent Ecosystem → Transition to Demo

**Title:** Specialized Expertise, Orchestrated Intelligence

**Layout:** Agent pipeline + demo preview

**Left Section — Pipeline Diagram:**

```
┌─────────────────────────────────────────┐
│  📋 Process Doc Analyst                 │
│     ↓                                   │
│  🛡️ Control    🎯 Client Journey        │
│  Analyst       Analyst                  │
│     ↓              ↓                    │
│  💡 Innovation  🔄 Transformation       │
│  Analyst        Agent                   │
│     ↓              ↓                    │
│  🏗️ IT Architect                        │
└─────────────────────────────────────────┘
```

**Right Section — Demo Preview:**

> "Two capabilities to demonstrate:"
>
> 1. **Document Extraction** — Capture process knowledge in 30 minutes
> 2. **Party Mode** — Multi-agent collaboration on complex questions

**Speaker Notes:**
> Briefly explain each agent's role (one sentence each). Then transition to live demo. "Let's see it in action."

---

## PHASE 2: DEMO SUPPORT SLIDES (Slides 4-11)

---

### Slide 4: Demo Context — What We're Documenting

**Title:** Demo Process: Client Complaints Management

**Visual:** Simple process flow

```
Complaint    →    Acknowledgment    →    Investigation    →    Resolution    →    Follow-up
Received          (24-48 hrs)            (5-10 days)          (Response)        (Feedback)
```

**Context Box:**
- Regulatory requirement: FCA DISP 8-week deadline
- Volume: ~5,000 complaints/month
- Current pain: Manual triage, inconsistent categorization

**Speaker Notes:**
> Set context before demo. This is a real banking process everyone understands. It has regulatory pressure (FCA), volume challenges, and clear pain points.

---

### Slide 5: Demo Part A — Elicitation Overview

**Title:** Progressive Knowledge Extraction

**Visual:** 9-step workflow diagram

```
┌───┐   ┌───┐   ┌───┐   ┌───┐   ┌───┐   ┌───┐   ┌───┐   ┌───┐   ┌───┐
│ 1 │ → │ 2 │ → │ 3 │ → │ 4 │ → │ 5 │ → │ 6 │ → │ 7 │ → │ 8 │ → │ 9 │
└───┘   └───┘   └───┘   └───┘   └───┘   └───┘   └───┘   └───┘   └───┘
 Init   Existing Overview Steps  Excep-  Pain   Controls Systems Valid-
        Docs                     tions   Points                  ation
```

**Key Design Principles:**
- Multiple-choice questions minimize typing burden
- "Skip" and "Pause" escape hatches respect SME time
- AI drafts content, SME validates
- Session saves every 5 minutes — no lost work

**Speaker Notes:**
> Show this before live demo to set expectations. The elicitation is structured, not free-form. Each step builds on previous.

---

### Slide 6: Structured Reference System

**Title:** Everything Cross-Referenced, Everything Traceable

**Visual:** ID system explanation

| Prefix | Meaning | Example |
|--------|---------|---------|
| PS# | Process Step | PS001: Receive complaint via email/phone/web |
| EX# | Exception | EX001: Escalation to senior handler |
| PP# | Pain Point | PP001: Manual triage causes delays |
| CP# | Control Point | CP001: 24-hour acknowledgment SLA |
| SYS# | System | SYS001: CRM system (Salesforce) |

**Visual:** Show how IDs link across documents

```
Pain Point PP003 ──► References PS005, PS006
                 ──► Triggers Control CP002
                 ──► Addressed by Innovation INV-007
```

**Speaker Notes:**
> This ID system is critical for traceability. When IT asks "why do we need this feature?" you can trace back to specific pain point and process step.

---

### Slide 7: Demo Output Preview — Document Suite

**Title:** One Session, Five Documents

**Visual:** Document stack/fan showing outputs

| Document | Purpose | Audience |
|----------|---------|----------|
| `as-is-process-documentation.md` | Comprehensive process detail | Process owners, analysts |
| `exec-summary-as-is.md` | 2-page overview | Executives, steering committee |
| `pain-points-detail.md` | Deep analysis of operational issues | Transformation team |
| `control-points-detail.md` | Compliance and control mapping | Risk, compliance |
| `structured-data.json` | Machine-readable data | Downstream agents, automation |

**Key Message:** "Same data, multiple altitudes — no additional SME time."

**Speaker Notes:**
> After live demo of elicitation, show these actual outputs. Have them open and ready to flip through.

---

### Slide 8: Demo Part B — Party Mode Introduction

**Title:** Multi-Agent Collaboration

**Visual:** Agent "conversation" preview

```
┌─────────────────────────────────────────────────────────────┐
│  USER: "How should we redesign complaints resolution?"      │
├─────────────────────────────────────────────────────────────┤
│  🎯 CLIENT JOURNEY ANALYST:                                 │
│  "Complaints are loyalty moments — speed of response        │
│   matters more than outcome..."                             │
├─────────────────────────────────────────────────────────────┤
│  🛡️ CONTROL ANALYST:                                        │
│  "We must maintain FCA DISP compliance — 48-hour            │
│   acknowledgment is non-negotiable..."                      │
├─────────────────────────────────────────────────────────────┤
│  💡 INNOVATION ANALYST:                                     │
│  "Fintech competitors are using AI chatbots for 60%         │
│   of first-line complaint handling..."                      │
├─────────────────────────────────────────────────────────────┤
│  🔄 TRANSFORMATION AGENT:                                   │
│  "Quick win: auto-acknowledge in 2 hours. Core change:      │
│   implement AI routing by complaint type..."                │
└─────────────────────────────────────────────────────────────┘
```

**Key Message:** "Multi-perspective analysis in minutes, not multiple meetings."

**Speaker Notes:**
> Set up what they're about to see. Party Mode is engaging and often surprising. Agents will build on each other's points and sometimes respectfully disagree.

---

### Slide 9: Party Mode — How It Works

**Title:** Intelligent Agent Selection

**Visual:** Selection logic diagram

```
┌─────────────────────┐
│    User Question    │
└──────────┬──────────┘
           │
           ▼
┌─────────────────────┐
│  Analyze for:       │
│  - Domain expertise │
│  - Technical depth  │
│  - Compliance needs │
│  - Customer impact  │
└──────────┬──────────┘
           │
           ▼
┌─────────────────────┐
│  Select 2-4 most    │
│  relevant agents    │
└──────────┬──────────┘
           │
           ▼
┌─────────────────────┐
│  Orchestrate        │
│  natural dialogue   │
└─────────────────────┘
```

**Features:**
- Agents maintain distinct personalities and expertise
- Natural cross-talk and building on points
- Professional disagreement encouraged
- Agents can ask clarifying questions

**Speaker Notes:**
> This isn't scripted — the agents genuinely analyze and respond. Different questions will surface different agents.

---

### Slide 10: Sample Outputs — What We Generated

**Title:** From Demo: Client Complaints Analysis

**Visual:** Key metrics from actual outputs

| Analysis | Key Finding |
|----------|-------------|
| **Client Effort Score** | 65/100 (HIGH effort — worse than industry benchmark 55-60) |
| **Friction Points** | 12 identified across 5 journey stages |
| **Compliance Controls** | 10 controls mapped to 12 regulations |
| **Innovations Identified** | 18 opportunities (7 MUST, 5 SHOULD, 4 COULD, 2 DEFER) |
| **Investment Estimate** | £450-600k over 36 months |

**Document Sizes:**
- Total documentation: ~200 KB across 8 files
- Equivalent manual effort: 4-6 weeks

**Speaker Notes:**
> These are real numbers from our test run. Show the actual documents if time permits.

---

### Slide 11: Transition to BMAD

**Title:** The Technology Behind ProcessMiner

**Visual:** Simple "built on" graphic

```
┌─────────────────────────────────────┐
│         ProcessMiner                │
│    (Banking Process Module)         │
└──────────────┬──────────────────────┘
               │
               │  Built on
               ▼
┌─────────────────────────────────────┐
│            BMAD                     │
│  (AI Agent Orchestration Framework) │
└─────────────────────────────────────┘
```

**Teaser:** "ProcessMiner is one application. The underlying framework has broader potential..."

**Speaker Notes:**
> Transition slide. This opens the door to Phase 3 — explaining BMAD and broader applications.

---

## PHASE 3: BMAD & BANKING APPLICATIONS (Slides 12-14)

---

### Slide 12: What is BMAD?

**Title:** BMAD: Build More, Architect Dreams

**Subtitle:** AI-Powered Framework for Orchestrating Specialized Agents

**Layout:** Framework overview + banking fit

**Left Section — Capabilities:**

```
┌─────────────────────────────────────┐
│           BMAD CORE                 │
├─────────────────────────────────────┤
│  19 Specialized Agents              │
│  50+ Guided Workflows               │
│  Built-in Audit Trails              │
│  Regulatory Framework Integration   │
│  Scale-Adaptive Intelligence        │
└─────────────────────────────────────┘
```

**Right Section — Why BMAD for Banking?**

| Generic AI | BMAD for Banking |
|------------|------------------|
| Ad-hoc prompting | Structured, auditable workflows |
| No compliance awareness | FCA, PRA, GDPR built-in |
| Context lost | Full traceability & version control |
| Hallucination risk | Domain-constrained outputs |

**Speaker Notes:**
> BMAD is purpose-built for regulated industries. Banking requires audit trails, compliance mapping, and structured outputs — not ad-hoc AI conversations.

---

### Slide 13: Banking Applications Beyond Complaints

**Title:** One Framework, Multiple Banking Transformations

**Layout:** Banking domain cards

**Banking Process Applications:**

```
┌─────────────┐ ┌─────────────┐ ┌─────────────┐
│  ONBOARDING │ │   LENDING   │ │  PAYMENTS   │
│             │ │             │ │             │
│     🏦      │ │     💳      │ │     💸      │
│             │ │             │ │             │
│ KYC/AML     │ │ Credit      │ │ Transaction │
│ workflows   │ │ decisioning │ │ processing  │
│ Document    │ │ Loan        │ │ Fraud       │
│ collection  │ │ origination │ │ detection   │
└─────────────┘ └─────────────┘ └─────────────┘

┌─────────────┐ ┌─────────────┐ ┌─────────────┐
│  OPERATIONS │ │    RISK     │ │ REGULATORY  │
│             │ │             │ │  REPORTING  │
│     ⚙️      │ │     📊      │ │     📋      │
│             │ │             │ │             │
│ Account     │ │ Credit risk │ │ FCA/PRA     │
│ servicing   │ │ Operational │ │ submissions │
│ Trade       │ │ risk        │ │ ICAAP/ILAAP │
│ settlements │ │ Model valid │ │ Pillar 3    │
└─────────────┘ └─────────────┘ └─────────────┘
```

**Key Message:** "Same methodology scales across the entire banking value chain"

**Speaker Notes:**
> ProcessMiner for complaints is the proof point. The same agent architecture applies to any banking process — onboarding, lending, payments, risk, regulatory. Each has SMEs, documentation gaps, and transformation needs.

---

### Slide 14: Summary + Next Steps

**Title:** Three Takeaways + Pilot Proposal

**Layout:** Left = takeaways, Right = banking pilot path

**Left Section — Remember This:**

```
┌───┐
│ 1 │  FLIP THE BURDEN
└───┘  AI drafts, SMEs validate — 70%+ time reduction

┌───┐
│ 2 │  ORCHESTRATED EXPERTISE
└───┘  6 specialized agents with banking domain knowledge

┌───┐
│ 3 │  BUILT FOR REGULATED INDUSTRIES
└───┘  Audit trails, compliance mapping, full traceability
```

**Right Section — Suggested Banking Pilot:**

```
     PILOT                 SCALE                  EXPAND
    ┌────────┐           ┌────────┐            ┌────────┐
    │Complaints│   ──►   │Onboarding│   ──►    │Lending │
    │KYC/AML  │          │Payments │           │Risk    │
    │Account  │          │Operations│          │Regulatory│
    │servicing│          │          │          │         │
    └────────┘           └────────┘            └────────┘

    2-3 processes         Division-wide         Enterprise
```

**Ideal Pilot Criteria:**
- Process with known pain points & regulatory pressure
- Engaged SME available for 2-3 sessions
- Clear transformation appetite

**Questions?**

[Your contact information]

**Speaker Notes:**
> Land the three points — especially #3 for banking audience. Suggest starting with complaints (already demonstrated) plus 1-2 additional processes. Offer to identify best pilot candidates together.

---

## BACKUP SLIDES (In Case of Demo Failure)

---

### Backup Slide B1: Elicitation Screenshots

**Title:** Document Extraction — Screenshots

**Visual:** 4-6 screenshots showing:
- Session initialization
- Multiple-choice question example
- Pain point capture
- Generated documentation preview

**Purpose:** If live demo fails, walk through these static screenshots

---

### Backup Slide B2: Party Mode Transcript

**Title:** Multi-Agent Collaboration — Example

**Visual:** Full transcript of a Party Mode conversation

**Purpose:** If live demo fails, show this as "here's what it looks like"

---

### Backup Slide B3: Output Document Samples

**Title:** Generated Documentation Examples

**Visual:** Side-by-side screenshots of:
- Executive summary
- Detailed process documentation
- Structured JSON

**Purpose:** Show actual outputs even if demo can't run

---

### Backup Slide B4: Technical Architecture

**Title:** Technical Deep Dive

**Visual:** Detailed architecture diagram showing:
- Workflow execution model
- Data flow between agents
- File storage structure

**Purpose:** For technical audience questions

---

### Backup Slide B5: Compliance Framework Mapping

**Title:** Banking Regulatory Coverage

**Visual:** Matrix showing regulations mapped:
- FCA DISP
- Consumer Duty
- GDPR
- SMCR
- Basel III

**Purpose:** For compliance-focused questions

---

### Backup Slide B6: Comparison with Alternatives

**Title:** Why Not [Alternative]?

**Visual:** Comparison matrix vs:
- Traditional BPM tools (Signavio, Aris)
- Generic AI (ChatGPT, Copilot)
- Consulting approaches

**Purpose:** For competitive questions

---

## DESIGN NOTES FOR SLIDE CREATION

### Color Palette
- Primary: Deep blue (#1a365d) — trust, enterprise
- Secondary: Teal (#319795) — innovation, transformation
- Accent: Gold (#d69e2e) — value, success
- Background: White or very light gray
- Text: Dark gray (#2d3748)

### Typography
- Headlines: Bold sans-serif (e.g., Inter, Helvetica Neue)
- Body: Regular sans-serif
- Code/Technical: Monospace (e.g., JetBrains Mono)

### Visual Principles
- Minimal text per slide (6x6 rule max)
- One key message per slide
- Consistent iconography throughout
- White space is your friend
- Diagrams over bullet points

### Animation Guidance
- Use sparingly — senior audience
- Fade-in for sequential reveals
- No flying/spinning effects
- Build complexity gradually (click to reveal)

---

## TIMING SUMMARY

| Phase | Slides | Time |
|-------|--------|------|
| Phase 1: Business Problem | 3 | ~8 min |
| Phase 2: Demo + Support | 8 | ~25 min |
| Phase 3: BMAD & Beyond | 3 | ~8 min |
| Q&A Buffer | — | ~4 min |
| **Total** | **14** | **45 min** |

---

## HANDOUT SUGGESTION

Create a 2-page PDF leave-behind:
- Page 1: Value proposition + 6-agent overview
- Page 2: Sample outputs + next steps

This gives attendees something physical to share with colleagues who weren't present.
