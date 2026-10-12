# HouseHunt Backend
Spring Boot REST backend for the HouseHunt rental management capstone.

Live website: https://househunt-production-6767.up.railway.app
Live Swagger: https://househunt-production-6767.up.railway.app/swagger-ui/index.html
Frontend code: https://github.com/Spoorthy2815/househunt-frontend

## Technologies
Java 21, Spring Boot, MVC, Spring Security, JWT, BCrypt, JPA/Hibernate, Jakarta Validation, MySQL, H2, caching, asynchronous processing, Actuator, Springdoc OpenAPI, JUnit, Mockito and MockMvc.

## Run locally
Requires Java 21 and Maven 3.9+.
mvn spring-boot:run

Default local profile uses persistent H2 under data/ and optional demonstration seeding.
API: http://localhost:8080/api
Health: http://localhost:8080/actuator/health
Swagger: http://localhost:8080/swagger-ui/index.html
Run the separate React frontend on http://localhost:5173 for the UI.

## MySQL
Configure process environment variables:
SPRING_PROFILES_ACTIVE=mysql
DB_URL=jdbc:mysql://localhost:3306/househunt
DB_USER=[application database user]
DB_PASSWORD=[set privately]
JWT_SECRET=[set privately; at least 32 characters]
CORS_ORIGIN=http://localhost:5173
SEED_DEMO=false

Create the database and grant the application user privileges first. Spring Boot does not automatically load .env files.
On a new deployment, an administrator can be provisioned using BOOTSTRAP_ADMIN_EMAIL and BOOTSTRAP_ADMIN_PASSWORD environment secrets. Remove them after initial provisioning. Do not enable known demonstration accounts on public deployments.

## Features
Registration/login, property CRUD/search, ownership checks, administrator moderation, booking approval/cancellation with overlap prevention, profiles, favorites and stored assistant history.
Mappings include one-to-one, one-to-many, many-to-one and many-to-many.
Only USER and ADMIN are account roles; property ownership controls owner actions.

## Assistant
LLM_API_KEY enables OpenAI-compatible responses. LLM_API_URL and LLM_MODEL are configurable.
Without a key, the assistant uses database retrieval with local feature-hashing embeddings and cosine similarity. Keys remain on the backend.

## Tests and build
mvn test
mvn package

The optional web Maven profile is for the original combined layout with ../frontend/dist and is not needed for this standalone API.
The Dockerfile builds the API jar; supply the mysql profile and database/secrets variables at runtime.

The existing live deployment remains connected to https://github.com/Spoorthy2815/househunt-capstone. This separate repository is for coursework review and independent development; pushing here does not update the live app automatically.
Never commit real credentials, tokens, database files or .env files.