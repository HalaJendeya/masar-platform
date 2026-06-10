# Notes for Codex

You are working on the MASAR project.

MASAR is a multi-tenant organization operations platform built to help organizations manage workspaces, staff, modules, role-based permissions, dashboards, shared spaces, search, analytics, notifications, and activity logs.

The project uses:

* Laravel backend
* PostgreSQL database
* REST API
* Laravel Sanctum authentication
* Role-Based Access Control
* Flutter mobile app
* Riverpod for Flutter state management

---

## Before Writing Code

Before generating or editing any code, read these files first:

* `README.md`
* `docs/requirements.md`
* `docs/database.md`
* `docs/api.md`
* `docs/flutter-structure.md`
* `docs/backend-structure.md`

Use these files as the source of truth for the project.

Do not invent features that are not documented.

---

## Important Project Rule

Organization registration is handled on the web platform, not inside the Flutter mobile app.

The Flutter mobile app starts from login only.

Mobile users are expected to already exist in the system because they were created, invited, or approved through the web platform.

Do not create mobile screens for:

* Organization registration
* Organization workspace creation
* Full organization setup
* Full role management
* Full permission management
* Full module activation management

These are mainly web platform responsibilities.

---

## General Development Rules

* Build incrementally.
* Do not build everything at once.
* Keep the code readable for a student team.
* Use clear file and folder names.
* Follow the documented architecture.
* Avoid unnecessary complexity.
* Do not add future features before the MVP is stable.
* Explain what files were created or changed after each major step.
* Keep frontend and backend responsibilities separated.
* Respect the MVP scope.

---

## Backend Rules

The backend should use Laravel best practices.

Use:

* Laravel Sanctum for authentication
* PostgreSQL as the database
* UUID primary keys where appropriate
* Form Request classes for validation
* Service classes for business logic
* Policies and Gates for authorization
* API Resources for JSON responses
* Middleware for repeated access checks
* Consistent JSON response format

Avoid:

* Fat controllers
* Hardcoded permissions
* Returning data from another organization
* Mixing validation logic directly inside controllers
* Building unnecessary future features too early

---

## Backend Architecture Rules

Controllers should be thin.

Controllers should only:

1. Receive the request
2. Use Form Request validation
3. Call the correct Service class
4. Return a clean JSON response

Business logic should be placed inside Service classes.

Authorization should be handled using:

* Policies
* Gates
* Middleware
* Permission checks

---

## Organization Isolation Rules

MASAR is multi-tenant.

Every protected query must be scoped by organization.

This means:

* A user must only access data from their own organization.
* Staff lists must only show staff from the authenticated user's organization.
* Shared space posts must only belong to the authenticated user's organization.
* Analytics must only show data from the authenticated user's organization.
* Search results must not include unauthorized organization data.
* Notifications must only show notifications for the authenticated user and organization.

Never trust organization IDs coming from the frontend without checking ownership and membership.

---

## Permission Rules

Every protected request should check:

1. User is authenticated.
2. User belongs to the organization.
3. Organization is active.
4. Requested module is enabled for the organization.
5. User has the required permission.
6. Requested data belongs to the same organization.

Example permissions:

* `view_dashboard`
* `manage_organization`
* `manage_modules`
* `manage_staff`
* `manage_roles`
* `view_analytics`
* `export_reports`
* `manage_shared_space`
* `view_shared_space`
* `search_records`
* `view_notifications`

---

## Flutter Rules

The Flutter app should use:

* Flutter
* Dart
* Riverpod
* Feature-first folder structure
* REST API integration
* Secure token storage
* Permission-based navigation
* Responsive UI

The Flutter app should not include organization registration.

The Flutter app should include:

* Splash screen
* Login screen
* Secure token storage
* Current user loading
* Permission loading
* Dashboard
* Modules list
* Shared space
* Search
* Notifications
* Analytics
* Profile
* Logout

---

## Flutter Architecture Rules

Use feature-first structure.

Main folders:

* `core/config`
* `core/network`
* `core/storage`
* `core/theme`
* `core/routing`
* `features/auth`
* `features/dashboard`
* `features/modules`
* `features/shared_space`
* `features/search`
* `features/analytics`
* `features/notifications`
* `features/profile`
* `shared/widgets`

Keep API logic separate from UI.

Keep reusable widgets inside:

* `shared/widgets`

Keep secure token logic inside:

* `core/storage`

Keep API client logic inside:

* `core/network`

Keep route guards inside:

* `core/routing`

---

## Mobile Authentication Flow

The mobile app should follow this flow:

1. User opens the app.
2. App checks if a token exists.
3. If no token exists, show login screen.
4. User enters email and password.
5. App sends login request to Laravel API.
6. API validates credentials.
7. API checks organization status.
8. API checks organization membership.
9. API returns token, user data, organization data, role, permissions, and enabled modules.
10. App stores the token securely.
11. App loads authorized dashboard.
12. App shows only allowed modules and actions.

---

## Permission-Based UI Rules

The mobile UI must respect permissions.

Rules:

* Hide unauthorized modules.
* Hide unauthorized buttons.
* Hide unauthorized dashboard widgets.
* Hide unauthorized analytics sections.
* Hide unauthorized shared space actions.
* Do not show disabled organization modules.
* Do not allow hidden actions to be triggered manually.
* Always rely on backend authorization as the final security layer.

Example:

If the user does not have `view_analytics`, do not show the analytics screen in navigation.

If the user does not have `manage_shared_space`, do not show the create post button.

---

## Common App States

Every screen should handle:

* Loading state
* Success state
* Empty state
* Error state
* Unauthorized state
* No internet state when needed

Do not leave screens without proper loading and error handling.

---

## API Rules

The API should return consistent JSON responses.

Login response should include:

* Token
* User data
* Organization data
* Role
* Permissions
* Enabled modules

Protected responses should always respect:

* Authentication
* Organization isolation
* Enabled modules
* Permissions

Common error responses should include clear messages for:

* Validation errors
* Unauthenticated access
* Unauthorized access
* Organization not active
* Module not enabled
* Resource not found

---

## MVP Priority

Build the backend and mobile app in small steps.

Recommended order:

1. Authentication and login
2. Current user endpoint
3. Permission loading
4. Organization profile endpoint
5. Dashboard endpoint
6. Modules endpoint
7. Staff management
8. Shared space
9. Search
10. Notifications
11. Analytics
12. Profile and logout

Do not build advanced future features before these are stable.

---

## Future Enhancements

Do not implement these until the MVP is stable:

* File uploads
* Real-time collaboration
* Offline mode
* Report exports
* Workflow approvals
* Audit center
* Multi-language support
* Custom modules
* AI insights

These features can be prepared for later, but should not block the MVP.

---

## Code Quality Rules

When writing code:

* Keep code readable.
* Use meaningful names.
* Avoid duplicate logic.
* Keep methods focused.
* Use comments only when needed.
* Do not over-engineer.
* Prefer simple working solutions.
* Follow Laravel and Flutter conventions.
* Keep project structure clean.

---

## Final Instruction

Always follow the documentation files in this repository.

If there is a conflict between generated code and the documentation, update the code to match the documentation.

Build MASAR step by step, starting with authentication, organization isolation, permissions, and the mobile login flow.
