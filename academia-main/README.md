# Academia

This repository contains the source code for the Academia project — a small platform composed of an Angular frontend, a Spring Boot backend, Keycloak configuration and themes, and supporting assets (uploads). This README provides a quick overview and developer instructions to run the system locally.

## Repository layout

- `academia-front/` — Angular frontend application (TypeScript, TailwindCSS).
- `academia.network/` — Spring Boot backend (Java, Maven).
- `keycloak/` — Keycloak realm export and custom theme(s).
- `uploads/` — directory used by the backend to store uploaded files (static content).
- `docker-compose.yml` — convenience compose file to run services (DB, Keycloak, backend, frontend as configured).

## Quick start (prerequisites)

Install these before running locally:

- Node.js (16+ recommended) and npm or yarn
- Java 11+ (or the JDK version required by the backend)
- Maven (optional; the repo includes the Maven wrapper `mvnw`/`mvnw.cmd`)
- Docker & Docker Compose (optional — to run everything via containers)

Notes for Windows users: PowerShell is the default shell used in examples.

## Run the frontend (development)

1. Open a terminal and go to the frontend folder:

```powershell
cd academia-front
```

2. Install dependencies and start the dev server:

```powershell
npm install
npm run start
```

This will run the Angular development server (typically at http://localhost:4200). See `academia-front/README.md` for any additional frontend-specific notes.

## Run the backend (development)

1. Open a terminal and go to the backend folder:

```powershell
cd academia.network
```

2. Use the Maven wrapper to run the application:

```powershell
# Windows
.\mvnw.cmd spring-boot:run

# macOS / Linux
./mvnw spring-boot:run
```

The application reads configuration from `src/main/resources/application.yml` and environment-specific files such as `application-dev.yml`. Adjust the active profile as needed.

## Run with Docker Compose

This repository provides `docker-compose.yml` to simplify running the stack (useful for local testing). From the repository root run:

```powershell
docker-compose up --build
```

This will start configured services (database, Keycloak, backend, etc.) depending on the compose file. Inspect `docker-compose.yml` to see what will be started and how ports are mapped.

## Keycloak

The `keycloak/realm/academia-realm.json` file contains a realm export you can import into a local Keycloak instance. Custom themes are in `keycloak/themes/` (for the login and account UI). When running Keycloak via Docker, mount the `keycloak/` directory into the container so Keycloak can load the realm and theme.

## Configuration

- Backend application configuration: `academia.network/src/main/resources/application.yml` and `application-dev.yml` (already included in `target/` for convenience in some builds).
- Frontend API configuration: `academia-front/src/app/services/api-configuration.ts` and environment files under `academia-front/src/environments/`.

Make sure the frontend's API base URL matches the running backend's address and Keycloak settings.

## Uploads & static files

Uploaded files and static content are stored under the `uploads/` directory (or `academia.network/target/static/uploads/` during build/run). Ensure this directory is writable by the backend process when running locally.

## Tests

- Frontend unit tests: from `academia-front` run `npm test`.
- Backend tests: from `academia.network` run `./mvnw test` (or `mvnw.cmd` on Windows).

## Developer notes

- If you change Keycloak realm or theme files, re-import or restart Keycloak to pick up changes.
- The project uses a Maven wrapper so you don't need a system Maven installed; on Windows use `mvnw.cmd` and on Unix-like systems use `./mvnw`.
- The Angular project includes Tailwind; rebuild the frontend if you change styles.

## Next steps / suggestions

- Add module-level README files: `academia-front/README.md`, `academia.network/README.md`, and `keycloak/README.md` with component-specific instructions and env vars.
- Add a simple Makefile or PowerShell script for common local commands (start/stop, build, test).
- Add CI configuration to run tests and builds automatically.

## License & contacts

Specify the project license here (if any). For questions, contact the maintainers or open an issue in the repository.

---

Generated README added to help new contributors and developers run the system locally.
