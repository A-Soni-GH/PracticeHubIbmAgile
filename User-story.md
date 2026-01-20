# GitHub Issues — Product Catalog Backlog
Each entry below is a ready-to-paste issue body. Use the title line as the GitHub issue title and paste the rest into the issue body. Labels and estimate are provided on each item.

---

### PBI-101 — Product data model and DB schema
Labels: backend, db, high-priority
Estimate: 3 points
Priority: High

Description:
As a backend developer, I need a well-designed product data model and database schema so that the application can reliably store and manage product information.

Acceptance Criteria:
- Schema includes: id (UUID), name, sku, description, price (decimal), currency, categories (array), images (array of URLs), stock (int), active (bool), created_at, updated_at.
- Migration script(s) are included and run locally.
- Local dev seed data with 10 example products provided.

Tasks:
- Design schema document
- Write DB migration(s)
- Add seed script
- Add unit tests for DB migrations

---

### PBI-102 — Create Product API (POST /products)
Labels: backend, api, high-priority
Estimate: 3 points
Priority: High

Description:
As an API consumer, I need an endpoint to create new products so that I can add new items to the product catalog programmatically.

Acceptance Criteria:
- POST /products accepts JSON and validates required fields.
- Returns 201 with created resource including id.
- Invalid input returns 400 with clear validation messages.
- Unit tests for happy and failure paths included.
- OpenAPI spec updated.

Tasks:
- Route/controller
- Service & persistence
- Validation
- Unit tests
- OpenAPI spec

---

### PBI-103 — Retrieve Product API (GET /products/{id})
Labels: backend, api, high-priority
Estimate: 2 points
Priority: High

Description:
As an API consumer, I need an endpoint to retrieve a specific product by ID so that I can fetch detailed product information.

Acceptance Criteria:
- GET /products/{id} returns 200 + product JSON when found.
- Returns 404 if not found.
- Response includes likes_count.
- Unit tests included.

Tasks:
- Controller and service
- DTO/serializers
- Tests
- API docs

---

### PBI-104 — Update Product API (PUT/PATCH /products/{id})
Labels: backend, api, high-priority
Estimate: 3 points
Priority: High

Description:
As an API consumer, I need an endpoint to update product information so that I can modify existing product details when needed.

Acceptance Criteria:
- PUT/PATCH updates allowed fields and returns 200 with updated resource.
- Protects immutable fields.
- Invalid updates return 400.
- Unit tests and docs updated.

Tasks:
- Implement update logic
- Validation rules
- Tests
- Docs

---

### PBI-105 — Delete Product API (DELETE /products/{id})
Labels: backend, api, high-priority
Estimate: 2 points
Priority: High

Description:
As an API consumer, I need an endpoint to delete products so that I can remove items from the catalog while maintaining data integrity through soft-delete behavior.

Acceptance Criteria:
- DELETE sets soft-delete flag and returns 204.
- Soft-deleted products do not appear in GET /products lists.
- Tests included.

Tasks:
- Add soft-delete field & logic
- Update queries to exclude deleted products
- Tests

---

### PBI-201 — Likes model and DB table
Labels: backend, db, medium-priority
Estimate: 2 points
Priority: Medium

Description:
As a backend developer, I need a likes table and database migration so that the system can track user likes on products.

Acceptance Criteria:
- Table columns: id, product_id (FK), user_id, created_at.
- Unique constraint on (product_id, user_id).
- Migration added and tested.

Tasks:
- Migration
- DB constraints
- Tests

---

### PBI-202 — Like/Unlike endpoints (POST/DELETE /products/{id}/like)
Labels: backend, api, auth, medium-priority
Estimate: 3 points
Priority: Medium

Description:
As an authenticated user, I need endpoints to like and unlike products so that I can express my preferences and engagement with products in the catalog.

Acceptance Criteria:
- POST /products/{id}/like creates a like if none exists.
- DELETE /products/{id}/like removes the like.
- Duplicate likes prevented.
- Likes count updates and reflected in GET endpoints.
- Integration tests included.

Tasks:
- Endpoints & service
- Auth check
- Tests

---

### PBI-203 — Expose likes count in product retrievals
Labels: backend, api, medium-priority
Estimate: 1 point
Priority: Medium

Description:
As an API consumer, I need the likes count included in product responses so that I can display engagement metrics to users.

Acceptance Criteria:
- likes_count present in product DTOs.
- Unit/integration tests added.

Tasks:
- DTO updates
- Tests

---

### PBI-301 — List products with pagination, sorting and filtering
Labels: backend, api, high-priority
Estimate: 5 points
Priority: High

Description:
As an API consumer, I need to list products with pagination, sorting, and filtering capabilities so that users can efficiently browse and discover products.

Acceptance Criteria:
- Supports page/limit (or cursor), sorting by name/price/created_at.
- Filter by category, price range, availability.
- Response includes metadata (total, page, per_page).
- Tests included.

Tasks:
- Query implementation
- Optimize for DB indexes
- Tests & docs

---

### PBI-302 — Basic text search (name/description)
Labels: backend, api, medium-priority
Estimate: 3 points
Priority: Medium

Description:
As an API consumer, I need a text search capability so that users can find products by searching product names and descriptions.

Acceptance Criteria:
- GET /products?q=term searches name and description.
- Reasonable relevance ordering.
- Tests included.

Tasks:
- Implement full-text or LIKE search
- Tests

---

### PBI-401 — Logging & structured logs
Labels: observability, medium-priority
Estimate: 2 points
Priority: Medium

Description:
As a DevOps/SRE engineer, I need structured JSON logging with correlation and trace IDs so that I can effectively monitor and debug application issues in production.

Acceptance Criteria:
- Logs emitted in JSON, include timestamp, level, message, trace_id, request_id.
- Errors include stack trace when appropriate.
- Tests or examples documented.

Tasks:
- Configure logger
- Add middleware to populate trace IDs

---

### PBI-402 — Metrics (Prometheus) + Health endpoint
Labels: observability, medium-priority
Estimate: 3 points
Priority: Medium

Description:
As a DevOps/SRE engineer, I need metrics and health check endpoints so that I can monitor application performance and availability in production.

Acceptance Criteria:
- /health returns liveness & readiness.
- /metrics exports basic counters and histograms for requests, latencies.
- Docs show how to scrape.

Tasks:
- Add metrics library integration
- Health handlers
- Tests

---

### PBI-501 — Auth integration (JWT) for protected endpoints
Labels: security, backend, high-priority
Estimate: 3 points
Priority: High

Description:
As a security-conscious developer, I need JWT-based authentication for state-changing endpoints so that only authorized users can modify product data.

Acceptance Criteria:
- State-changing endpoints require valid JWT.
- Public read endpoints remain readable without auth.
- Tests for auth behavior.

Tasks:
- Auth middleware
- Token validation (public keys / secret)
- Tests

---

### PBI-502 — Input validation + rate limiting
Labels: security, backend, medium-priority
Estimate: 2 points
Priority: Medium

Description:
As a security-conscious developer, I need input validation and rate limiting so that the API is protected against malformed requests and abuse.

Acceptance Criteria:
- All inputs validated with clear messages.
- Rate limiting enforced (configurable).
- Tests/examples included.

Tasks:
- Integrate validation library
- Add rate limiter middleware
- Tests

---

### PBI-601 — Dockerize service
Labels: infra, devops, high-priority
Estimate: 2 points
Priority: High

Description:
As a developer, I need Docker support with Dockerfile and docker-compose so that I can run the service locally in a consistent environment.

Acceptance Criteria:
- Dockerfile builds image reproducibly.
- docker-compose config for local DB + app.
- README instructions included.

Tasks:
- Create Dockerfile
- Create docker-compose
- Document local run steps

---

### PBI-602 — CI pipeline (unit tests, build, lint)
Labels: ci, devops, high-priority
Estimate: 3 points
Priority: High

Description:
As a development team, I need a CI pipeline to run tests and linting so that code quality is maintained and issues are caught early.

Acceptance Criteria:
- Workflow triggers on PRs.
- Lint and tests must pass for merge.
- Workflow file present in repo.

Tasks:
- Add .github/workflows/ci.yml
- Add status checks

---

### PBI-603 — CD to staging (automated deployment)
Labels: ci, devops, high-priority
Estimate: 5 points
Priority: High

Description:
As a deployment engineer, I need automated deployment to staging so that changes are continuously delivered and tested in a production-like environment.

Acceptance Criteria:
- Merge to develop triggers build and deploy to staging.
- Deploy manifests/helm chart available.
- Rollback documented.

Tasks:
- Build & push image in CI
- Add deployment step (kubectl/helm)
- Test deploy

---

### PBI-604 — Infrastructure as code for staging (Terraform/Helm)
Labels: infra, devops, high-priority
Estimate: 5 points
Priority: High

Description:
As an infrastructure engineer, I need infrastructure-as-code using Terraform and Helm so that the staging environment can be provisioned reproducibly.

Acceptance Criteria:
- Terraform/Helm manifests manage DB and app resources.
- Secrets stored in a secrets manager (instructions provided).
- Deploy reproducible staging environment.

Tasks:
- Terraform module for DB
- Helm chart for app
- Docs for secrets & env

---

### PBI-701 — Integration tests for CRUD flows
Labels: tests, qa, high-priority
Estimate: 5 points
Priority: High

Description:
As a QA engineer, I need comprehensive integration tests for CRUD operations so that the application functionality is verified end-to-end.

Acceptance Criteria:
- Integration tests for create/retrieve/update/delete and likes.
- CI runs the integration suite for nightly or PR gating.
- Tests stable & reproducible.

Tasks:
- Write integration tests
- Configure CI to run integration tests (ephemeral DB)

---

### PBI-702 — Load test plan for read endpoints (1000 RPS target)
Labels: perf, qa, medium-priority
Estimate: 5 points
Priority: Medium

Description:
As a performance engineer, I need load testing for read endpoints so that I can ensure the system meets performance targets and identify scaling needs.

Acceptance Criteria:
- Load test plan and script (k6 or JMeter) included.
- Run shows p95 latency and error rates; report with scaling recommendations.
- Document suggested autoscaling thresholds.

Tasks:
- Create load test scripts
- Run in staging and capture metrics
- Produce report

---

### PBI-801 — OpenAPI spec & API docs
Labels: docs, high-priority
Estimate: 2 points
Priority: High

Description:
As an API consumer, I need comprehensive OpenAPI documentation so that I can understand and integrate with all available endpoints.

Acceptance Criteria:
- OpenAPI spec generated.
- /docs served in staging.
- Examples for main endpoints included.

Tasks:
- Add OpenAPI annotations
- Host swagger UI

---

### PBI-802 — README and runbook for devs + deploy steps
Labels: docs, high-priority
Estimate: 1 point
Priority: High

Description:
As a developer or operator, I need clear documentation with setup and deployment instructions so that I can quickly get started and deploy the application reliably.

Acceptance Criteria:
- README includes build/test/run instructions.
- Runbook describes deploy steps, rollbacks, and who to contact.

Tasks:
- Author README
- Author deploy runbook

---

(End of issues list)