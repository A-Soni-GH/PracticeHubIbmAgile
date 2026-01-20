# GitHub Issues — Product Catalog Backlog
Each entry below is a ready-to-paste issue body. Use the title line as the GitHub issue title and paste the rest into the issue body. Labels and estimate are provided on each item.

---

### PBI-101 — Product data model and DB schema
Labels: backend, db, high-priority
Estimate: 3 points
Priority: High

Description:
Design and implement the product data model and database schema.

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
Implement endpoint to create a new product.

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
Implement endpoint to fetch a single product by id.

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
Implement update endpoint for products.

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
Implement soft-delete behavior for products.

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
Create likes table and migration.

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
Allow authenticated users to like/unlike products.

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
Include likes_count in GET /products and GET /products/{id} responses.

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
Implement GET /products with pagination, sorting and filters.

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
Implement q= query param for basic product text search.

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
Add structured JSON logging with correlation/trace IDs.

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
Expose /metrics and /health endpoints.

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
Add JWT-based authentication for state-changing endpoints.

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
Add payload validation and basic rate limiting for public endpoints.

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
Provide Dockerfile and docker-compose for local development.

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
Create GitHub Actions workflow to run lint, unit tests, and build.

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
Automate deployment to a staging cluster on merge to develop/main.

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
Provision staging infra reproducibly (DB, k8s objects, secrets).

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
Add integration tests that run against an ephemeral DB (Testcontainers or similar).

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
Design and run load tests for read endpoints and report results.

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
Provide OpenAPI/Swagger documentation for all endpoints.

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
Create README with local dev steps and a deploy runbook for staging/prod.

Acceptance Criteria:
- README includes build/test/run instructions.
- Runbook describes deploy steps, rollbacks, and who to contact.

Tasks:
- Author README
- Author deploy runbook

---

(End of issues list)