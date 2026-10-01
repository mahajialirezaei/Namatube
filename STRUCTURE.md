# Namatube Project Structure

This document outlines the high-level project structure for the Namatube platform.

## Root Directory (`/`)
The root directory serves as the foundation for the entire monorepo/multi-module setup. It contains global configuration files, documentation, and the primary application modules.

- `.claude/` / `.specify/`: Configuration, skills, and memory for the Claude AI agent workflow and constitution governance.
- `docs/`: Project documentation, including functional, non-functional requirements, architecture, and system diagrams.
- `API.md`: **API Contract Document** - The single source of truth for all REST API endpoints connecting NamaFront (React) and NamaBackend (Django). Documents request/response schemas, authentication, error codes, and versioning.
- `docker-compose.yml`: Orchestration file for the complete local development environment (PostgreSQL, MongoDB, Redis, RabbitMQ, MinIO, microservices, API Gateway).
- `Dockerfile` / per-service Dockerfiles: Container definitions for each microservice and component.
- `AGENTS.md`: Rules and constraints for AI agents interacting with the repository.
- `STRUCTURE.md`: This file, detailing the layout of the project.
- `README.md` / `MEMORY.md`: High-level entry point definitions and index files.

## Frontend Module (`/NamaFront`)
The monolithic/modular React application replacing the old prototype.
- **Role:** Handles all user interface, client-side routing, and rendering.
- **Tech Stack:** React (to be structured appropriately).
- **Architecture:** Must integrate with the API Gateway endpoints.

## Backend Module (`/NamaBackend`)
The core backend ecosystem implementing the microservices architecture using Django.
- **Role:** Houses the microservices (Auth, Video, Interaction, Channel, Admin, Search, Recommendation).
- **Tech Stack:** Django (often using Django REST Framework for creating the microservices), interacting with PostgreSQL, MongoDB, MinIO/S3, Redis, and RabbitMQ.
- **Architecture:** 
  - Each microservice should ideally be decoupled, potentially in its own isolated app or sub-directory with independent `Dockerfile`s.
  - Requires integration logic for the API Gateway and Message Queue.
