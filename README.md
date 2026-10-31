

<div align="center">

# 🌿 Mission City Chakra Map


**A collaborative map of zero-waste restaurants, schools, grocery stores and recycling initiatives across Pune**

<br/>



<br/>

[![Status](https://img.shields.io/badge/Status-Live-059669?style=for-the-badge&logo=statuspage&logoColor=white)](#)

[![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=for-the-badge&logo=html5&logoColor=white)](#)
[![CSS3](https://img.shields.io/badge/CSS3-1572B6?style=for-the-badge&logo=css3&logoColor=white)](#)
[![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black)](#)
[![Node.js](https://img.shields.io/badge/Node.js-339933?style=for-the-badge&logo=node.js&logoColor=white)](#)
[![Express.js](https://img.shields.io/badge/Express.js-000000?style=for-the-badge&logo=express&logoColor=white)](#)
[![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169E1?style=for-the-badge&logo=postgresql&logoColor=white)](#)
[![Google Sheets](https://img.shields.io/badge/Google_Sheets-34A853?style=for-the-badge&logo=googlesheets&logoColor=white)](#)
[![Google Forms](https://img.shields.io/badge/Google_Forms-7248B9?style=for-the-badge&logo=googleforms&logoColor=white)](#)
[![Google OAuth 2.0](https://img.shields.io/badge/Google_OAuth_2.0-4285F4?style=for-the-badge&logo=google&logoColor=white)](#)
[![Vercel](https://img.shields.io/badge/Vercel-000000?style=for-the-badge&logo=vercel&logoColor=white)](#)
[![Render](https://img.shields.io/badge/Render-46E3B7?style=for-the-badge&logo=render&logoColor=black)](#)

<br/>

[![View Live Site](https://img.shields.io/badge/View_Live_Site-Visit_Map-059669?style=for-the-badge&logo=globe&logoColor=white)](https://missioncitychakra.com/wp-content/uploads/map-project/navbar.html)

<br/>

> **Notice**: Source code is private. Architecture and design are documented below.

</div>

---

##  Overview

Mission City Chakra Map is an interactive, crowdsourced web application created to locate and celebrate sustainable, zero-waste initiatives across Pune. Designed for both everyday residents and local contributors, it surfaces a verified directory of restaurants, schools, grocery outlets, and recycling centers. By coupling public submissions with an authenticated administrative moderation barrier, the project promotes responsible living while safeguarding data integrity.

| Dimension | Specification |
| :--- | :--- |
| **Type** | Web Application (Public Interactive Map & Moderation Console) |
| **Status** | Live |
| **Role** | Dipesh Karalkar, Soham Pawar |
| **Duration** | 2025 / 2026 |
| **Stack Summary** | HTML5, CSS3, JavaScript, Node.js, Express.js, PostgreSQL, Google Workspace, Vercel, Render |

---

##  Features

| Marker | Feature | Description |
| :---: | :--- | :--- |
|  | **Community Submissions** | Users click "Add Place" and submit a location through a Google Form. |
|  | **Categorised Map Layers** | Places grouped by type (restaurants, schools, grocery stores, recycling initiatives). |
|  | **Search Filters** | Users can search and filter places on the map. |
|  | **Ratings** | Places can be rated. |
|  | **Admin Moderation Workflow** | Admins sign in with Google OAuth 2.0, review each submission, approve valid entries and reject spam or invalid ones. |
|  | **Verified-Only Public Data** | Only approved entries appear on the live map. |

### Feature Visuals

####  Community Submissions
![Community Submissions](assets/community-submissions.png)
*Figure 1: Community crowdsourcing entry point routing users to the structured Google Form intake.*

####  Categorised Map Layers
![Categorised Map Layers](assets/categorised-map-layers.png)
*Figure 2: Categorical map visualization organizing zero-waste restaurants, schools, grocers, and recycling centers.*

####  Search Filters
![Search Filters](assets/search-filters.png)
*Figure 3: Interactive filtering interface enabling location discovery by category and keyword search.*

####  Ratings
![Ratings](assets/ratings.png)
*Figure 4: Community rating display allowing users to evaluate and recognize sustainable establishments.*

####  Admin Moderation Workflow
![Admin Moderation Workflow](assets/admin-moderation-workflow.png)
*Figure 5: Protected administrative dashboard with Google OAuth 2.0 authentication and review actions.*

####  Verified-Only Public Data
![Verified Public Data](assets/verified-public-data.png)
*Figure 6: Public map rendering exclusively sanitised and verified production datasets.*

---

##  Architecture

The Mission City Chakra platform is engineered as an air-gapped, two-tier system: a public-facing read map hosted on Vercel and an authenticated moderation backend hosted on Render, bridged by Google Forms and Google Sheets.

![Architecture](assets/architecture.png)
*Figure 7: Master system architecture diagram exported from the technical design documentation.*

### a) System Context Diagram

```mermaid
flowchart TD
    classDef actor fill:#E0F2FE,stroke:#0284C7,stroke-width:2px,color:#0F172A;
    classDef core fill:#ECFDF5,stroke:#059669,stroke-width:2px,color:#064E3B;
    classDef external fill:#F8FAFC,stroke:#94A3B8,stroke-width:2px,color:#334155;

    subgraph Users[" Stakeholders & Users "]
        Citizen["Public Visitor<br/>(Pune Citizen)"]:::actor
        Contributor["Community Contributor<br/>(Submits Places)"]:::actor
        Admin["Platform Administrator<br/>(Moderator)"]:::actor
    end

    subgraph MCCSystem[" Mission City Chakra Map System "]
        PublicApp["Public Map Platform<br/>(Static Client & Read API)"]:::core
        AdminApp["Admin Moderation Console<br/>(Express.js & Session Store)"]:::core
    end

    subgraph ThirdParty[" External Managed Services "]
        GoogleIntake["Google Workspace<br/>(Google Forms & Sheets)"]:::external
        GoogleAuth["Google Identity<br/>(OAuth 2.0 Service)"]:::external
    end

    Citizen -->|"Explores sustainable places"| PublicApp
    Contributor -->|"Navigates to 'Add Place'"| PublicApp
    PublicApp -.->|"Redirects for intake"| GoogleIntake
    Contributor -->|"Submits new location"| GoogleIntake

    Admin -->|"Authenticates (OAuth)"| GoogleAuth
    GoogleAuth -->|"Validates identity"| AdminApp
    Admin -->|"Reviews pending records"| AdminApp
    AdminApp -->|"Fetches raw / Writes verified"| GoogleIntake

    PublicApp -->|"Fetches verified records"| GoogleIntake
```
*System Context Diagram: Interactions between public visitors, contributors, moderators, and cloud services.*

### b) High-Level Architecture Diagram

```mermaid
flowchart TD
    classDef client fill:#E0F2FE,stroke:#0284C7,stroke-width:2px,color:#0F172A;
    classDef hosting fill:#ECFDF5,stroke:#059669,stroke-width:2px,color:#064E3B;
    classDef backend fill:#FEF3C7,stroke:#D97706,stroke-width:2px,color:#78350F;
    classDef data fill:#F3E8FF,stroke:#7C3AED,stroke-width:2px,color:#4C1D95;
    classDef service fill:#F1F5F9,stroke:#64748B,stroke-width:2px,color:#1E293B;

    subgraph Clients[" Client Presentation Layer "]
        Browser["Public Web Browser<br/>(Desktop / Mobile)"]:::client
        AdminBrowser["Admin Web Browser"]:::client
    end

    subgraph VercelEdge[" Edge & Map Hosting (Vercel Hobby Tier) "]
        StaticUI["MCC Map Frontend<br/>(HTML5 / CSS3 / JavaScript)"]:::hosting
        MapAPI["Map Data API<br/>(Data Delivery Gateway)"]:::hosting
    end

    subgraph RenderPlatform[" Admin Control Plane (Render Free Tier) "]
        AdminServer["Admin Backend<br/>(Node.js / Express.js)"]:::backend
        PGStore[("Session Store<br/>(PostgreSQL)")]:::backend
    end

    subgraph GoogleData[" Storage & Intake Pipeline (Google Workspace) "]
        GForm["Google Forms Intake"]:::service
        ResponsesSheet[("Google Sheets<br/>'Responses' (Unverified)")]:::data
        VerifiedSheet[("Google Sheets<br/>'Verified Entries' (Production)")]:::data
    end

    subgraph IdentityService[" Identity Provider "]
        OAuthProvider["Google OAuth 2.0"]:::service
    end

    Browser -->|"Requests page & interactions"| StaticUI
    StaticUI -->|"Queries verified coordinates"| MapAPI
    MapAPI -->|"Serves verified records"| VerifiedSheet

    Browser -.->|"Redirects to submit"| GForm
    GForm -->|"Auto-appends submission"| ResponsesSheet

    AdminBrowser -->|"Admin sign-in"| OAuthProvider
    OAuthProvider -->|"Grants tokens"| AdminServer
    AdminServer <-->|"Maintains 60-min sessions"| PGStore

    AdminBrowser -->|"Moderation actions"| AdminServer
    AdminServer -->|"Pulls pending entries"| ResponsesSheet
    AdminServer -->|"Commits approved entries"| VerifiedSheet
```
*High-Level Architecture Diagram: Layered decomposition of clients, Vercel edge delivery, Render backend, and Google data pipelines.*

### c) Request Lifecycle Sequence Diagram

```mermaid
sequenceDiagram
    autonumber
    actor Contributor as Contributor
    actor Admin as Administrator
    participant Map as MCC Map Frontend
    participant GForm as Google Forms
    participant SheetRaw as "Sheet (Responses)"
    participant AdminAPI as Admin Backend (Render)
    participant OAuth as Google OAuth 2.0
    participant PG as PostgreSQL
    participant SheetVer as "Sheet (Verified Entries)"
    participant MapAPI as Map Data API (Vercel)
    actor Visitor as Public Visitor

    Note over Contributor,SheetRaw: Phase 1: Community Submission Pipeline
    Contributor->>Map: Click "Add Place"
    Map-->>Contributor: Redirect to Google Form
    Contributor->>GForm: Enter place name, category, location & details
    GForm->>SheetRaw: Store entry automatically as unverified (hidden from public)

    Note over Admin,SheetVer: Phase 2: Administrative Moderation Workflow
    Admin->>AdminAPI: Access Admin Moderation Console
    AdminAPI->>OAuth: Initiate Google OAuth 2.0 login
    OAuth-->>AdminAPI: Authenticate & issue credentials
    AdminAPI->>PG: Store session & authentication tokens (60-min validity)
    AdminAPI->>SheetRaw: Query unverified submissions
    SheetRaw-->>AdminAPI: Return pending candidate locations
    Admin->>AdminAPI: Review submission details
    alt Valid Submission Approved
        AdminAPI->>SheetVer: Append approved record to "Verified Entries"
    else Spam or Invalid Submission
        AdminAPI->>SheetRaw: Mark as rejected / Exclude
    end

    Note over Visitor,SheetVer: Phase 3: Verified Map Delivery
    Visitor->>Map: Open MCC Sustainability Map
    Map->>MapAPI: Fetch verified map markers
    MapAPI->>SheetVer: Query trusted "Verified Entries"
    SheetVer-->>MapAPI: Deliver verified locations
    MapAPI-->>Map: Deliver sanitized JSON data
    Map-->>Visitor: Render markers, categorized layers & ratings
```
*Request Lifecycle Sequence Diagram: Step-by-step path from contributor submission through OAuth moderation to public map rendering.*

### d) Data Model / ER Diagram

```mermaid
erDiagram
    POSTGRESQL_SESSION {
        string session_id PK
        string admin_id
        string token_hash
        timestamp expires_at "60-minute duration"
        timestamp created_at
    }

    GOOGLE_SHEET_RESPONSES {
        string response_id PK "Generated row ID"
        string place_name
        string category "Restaurant, School, Grocery, Recycling"
        string location_address
        string coordinates
        string status "Unverified, Rejected, Approved"
        timestamp submission_timestamp
    }

    GOOGLE_SHEET_VERIFIED {
        string verified_id PK
        string place_name
        string category
        string location_address
        string coordinates
        float rating "Place rating"
        timestamp verified_at
        string verified_by "Admin reference"
    }

    POSTGRESQL_SESSION ||--o{ GOOGLE_SHEET_VERIFIED : "moderates and transfers"
    GOOGLE_SHEET_RESPONSES ||--o{ GOOGLE_SHEET_VERIFIED : "promoted on approval"
```
*Data Model Diagram: Relational mapping between PostgreSQL session tokens, unverified Google Sheet submissions, and production verified records.*

### e) Deployment and Infrastructure Flow Diagram

```mermaid
flowchart LR
    classDef edge fill:#ECFDF5,stroke:#059669,stroke-width:2px,color:#064E3B;
    classDef server fill:#EFF6FF,stroke:#2563EB,stroke-width:2px,color:#1E3A8A;
    classDef google fill:#F5F3FF,stroke:#7C3AED,stroke-width:2px,color:#4C1D95;

    subgraph VercelTier[" Vercel Hosting (Hobby Tier) "]
        VercelCDN["Global CDN Edge"]:::edge
        PublicMapApp["MCC Map Frontend<br/>(HTML5 / CSS3 / JS)"]:::edge
        DataAPIEdge["Map Data API Route"]:::edge
    end

    subgraph RenderTier[" Render Hosting (Free Tier) "]
        AdminBackend["Admin Service Container<br/>(Node.js / Express.js)"]:::server
        PostgresInstance[("Managed PostgreSQL<br/>(Session Database)")]:::server
    end

    subgraph GoogleCloud[" Google Cloud Platform "]
        FormsSvc["Google Forms Service"]:::google
        RawSheet[("Google Sheets<br/>'Responses'")]:::google
        LiveSheet[("Google Sheets<br/>'Verified Entries'")]:::google
    end

    PublicMapApp -->|"Fetches data"| DataAPIEdge
    DataAPIEdge -->|"Reads verified dataset"| LiveSheet
    FormsSvc -->|"Appends rows"| RawSheet

    AdminBackend -->|"Validates & stores sessions"| PostgresInstance
    AdminBackend -->|"Reads pending entries"| RawSheet
    AdminBackend -->|"Promotes approved entries"| LiveSheet
```
*Deployment Topology Diagram: Distribution of services across Vercel edge delivery, Render container hosting, and Google Cloud services.*

### f) User Journey Flowchart

```mermaid
flowchart TD
    classDef start fill:#E0F2FE,stroke:#0284C7,stroke-width:2px,color:#0C4A6E;
    classDef action fill:#F0FDF4,stroke:#16A34A,stroke-width:2px,color:#14532D;
    classDef decision fill:#FEF3C7,stroke:#D97706,stroke-width:2px,color:#78350F;
    classDef finish fill:#F1F5F9,stroke:#64748B,stroke-width:2px,color:#1E293B;

    Start(["Citizen loads MCC Map"]):::start --> Browse["Explore Map Layers<br/>(Restaurants, Schools, Grocers, Recycling)"]:::action
    Browse --> Search["Filter by Keyword or Category"]:::action
    Search --> FoundCheck{"Location exists on map?"}:::decision

    FoundCheck -->|"Yes"| InspectPlace["View Place Details & Rating"]:::action
    InspectPlace --> RatePlace["Submit Place Rating"]:::action
    RatePlace --> EndExplore(["Discovery Session Complete"]):::finish

    FoundCheck -->|"No (New sustainable place)"| ClickAdd["Click 'Add Place' Button"]:::action
    ClickAdd --> RedirectForm["Redirected to Google Form"]:::action
    RedirectForm --> FillForm["Submit Place Details & Coordinates"]:::action
    FillForm --> SaveRaw["Stored in 'Responses' Sheet (Unverified)"]:::action
    SaveRaw --> AdminReview["Admin reviews in Moderation Console"]:::action

    AdminReview --> ValidCheck{"Valid sustainable spot?"}:::decision
    ValidCheck -->|"Spam / Invalid"| RejectAction(["Submission Rejected & Discarded"]):::finish
    ValidCheck -->|"Verified"| ApproveAction["Moved to 'Verified Entries' Sheet"]:::action
    ApproveAction --> PublishedLive(["Marker Published to Live Map"]):::finish
```
*User Journey Flowchart: Paths for viewers exploring verified places and contributors submitting new initiatives for admin review.*

---

##  Tech Stack

| Layer | Technology | Purpose | Badge |
| :--- | :--- | :--- | :--- |
| **Frontend Structure** | HTML5 | Page structure of the MCC map | [![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=flat-square&logo=html5&logoColor=white)](#) |
| **Frontend Styling** | CSS3 | Styling and responsive layout | [![CSS3](https://img.shields.io/badge/CSS3-1572B6?style=flat-square&logo=css3&logoColor=white)](#) |
| **Frontend Logic** | JavaScript | Map interaction and frontend logic | [![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=flat-square&logo=javascript&logoColor=black)](#) |
| **Map Library** | OpenStreetMap | Map tiles | [![OpenStreetMap](https://img.shields.io/badge/OpenStreetMap-green)](#) |
| **Backend Runtime** | Node.js | Backend runtime environment for the admin console | [![Node.js](https://img.shields.io/badge/Node.js-339933?style=flat-square&logo=node.js&logoColor=white)](#) |
| **API Framework** | Express.js | Server-side APIs and admin moderation workflows | [![Express.js](https://img.shields.io/badge/Express.js-000000?style=flat-square&logo=express&logoColor=white)](#) |
| **Session Database** | PostgreSQL | Secure storage of authentication sessions and tokens | [![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169E1?style=flat-square&logo=postgresql&logoColor=white)](#) |
| **Submission Form** | Google Forms | Collects location details from users | [![Google Forms](https://img.shields.io/badge/Google_Forms-7248B9?style=flat-square&logo=googleforms&logoColor=white)](#) |
| **Data Store** | Google Sheets | "Responses" holds unverified data; "Verified Entries" holds production data | [![Google Sheets](https://img.shields.io/badge/Google_Sheets-34A853?style=flat-square&logo=googlesheets&logoColor=white)](#) |
| **Authentication** | Google OAuth 2.0 | Admin login; secure sign-in with sessions valid for 60 minutes | [![Google OAuth 2.0](https://img.shields.io/badge/Google_OAuth_2.0-4285F4?style=flat-square&logo=google&logoColor=white)](#) |
| **Data Delivery API** | Map data API | Serves verified entries from "Verified Entries" sheet to live map | [![API](https://img.shields.io/badge/Map_Data_API-Data_Delivery-059669?style=flat-square)](#) |
| **Frontend/API Host** | Vercel (Hobby tier) | Hosts the map data API and the live map | [![Vercel](https://img.shields.io/badge/Vercel-000000?style=flat-square&logo=vercel&logoColor=white)](#) |
| **Backend/DB Host** | Render (free tier) | Hosts the admin backend and the PostgreSQL database | [![Render](https://img.shields.io/badge/Render-46E3B7?style=flat-square&logo=render&logoColor=black)](#) |

### Why These Choices

The system prioritises rapid community intake and operational simplicity over monolithic complexity. By pairing Google Forms and Google Sheets as a headless ingestion layer, crowdsourced entries are collected with zero upfront form development and zero hosting costs. Splitting hosting between Vercel (static map client and read API edge) and Render (stateful Node.js admin runtime and PostgreSQL) separates public read traffic from administrative write workloads. Google OAuth 2.0 paired with PostgreSQL token persistence enforces centralized admin identity without requiring the risk or maintenance of custom password authentication.

---

##  Key Engineering Decisions

<details>
<summary><strong>Decision 1: Google Forms & Sheets as a Headless Crowdsourcing Pipeline</strong></summary>

- **Problem**: Needed a reliable, frictionless data submission pipeline for community members without spending cycles developing custom authenticated form pages, input sanitation logic, and storage schemas.
- **Options Considered**: Building a custom in-app submission form connected to an API endpoint vs. delegating ingestion to Google Forms linked to Google Sheets.
- **Decision**: Adopted Google Forms for submission intake, writing incoming submissions into a raw "Responses" Google Sheet.
- **Result**: Immediate zero-maintenance submission interface with zero database write load on the public map infrastructure.
</details>

<details>
<summary><strong>Decision 2: Two-Sheet Isolation for Moderation Integrity</strong></summary>

- **Problem**: Direct-to-production crowdsourcing invites spam, offensive content, and inaccurate map markers that degrade platform trustworthiness.
- **Options Considered**: Immediate public publishing with post-hoc community reporting vs. strict two-tier data segregation with mandatory admin sign-off.
- **Decision**: Implemented a two-sheet data boundary where unverified submissions remain isolated in "Responses", and only reviewed and approved records are moved into "Verified Entries".
- **Result**: The public map API queries only "Verified Entries", guaranteeing 100% human-verified live data and complete isolation from unverified entries.
</details>

<details>
<summary><strong>Decision 3: Delegated Google OAuth 2.0 Authentication with PostgreSQL Session Storage</strong></summary>

- **Problem**: Ensuring secure access to the admin moderation backend without storing or managing administrator passwords and credentials.
- **Options Considered**: Custom credential authentication (username/password with bcrypt and JWT) vs. federated Google OAuth 2.0 with a persistent session store.
- **Decision**: Integrated Google OAuth 2.0 for administrative authentication, issuing 60-minute time-boxed sessions stored and validated inside PostgreSQL.
- **Result**: Zero credential liability, strict time-limited administrative sessions, and seamless revocation workflows.
</details>

<details>
<summary><strong>Decision 4: Multi-Cloud Tiered Free-Tier Architecture (Vercel + Render)</strong></summary>

- **Problem**: Deploying both a high-availability public map and a stateful administrative control plane within zero operational infrastructure budgets.
- **Options Considered**: Running all workloads on a single free virtual machine vs. decoupling static public delivery (Vercel) from stateful moderation services (Render).
- **Decision**: Deployed the public map frontend and read API on Vercel (Hobby tier), while placing the Node.js/Express.js admin backend and PostgreSQL database on Render (free tier).
- **Result**: Fast, globally cached edge delivery for public viewers, alongside dedicated containerized execution for admin moderation, accepting backend cold starts as a calculated trade-off.
</details>

---

##  Security and Performance

### Authentication & Authorization
Administrative operations are guarded by Google OAuth 2.0. Sessions and auth tokens are persisted in PostgreSQL with an enforced **60-minute time-to-live (TTL)**. Unauthorized requests to moderation endpoints are rejected at the Express.js middleware boundary.

### Data Protection & Boundary Isolation
The public map has no read or write access to unverified submissions. The submission pipeline enforces an air gap: user inputs are captured via Google Forms into the "Responses" sheet and remain quarantined until an administrator validates the record and manually commits it to the "Verified Entries" sheet.

### Caching, Edge Delivery & Optimization
The public map interface and the read-only Map Data API reside on Vercel's global edge network, minimizing latency for Pune residents querying map pins and categorical layers.

### Scaling & Infrastructure Trade-offs
The infrastructure operates on free tiers (Vercel Hobby and Render Free tier). Under this architecture:
- Public map viewing remains consistently responsive via Vercel edge delivery.
- The Render administrative backend experiences occasional container spin-down after periods of inactivity, resulting in a brief cold start upon initial admin login.

| Metric | Target / Observed |
| :--- | :--- |
| **Admin Session Validity** | 60 minutes |


---


### Operational Trade-off: Free-Tier Cold Starts
A known operational trade-off of the Render free-tier environment is container idling. After periods of inactivity, the admin service spins down, resulting in a cold start latency when an administrator initially accesses the moderation dashboard. Because moderation is an asynchronous internal task rather than a user-blocking flow, this latency was accepted to keep running costs at zero while maintaining full database-backed session security.

---

##  Roadmap

- [x] Public MCC map interface with responsive HTML5, CSS3, and JavaScript
- [x] Categorised map layers for restaurants, schools, grocers, and recycling centers
- [x] Search and filtering interface for Pune locations
- [x] Community ratings system for sustainable establishments
- [x] "Add Place" community crowdsourcing workflow via Google Forms
- [x] Dual-dataset pipeline isolating unverified "Responses" from "Verified Entries"
- [x] Node.js & Express.js moderation backend on Render
- [x] Google OAuth 2.0 authentication for administrators
- [x] PostgreSQL session and token store with 60-minute automated expiry
- [x] Public Map Data API deployment on Vercel

---

##  Access and Contact

### Code Access
> **Code Access Policy**: The source code for Mission City Chakra Map is maintained in a private repository to protect administrative workflow logic and backend infrastructure configurations. Full code walkthroughs or temporary repository access can be provided upon request for technical interviews, recruiters, and engineering reviews.

### Engineering Team

[![Dipesh Karalkar](https://img.shields.io/badge/Dipesh_Karalkar-Developer-059669?style=for-the-badge&logo=github&logoColor=white)](—)
[![Soham Pawar](https://img.shields.io/badge/Soham_Pawar-Developer-10B981?style=for-the-badge&logo=github&logoColor=white)](—)

| Contact Channel | Dipesh Karalkar | Soham Pawar |
| :--- | :--- | :--- |
| **LinkedIn** | https://www.linkedin.com/in/dipesh-karalkar-2552b5341/ | https://www.linkedin.com/in/soham-pawar-99717b346/ |
| **Email** | atharvkaralkar07@gmail.com | sohampawar261933@gmail.com |

---

##  Missing Info to Complete This README

The following items were provided as dashes (`—`) and require population when details become available:

1. **Live Site URL**: Direct link to the public production website.
2. **Project Duration**: Specific build duration / calendar months in 2026.
3. **Frontend Map Library**: Library used for map rendering (e.g., Leaflet.js, Mapbox GL JS, Google Maps API, or OpenLayers).
4. **CI/CD / DevOps**: Build scripts, continuous integration tools, or automated deployment triggers.
5. **Monitoring & Analytics**: Telemetry or visitor tracking tools (e.g., Google Analytics, Vercel Analytics, UptimeRobot).
6. **Other Developer Tools**: Linter, formatter, or package managers utilized.
7. **Biggest Technical Challenge**: Specific architectural challenge, implementation solution, and takeaway.
8. **Performance Metrics**: Concrete benchmarks for page load time, monthly active contributors, and uptime.
9. **Future Roadmap Items**: Specific upcoming milestones or planned roadmap features.
10. **Contact Links**: LinkedIn profiles, portfolio URLs, and direct contact email addresses for both Dipesh Karalkar and Soham Pawar.
