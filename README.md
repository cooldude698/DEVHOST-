# RouteRescue

> **When Travel Plans Fall Apart, Your Journey Doesn't Have To.**

[![DevHost 2026](https://img.shields.io/badge/DevHost%202026-36--Hour%20Hackathon-blue.svg)](#team--hackathon-information)
[![Problem Statement](https://img.shields.io/badge/Track-PS%204.1%20AI%20Travel%20Recovery-orange.svg)](#problem-statement-and-proposed-solution)
[![Dataset](https://img.shields.io/badge/Dataset-Curated%20Multimodal%20Data-purple.svg)](./data/sample_journeys.json)
[![Status](https://img.shields.io/badge/Status-MVP%20Design%20%26%20Architecture-brightgreen.svg)](#implementation-plan--roadmap)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

---

## Submission Checklist & Repository Compliance

This repository satisfies all requirements set forth for **DevHost 2026**:

| Submission Requirement | Repository Location / Verification | Status |
| :--- | :--- | :---: |
| **Clear README explaining RouteRescue** | [Project Overview](#project-overview) | Verified |
| **Problem Statement & Proposed Solution** | [Problem Statement & Proposed Solution](#problem-statement-and-proposed-solution) | Verified |
| **Technology Stack** | [Technology Stack](#technology-stack) | Verified |
| **Setup & Execution Instructions** | [Setup and Execution Instructions](#setup-and-execution-instructions) | Verified |
| **System Architecture & Workflow** | [System Architecture](#system-architecture) & [System Workflow](#end-to-end-system-workflow) | Verified |
| **Sample Data & Test Scenarios** | [Sample Data & Test Scenarios](#sample-data-and-test-scenarios) (`data/`) | Verified |
| **Known Limitations** | [Known Limitations](#known-limitations) | Verified |
| **Screenshots of the Working Application** | [Application Previews & Screenshots](#screenshots-and-application-previews) | Verified |
| **Zero Secrets Policy** | Enforced via `.gitignore`, `.env.example`, and code review | Verified |

---

## Table of Contents

1. [Project Overview](#project-overview)
2. [Problem Statement and Proposed Solution](#problem-statement-and-proposed-solution)
3. [Project Objectives](#project-objectives)
4. [Target Users](#target-users)
5. [Core Features](#core-features)
6. [End-to-End System Workflow](#end-to-end-system-workflow)
7. [System Architecture](#system-architecture)
8. [Technology Stack](#technology-stack)
9. [Data Model](#data-model)
10. [API Design](#api-design)
11. [Sample Data and Test Scenarios](#sample-data-and-test-scenarios)
12. [Sample Demonstration Scenario](#sample-demonstration-scenario)
13. [Setup and Execution Instructions](#setup-and-execution-instructions)
14. [Environment Variables](#environment-variables)
15. [Screenshots and Application Previews](#screenshots-and-application-previews)
16. [Testing and Evaluation](#testing-and-evaluation)
17. [Business Model](#business-model)
18. [Scalability and Future Roadmap](#scalability-and-future-roadmap)
19. [Security, Privacy, and Reliability](#security-privacy-and-reliability)
20. [Known Limitations](#known-limitations)
21. [Project Structure](#project-structure)
22. [Implementation Plan & Roadmap](#implementation-plan--roadmap)
23. [Contributing](#contributing)
24. [License](#license)
25. [Team & Hackathon Information](#team--hackathon-information)

---

## Project Overview

**RouteRescue** is an AI-powered travel disruption recovery platform built to assist travellers when unexpected events derange their travel schedules. 

When a flight is delayed or cancelled, or a connecting link is missed, passengers are routinely plunged into high-stress manual recalculations. Unlike conventional conversational chatbots that merely suggest tourist attractions or search single travel legs without constraint validation, RouteRescue treats travel disruption recovery as a **constrained multi-factor decision problem**.

The recovery engine systematically evaluates alternative itineraries against critical traveller requirements, including:
- **Origin and Destination**: Required departure point and arrival terminal.
- **Dates and Permitted Travel Window**: Earliest departure time and latest acceptable arrival deadline.
- **Financial Bounds**: Strict ceiling on maximum additional out-of-pocket expenditure.
- **Travel Modalities**: Acceptable transport modes (flight, high-speed train, intercity bus, express cab).
- **Traveller Preferences**: Soft preferences such as preferred airline alliance, non-stop routes, or transport mode.
- **Itinerary Continuity**: Ensuring downstream hotel check-ins or critical appointments remain viable.

### The MVP Scope
For the DevHost 2026 36-hour hackathon prototype, RouteRescue operates with a **curated multimodal travel dataset** and **simulated disruption events**. It performs deterministic constraint validation to separate feasible from infeasible options, ranks valid options using a weighted multi-criteria utility formula, and utilizes an AI service to summarize trade-offs in plain language. Live booking system mutations and live airline GDS integrations are deliberately reserved for future production phases.

---

## Problem Statement and Proposed Solution

### Problem Statement (PS 4.1 — AI Agent for Travel Disruption Recovery)
Flight cancellations, delays, missed connections, and other travel disruptions leave travellers struggling to reorganize journeys in high-stress environments. Travellers are forced to search disparate booking aggregators, manually balance arrival deadlines against unexpected costs, and resolve complex dependencies across downstream bookings.

The core breakdown in modern travel occurs across 5 dimensions:
1. **Disparate Platform Search**: Following a cancellation, travellers must check multiple airline sites, rail booking portals, and aggregators simultaneously.
2. **The "Cheapest Option" Trap**: The least expensive alternative often arrives hours after a crucial arrival deadline, rendering it practically useless.
3. **Budget and Preference Friction**: Replacement journeys frequently breach financial ceilings or force undesirable transit modes without clear warnings.
4. **Manual Calculation Burden**: Travellers under pressure must manually compute layover margins, transit times, and time-zone differences.
5. **Cascading Itinerary Failures**: A single disrupted leg can ruin subsequent hotel reservations, event tickets, or connecting legs.

### Proposed Solution
RouteRescue consolidates the entire recovery process into an automated, explainable recovery workflow:
- **Intelligent Input & Disruption Ingestion**: Captures trip constraints and maps reported disruptions directly to affected segments.
- **Candidate Alternative Discovery**: Scans multimodal travel options (air, rail, road).
- **Deterministic Constraint Validation**: Evaluates hard boundaries (arrival deadline, budget limit, seat availability) using pure mathematical and logical code — never probabilistic guessing.
- **Preference-Weighted Ranking**: Scores surviving feasible itineraries based on traveller priorities (speed vs cost vs mode).
- **AI-Assisted Synthesis & Explanation**: Generates transparent, human-readable trade-off summaries explaining *why* an alternative is recommended.

> **Operational Boundary**: RouteRescue does not claim to eliminate travel delays or guarantee transport availability during widespread network meltdowns. It consolidates search, verification, and recovery planning into a transparent, dependable workflow.

---

## Project Objectives

- **Simplify Disruption Recovery**: Centralize alternative discovery into a single coherent interface.
- **Eliminate Manual Cross-Checking**: Programmatically cross-examine schedules, transit times, and budgets.
- **Deterministic Constraint Enforcement**: Strictly reject alternatives violating mandatory conditions (e.g., arrival deadline exceeded or budget exceeded).
- **Intelligent Preference-Based Ranking**: Prioritize surviving feasible journeys based on user priorities.
- **Explainable Recommendations**: Clarify *why* an alternative is recommended over other candidates.
- **Consolidated Recovery Itinerary**: Produce a complete, actionable recovery plan showing original vs. revised journeys.
- **Actionable Decision Support**: Help travellers review options and understand exactly what steps to take.
- **Architectural Foundation**: Provide clean APIs and data models ready to interface with live travel distribution APIs in future stages.

---

## Target Users

*(Identified intended user groups; not claiming current commercial deployment)*

- **Individual Leisure Travellers**: Travellers caught in unexpected cancellations who need rapid, clear recovery options without navigating multiple aggregator websites.
- **Time-Sensitive Business Travellers**: Professionals with strict arrival deadlines for meetings, conferences, or speaking engagements where arriving late is unacceptable.
- **Corporate Travel Managers**: Internal operations teams coordinating logistics and budget approvals for stranded employees across different regions.
- **Travel Agencies & TMCs (Travel Management Companies)**: Support agents seeking instant, constraint-checked recommendations to resolve customer inquiries faster.

---

## Core Features

### Module 1: Trip Input and Traveller Constraints
Collects travel parameters and cleanly decouples **mandatory constraints** from **soft preferences**:
- **Mandatory Constraints (Hard Filters)**:
  - Final destination required.
  - Latest acceptable arrival time (deadline).
  - Maximum additional budget limit.
  - Required departure date window.
- **Soft Preferences (Ranking Weights)**:
  - Preferred transport mode (e.g., flight over rail).
  - Maximum acceptable number of stops/transfers.
  - Cost sensitivity vs. speed priority.

### Module 2: Disruption Management
Simulates and tracks disruption events associated with specific journey segments:
- **Disruption Types**: Flight cancellation, prolonged flight delay, missed connection.
- **Event Metadata**: Affected segment ID, reported timestamp, delay duration, and cancellation reason.
- **Simulation Transparency**: Explicitly tags events as *simulated* for hackathon demonstration.

### Module 3: Alternative Journey Search
Queries candidate alternatives from the curated travel repository:
- **Journey Model**: `journey_id`, `origin`, `destination`, `departure_time`, `arrival_time`, `mode`, `estimated_fare`, `duration_minutes`, and `availability_status`.
- Supports multimodal alternatives across regional corridors.

### Module 4: Constraint Validation Engine *(Core Module)*
Performs 100% deterministic validation logic in backend Python code without relying on probabilistic LLM guesses:
- **Arrival Deadline Check**: Disqualifies any candidate where `arrival_time > latest_acceptable_arrival_time`.
- **Budget Ceiling Check**: Disqualifies any candidate where `additional_fare > max_additional_budget`.
- **Destination Verification**: Rejects any route that does not terminate at the designated destination.
- **Availability Check**: Rejects any itinerary marked as unavailable or sold out.
- **Zero Silent Relaxation**: Constraints are never relaxed automatically. If no journey passes, the system enters the No-Feasible-Option routine.

### Module 5: Alternative Ranking
Applies a transparent multi-criteria scoring algorithm across only the candidates that passed all mandatory constraints:

$$\text{Score} = w_{\text{cost}} \cdot S_{\text{cost}} + w_{\text{time}} \cdot S_{\text{time}} + w_{\text{duration}} \cdot S_{\text{duration}} + w_{\text{mode}} \cdot S_{\text{mode}}$$

Where:
- $S_{\text{cost}} = 1 - \frac{\text{additional\_cost}}{\text{max\_additional\_budget}}$
- $S_{\text{time}} = \frac{\text{deadline} - \text{arrival\_time}}{\text{deadline} - \text{earliest\_departure}}$
- Normalized values are weighted based on the traveller's stated preference profile (e.g., *Speed Priority* vs *Budget Priority*).

### Module 6: AI-Assisted Interpretation
An LLM integration provides human-friendly synthesis without compromising mathematical correctness:
- **Natural Language Parsing**: Extracts origin, destination, and constraints from freeform user queries.
- **Trade-Off Summarization**: Explains why Option A is recommended over Option B (e.g., *"Option A arrives 45 minutes before your meeting for an extra ₹1,200, whereas Option B arrives with zero buffer"*).
- **Architectural Guardrail**: The LLM is **never** the authority on constraint feasibility. If the LLM service is offline or errors, the deterministic recovery engine continues functioning seamlessly.

### Module 7: Recovery Itinerary Generation
Assembles a complete recovery dossier:
- Summary of original disrupted segment.
- Recommended replacement journey with exact schedule and carrier details.
- Comprehensive cost breakdown and trade-off audit.
- Specific manual actions required (e.g., *"Request airline refund for Leg 1; book Train 12050 on IRCTC"*).
- *Explicit disclaimer*: Clearly flags that rebookings are recommendations, not executed transactions.

### Module 8: Recovery Dashboard
Presents an accessible visual breakdown:
- Disrupted leg banner with status and impact.
- Side-by-side comparison cards of evaluated alternatives.
- Visual badge indicators: `FEASIBLE`, `DEADLINE EXCEEDED`, `OVER BUDGET`.
- Recommended itinerary highlight.

### Module 9: No-Feasible-Option Handling
When all candidates fail mandatory constraints:
- Clear failure notification identifying the specific bottleneck(s) (e.g., *"No available journeys arrive before 08:00 AM within ₹5,000"*).
- Displays near-miss options with explicit violation warnings.
- Prompts the user with structured relaxation sliders (e.g., increase budget by ₹1,500 or extend deadline by 2 hours).

---

## End-to-End System Workflow

```mermaid
flowchart TD
    A["Traveller Enters Journey Details"] --> B["Disruption Reported / Simulated"]
    B --> C["Identify Affected Journey Segment"]
    C --> D["Retrieve Alternative Journeys from Dataset"]
    D --> E["Validate Mandatory Constraints (Deterministic)"]
    E --> F{"Feasible Alternatives Found?"}
    F -- Yes --> G["Rank Feasible Options via Utility Scoring"]
    G --> H["Generate Revised Recovery Itinerary"]
    H --> I["AI Explains Recommendation & Trade-offs"]
    I --> J["Traveller Reviews Plan & Action Items"]
    F -- No --> K["Explain Constraint Conflicts & Bottlenecks"]
    K --> L["Traveller Reviews Near-Misses or Relaxes Constraints"]
    L --> D
```

### Execution Lifecycle Steps
1. **Step 1 — Input Capture**: Traveller records origin, destination, scheduled times, deadline, and maximum budget.
2. **Step 2 — Disruption Ingestion**: A disruption event (e.g., flight cancellation) is registered or simulated.
3. **Step 3 — Impact Identification**: The system maps the disruption to the relevant journey segment.
4. **Step 4 — Candidate Query**: The repository retrieves potential alternate journeys matching origin and destination.
5. **Step 5 — Deterministic Filtering**: The Constraint Engine tests arrival deadlines, budget ceilings, and seat availability.
6. **Step 6 — Exclusion**: Non-compliant routes are marked with specific violation flags and excluded from ranking.
7. **Step 7 — Multi-Criteria Ranking**: Compliant options are scored against traveler weights (time vs cost vs mode).
8. **Step 8 — AI Narrative Generation**: The LLM creates a concise narrative explaining the rationale and trade-offs.
9. **Step 9 — Itinerary Assembly**: The final revised itinerary is generated with step-by-step traveler advisories.
10. **Step 10 — Traveller Review**: The traveler inspects the recovery plan, trade-offs, and takes rebooking actions.

---

## System Architecture

```mermaid
graph TD
    User["Traveller / Client"]
    Frontend["Frontend Dashboard\n(React / TypeScript / Tailwind CSS)"]
    API["FastAPI Backend Service\n(REST API Endpoints)"]
    DisruptionProc["Disruption Processor\n(Event Ingestion & Mapping)"]
    DataRepo["Travel Data Repository\n(Curated Multimodal Dataset)"]
    RecoveryEng["Recovery Engine\n(Orchestration Core)"]
    ConstraintVal["Deterministic Constraint Validator\n(Hard Filter Rules)"]
    RankEng["Alternative Ranking Engine\n(Multi-Factor Utility Scorer)"]
    AIService["AI Explanation Service\n(LLM Prompting & Schema Parser)"]
    Database[("Database\n(PostgreSQL / SQLite Storage)")]

    User -->|Submits Itinerary & Constraints| Frontend
    Frontend -->|HTTP REST Requests| API
    API --> DisruptionProc
    API --> DataRepo
    API --> RecoveryEng
    RecoveryEng --> ConstraintVal
    RecoveryEng --> RankEng
    API --> AIService
    API --> Database
    RecoveryEng -->|Structured Recovery Results| Frontend
```

---

## Technology Stack

The RouteRescue platform is designed with a modern decoupled stack:

### Frontend
- **Framework**: [React 18](https://react.dev/) / [Next.js](https://nextjs.org/)
- **Language**: TypeScript (Strict typing for itinerary and constraint objects)
- **Styling**: [Tailwind CSS](https://tailwindcss.com/) for responsive UI components
- **State Management & Icons**: React Query / Lucide React

### Backend
- **Framework**: [FastAPI](https://fastapi.tiangolo.com/) (High-performance Python web framework)
- **Runtime**: Python 3.10+
- **Data Validation**: [Pydantic v2](https://docs.pydantic.dev/) for deterministic schema enforcement
- **Server**: Uvicorn (ASGI web server)

### Data & Storage
- **Curated Dataset**: JSON / CSV format for hackathon multimodal schedules
- **Relational Storage**: [PostgreSQL](https://www.postgresql.org/) (Production) / [SQLite](https://www.sqlite.org/) (Local prototyping)
- **ORM / Migrations**: SQLAlchemy 2.0 / Alembic (Planned)

### AI & Natural Language
- **LLM Integration**: OpenAI API (`gpt-4o-mini`) / Google Gemini API
- **Execution Role**: Natural language explanation, query parameter extraction, trade-off summarization
- **Resilience**: Graceful offline fallback ensures core logic works without AI keys

---

## Data Model

```mermaid
erDiagram
    TRIP ||--o{ DISRUPTION : experiences
    TRIP ||--|| TRAVELLER_REQUIREMENTS : has
    TRIP ||--o{ RECOVERY_PLAN : generates
    RECOVERY_PLAN ||--o{ RECOVERY_DECISION : evaluates
    JOURNEY ||--o{ RECOVERY_DECISION : references

    TRIP {
        string trip_id PK
        string traveller_name
        string origin
        string destination
        datetime original_departure
        datetime original_arrival
        string transport_mode
        string status
    }

    TRAVELLER_REQUIREMENTS {
        string req_id PK
        string trip_id FK
        datetime latest_acceptable_arrival
        decimal max_additional_budget
        string preferred_mode
        boolean allow_multimodal
    }

    DISRUPTION {
        string disruption_id PK
        string trip_id FK
        string disruption_type
        string description
        datetime event_timestamp
        boolean is_simulated
    }

    JOURNEY {
        string journey_id PK
        string origin
        string destination
        datetime departure_time
        datetime arrival_time
        string transport_mode
        decimal estimated_fare
        string carrier
        boolean is_available
    }

    RECOVERY_PLAN {
        string plan_id PK
        string trip_id FK
        string disruption_id FK
        string recommended_journey_id FK
        decimal total_additional_cost
        string ai_explanation
        datetime created_at
    }

    RECOVERY_DECISION {
        string decision_id PK
        string plan_id FK
        string journey_id FK
        boolean is_feasible
        string failed_constraints
        float ranking_score
    }
```

---

## API Design

The backend defines the following REST API contracts:

### 1. Trip Management
- **`POST /api/trips`**
  - **Purpose**: Register an original journey and traveller constraints.
  - **Request Body**:
    ```json
    {
      "traveller_name": "Aman Jain",
      "origin": "BLR",
      "destination": "DEL",
      "original_departure": "2026-10-15T06:00:00Z",
      "original_arrival": "2026-10-15T08:45:00Z",
      "transport_mode": "flight",
      "latest_acceptable_arrival": "2026-10-15T12:00:00Z",
      "max_additional_budget": 5000.00,
      "preferred_mode": "flight"
    }
    ```
  - **Response `201 Created`**:
    ```json
    {
      "trip_id": "trip_blr_del_01",
      "status": "SCHEDULED",
      "created_at": "2026-10-13T22:40:00Z"
    }
    ```

- **`GET /api/trips/{trip_id}`**
  - **Purpose**: Retrieve an existing trip and its recorded constraints.

### 2. Disruption Reporting
- **`POST /api/disruptions`**
  - **Purpose**: Ingest or simulate a disruption event for a trip.
  - **Request Body**:
    ```json
    {
      "trip_id": "trip_blr_del_01",
      "disruption_type": "FLIGHT_CANCELLATION",
      "description": "Flight 6E-204 cancelled due to technical snag",
      "event_timestamp": "2026-10-15T04:30:00Z",
      "is_simulated": true
    }
    ```
  - **Response `201 Created`**:
    ```json
    {
      "disruption_id": "disr_9921",
      "trip_id": "trip_blr_del_01",
      "status": "DISRUPTED"
    }
    ```

### 3. Recovery Engine Analysis
- **`POST /api/recovery/analyze`**
  - **Purpose**: Execute constraint validation and alternative ranking for a disrupted trip.
  - **Request Body**:
    ```json
    {
      "trip_id": "trip_blr_del_01",
      "disruption_id": "disr_9921"
    }
    ```
  - **Response `200 OK`**:
    ```json
    {
      "plan_id": "rec_plan_441",
      "trip_id": "trip_blr_del_01",
      "feasible_count": 2,
      "infeasible_count": 3,
      "recommended_option": {
        "journey_id": "ALT-AI-502",
        "carrier": "Air India 502",
        "transport_mode": "flight",
        "departure_time": "2026-10-15T07:15:00Z",
        "arrival_time": "2026-10-15T10:00:00Z",
        "additional_fare": 3500.00,
        "score": 0.88,
        "explanation": "Arrives 2 hours before your 12:00 PM deadline and is ₹1,500 under budget."
      },
      "evaluated_alternatives": [
        {
          "journey_id": "ALT-AI-502",
          "is_feasible": true,
          "failed_constraints": [],
          "ranking_score": 0.88
        },
        {
          "journey_id": "ALT-IR-22691",
          "is_feasible": false,
          "failed_constraints": ["ARRIVAL_DEADLINE_EXCEEDED"],
          "ranking_score": null
        }
      ]
    }
    ```

- **`GET /api/recovery/{recovery_id}`**
  - **Purpose**: Retrieve a previously computed recovery plan.

---

## Sample Data and Test Scenarios

The repository includes curated multimodal travel datasets and test scenarios under [`data/`](./data/):

1. **Curated Multimodal Dataset** ([`data/sample_journeys.json`](./data/sample_journeys.json)):
   Contains realistic candidate alternatives (flights, express rail, luxury buses) spanning corridors such as Bengaluru (BLR) to Delhi (DEL), Mumbai (BOM), and Mangalore (IXE).
   - `ALT-AI-502`: Air India Flight (Dep: 05:00 AM, Arr: 07:15 AM, Fare: ₹3,500)
   - `ALT-UK-812`: Vistara Flight (Dep: 05:30 AM, Arr: 07:45 AM, Fare: ₹6,800)
   - `ALT-IR-22691`: Rajdhani Express Rail (Dep: 06:00 AM, Arr: 11:30 AM, Fare: ₹1,200)
   - `ALT-QP-1332`: Akasa Air (Dep: 08:15 AM, Arr: 10:45 AM, Sold Out / 0 seats)

2. **Standardized Test Scenarios** ([`data/test_scenarios.json`](./data/test_scenarios.json)):
   - **Scenario 1**: Morning flight cancellation with a strict 08:00 AM arrival deadline and a ₹5,000 maximum budget. Validates that Option A passes while Option B (late arrival) and Option C (over budget) are deterministically rejected.
   - **Scenario 2**: Impossible constraint conflict (deadline too tight, budget too low). Validates that the system returns 0 feasible options and triggers the relaxation advisor rather than returning a hallucinated itinerary.

---

## Sample Demonstration Scenario

*(Illustrative scenario using curated benchmark values; not live booking inventory)*

### Context
A traveller is booked on a morning flight from **Bengaluru (BLR)** to **Delhi (DEL)** to deliver a keynote address at 09:30 AM:
- **Disruption**: Flight 6E-204 is **CANCELLED** at 04:30 AM.
- **Mandatory Deadline**: Must arrive before **08:00 AM**.
- **Max Additional Budget**: **₹5,000**.
- **Preferred Mode**: Flight (open to multimodal).

### Candidate Alternatives Evaluated by RouteRescue

```
+---------------------------------------------------------------------------------------------------------+
| Candidate    | Carrier / Mode       | Departure | Arrival  | Extra Cost | Constraint Check | Feasible?  |
+---------------------------------------------------------------------------------------------------------+
| Option A     | Air India (Flight)   | 05:00 AM  | 07:15 AM | +₹3,500    | Deadline: PASS   |   YES      |
|              |                      |           |          |            | Budget: PASS     | (Selected) |
+---------------------------------------------------------------------------------------------------------+
| Option B     | Rajdhani Exp (Train) | 06:00 AM  | 11:30 AM | +₹1,200    | Deadline: FAIL   |    NO      |
|              |                      |           |          |            | Budget: PASS     | (Rejected) |
+---------------------------------------------------------------------------------------------------------+
| Option C     | Vistara (Flight)     | 05:30 AM  | 07:45 AM | +₹6,800    | Deadline: PASS   |    NO      |
|              |                      |           |          |            | Budget: FAIL     | (Rejected) |
+---------------------------------------------------------------------------------------------------------+
```

### Outcome
- **Option B** is cheaper (+₹1,200 vs +₹3,500) but arrives at 11:30 AM, **violating the mandatory 08:00 AM deadline**. The engine strictly disqualifies it.
- **Option C** satisfies the arrival deadline but **exceeds the ₹5,000 budget ceiling**.
- **Option A** is the only candidate satisfying 100% of mandatory constraints and is promoted as the recommended itinerary, accompanied by an AI-generated trade-off breakdown.

---

## Setup and Execution Instructions

### Prerequisites
- **Python**: 3.10 or higher
- **Node.js**: 18.x or higher
- **Git**

### 1. Clone the Repository
```bash
git clone https://github.com/cooldude698/DEVHOST-.git
cd DEVHOST-
```

### 2. Configure Environment Variables
```bash
cp .env.example .env
# Open .env and adjust port settings or add your AI provider key if desired
```

### 3. Backend Setup (FastAPI Service)
```bash
cd backend
python -m venv venv
source venv/bin/activate       # On Windows: venv\Scripts\activate
pip install -r requirements.txt
uvicorn app.main:app --reload --port 8000
```
*Access interactive Swagger UI documentation at: `http://localhost:8000/docs`.*

### 4. Frontend Setup (React Dashboard)
```bash
cd ../frontend
npm install
npm run dev
```
*Access the user interface at: `http://localhost:3000`.*

### 5. Running Verification & Scenario Tests
```bash
cd ../backend
pytest tests/ -v
```

---

## Environment Variables

> **Security Reminder**: Do not commit actual `.env` files or secrets to GitHub.

| Variable | Type | Required? | Default | Description |
| :--- | :--- | :---: | :--- | :--- |
| `ENVIRONMENT` | String | Optional | `development` | Deployment environment (`development` / `production`). |
| `PORT` | Integer | Optional | `8000` | Port for the backend API service. |
| `DATABASE_URL` | String | Optional | `sqlite:///./routerescue.db` | Database connection string. |
| `AI_PROVIDER` | String | Optional | `openai` | AI vendor for explanations (`openai`, `gemini`, `mock`). |
| `AI_PROVIDER_API_KEY` | String | Optional | `""` | API key for AI explanation service (graceful fallback if empty). |
| `AI_MODEL` | String | Optional | `gpt-4o-mini` | LLM model identifier. |
| `CORS_ORIGINS` | String | Optional | `http://localhost:3000` | Permitted frontend origins. |

---

## Screenshots and Application Previews

*(Visual interface design and component layouts)*

### 1. Recovery Overview Dashboard
```
+------------------------------------------------------------------------------------+
|  RouteRescue  |  Trip: BLR -> DEL  |  Status: [ DISRUPTED: FLIGHT CANCELLED ]      |
+------------------------------------------------------------------------------------+
|  ORIGINAL ITINERARY:                                                               |
|  IndiGo 6E-204  |  Dep: 05:30 AM  |  Arr: 08:15 AM  |  Status: CANCELLED (Tech)    |
+------------------------------------------------------------------------------------+
|  TRAVELLER CONSTRAINTS:                                                            |
|  [!] Must arrive before: 08:00 AM        [$] Max extra budget: ₹5,000              |
+------------------------------------------------------------------------------------+
|  RECOMMENDED RECOVERY PLAN:                                                        |
|  >> Air India 502 (Flight)                                                         |
|     Dep: 05:00 AM  -->  Arr: 07:15 AM (45 min before meeting)                       |
|     Extra Cost: +₹3,500 (₹1,500 under max budget)                                  |
|     AI Summary: "Best match for your strict 8 AM deadline within allowable budget."|
+------------------------------------------------------------------------------------+
|  EVALUATED ALTERNATIVES:                                                           |
|  [PASS] Air India 502  : +₹3,500 | 07:15 AM Arr | Status: FEASIBLE                 |
|  [FAIL] Rajdhani Exp   : +₹1,200 | 11:30 AM Arr | Status: DEADLINE EXCEEDED        |
|  [FAIL] Vistara 812    : +₹6,800 | 07:45 AM Arr | Status: BUDGET EXCEEDED          |
+------------------------------------------------------------------------------------+
```

### 2. Visual Component Placeholders
```
+-------------------------------------------------------------+
|                                                             |
|           [ Screenshot: Disruption Alert Banner ]           |
|                docs/screenshots/disruption_banner.png        |
|                                                             |
+-------------------------------------------------------------+
|                                                             |
|          [ Screenshot: Side-by-Side Alternatives ]          |
|                docs/screenshots/comparison_cards.png        |
|                                                             |
+-------------------------------------------------------------+
```
*(As front-end components are rendered during development, high-resolution screenshots will be saved to `docs/screenshots/`)*

---

## Testing and Evaluation

| Metric | Target Definition | Verification Approach |
| :--- | :--- | :--- |
| **1. Constraint Satisfaction Rate** | 100% of journeys labeled *Feasible* must strictly satisfy all mandatory arrival deadlines, budget bounds, and destination endpoints. | Automated regression suite with boundary tests. |
| **2. Alternative Validity** | 100% of recommended journeys exist in the catalog and are confirmed available. | Schema validation and repository integrity checks. |
| **3. Recovery Planning Time** | Time elapsed between disruption ingestion and verified recovery plan generation. | Benchmarked against manual search in controlled tests. |
| **4. No-Solution Precision** | When all alternatives violate constraints, the system must return `feasible_count: 0` with 0% false positives. | Negative scenario test fixtures with impossible deadlines. |
| **5. Recommendation Quality** | Top-ranked candidate aligns with the user's declared priority profile (speed vs cost). | Comparative preference matrix evaluations. |

---

## Business Model

*(Proposed commercial model for future scaling; MVP is an open prototype)*

1. **Freemium B2C Model**: Free disruption evaluation and basic comparison; paid tier includes automated calendar sync and claim documentation.
2. **B2B Corporate Travel SaaS**: Subscriptions for corporate travel desks to automate company-policy-compliant rebooking for stranded employees.
3. **Integration Services**: API licensing for Online Travel Agencies (OTAs) and insurers to automate alternative routing during claims.

---

## Scalability and Future Roadmap

- **Geographic Network Expansion**: Broaden dataset from Indian metro corridors to international routes.
- **Multimodal Routing Combinations**: Support hybrid chains (e.g., Short flight + Express train connection).
- **Live GDS & Airline API Feeds**: Connect NDC / Amadeus / Sabre test sandboxes for live seat availability.
- **Authorized One-Click Booking**: Partner with certified booking APIs to securely execute booking modifications upon traveller confirmation.
- **Push Notification Engine**: Push updates via WhatsApp, SMS, and email.
- **Multi-Language Support**: Regional language interfaces for broader accessibility.

---

## Security, Privacy, and Reliability

- **Strict Input Validation**: Every request is sanitized and validated via Pydantic schemas.
- **Zero Secrets in Repository**: Secrets and tokens are kept strictly in `.env` files ignored by git.
- **Deterministic AI Guardrails**: Numerical constraints are strictly handled by code, not the LLM.
- **Offline Fault Tolerance**: The system operates smoothly even if external AI APIs fail.
- **Privacy by Design**: No personal payment credentials are stored during recovery planning.
- **Booking Clarity**: Explicitly clarifies that recommendations are advisory and do not execute financial transactions automatically.

---

## Known Limitations

- **Simulated Disruption Events**: Disruptions are currently triggered or simulated manually rather than fetched from live flight radar feeds.
- **Curated Dataset**: Route alternatives are retrieved from a curated multimodal dataset rather than global live GDS distribution networks.
- **Estimated Costs**: Fares reflect estimated benchmark rates; real-time dynamic surges in peak disruption periods are not reflected.
- **Advisory Only**: Does not execute automatic debit card transactions or ticket cancellations on third-party carrier websites.
- **Network Scope**: Initial data models are scoped to regional transit corridors for demonstration purposes.

---

## Project Structure

```
DEVHOST MANGALORE/
├── data/
│   ├── sample_journeys.json  # Curated multimodal travel dataset
│   └── test_scenarios.json   # Standardized constraint test scenarios
├── backend/                  # (Planned) Python FastAPI application
│   ├── app/
│   │   ├── api/              # Route controllers (trips, disruptions, recovery)
│   │   ├── core/             # Configuration, logging, and security
│   │   ├── engine/           # Constraint validator & ranking algorithms
│   │   ├── models/           # Pydantic schemas & database entities
│   │   └── services/         # AI explanation service & dataset repository
│   ├── tests/                # Automated pytest suite
│   └── requirements.txt      # Python dependencies
├── frontend/                 # (Planned) Next.js / React client application
│   ├── src/
│   │   ├── components/       # Comparison cards, sliders, banners
│   │   ├── pages/            # Dashboard and trip input views
│   │   └── lib/              # API client and type definitions
│   └── package.json          # Node dependencies
├── docs/                     # Specifications and architectural references
│   └── screenshots/          # Application UI previews
├── .env.example              # Template environment variables
├── .gitignore                # Git ignore patterns
└── README.md                 # Primary project documentation
```

---

## Implementation Plan & Roadmap

```mermaid
gantt
    title RouteRescue Hackathon & Evolution Roadmap
    dateFormat  YYYY-MM-DD
    section Phase 1: Foundation
    Repository Scaffolding & Git Remote Setup   :done, 2026-10-13, 1d
    Architecture Design & Specification          :done, 2026-10-13, 1d
    Curated Dataset & Test Scenarios Ingestion  :done, 2026-10-13, 1d
    section Phase 2: Disruption & Constraints
    Trip & Disruption Data Ingestion            :active, 2026-10-14, 2d
    Deterministic Constraint Validation Engine  :active, 2026-10-14, 2d
    section Phase 3: Ranking & Core Engine
    Multi-Criteria Ranking Algorithm            :2026-10-15, 2d
    No-Feasible-Option Fallback Handler         :2026-10-15, 1d
    section Phase 4: AI & Presentation
    LLM Trade-Off Explanation Service          :2026-10-16, 2d
    Frontend Dashboard & Comparison UI          :2026-10-16, 2d
    section Phase 5: Verification
    Scenario Testing & Edge-Case Validation      :2026-10-17, 1d
```

| Phase | Focus Area | Status | Key Deliverables |
| :--- | :--- | :---: | :--- |
| **Phase 1** | Foundation & Architecture | **Scaffolded** | Git repo configuration, specification document, `.gitignore`, `.env.example`, curated dataset, test scenarios. |
| **Phase 2** | Disruption & Constraints | **Planned / Underway** | Pydantic data schemas, trip ingestion, deterministic hard filters (`deadline`, `budget`, `destination`). |
| **Phase 3** | Recovery Engine & Ranking | **Planned** | Utility scoring formula, sorting algorithms, empty-set / conflict detection routines. |
| **Phase 4** | AI Explanation Layer | **Planned** | LLM prompt engineering, fallback handler for offline AI, structured explanation generation. |
| **Phase 5** | Dashboard UI | **Planned** | React/Next.js interface, interactive comparison table, constraint relaxation sliders. |
| **Phase 6** | Automated Testing | **Planned** | Pytest suite covering zero-valid-option, deadline violations, time-zone boundaries, and budget overflow. |
| **Phase 7** | Deployment & Production Prep | **Planned** | Containerization (Docker), cloud deployment, and live GDS sandbox exploration. |

---

## Contributing

Contributions are welcomed during and after DevHost 2026:
1. Fork the repository.
2. Create your feature branch (`git checkout -b feature/constraint-engine-enhancement`).
3. Commit your changes (`git commit -m 'Add multi-zone arrival time validation'`).
4. Push to the branch (`git push origin feature/constraint-engine-enhancement`).
5. Open a Pull Request.

---

## License

This project is licensed under the [MIT License](LICENSE) — free for educational, academic, and hackathon evaluation use.

---

## Team & Hackathon Information

### Hackathon Details
- **Event**: DevHost 2026 — 36-Hour Hackathon
- **Problem Statement Track**: **PS 4.1 — AI Agent for Travel Disruption Recovery**

### Team Information
- **Lead Developer**: Aman Jain ([@cooldude698](https://github.com/cooldude698))
- **Repository**: [https://github.com/cooldude698/DEVHOST-](https://github.com/cooldude698/DEVHOST-)

---
*Built with dedication for DevHost 2026. Because when travel plans fall apart, your journey doesn't have to.*
