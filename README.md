# HaqVani

> **Speak your situation. Discover your benefits. Get ready to apply.**

**PS41 — Applied AI | HackSprint 2026**

HaqVani is a **voice-first, multilingual citizen benefit assistant** built around a simple idea:

> **Citizens should not have to learn the language of government systems to understand the benefits available to them.**

A citizen can describe their situation in an Indian language through **WhatsApp**. HaqVani converts that spoken story into structured facts, checks those facts against a **curated registry of verified government-benefit rules**, explains exactly why the citizen qualifies or what information is missing, and produces an **application-ready document packet**.

---

## The Problem

Government benefits may exist, but accessing them can still be difficult.

A citizen may know that assistance exists and still be unable to answer:

- **Does this benefit apply to me?**
- **Why am I eligible or not eligible?**
- **What information is missing?**
- **Which documents do I need?**
- **What should I do next?**

The challenge becomes even greater for **vernacular-first and low-literacy users** who find text-heavy government portals and application processes difficult to navigate.

HaqVani focuses on this interaction gap between:

**Government benefit → eligibility rules → digital forms/portals → citizen understanding**

---

## Our Solution

HaqVani changes the starting point.

Instead of asking:

> **“Which government scheme are you searching for?”**

HaqVani asks:

> **“Tell me about your situation.”**

The citizen does not need to know the scheme name, department, eligibility terminology, or application terminology.

### Core journey

**Citizen voice → Speech-to-text → Structured profile → Missing information → Verified rules → Explainable eligibility → Documents → Application-ready PDF → Voice response**

This is **situation-first benefit discovery**, rather than scheme-first search.

---

## Example: A Citizen's Story

Imagine **Lakshmi**, a synthetic demo citizen in Karnataka.

She sends a Kannada voice message:

> “ನನಗೆ 62 ವರ್ಷ. ನನ್ನ ಗಂಡ ತೀರಿಕೊಂಡಿದ್ದಾರೆ. ಬಿಪಿಎಲ್ ಕಾರ್ಡ್ ಇದೆ.”

HaqVani converts the message into structured information:

```json
{
  "age": 62,
  "marital_status": "widowed",
  "bpl": true,
  "state": "Karnataka",
  "annual_income": null
}
```

HaqVani detects that annual income is required but has not been provided.

Instead of guessing, it asks a clarification question in Kannada:

> “ನಿಮ್ಮ ಅಂದಾಜು ವಾರ್ಷಿಕ ಆದಾಯ ಎಷ್ಟು?”

The citizen replies:

```text
₹0
```

The eligibility engine then evaluates the configured scheme rules and returns a criterion-level result.

### Demonstrated outcome

**Indira Gandhi National Destitute Widow Pension Scheme (IGNWPS/IGNDWP) — Karnataka**

Configured demo criteria:

- Age: **18–64**
- BPL family: **Yes**
- Annual income: **≤ ₹32,000**
- Husband legally dead: **Yes**

Result:

**Eligible — 4/4 configured criteria met**

HaqVani can then present:

- Eligibility explanation
- Document checklist
- Application-ready PDF draft
- Next-step guidance
- Kannada voice response

**The PDF is a draft for the citizen to use at the relevant portal/service centre; HaqVani does not claim automatic government submission.**

**Rules source:** Karnataka Revenue Department, DSSP Annual Report 2023–24.

---

## Why HaqVani Is Not Just a Chatbot

### Typical chatbot

```text
User question
     ↓
    LLM
     ↓
Generated answer
```

### HaqVani

```text
Citizen voice
     ↓
Speech understanding
     ↓
Structured citizen facts
     ↓
Missing information detection
     ↓
Verified scheme rules
     ↓
Deterministic eligibility decision
     ↓
Criterion-level explanation
     ↓
Documents + application-ready output
     ↓
Voice response
```

The LLM is **not** the eligibility authority.

### Our trust architecture

> **AI understands. Rules decide. Evidence explains.**

Sarvam handles language understanding and interaction.  
Our deterministic rules engine evaluates eligibility.  
Each configured rule is tied to the verified scheme information used by the system.

This separation reduces the risk of allowing a generative model to invent eligibility decisions.

---

## Why Voice + WhatsApp?

### Voice-first

The citizen can speak instead of filling long text forms or navigating complex interfaces.

### WhatsApp-first

The product does not require the citizen to learn a new application. WhatsApp acts as the conversational entry point.

### Indian-language interaction

The experience is designed for multilingual, vernacular-first interaction, beginning with **Kannada and Hindi** for the MVP.

---

## Sarvam AI Integration

Sarvam is a core part of HaqVani's interaction layer rather than a decorative API integration.

| Sarvam capability | HaqVani usage |
|---|---|
| **Saaras** | Citizen voice → text |
| **Sarvam-105B** | Transcript → structured citizen profile + clarification dialogue |
| **Bulbul** | Text result → Indian-language voice response |

### Why Sarvam?

HaqVani needs strong Indian-language speech and language capabilities because the core product experience begins with how a citizen naturally communicates — **their own voice and language**.

---

## System Architecture

```text
                         HAQVANI
                            │
                    WhatsApp Interface
                            │
                            ▼
                    Voice / Text Input
                            │
                            ▼
                   ┌─────────────────┐
                   │  Sarvam Saaras  │
                   │   Speech → Text │
                   └────────┬────────┘
                            │
                            ▼
                    Citizen Transcript
                            │
                            ▼
                   ┌─────────────────┐
                   │  Sarvam-105B    │
                   │ Profile Extractor│
                   │   Structured JSON│
                   └────────┬────────┘
                            │
                            ▼
                     Citizen Profile
                            │
                    ┌───────┴────────┐
                    │                │
                    ▼                ▼
            Missing Information   Scheme Registry
                    │                │
                    ▼                │
            Voice Clarification     │
                    │                │
                    └───────┬────────┘
                            ▼
                    Deterministic Rules
                         Engine
                            │
                            ▼
                   Eligibility Results
                     /      |       \
                    /       |        \
                Reason   Documents   Source
                    \       |        /
                     \      |       /
                            ▼
                  Application Generator
                     │      │      │
                     ▼      ▼      ▼
                    PDF Checklist Summary
                            │
                            ▼
                       Sarvam Bulbul
                            │
                            ▼
                       Voice Reply
                            │
                            ▼
                          Citizen
```

---

## Technology Stack

**Frontend**
- Next.js
- TypeScript
- Tailwind CSS

**Backend**
- FastAPI
- Python

**Database**
- PostgreSQL

**Messaging**
- WhatsApp Cloud API

**AI / Language**
- Sarvam Saaras
- Sarvam-105B
- Sarvam Bulbul

**Document Generation**
- Python PDF generation

**Deployment**
- Vercel
- FastAPI backend
- PostgreSQL

---

## The Eligibility Engine

The eligibility layer is intentionally deterministic.

The system first turns a citizen's natural-language story into structured facts. Then those facts are evaluated against configured scheme criteria.

Conceptually:

```text
Citizen Profile
      +
Scheme Rules
      ↓
Eligibility Engine
      ↓
Per-criterion result
      +
Explanation
      +
Required documents
      +
Source
```

Example:

```text
Age 18–64                    ✓
BPL family                   ✓
Annual income ≤ ₹32,000      ✓
Husband legally dead         ✓

RESULT: Eligible
```

If required information is missing:

```text
Required field absent
        ↓
Ask citizen
        ↓
Update profile
        ↓
Re-run deterministic rules
```

### Important principle

**Never guess a missing eligibility fact. Ask for it.**

---

## Evidence and Explainability

A key design decision is that eligibility results should be explainable.

For every configured criterion, HaqVani aims to retain:

```text
Criterion
   ↓
Configured rule
   ↓
Result
   ↓
Supporting scheme source
```

This makes it possible to answer:

> **“Why did HaqVani say I am eligible?”**

Instead of returning a black-box answer, the product can show the citizen the individual criteria that were met or not met.

---

## Application-Ready Output

HaqVani does not stop at:

> **“You are eligible.”**

The workflow continues toward action.

The application-ready packet can contain:

### 1. Citizen summary
- Available citizen details
- Relevant family/status information
- Location and income information where provided

### 2. Matched benefit
- Scheme name
- Eligibility status
- Explanation

### 3. Document checklist
- Required documents
- Known/missing items

### 4. Application draft
- A generated PDF containing the information available to the workflow

This positions HaqVani as an **accessibility layer before the formal government application process**, not a replacement for official government portals.

---

## MVP Scope

For the hackathon, we deliberately avoid overbuilding.

### MVP target

- **Kannada + Hindi**
- **10–15 carefully selected schemes**
- WhatsApp voice workflow
- Sarvam speech-to-text
- Sarvam structured profile extraction
- Clarification questions
- Deterministic eligibility engine
- Explainable eligibility card
- Document checklist
- Application-ready PDF
- Sarvam text-to-speech response

The scheme count is a **targeted MVP scope**, not a claim that HaqVani already covers every government scheme.

---

## Scalability

The architecture separates the language layer from the eligibility layer.

### Add a language
→ Extend the Sarvam language interface

### Add a scheme
→ Add a validated rule definition + evidence source

### Add a state
→ Add state-specific schemes/rules

### Add a distribution partner
→ Reuse the same backend

Potential distribution partners include:

- NGOs
- Self-help groups (SHGs)
- Citizen-service kiosks
- Community workers
- Bank BC agents

This enables a practical **B2B2C / assisted-access model** where organizations that already serve citizens can use HaqVani as an accessibility layer.

---

## What HaqVani Does Differently

| Traditional approach | HaqVani |
|---|---|
| Starts with a scheme/search query | Starts with the citizen's situation |
| Often text-heavy | Voice-first |
| Citizen must know what to ask | Citizen simply describes their situation |
| LLM-generated answer | Structured facts + deterministic rules |
| May stop at information | Continues toward documents and application readiness |
| Eligibility can be opaque | Criterion-level explanation |
| Language can be a barrier | Indian-language interaction |

### The core differentiator

> **Search starts with a scheme. HaqVani starts with a person.**

---

## Demo Flow

The intended product demonstration is a single end-to-end journey:

```text
00:00  Send Kannada voice message
00:05  Show transcript
00:15  Show structured citizen profile
00:25  Show eligibility engine
00:35  Show eligibility result
00:45  Show document requirements
00:50  Ask a missing-information question
01:00  Citizen replies
01:10  Generate application-ready PDF
01:20  Play Kannada voice response
01:35  Show HaqVani Benefit Card
```

The key demonstration is:

> **A Kannada voice note becomes an explainable benefit decision and an application-ready packet — then the system speaks back in Kannada.**

---

## Responsible Design

Because HaqVani deals with citizen information, the hackathon prototype is designed around:

- **Synthetic demo citizens**
- No real Aadhaar numbers in the demo
- No real sensitive personal documents
- Information collection limited to what is needed for the eligibility workflow
- Eligibility decisions separated from generative AI
- Clear distinction between an application draft and actual government submission

---

## What We Are Not Claiming

HaqVani is **not** claiming to:

- Know every government scheme in India
- Replace official government portals
- Automatically submit government applications
- Let an LLM independently decide eligibility
- Guarantee a government benefit approval

Instead, HaqVani focuses on one clear problem:

> **Helping a citizen understand potential benefit eligibility and become ready to apply.**

---

## Project Status

**HackSprint Round 1 — Concept / prototype development**

The project is being prepared for the 24-hour in-person build, with the core product journey centered on:

**Kannada voice → structured citizen profile → clarification → eligibility → explanation → PDF → Kannada voice**

The priority is reliability of one complete citizen journey rather than a large number of partially implemented features.

---

## Team

**RUNTIME TERROR**

- Monish MR
- Suhan DK
- Mayank Gawali

---

## One-Line Pitch

> **HaqVani lets a citizen speak their situation in their own language and turns that voice into an explainable benefit match and application-ready packet.**

## 30-Second Pitch

> **HaqVani is a voice-first WhatsApp assistant for citizens who struggle with text-heavy government services. A citizen describes their situation in Kannada, Hindi or another supported Indian language. Sarvam converts that voice into structured facts. Our deterministic rules engine checks those facts against verified benefit criteria, explains exactly why the citizen qualifies or what information is missing, and generates an application-ready document checklist and form draft. AI understands the citizen — deterministic rules make the decision.**

---

## PS41 Alignment

HaqVani is designed specifically around **PS41 — Applied AI** through:

- Meaningful real-world accessibility problem
- Voice-first interaction
- Indian-language AI
- Sarvam API integration
- Structured language understanding
- Deterministic eligibility reasoning
- Explainability and evidence
- Action-oriented application readiness

> **AI interprets. Rules verify. Sources explain.**

**From citizen story to benefit readiness.**
