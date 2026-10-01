# Agent Implementation Guidelines & Rules

All autonomous agents and AI assistants MUST read and adhere to these guidelines before beginning any implementation tasks on the Namatube project.

## 1. Required Reading Context
Before implementing a feature, refactoring, or modifying the architecture, you MUST parse and understand the constraints from the following files:
- `API.md` (API contract between frontend and backend)
- `docs/System-Architecture-Document.md`
- `docs/Functional.md`
- `docs/Non-Functional.md`
- `STRUCTURE.md`
- `.specify/memory/constitution.md` (for governance, standards, and tech stack uniformity)
- `docker-compose.yml` (infrastructure and database configuration)

## 2. Core Architectural Constraints
- **API Contract First:** All frontend-backend communication must strictly follow the specifications in `API.md`. Any deviation requires updating the contract document first and obtaining approval.
- **Microservices Constraint:** Features belonging to the backend (`/NamaBackend`) must be implemented as distinct, loosely coupled Django services (Auth, Video, Interaction, Channel, Admin, Search, Recommendation). Do NOT entangle concerns.
- **Frontend Refactor:** The frontend (`/NamaFront`) is transitioning from a prototype to a fully-developed React application. Ensure the UI code is strictly separated from backend logic and relies on REST API calls.
- **Polyglot Persistence:** Do not force all data into SQL. Respect the data layer rules: PostgreSQL for relational data, MongoDB for unstructured (comments, metadata), Object Storage (S3/MinIO) for media, and Redis for caching.
- **Asynchronous Operations:** Heavy tasks (e.g., Video Transcoding via FFmpeg) MUST NOT block API responses. Offload them to a Message Queue (RabbitMQ).
- **Containerization:** All services, databases, and infrastructure components must be defined in Docker containers. Use `docker-compose.yml` for local development orchestration.

## 3. Communication & Code Standards
- **RESTful APIs:** All communication flows through the API Gateway, and all endpoints must strictly follow RESTful design and use JSON.
- **Security First:** Endpoints must validate JWT tokens (or OAuth credentials).
- **Testing Requirements:** Every feature implementation MUST include automated tests. Frontend (NamaFront): component tests, integration tests with API mocks. Backend (NamaBackend): unit tests for service logic, integration tests for API endpoints and database interactions.
- **CI/CD Compliance:** All branches are subject to automated CI/CD checks via GitHub Actions. Code that does not pass linting, testing, or build verification cannot be merged.
- **Code Style:** Comply with standard React and Django stylistic guidelines. Code must be heavily documented, and APIs need OpenAPI/Swagger annotations.

## 4. Work Execution 
- **Isolated Modules:** Execute tasks bounded to the module they belong to (`NamaFront/` vs `NamaBackend/`). 
- **Check-ins:** If an implementation necessitates an architectural change or introduces a new dependency (e.g., adding a new database engine), PAUSE and consult the user, as this violates the project `.specify/memory/constitution.md`.
