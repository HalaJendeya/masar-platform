# MASAR API Documentation

MASAR uses a Laravel REST API to connect the backend with the Flutter mobile app and any future web frontend.

The API is responsible for:

* Authentication
* Organization registration
* Organization workspace management
* Staff management
* Role-based access control
* Module management
* Dashboard data
* Shared space
* Search
* Analytics
* Notifications

Authentication is handled using **Laravel Sanctum**.

All protected API routes must check:

1. User authentication
2. Organization membership
3. Organization status
4. Enabled modules
5. User role
6. User permissions
7. Data ownership and organization isolation

---

## Base API Structure

Suggested API prefix:

```text
/api
```

Example full routes:

```text
POST /api/auth/register
POST /api/auth/login
POST /api/auth/logout
GET  /api/dashboard
GET  /api/staff
GET  /api/search
```

---

## Authentication Routes

Authentication routes handle organization registration, login, logout, and token management.

```php
Route::prefix('auth')->group(function () {
    Route::post('/register', [AuthController::class, 'register']);
    Route::post('/login', [AuthController::class, 'login']);

    Route::middleware('auth:sanctum')->group(function () {
        Route::post('/logout', [AuthController::class, 'logout']);
        Route::get('/me', [AuthController::class, 'me']);
    });
});
```

---

## Authentication Endpoints

### Register Organization

```text
POST /api/auth/register
```

Used when an organization admin creates a new organization workspace.

#### Request Body

```json
{
  "admin_name": "Organization Admin",
  "admin_email": "admin@example.com",
  "admin_phone": "+970599000000",
  "password": "securePassword123",
  "password_confirmation": "securePassword123",
  "organization_name": "Example Organization",
  "organization_type": "NGO",
  "sector": "Humanitarian",
  "organization_size": "50-100",
  "country": "Palestine",
  "city": "Gaza"
}
```

#### Success Response

```json
{
  "message": "Organization registered successfully.",
  "organization": {
    "id": "uuid",
    "name": "Example Organization",
    "status": "pending"
  },
  "user": {
    "id": "uuid",
    "name": "Organization Admin",
    "email": "admin@example.com",
    "status": "active"
  }
}
```

#### Validation Rules

* Admin name is required.
* Admin email is required and must be unique.
* Password is required and must be confirmed.
* Organization name is required.
* Organization type is required.
* Country and city are required.
* Duplicate organization names/slugs should be handled safely.

---

### Login

```text
POST /api/auth/login
```

Used by organization admins and staff members to sign in.

#### Request Body

```json
{
  "email": "admin@example.com",
  "password": "securePassword123"
}
```

#### Success Response

```json
{
  "message": "Login successful.",
  "token": "sanctum_token_here",
  "user": {
    "id": "uuid",
    "name": "Organization Admin",
    "email": "admin@example.com"
  },
  "organization": {
    "id": "uuid",
    "name": "Example Organization",
    "status": "active"
  },
  "permissions": [
    "view_dashboard",
    "manage_staff",
    "manage_modules"
  ]
}
```

#### Error Responses

Invalid credentials:

```json
{
  "message": "Invalid email or password."
}
```

Unauthorized organization:

```json
{
  "message": "Your organization account is not active."
}
```

---

### Logout

```text
POST /api/auth/logout
```

Requires authentication.

#### Headers

```text
Authorization: Bearer {token}
```

#### Success Response

```json
{
  "message": "Logged out successfully."
}
```

---

### Get Current User

```text
GET /api/auth/me
```

Returns the currently authenticated user, organization membership, role, and permissions.

#### Success Response

```json
{
  "user": {
    "id": "uuid",
    "name": "Organization Admin",
    "email": "admin@example.com"
  },
  "organization": {
    "id": "uuid",
    "name": "Example Organization"
  },
  "role": {
    "id": "uuid",
    "name": "Organization Owner"
  },
  "permissions": [
    "view_dashboard",
    "manage_staff",
    "manage_modules"
  ]
}
```

---

## Protected Routes

All routes below require authentication using Sanctum.

```php
Route::middleware('auth:sanctum')->group(function () {
    Route::apiResource('organization', OrganizationController::class);

    Route::get('/dashboard', [DashboardController::class, 'index']);

    Route::apiResource('staff', StaffController::class);

    Route::apiResource('roles', RoleController::class);

    Route::apiResource('modules', ModuleController::class);

    Route::apiResource('shared-space', SharedSpaceController::class);

    Route::get('/search', [SearchController::class, 'index']);

    Route::get('/analytics', [AnalyticsController::class, 'index']);

    Route::get('/notifications', [NotificationController::class, 'index']);
});
```

---

# Organization API

Organization routes manage the organization profile, workspace information, and organization settings.

## Get Organization

```text
GET /api/organization
```

Returns the current user's organization.

### Success Response

```json
{
  "organization": {
    "id": "uuid",
    "name": "Example Organization",
    "slug": "example-organization",
    "type": "NGO",
    "sector": "Humanitarian",
    "country": "Palestine",
    "city": "Gaza",
    "status": "active"
  }
}
```

---

## Update Organization

```text
PUT /api/organization/{id}
```

Allows authorized organization admins to update organization details.

### Request Body

```json
{
  "name": "Updated Organization Name",
  "type": "NGO",
  "sector": "Humanitarian",
  "country": "Palestine",
  "city": "Gaza"
}
```

### Required Permissions

```text
manage_organization
```

---

# Dashboard API

The dashboard API returns a personalized dashboard based on the user's permissions.

## Get Dashboard

```text
GET /api/dashboard
```

### Success Response

```json
{
  "widgets": {
    "active_modules": 5,
    "staff_count": 24,
    "recent_activity": [],
    "notifications_count": 3,
    "pending_approvals": 2,
    "analytics_summary": {}
  }
}
```

### Rules

* Dashboard data must be scoped to the user's organization.
* Users should only see widgets they have permission to view.
* Analytics summaries should respect role and module permissions.

### Required Permission

```text
view_dashboard
```

---

# Staff API

Staff routes allow organization admins to invite, view, update, and manage staff members.

## List Staff

```text
GET /api/staff
```

### Success Response

```json
{
  "data": [
    {
      "id": "uuid",
      "name": "Staff Member",
      "email": "staff@example.com",
      "phone": "+970599000000",
      "job_title": "Field Officer",
      "department": "Operations",
      "role": "Staff",
      "status": "active"
    }
  ]
}
```

### Required Permission

```text
manage_staff
```

---

## Create Staff Invitation

```text
POST /api/staff
```

Creates a staff invitation.

### Request Body

```json
{
  "name": "Staff Member",
  "email": "staff@example.com",
  "phone": "+970599000000",
  "job_title": "Field Officer",
  "department": "Operations",
  "role_id": "uuid",
  "assigned_modules": [
    "uuid",
    "uuid"
  ]
}
```

### Success Response

```json
{
  "message": "Staff invitation created successfully.",
  "staff": {
    "id": "uuid",
    "name": "Staff Member",
    "email": "staff@example.com",
    "status": "invited"
  }
}
```

### Required Permission

```text
manage_staff
```

---

## Update Staff

```text
PUT /api/staff/{id}
```

Updates staff details, role, department, status, or assigned modules.

### Request Body

```json
{
  "job_title": "Supervisor",
  "department": "Field Operations",
  "role_id": "uuid",
  "status": "active"
}
```

### Required Permission

```text
manage_staff
```

---

## Delete or Deactivate Staff

```text
DELETE /api/staff/{id}
```

Recommended behavior: deactivate staff instead of permanently deleting them.

### Success Response

```json
{
  "message": "Staff member deactivated successfully."
}
```

### Required Permission

```text
manage_staff
```

---

# Roles API

Roles define what users can do inside an organization.

## List Roles

```text
GET /api/roles
```

### Success Response

```json
{
  "data": [
    {
      "id": "uuid",
      "name": "Organization Admin",
      "description": "Can manage organization settings and staff."
    },
    {
      "id": "uuid",
      "name": "Staff",
      "description": "Can access assigned modules only."
    }
  ]
}
```

---

## Create Role

```text
POST /api/roles
```

### Request Body

```json
{
  "name": "Supervisor",
  "description": "Can supervise staff and view reports.",
  "permissions": [
    "view_dashboard",
    "view_analytics",
    "manage_shared_space"
  ]
}
```

### Required Permission

```text
manage_roles
```

---

## Update Role

```text
PUT /api/roles/{id}
```

### Request Body

```json
{
  "name": "Updated Role Name",
  "description": "Updated role description.",
  "permissions": [
    "view_dashboard",
    "manage_staff"
  ]
}
```

### Required Permission

```text
manage_roles
```

---

## Delete Role

```text
DELETE /api/roles/{id}
```

### Required Permission

```text
manage_roles
```

---

# Modules API

Modules allow organizations to enable or disable operational sections.

## List Modules

```text
GET /api/modules
```

Returns all available platform modules and indicates which ones are enabled for the current organization.

### Success Response

```json
{
  "data": [
    {
      "id": "uuid",
      "name": "Staff Management",
      "slug": "staff-management",
      "enabled": true
    },
    {
      "id": "uuid",
      "name": "Shared Space",
      "slug": "shared-space",
      "enabled": true
    }
  ]
}
```

---

## Enable Module

```text
POST /api/modules/{id}/enable
```

### Success Response

```json
{
  "message": "Module enabled successfully."
}
```

### Required Permission

```text
manage_modules
```

---

## Disable Module

```text
POST /api/modules/{id}/disable
```

### Success Response

```json
{
  "message": "Module disabled successfully."
}
```

### Required Permission

```text
manage_modules
```

---

# Shared Space API

Shared Space allows staff members to collaborate through posts, announcements, notes, files, and discussions.

## List Shared Posts

```text
GET /api/shared-space
```

### Success Response

```json
{
  "data": [
    {
      "id": "uuid",
      "title": "Important Announcement",
      "content": "Meeting tomorrow at 10 AM.",
      "visibility": "organization",
      "created_by": "Admin Name",
      "created_at": "2026-06-10T10:00:00Z"
    }
  ]
}
```

### Required Permission

```text
manage_shared_space
```

or

```text
view_shared_space
```

---

## Create Shared Post

```text
POST /api/shared-space
```

### Request Body

```json
{
  "title": "Important Announcement",
  "content": "Meeting tomorrow at 10 AM.",
  "visibility": "organization"
}
```

### Visibility Options

```text
organization
department
module
private
```

### Required Permission

```text
manage_shared_space
```

---

## Update Shared Post

```text
PUT /api/shared-space/{id}
```

### Request Body

```json
{
  "title": "Updated Announcement",
  "content": "Updated content.",
  "visibility": "department"
}
```

### Required Permission

```text
manage_shared_space
```

---

## Delete Shared Post

```text
DELETE /api/shared-space/{id}
```

### Required Permission

```text
manage_shared_space
```

---

# Search API

Search allows users to search through accessible organization data.

## Global Search

```text
GET /api/search?query=keyword
```

### Searchable Resources

* Staff
* Modules
* Records
* Reports
* Shared posts
* Files
* Tasks

### Success Response

```json
{
  "query": "keyword",
  "results": {
    "staff": [],
    "modules": [],
    "shared_posts": [],
    "reports": [],
    "tasks": []
  }
}
```

### Search Rules

* Search must be scoped to the authenticated user's organization.
* Search must respect permissions.
* Search must respect module restrictions.
* Users should not see unauthorized data in search results.

### Required Permission

```text
search_records
```

---

# Analytics API

Analytics provides operational insights for the organization.

## Get Analytics

```text
GET /api/analytics
```

### Example Response

```json
{
  "staff_activity": {},
  "module_usage": {},
  "search_trends": {},
  "monthly_growth": {},
  "operational_statistics": {},
  "dashboard_metrics": {}
}
```

### Analytics Examples

* Staff activity
* Module usage
* Search trends
* Monthly growth
* Operational statistics
* Dashboard metrics

### Rules

* Analytics must be organization scoped.
* Analytics must respect user role and permissions.
* Sensitive data should not be exposed to unauthorized users.

### Required Permission

```text
view_analytics
```

---

# Notifications API

Notifications inform users about invitations, activity alerts, module updates, and organization events.

## List Notifications

```text
GET /api/notifications
```

### Success Response

```json
{
  "data": [
    {
      "id": "uuid",
      "type": "staff_invitation",
      "title": "New Staff Invitation",
      "body": "You have been invited to join Example Organization.",
      "read_at": null,
      "created_at": "2026-06-10T10:00:00Z"
    }
  ]
}
```

---

## Mark Notification as Read

```text
POST /api/notifications/{id}/read
```

### Success Response

```json
{
  "message": "Notification marked as read."
}
```

---

## Mark All Notifications as Read

```text
POST /api/notifications/read-all
```

### Success Response

```json
{
  "message": "All notifications marked as read."
}
```

---

# Permission Rules

Every protected request should validate:

1. The user is authenticated.
2. The user belongs to the organization.
3. The organization is active.
4. The requested module is enabled for the organization.
5. The user has the required permission.
6. The requested data belongs to the same organization.

---

# Common Permissions

Example permissions:

```text
view_dashboard
manage_organization
manage_modules
manage_staff
manage_roles
view_analytics
export_reports
manage_shared_space
view_shared_space
search_records
view_notifications
```

---

# Common Error Responses

## Validation Error

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

## Unauthenticated

```json
{
  "message": "Unauthenticated."
}
```

---

## Unauthorized

```json
{
  "message": "You do not have permission to perform this action."
}
```

---

## Organization Not Active

```json
{
  "message": "Your organization account is not active."
}
```

---

## Module Not Enabled

```json
{
  "message": "This module is not enabled for your organization."
}
```

---

## Not Found

```json
{
  "message": "Resource not found."
}
```

---

# API Development Notes

When implementing the API:

* Use Laravel Sanctum for authentication.
* Use Request classes for validation.
* Use Policies and Gates for authorization.
* Keep controllers clean.
* Move business logic to Service classes.
* Scope all queries by organization ID.
* Never return data from another organization.
* Use UUID identifiers where appropriate.
* Log important actions in activity logs.
* Return consistent JSON responses.
* Handle validation and authorization errors clearly.
* Keep API responses mobile-friendly.
* Do not build future enhancements before MVP endpoints are stable.

---

# MVP API Priority

Build the API in this order:

1. Authentication and organization registration
2. Current user and permission loading
3. Organization profile
4. Dashboard
5. Module management
6. Staff management
7. Roles and permissions
8. Shared space
9. Search
10. Analytics
11. Notifications

---

# Notes for Codex

Before generating code for the API, read:

* `README.md`
* `docs/requirements.md`
* `docs/database.md`
* `docs/api.md`
* `docs/backend-structure.md`

Codex should:

* Follow Laravel best practices.
* Build incrementally.
* Avoid unnecessary complexity.
* Use Laravel Sanctum.
* Use PostgreSQL.
* Prefer UUID primary keys.
* Use service classes.
* Use request validation.
* Use policies and gates.
* Keep organization isolation strict.
* Respect RBAC permissions.
* Return consistent JSON responses.
