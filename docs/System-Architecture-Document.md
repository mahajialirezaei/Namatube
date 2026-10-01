# Namatube System Architecture Document

This document outlines the architecture, components, deployment, and data flow of the Namatube video sharing platform.

## API Contract Documentation
All API endpoints connecting the frontend (NamaFront) and backend (NamaBackend) are documented in the root-level `API.md` file. This serves as the single source of truth for:
- Request/response schemas for all endpoints
- Authentication and authorization requirements
- Error codes and handling
- API versioning strategy

Both frontend and backend implementations must adhere strictly to the contracts defined in `API.md`.

## Containerization & Local Development
The entire platform is containerized using Docker:
- Each microservice has its own `Dockerfile`
- A `docker-compose.yml` at the root orchestrates the full local development stack including:
  - PostgreSQL (relational database)
  - MongoDB (NoSQL database for metadata/comments)
  - Redis (caching layer)
  - RabbitMQ (message queue)
  - MinIO (S3-compatible object storage)
  - All microservices (Auth, Video, Interaction, Channel, Admin, Search, Recommendation)
  - API Gateway (Nginx/Kong)

Developers can spin up the entire environment with a single command.

## 1. Architecture Diagram
Namatube is designed as a **Microservices** platform.
- **Core Services:** Auth, Video, Interaction, Channel, Admin/Network, Search, Recommendation.
- **Gateway:** All services are containerized (Docker) and exposed to the client (Browser/Mobile) via an **API Gateway** (e.g., Nginx, Kong).
- **Communication:** Services communicate asynchronously for heavy tasks like video processing using a **Message Queue** (RabbitMQ) or synchronously via REST APIs (JSON format).
- **Data Layers:**
  - **SQL Database (PostgreSQL):** For relational entities like users and subscriptions.
  - **NoSQL Database (MongoDB):** For unstructured data like video metadata, comments, and transactions.
  - **Object Storage (S3 / MinIO):** For media files (video files, thumbnails).
  - **Redis Cache:** For fast retrieval tasks.
- **Delivery:** A CDN is used alongside a Load Balancer for global, fast video streaming.

## 2. Component Diagram
Each microservice functions independently with specific internal components:
- **Auth Service:** Authentication, 2FA Handler, OAuth Client (Federated login via Google/GitHub), JWT Token Manager.
- **Video Service:** Upload API, Video Processor (FFmpeg transcoding, thumbnail extraction), Streaming Controller (CDN manager), Metadata Store.
- **Interaction Service:** Like/Dislike Manager, Comment CRUD, Subscribe/Unsubscribe Manager.
- **Channel Service:** Channel Profile, Playlist Manager, Video Lister.
- **Admin/Network Service:** User Management, Report Generator, Network Simulator (NAT/DHCP/Subnet simulation).

## 3. Deployment Diagram
- **Containerization:** The project is fully containerized (Docker).
- **Orchestration:** **Kubernetes** is used to coordinate the pods (Auth Service Pod, Video Service Pod, etc.). The setup includes Master and Worker nodes.
- **Ingress:** A Kubernetes Ingress Controller functions as the entry point and Load Balancer.
- **Persistence & External Services:** Persistent Volumes are used for storage. The CDN and Object Storage are leveraged outside the primary cluster to serve heavy streaming traffic globally.

## 4. Data Flow Diagram (DFD)
- **Level 0 (Context Diagram):** External entities interacting with the platform include "Viewer" (searches, watches, comments), "Content Creator" (uploads, manages channel), and "Administrator" (manages reports, networks).
- **Level 1 (Detailed Data Flow):** 
  - User flows authenticate to User Management -> backed by SQL (D1).
  - Upload flows through Video Management -> saves metadata to NoSQL (D2) and media to Object Storage (D3).
  - Interactions (likes, views) flow through Interaction Management -> backed by Redis Cache (D4) and NoSQL.
  - Logs are piped to a dedicated Logs and Reports Storage (D5).
