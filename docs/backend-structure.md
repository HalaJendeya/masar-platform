# MASAR Laravel Backend Structure

The MASAR backend is built using Laravel and PostgreSQL.

The backend provides the REST API used by the Flutter mobile app and any future web frontend. It handles authentication, organization workspaces, staff access, modules, roles, permissions, dashboard data, shared space, search, analytics, notifications, and activity logs.

MASAR follows a multi-tenant architecture. This means each organization has its own isolated workspace and data. Even though all organizations use the same platform, one organization must never access another organization's data.

---

## Backend Technology Stack

The backend uses:

* Laravel
* PHP
* PostgreSQL
* REST API
* Laravel Sanctum Authentication
* Laravel Policies and Gates
* Role-Based Access Control
* Service Layer Architecture
* Request Validation
* Queue Jobs and Notifications
* UUID primary keys where appropriate

---

## Main Backend Responsibilities

The Laravel backend is responsible for:

* User authentication
* Secure login and logout
* Organization workspace management
* Staff management
* Role and permission management
* Module management
* Dashboard API
* Shared space API
* Search API
* Analytics API
* Notifications API
* Activity logging
* Organization data isolation
* Validation and authorization

---

## Suggested Laravel Folder Structure

```text
app/

  Models/
    User.php
    Organization.php
    OrganizationMember.php
    Module.php
    OrganizationModule.php
    Role.php
    Permission.php
    RolePermission.php
    SharedPost.php
    Notification.php
    ActivityLog.php

  Services/
    Auth/
      AuthService.php

    Organization/
      OrganizationService.php

    Staff/
      StaffService.php

    Module/
      ModuleService.php

    Role/
      RoleService.php

    Dashboard/
      DashboardService.php

    SharedSpace/
      SharedSpaceService.php

    Search/
      SearchService.php

    Analytics/
      AnalyticsService.php

    Notification/
      NotificationService.php

  Http/

    Controllers/
      AuthController.php
      OrganizationController.php
      DashboardController.php
      ModuleController.php
      StaffController.php
      RoleController.php
      PermissionController.php
      SharedSpaceController.php
      SearchController.php
      AnalyticsController.php
      NotificationController.php

    Requests/
      Auth/
        LoginRequest.php

      Staff/
        StoreStaffRequest.php
        UpdateStaffRequest.php

      Organization/
        UpdateOrganizationRequest.php

      Role/
        StoreRoleRequest.php
        UpdateRoleRequest.php

      SharedSpace/
        StoreSharedPostRequest.php
        UpdateSharedPostRequest.php

    Resources/
      UserResource.php
      OrganizationResource.php
      StaffResource.php
      ModuleResource.php
      RoleResource.php
      SharedPostResource.php
      NotificationResource.php

  Policies/
    OrganizationPolicy.php
    StaffPolicy.php
    ModulePolicy.php
    RolePolicy.php
    SharedPostPolicy.php
    AnalyticsPolicy.php

  Middleware/
    EnsureOrganizationIsActive.php
    EnsureUserBelongsToOrganization.php
    EnsureModuleIsEnabled.php
    CheckPermission.php

routes/
  api.php

database/
  migrations/
  seeders/
  factories/
```

---

## Models

### User

Represents a platform user.

A user can be:

* Organization owner
* Organization admin
* Manager
* Supervisor
* Staff member
* Viewer
* Analyst

Important relationships:

* A user can belong to one or more organizations.
* A user can have a role inside an organization.
* A user can create shared posts, notifications, and activity logs.

---

### Organization

Represents an organization workspace.

Each organization has:

* Name
* Slug
* Type
* Sector
* Country
* City
* Status
* Created by user

Organization status examples:

* pending
* active
* suspended
* rejected

Important rule:

Every organization must have isolated data.

---

### OrganizationMember

Represents the relationship between a user and an organization.

This model connects:

* User
* Organization
* Role
* Department
* Job title
* Status

This model is important because the same user may have a different role depending on the organization.

---

### Module

Represents a platform module.

Example modules:

* Staff Management
* Shared Space
* Analytics
* Notifications
* Tasks
* Documents
* Reports

Modules are global platform features.

---

### OrganizationModule

Represents the modules enabled for a specific organization.

Example:

An organization may enable:

* Shared Space
* Analytics
* Notifications

And disable:

* Inventory
* Case Management

The backend must check if the module is enabled before allowing access.

---

### Role

Represents a role inside an organization.

Example roles:

* Organization Owner
* Organization Admin
* Manager
* Supervisor
* Staff
* Viewer
* Analyst

Roles are organization-scoped.

This means each organization can have its own roles.

---

### Permission

Represents an action a user can perform.

Example permissions:

* view_dashboard
* manage_organization
* manage_modules
* manage_staff
* manage_roles
* view_analytics
* export_reports
* manage_shared_space
* view_shared_space
* search_records
* view_notifications

---

### RolePermission

Connects roles with permissions.

Example:

The role `Organization Admin` may have:

* view_dashboard
* manage_staff
* manage_modules
* manage_roles
* view_analytics

---

### SharedPost

Represents posts inside the shared space.

A shared post may be:

* Announcement
* Note
* Discussion
* Update

Visibility options:

* organization
* department
* module
* private

---

### Notification

Represents notifications sent to users.

Notifications may include:

* Staff invitations
* Activity alerts
* Module updates
* Shared space updates
* Task updates
* Organization events

---

### ActivityLog

Stores important user actions.

Examples:

* User logged in
* Staff member invited
* Role updated
* Module enabled
* Shared post created
* Organization settings updated

Activity logs help with auditing and tracking system usage.

---

## Controllers

Controllers should be thin.

Controllers should only:

* Receive request
* Validate through Request classes
* Call Service classes
* Return JSON responses

Controllers should not contain heavy business logic.

---

## Services

Services contain the main business logic.

Examples:

### AuthService

Responsible for:

* Login
* Logout
* Token creation
* Current user loading
* Permission loading

---

### OrganizationService

Responsible for:

* Getting organization profile
* Updating organization details
* Checking organization status
* Managing workspace settings

---

### StaffService

Responsible for:

* Listing staff
* Creating staff invitations
* Updating staff
* Deactivating staff
* Assigning roles
* Assigning modules

---

### ModuleService

Responsible for:

* Listing available modules
* Listing organization modules
* Enabling modules
* Disabling modules
* Checking module availability

---

### RoleService

Responsible for:

* Listing roles
* Creating roles
* Updating roles
* Deleting roles
* Assigning permissions to roles

---

### DashboardService

Responsible for:

* Dashboard widgets
* Recent activity
* Staff count
* Active modules
* Notification summary
* Permission-based dashboard data

---

### SharedSpaceService

Responsible for:

* Listing shared posts
* Creating posts
* Updating posts
* Deleting posts
* Applying visibility rules

---

### SearchService

Responsible for:

* Searching organization data
* Filtering results by permissions
* Filtering results by enabled modules
* Returning grouped search results

---

### AnalyticsService

Responsible for:

* Staff activity analytics
* Module usage analytics
* Search trends
* Monthly growth
* Operational statistics
* Dashboard metrics

---

### NotificationService

Responsible for:

* Listing notifications
* Creating notifications
* Marking notifications as read
* Marking all notifications as read

---

## Request Validation

Use Laravel Form Request classes for validation.

Examples:

* LoginRequest
* StoreStaffRequest
* UpdateStaffRequest
* UpdateOrganizationRequest
* StoreRoleRequest
* UpdateRoleRequest
* StoreSharedPostRequest
* UpdateSharedPostRequest

Validation should not be written directly inside controllers.

---

## Resources

Use Laravel API Resources to return clean JSON responses.

Resources help keep API responses consistent.

Example resources:

* UserResource
* OrganizationResource
* StaffResource
* ModuleResource
* RoleResource
* SharedPostResource
* NotificationResource

---

## Middleware

Middleware should protect routes before they reach controllers.

Suggested middleware:

### EnsureOrganizationIsActive

Checks that the user's organization is active.

If the organization is pending, suspended, or rejected, the request should be blocked.

---

### EnsureUserBelongsToOrganization

Checks that the authenticated user belongs to the requested organization.

This prevents users from accessing another organization's data.

---

### EnsureModuleIsEnabled

Checks that the requested module is enabled for the organization.

Example:

If the Analytics module is disabled, the user should not access analytics endpoints.

---

### CheckPermission

Checks that the user has the required permission.

Example:

A user cannot access staff management unless they have:

```text
manage_staff
```

---

## Policies and Gates

Use Laravel Policies and Gates for authorization.

Policies should check:

* User role
* User permissions
* Organization membership
* Resource ownership
* Organization isolation

Example policies:

* OrganizationPolicy
* StaffPolicy
* ModulePolicy
* RolePolicy
* SharedPostPolicy
* AnalyticsPolicy

---

## API Route Structure

Main API routes are stored inside:

```text
routes/api.php
```

Suggested route groups:

```php
Route::prefix('auth')->group(function () {
    Route::post('/login', [AuthController::class, 'login']);

    Route::middleware('auth:sanctum')->group(function () {
        Route::post('/logout', [AuthController::class, 'logout']);
        Route::get('/me', [AuthController::class, 'me']);
    });
});

Route::middleware(['auth:sanctum'])->group(function () {
    Route::get('/organization', [OrganizationController::class, 'show']);
    Route::put('/organization/{organization}', [OrganizationController::class, 'update']);

    Route::get('/dashboard', [DashboardController::class, 'index']);

    Route::apiResource('staff', StaffController::class);
    Route::apiResource('roles', RoleController::class);
    Route::apiResource('modules', ModuleController::class);
    Route::apiResource('shared-space', SharedSpaceController::class);

    Route::get('/search', [SearchController::class, 'index']);
    Route::get('/analytics', [AnalyticsController::class, 'index']);

    Route::get('/notifications', [NotificationController::class, 'index']);
    Route::post('/notifications/{notification}/read', [NotificationController::class, 'markAsRead']);
    Route::post('/notifications/read-all', [NotificationController::class, 'markAllAsRead']);
});
```

---

## Important Registration Note

The Flutter mobile app does not handle organization registration.

Organization registration and full organization setup are handled through the web platform.

The backend may still support organization registration for the web platform, but the mobile app only uses login and authenticated user access.

Mobile users are expected to already exist in the system.

---

## Authentication Rules

Authentication uses Laravel Sanctum.

Login response should return:

* Token
* User data
* Organization data
* Role
* Permissions
* Enabled modules

The Flutter app uses this response to decide what screens and actions the user can access.

---

## Organization Isolation Rules

Every protected query must be scoped by organization.

Example:

A staff list query must only return staff from the authenticated user's organization.

A shared space query must only return posts from the authenticated user's organization.

An analytics query must only return analytics from the authenticated user's organization.

Never trust IDs from the frontend without checking organization ownership.

---

## Permission Rules

Every protected request should validate:

1. User is authenticated.
2. User belongs to the organization.
3. Organization is active.
4. Requested module is enabled.
5. User has the required permission.
6. Requested data belongs to the same organization.

---

## Security Requirements

The backend must include:

* Password hashing
* Laravel Sanctum authentication
* Organization isolation
* RBAC enforcement
* Request validation
* Policies and Gates
* Secure token handling
* Activity logging
* PostgreSQL constraints
* UUID identifiers where appropriate
* Consistent error responses
* Protection against unauthorized data access

---

## Common Error Responses

### Unauthenticated

```json
{
  "message": "Unauthenticated."
}
```

---

### Unauthorized

```json
{
  "message": "You do not have permission to perform this action."
}
```

---

### Organization Not Active

```json
{
  "message": "Your organization account is not active."
}
```

---

### Module Not Enabled

```json
{
  "message": "This module is not enabled for your organization."
}
```

---

### Validation Error

```json
{
  "message": "The given data was invalid.",
  "errors": {
    "email": [
      "The email field is required."
    ]
  }
}
```

---

## Database Notes

The database is documented separately in:

```text
docs/database.md
```

Backend developers should read that file before creating migrations.

Important database rules:

* Use PostgreSQL.
* Use UUID identifiers where appropriate.
* Add foreign keys.
* Add indexes for organization_id.
* Add indexes for user_id where needed.
* Use jsonb for flexible metadata fields.
* Keep organization data isolated.

---

## Development Rules

Backend developers should follow these rules:

* Use Laravel best practices.
* Keep controllers thin.
* Put business logic inside services.
* Use Form Requests for validation.
* Use API Resources for responses.
* Use Policies and Gates for authorization.
* Use Middleware for repeated access checks.
* Scope all data by organization.
* Do not expose data from another organization.
* Use consistent JSON responses.
* Log important actions.
* Keep code readable and maintainable.
* Avoid unnecessary complexity.
* Build incrementally according to MVP priority.

---

## MVP Backend Priority

Build the backend in this order:

1. Authentication and login
2. Current user endpoint
3. Organization profile
4. Role and permission loading
5. Dashboard endpoint
6. Modules endpoint
7. Staff management
8. Shared space
9. Search
10. Notifications
11. Analytics

Organization registration can be handled for the web platform, but it is not part of the mobile app flow.

---

## Notes for Codex

When generating backend code for MASAR:

* Read `README.md`.
* Read `docs/requirements.md`.
* Read `docs/database.md`.
* Read `docs/api.md`.
* Read `docs/backend-structure.md`.
* Use Laravel best practices.
* Use PostgreSQL.
* Use Laravel Sanctum.
* Keep controllers thin.
* Use services for business logic.
* Use request validation.
* Use policies and gates.
* Keep organization isolation strict.
* Respect RBAC permissions.
* Return consistent JSON responses.
* Do not build unnecessary future features before MVP endpoints are stable.
