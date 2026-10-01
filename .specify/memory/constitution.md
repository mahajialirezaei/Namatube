<!--
Sync Impact Report:
- Version change: 1.0.0 -> 1.2.0
- Modified Principles:
  - Added VI. Testing & Continuous Integration (new principle)
  - Added VII. API Contract Documentation (new principle)
  - Added VIII. Infrastructure as Code (new principle)
- Modified Sections:
  - Development Workflow: Enhanced with test-driven quality requirements and CI/CD pipeline mandates
- Summary: Added mandatory testing requirements, API.md contract documentation requirement,
  and Docker containerization with full database stack (PostgreSQL, MongoDB, Redis, RabbitMQ, MinIO).
-->
# Namatube Constitution

## Core Principles

### I. Microservices Architecture
The platform must be structured as loosely coupled microservices (Auth, Video, Interaction, Channel, Admin, Search, Recommendation). All microservices must be containerized (Docker) and communicate through RESTful APIs via an API Gateway (e.g., Nginx, Kong).

### II. Technology Stack Uniformity
The project is a multi-module system incorporating a React frontend and a Django-based backend ecosystem. Data persistence is polyglot, utilizing PostgreSQL for relational data, MongoDB for unstructured metadata/documents, S3-compatible Object Storage (MinIO/AWS S3) for media, and Redis for caching and rapid state retrieval.

### III. Scalability and Performance
The system MUST support high concurrent loads (1000+ concurrent users) maintaining a 99.9% uptime. API response times must be kept strictly under 2 seconds. Video streaming must be adaptive, leveraging a CDN to minimize latency, while intensive asynchronous operations like video transcoding must be decoupled using a Message Queue (RabbitMQ).

### IV. Security-First Approach
All external and internal communications MUST be encrypted using TLS 1.3. User authentication is strictly managed through JWT sessions, with provisions for federated OAuth logins and 2-Factor Authentication. The API Gateway must consistently enforce rate limiting to protect operational integrity.

### V. Observability & Maintainability
To ensure a robust operational lifecycle, every service MUST expose health check endpoints (/health). Logs must be centralized and uniformly formatted in structured JSON. Additionally, API contracts across boundaries must be automatically documented using OpenAPI/Swagger standards.

### VI. Testing & Continuous Integration
Comprehensive automated testing is mandatory for both frontend (NamaFront) and backend (NamaBackend) modules. All code changes MUST include appropriate test coverage (unit, integration, and end-to-end as applicable). A CI/CD pipeline must be configured in GitHub Actions (or equivalent) to automatically run the full test suite on every branch push and pull request, ensuring no untested code reaches production.

### VII. API Contract Documentation
A canonical `API.md` file MUST be maintained at the project root, serving as the single source of truth for all API endpoints connecting the frontend (NamaFront) and backend (NamaBackend). This document must specify request/response schemas, authentication requirements, error codes, and versioning for every exposed endpoint. Both frontend and backend teams must synchronize changes to this contract before implementation.

### VIII. Infrastructure as Code
The entire platform MUST be containerized using Docker, with each microservice having its own `Dockerfile`. A `docker-compose.yml` (or equivalent orchestration configuration) must define the complete local development environment including all required databases (PostgreSQL, MongoDB), caching layer (Redis), message queue (RabbitMQ), and object storage (MinIO). The configuration should mirror production infrastructure and enable one-command local setup.

## Non-Functional & Standard Requirements

- **Cloud-Agnostic Delivery:** Deployments should rely on container orchestration (Kubernetes) to ensure that the platform can scale on any compliant cloud provider without significant architectural rewrites.
- **RESTful Compliance:** Explicit adherence to REST semantics across all exposed HTTP interfaces.
- **S3 Standardized Storage:** Media uploads (videos, thumbnails) must be directed to an S3-compatible API for storage.
- **User Interface Standards:** The UI MUST be fully responsive across mobile and desktop environments, providing comprehensive multilingual support (including Unicode/Persian).

## Development Workflow

- **Modular Development:** Features must be built within their distinct modules. The transition from the existing `NamaFront` prototype to a robust React application should be treated as an isolated UI initiative bounded by agreed API contracts.
- **Test-Driven Quality:** All feature implementations must include automated tests. Frontend tests (NamaFront) should cover component rendering, user interactions, and integration with backend APIs. Backend tests (NamaBackend) must validate service logic, API contracts, and database interactions.
- **CI/CD Pipeline:** GitHub Actions (or equivalent) must be configured to run on all branches. The pipeline must execute linting, unit tests, integration tests, and build verification. Pull requests cannot be merged without passing CI checks.
- **Quality Gates:** Before a deployment goes live, periodic load testing must be successful to validate concurrent streaming and interaction capacities.
- **Code Review:** Peer reviews must rigorously check for standard adherence (e.g., structured logging, TLS boundaries, proper asynchronous dispatching, and test coverage).

## Governance

This Constitution supersedes local service patterns. Introducing new core technologies (databases, brokers) or changing architectural patterns requires a formal amendment process and review.
- Compliance checks against response times and security mandates are strictly enforced as part of routine PR and deployment pipelines.
- As the project grows, major functional changes driven by User Stories dictate the evolution of microservice boundaries.

**Version**: 1.2.0 | **Ratified**: 2026-10-02 | **Last Amended**: 2026-10-02
