# Earned Authority Model (EAM): A Governance Framework Based on Experience, Transparency, and Citizen Oversight

> **This is a theoretical model for institutional design. It does not constitute policy advice.**  
> The EAM proposes an alternative to winner-take-all electoral politics by tying public authority to demonstrated competence, peer validation, and radical transparency—not just ballot-box mandates.

---

## Core Principle: From Electoral Mandate to Earned Legitimacy

Public office should not be granted solely through periodic elections. Instead, authority must be **earned incrementally** through verified experience, multi-source evaluation, and continuous accountability. The model retains democratic foundations but upgrades them with meritocratic safeguards and structural transparency.

---

## Key Design Elements

### 1. Tiered Eligibility: No Jumping the Ladder

- All elected and key appointed officials must ascend through **four administrative tiers**:  
  **Municipal → County → State → Federal**
- **Minimum tenure**: One full term (or 1 year) of service at a given tier is required before eligibility for the next.
- Applies to: Mayors, Governors, U.S. Senators/Representatives, Judges, Sheriffs, District Attorneys, and other constitutionally significant offices.

> *Rationale*: Prevents “celebrity candidacies” and ensures leaders possess grounded, cross-level governance experience.

---

### 2. Competitive Scoring System: Multi-Source Evaluation

Replaces simple plurality/plurality-runoff with a **weighted scoring mechanism**. The candidate with the highest composite score wins—no minimum threshold required.

| Office Type       | Scoring Formula                                                                 | Implementation Notes |
|-------------------|----------------------------------------------------------------------------------|----------------------|
| **Elected Offices**<br>(e.g., Governor, Mayor) | `Voter Support × 50%`<br>`+ Peer & Subordinate Endorsement × 40%`<br>`+ Superior Veto Check × 10%` | Voter support drawn from simulated districts (50K–250K residents). Peer pool includes 15–100 sitting officials at same tier. |
| **Appointed Offices**<br>(e.g., Judge, DA) | `Endorsement by Local Electeds × 60%`<br>`+ Superior Veto Check × 30%`<br>`+ Anonymous Peer Review × 10%` | “Local Electeds” = city council, county commission, etc. Peer review published 14 days pre-decision. |

- **Superior Veto Check**: Binary (0 = blocked, 1 = approved). Only one superior official may exercise this (e.g., Governor for state judges).
- **Anonymous Peer Review**: 70–100 qualified peers rate candidate on a 0–10 scale; converted to percentile and made public.

---

### 3. High Compensation & Security: Enabling Integrity

- **Salary**: Set at **200%–300%** of the local private-sector executive compensation median (adjusted annually for CPI).
- **Healthcare**: Fully covered for official and immediate family.
- **Housing Stipend**:
  - Available only to officials with **no owned real property**.
  - Equal to **30% of base salary**, paid over 5 years.
  - Funds restricted to purchase of **first primary residence** (verified via deed recording).

> *Goal*: Eliminate financial insecurity as a driver of corruption; make public service a prestigious, sustainable career.

---

### 4. Radical Financial Transparency

- All individual or official expenditures exceeding **$10,000 USD** must be logged in a **public ledger within 72 hours**.
- Disclosed fields: Date, amount, purpose, payee (personally identifiable info redacted per FOIA standards).
- Data published in machine-readable formats (JSON/CSV) for public audit and third-party analysis.

---

### 5. Citizen Oversight Panels: Structured Public Input

- **Selection**: Open volunteer sign-up; if oversubscribed, members selected by **stratified random draw**.
- **Term**: 1 year (renewable once).
- **Powers**: Observational and advisory only—**no voting, investigative, or veto authority**.
- **Core Functions**:
  1. Aggregate input from three channels:  
     - Constituents (bottom-up)  
     - Peer officials (lateral)  
     - Supervising executives (top-down)
  2. Publish a **Public Governance Agenda** 60 days before each election/appointment cycle.
  3. Track candidate commitments and issue a **Performance Accountability Report** 30 days prior to the next cycle.

> *Design intent*: Channel public sentiment into structured, forward-looking input—not reactive outrage.

---

### 6. EAM Navigator: Interactive Simulation Engine

- **Scope**: Simulates 500 officials across all four tiers + dynamic citizen panel rotation.
- **Tracked Metrics**: Experience accumulation, ambition calibration, voter appeal, peer respect, executive favor.
- **Dashboard Features**:
  - Real-time KPIs: Promotion rate, avg. tenure, attrition
  - Top 8 career trajectories
  - Last 5 election/appointment score breakdowns
  - Full public expenditure ledger (> $10K)
- **Tech Stack**: Client-side only (JavaScript/D3.js); runs in-browser; open-source (MIT License).

---

## Keywords for Discovery  
governance reform, merit-based leadership, transparent government, citizen oversight, public administration, electoral innovation, civic tech, institutional design, anti-corruption, post-electoral democracy
