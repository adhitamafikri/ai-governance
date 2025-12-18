# Bun Backend Scaffolding
This is the guide for AI Agent to execute project scaffolding creation. Adhere to these rules to produce a well-architected Bun + Typescript + Elysia backend project structure that provides great DX, highly maintainable and scalable for 2026 onwards.

## Project Architecture
The architecture of the project should adhere to the *Domain Driven Design*, *Modular Monolith*, and *Clean Code* principles. Providing robust, highly maintainable, testable, and scalable backend sytem.

## Primary Tech Stacks
- **bun v1.2.23** as runtime and package manager
- **Typescript**: static typing
- **Elysia**: backend framework
- **zod**: validation library. Validating Request schemas and Response schemas
- **drizzle**: handles database connection and operation to any SQL databases
- **mongodb**: handles connection and operation to mongodb
- **node-redis**: handles connection and operation to redis
- **bullmq**: handles background jobs with redis as driver
- **socketio**: handles real-time connection and communication using WebSocket
- **jsonwebtoken**: JWT Auth

### Testing Stacks
- **bun**: built in unit testing tool from bun itself
- **Elysia .handle()**: built in method to test handlers directly without HTTP overhead
- **testcontainers**: testing with real databases and services in Docker containers (integration testing)
- **faker-js**: realistic test data generator
- **playwright**: e2e testing tool

### Plumbing Stacks
- **biomejs**: code formatter and quality checker
- **prototools**: The toolchain for controlling the tool or runtime version that should be used in the project. Read [https://moonrepo.dev/proto](https://moonrepo.dev/proto). Tools or runtime version can be defined in a `.prototools` file

### Build and Deployment
- **Dockerfile**: Dockerfile for production build
- **Dockerfile.dev**: Dockerfile for local development (must support hot reloading)
- **docker-compose.yml**: Simplifies service orchestration for local development process
- **Makefile**: Make commands that simplifies working with Docker and docker compose

### Managing Module Imports
- Prefer import aliasing over relative import style.
    - Use `@` symbol to alias the `src`
    - Example: prefer `@/modules/user/application/infrastructure/database/schema`, instead of `../../modules/user/application/infrastructure/database/schema`