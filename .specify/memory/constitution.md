## Helpdesk Web App Constitution

### Purpose
Provide the minimal, clear requirements for an IT helpdesk web application MVP used to receive, track, and resolve user IT issues.

### Scope
Core web app for ticket intake, triage, assignment, updates, and resolution. Includes a simple REST API, a basic web UI, authentication, and audit logging. Excludes integrations with enterprise asset management or advanced analytics (optional later).

### Core Principles
- Simplicity: Start with smallest useful workflow that solves ticket lifecycle.
- Secure by default: Enforce authentication and least-privilege access.
- Observable: Audit actions and expose basic metrics and logs.
- Testable: Critical flows have automated tests (create, update, assign, close).

### Users & Roles
- End User: Creates and views own tickets.
- Agent: Views, comments, updates, assigns tickets.
- Admin: Manages users, roles, and system settings.

### MVP Functional Requirements (bare minimum)
- Ticket creation: title, description, reporter, priority, optional attachments.
- Ticket listing & filtering: by status, priority, assignee, reporter.
- Ticket detail: comments, status changes, assignment, timestamps.
- Assignment: agents can claim or be assigned tickets.
- Notifications: email or in-app notification on assignment and status change (basic).
- Authentication: login (local or single-sign-on) and protected endpoints.

### Minimal Data Model
- Ticket: id, title, description, reporter_id, assignee_id, status (open, in_progress, resolved, closed), priority, created_at, updated_at.
- User: id, name, email, role, password_hash (or external id for SSO), created_at.
- Comment: id, ticket_id, author_id, body, created_at.

### Public API (minimal surface)
- POST /api/tickets — create ticket (returns JSON ticket)
- GET /api/tickets — list tickets (supports query filters)
- GET /api/tickets/{id} — ticket detail
- PATCH /api/tickets/{id} — update ticket (status, assignee, fields)
- POST /api/tickets/{id}/comments — add comment
- POST /api/auth/login — authenticate user

### UI (minimum screens)
- Login screen
- New ticket form
- Ticket list with filters
- Ticket detail with comment box and actions (assign, change status)
- Admin user management (basic)

### Non-functional Requirements
- Availability: single-region, 99% uptime for MVP.
- Performance: list and get endpoints respond < 1s under light load.
- Data retention: tickets and comments retained per policy; soft delete support.
- Security: HTTPS required, passwords hashed, role-based access control, input validation.
- Logging & Auditing: record create/update/delete actions with user and timestamp.

### Security & Privacy
- Only authenticated users may create or view tickets; users can view only their own tickets unless agent/admin.
- Encrypt data in transit; sensitive fields encrypted at rest where practical.
- Minimal PII stored: name, email; avoid unnecessary personal data.

### Acceptance Criteria (MVP)
- A user can create a ticket and receive an identifier.
- An agent can view, comment, change status, and assign a ticket.
- API authenticates and rejects unauthenticated requests.
- Basic UI pages render and allow the listed flows.
- Automated tests cover the create → update → close happy path.

### Integrations (optional, out of scope for MVP)
- External email gateway, SSO providers, asset database.

### Governance
Constitution changes require a short rationale, a migration plan if schema changes, and one approver from product and one from engineering. Track version and ratification date below.

**Version**: 0.1 | **Ratified**: [RATIFICATION_DATE] | **Last Amended**: [LAST_AMENDED_DATE]
