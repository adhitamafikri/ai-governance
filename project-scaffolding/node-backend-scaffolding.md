# Node Backend Scaffolding
This is the guide for AI Agent to execute project scaffolding creation. Adhere to these rules to produce a well-architected Node JS + Typescript backend project structure that provides great DX, highly maintainable and scalable for 2026 onwards.

## Project Architecture
The architecture of the project should adhere to the *Domain Driven Design*, *Modular Monolith*, and *Clean Code* principles. Providing robust, highly maintainable, testable, and scalable backend sytem.

## Primary Tech Stacks
- **node v24 LTS**: runtime
- **npm**: package manager
- **Typescript**: static typing
- **Express**: backend framework
- **zod**: validation library. Validating Request schemas and Response schemas
- **drizzle**: handles database connection and operation to any SQL databases
- **mongodb**: handles connection and operation to mongodb
- **node-redis**: handles connection and operation to redis
- **bullmq**: handles background jobs with redis as driver
- **socketio**: handles real-time connection and communication using WebSocket
- **jsonwebtoken**: JWT Auth

### Testing Stacks
- **vitest**: unit testing tool
- **supertest**: http assertition testing tool (integration testing)
- **testcontainers**: testing with real databases and services in Docker containers (integration testing)
- **faker-js**: realistic test data generator
- **playwright**: e2e testing tool

#### Testing Directory Structure
- *Unit Tests* should be colocated with their respective files. Making it easier for us to navigate and to ensure that all of our files have their unit test file.
    - Unit test files should have name with the format of `file-name.spec.ts`
- Make sure we have `tests/` directory on the root of our project to contain our *E2E Tests*, *Test Helpers*, and *Test Factories*. Here are the sub-directories of the `tests/`
    - **e2e/**: Contains all of our e2e test cases. E2E test files should have name with the format of `file-name.spec.ts`
    - **helpers/**: Contains reusable test helper functions that can be used across the app
    - **factories/**: Contains factory functions that can be used to generate proper fake testing data

### Plumbing Stacks
- **prettier@^3.8.0**: code formatter
- **eslint^8.50.0**: code quality checker
- **eslint-config-prettier@latest**: disables conflicting formatting rules with Prettier
- **eslint-plugin-prettier@latest**: ESLint to report formatting issues
- **@typescript-eslint/parser@^7.0.0 + @typescript-eslint/eslint-plugin@^7.0.0**: Typescript
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
