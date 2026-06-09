# Phase 1: App Foundation and Staff Access - Context

**Gathered:** 2026-06-09
**Status:** Ready for planning

<domain>
## Phase Boundary

This phase delivers the initial runnable Spring Boot application shell for the library system: email-based staff login, role-based access for Admin and Librarian users, a dashboard-first landing page, and starter demo data wired through `data.sql`.

</domain>

<decisions>
## Implementation Decisions

### Login and Accounts
- **D-01:** Staff users log in with email, not username.
- **D-02:** Password policy is intentionally simple for coursework: minimum 6 characters.
- **D-03:** Staff accounts are seeded through `data.sql` instead of being created through an admin UI in Phase 1.

### Role Access
- **D-04:** Admin manages staff and members.
- **D-05:** Librarian manages books and borrowing.
- **D-06:** Phase 1 authorization should enforce these role boundaries at the route/service level, not just by hiding navigation links.

### First-Screen Layout
- **D-07:** The landing page after login is a dashboard-only home screen.
- **D-08:** The dashboard should use quick metric cards to summarize the system rather than opening directly into a CRUD screen.

### Demo Data
- **D-09:** Include sample users and starter books in `data.sql` so the project can be demonstrated immediately after startup.

### the agent's Discretion
- JWT, OAuth, password reset, and multi-factor login are not needed for this phase.
- The exact visual style of the dashboard cards is left to the planner, as long as the screen stays simple and staff-focused.

</decisions>

<canonical_refs>
## Canonical References

**Downstream agents MUST read these before planning or implementing.**

### Project Scope
- `.planning/PROJECT.md` - Project purpose, core value, constraints, and active requirements.
- `.planning/REQUIREMENTS.md` - Approved v1 requirements and traceability.
- `.planning/ROADMAP.md` - Phase 1 scope, goals, and success criteria.
- `.planning/STATE.md` - Current project memory and phase position.

### Research Context
- `.planning/research/SUMMARY.md` - Consolidated research findings for stack, features, architecture, and pitfalls.
- `.planning/research/STACK.md` - Recommended stack choices and versions.
- `.planning/research/FEATURES.md` - Feature landscape and MVP boundaries.
- `.planning/research/ARCHITECTURE.md` - Suggested application structure and data flow.
- `.planning/research/PITFALLS.md` - Phase-specific risks and failure modes.

### Project Instructions
- `AGENTS.md` - Generated project guidance for this workspace.

</canonical_refs>

<code_context>
## Existing Code Insights

### Reusable Assets
- None. This repository does not yet contain application source code for the library system.

### Established Patterns
- Greenfield workspace: there are no prior app modules, controllers, entities, or templates to reuse.

### Integration Points
- `data.sql` will seed staff users and starter books.
- Spring Security will gate staff routes.
- Thymeleaf will render the dashboard and navigation shell.

</code_context>

<specifics>
## Specific Ideas

- Email login should be the only staff identifier in Phase 1.
- The dashboard should be the default post-login landing page.
- Role separation should be visible in navigation and enforced by access control.
- Demo startup should be possible without manual data entry because sample users and books are preloaded.

</specifics>

<deferred>
## Deferred Ideas

None - discussion stayed within Phase 1 scope.

</deferred>

---

*Phase: 01-App Foundation and Staff Access*
*Context gathered: 2026-06-09*
