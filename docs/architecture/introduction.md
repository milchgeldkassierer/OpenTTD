# Introduction

This document outlines the overall project architecture for Ultimate OpenTTD AI, including backend systems, shared services, and non-UI specific concerns. Its primary goal is to serve as the guiding architectural blueprint for AI-driven development, ensuring consistency and adherence to chosen patterns and technologies.

**Relationship to Frontend Architecture:**
This project operates as an autonomous AI system within OpenTTD with minimal direct user interface requirements. However, development tools, performance monitoring dashboards, and analysis interfaces may require frontend components that will be detailed in a separate Frontend Architecture Document if needed.

## Starter Template or Existing Project

The PRD indicates this is a greenfield OpenTTD AI project with an embedded Squirrel script architecture. The system operates within the existing OpenTTD game engine using:
- **Squirrel 2.2.5 VM** as the runtime environment
- **OpenTTD Script API** for game integration
- **Monorepo structure** containing AI source code, documentation, testing tools, and analysis frameworks

No external starter templates are mentioned, but the project leverages the OpenTTD AI development framework as its foundation. The architecture must work within OpenTTD's constraints:
- 128MB memory limit
- 10,000 operations per execution cycle
- Event-driven execution model
- Embedded script environment

## Change Log

| Date | Version | Description | Author |
|------|---------|-------------|--------|
| 2025-08-20 | 1.0 | Initial architecture document for Ultimate OpenTTD AI | Winston (Architect) |

---
