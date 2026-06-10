# masar-platform
MASAR is a multi-tenant operations platform for organizations, offering workspace management, modules, staff roles, RBAC permissions, dashboards, shared spaces, search, analytics, notifications, and mobile/web support.
# MASAR — Organization Operations Platform

MASAR is a modular multi-platform operations, workspace, and organizational management system built to support organizations of different sizes and sectors.

The platform provides organizations with a centralized environment to manage operations through configurable modules, staff access, role-based permissions (RBAC), dashboards, collaboration spaces, search, analytics, notifications, and mobile/web access.

MASAR follows a **multi-tenant architecture** where each organization operates inside its own isolated workspace while sharing the same platform infrastructure.

Organizations register once, create their workspace, activate modules, invite staff members, assign permissions, and manage operations securely.

---

## Project Overview

MASAR provides a centralized operational portal for organizations.

An organization administrator can:

* Register and configure an organization workspace
* Manage organization profile and settings
* Access organization dashboards
* Enable or disable operational modules
* Add and manage staff members
* Assign roles and permissions
* Control access by department, role, and module
* Manage collaboration through shared spaces
* Search organization data
* View analytics and operational insights
* Monitor activity logs
* Configure notifications and workspace preferences

Staff members can:

* Sign in securely
* Access only authorized modules
* View personalized dashboards
* Collaborate through shared spaces
* Perform actions based on assigned permissions
* Receive notifications and updates
* Search accessible organization data

---

## Tech Stack

### Backend

* Laravel
* REST API
* Laravel Sanctum Authentication
* PostgreSQL
* Laravel Policies & Gates
* Role-Based Access Control (RBAC)
* Service Layer Architecture
* Queue Jobs & Notifications

### Mobile App

* Flutter
* Dart
* REST API Integration
* Responsive UI
* Secure Authentication
* Offline-ready architecture (future support)

### Web Support

Web administration and operations may use:

* Laravel Blade
* Livewire
* Inertia
* Vue.js
* React

Flutter Web may be introduced later if unified frontend support becomes necessary.

---

## Core Architecture

MASAR follows:

* Multi-Tenant Organization Isolation
* Modular Feature Architecture
* API-First Backend
* Feature-Based Flutter Structure
* RBAC Authorization
* Service-Oriented Backend Logic
* Scalable PostgreSQL Database Design

---

## Main Features

### 1. Organization Registration

Organizations register and create their workspace.

Registration collects:

* Organization name
* Organization type
* Sector
* Organization size
* Country
* City
* Organization contact information
* Admin full name
* Admin email
* Admin phone
* Password
* Verification information

Registration flow:

1. Organization submits registration.
2. Organization record is created.
3. Admin account is created.
4. Organization workspace is initialized.
5. Default modules are assigned.
6. Default roles and permissions are generated.
7. Organization enters onboarding.

---

### 2. Organization Workspace

Each organization receives an isolated workspace.

Workspace includes:

* Organization profile
* Dashboard
* Module management
* Staff management
* Roles & permissions
* Shared space
* Search
* Analytics
* Notifications
* Activity logs

All organization data must remain isolated.

---

### 3. Modular System

MASAR uses dynamic modules.

Organizations can activate only required modules.

Example modules:

* Staff Management
* Beneficiary Management
* Case Management
* Inventory
* Reports
* Shared Space
* Analytics
* Notifications
* Tasks
* Documents

Each module contains:

* Screens
* Permissions
* Records
* Widgets
* Analytics

---

### 4. Staff Management

Organization administrators manage staff access.

Staff profile includes:

* Full name
* Email
* Phone
* Job title
* Department
* Assigned modules
* Assigned role
* Status
* Profile image

Staff onboarding:

1. Admin creates invitation.
2. Staff receives invitation.
3. Staff activates account.
4. Staff logs in.

---

### 5. Role-Based Access Control (RBAC)

Access control is organization scoped.

Authorization layers:

* Organization
* Role
* Permission
* Department
* Module

Example roles:

* Organization Owner
* Organization Admin
* Manager
* Supervisor
* Staff
* Viewer
* Analyst

Example permissions:

* View dashboard
* Manage organization
* Manage modules
* Manage staff
* Manage roles
* View analytics
* Export reports
* Manage shared space
* Search records

Users only see authorized modules and actions.

---

### 6. Dashboard

Dashboard provides operational visibility.

Widgets may include:

* Active modules
* Staff count
* Recent activity
* Notifications
* Pending approvals
* Analytics summaries
* Quick actions
* Organization insights

Dashboard adapts to user permissions.

---

### 7. Shared Space

Shared space enables collaboration.

Features:

* Announcements
* Internal posts
* Comments
* Shared notes
* Files
* Discussions
* Organization updates

Visibility options:

* Organization-wide
* Department
* Module
* Private

---

### 8. Search

Global search supports organization-wide discovery.

Search supports:

* Staff
* Modules
* Records
* Reports
* Shared posts
* Files
* Tasks

Search rules:

* Organization isolation
* Permission filtering
* Module restrictions

---

### 9. Analytics

Analytics provides operational insights.

Examples:

* Staff activity
* Module usage
* Search trends
* Monthly growth
* Operational statistics
* Dashboard metrics

Analytics respects organization permissions.

---

### 10. Notifications

Notification system supports:

* In-app notifications
* Email notifications
* Activity alerts
* Module updates
* Staff invitations

---

### 11. Mobile and Web Support

Flutter Mobile supports:

* Authentication
* Dashboard
* Modules
* Shared space
* Search
* Notifications
* Analytics

Web supports:

* Full administration
* Organization setup
* Staff management
* RBAC
* Reports
* Analytics

---

## Suggested Laravel Backend Structure

```text
app/
  Models/
    User.php
    Organization.php
    OrganizationMember.php
    Module.php
    Role.php
    Permission.php
    SharedPost.php
    Notification.php
    ActivityLog.php

  Services/
    Auth/
    Organization/
    Staff/
    Module/
    Dashboard/
    Analytics/
    Search/

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
      RegisterOrganizationRequest.php
      LoginRequest.php
      StoreStaffRequest.php
      UpdateStaffRequest.php

  Policies/

routes/
  api.php

database/
  migrations/
  seeders/
```

---

## Suggested PostgreSQL Database Tables

### users

Stores platform users.

Fields:

* id (uuid)
* name
* email
* phone
* password
* status
* email_verified_at
* created_at
* updated_at

---

### organizations

Stores organizations.

Fields:

* id (uuid)
* name
* slug
* type
* sector
* country
* city
* status
* created_by
* created_at
* updated_at

---

### organization_members

Organization membership.

Fields:

* id (uuid)
* organization_id
* user_id
* role_id
* department
* job_title
* status

---

### modules

Fields:

* id (uuid)
* name
* slug
* description
* is_active

---

### organization_modules

Fields:

* id (uuid)
* organization_id
* module_id
* enabled_at

---

### roles

Fields:

* id (uuid)
* organization_id
* name
* description

---

### permissions

Fields:

* id (uuid)
* module_id
* name
* slug

---

### role_permissions

Fields:

* id (uuid)
* role_id
* permission_id

---

### shared_posts

Fields:

* id (uuid)
* organization_id
* user_id
* title
* content
* visibility

---

### notifications

Fields:

* id (uuid)
* organization_id
* user_id
* type
* title
* body
* read_at

---

### activity_logs

Fields:

* id (uuid)
* organization_id
* user_id
* action
* metadata (jsonb)
* ip_address

---

## API Routes

```php
Route::prefix('auth')->group(function () {
    Route::post('/register', 'register');
    Route::post('/login', 'login');
    Route::post('/logout', 'logout');
});

Route::middleware('auth:sanctum')->group(function () {

    Route::apiResource('organization', OrganizationController::class);

    Route::get('/dashboard', 'dashboard');

    Route::apiResource('staff', StaffController::class);

    Route::apiResource('roles', RoleController::class);

    Route::apiResource('modules', ModuleController::class);

    Route::apiResource('shared-space', SharedSpaceController::class);

    Route::get('/search', 'search');

    Route::get('/analytics', 'analytics');

    Route::get('/notifications', 'notifications');
});
```

---

## Flutter Mobile Structure

```text
lib/

core/
  config/
  constants/
  network/
  storage/
  theme/

features/

  auth/
  dashboard/
  organization/
  modules/
  staff/
  shared_space/
  analytics/
  notifications/
  search/

shared/
  widgets/
  services/
```

---

## Flutter State Management

Recommended:

* Riverpod
* BLoC

Preferred:

* Riverpod

Reasons:

* Better scalability
* Cleaner dependency injection
* Easier testing
* Better modular separation

---

## Authentication Flow

### Organization Registration

1. Register organization.
2. Create admin.
3. Assign owner role.
4. Generate workspace.
5. Enable defaults.
6. Redirect to onboarding.

### Staff Login

1. Receive invitation.
2. Activate account.
3. Login.
4. Receive token.
5. Load permissions.
6. Render authorized UI.

---

## Permission Rules

Every request validates:

1. Authentication
2. Organization membership
3. Organization status
4. Module availability
5. Permission access
6. Data ownership

---

## Security Requirements

* Password hashing
* Sanctum authentication
* Organization isolation
* RBAC enforcement
* Activity logging
* Validation rules
* Secure token storage
* Protected analytics
* PostgreSQL constraints
* UUID identifiers

---

## MVP Scope

Initial release includes:

* Organization registration
* Authentication
* Dashboard
* Modules
* Staff management
* RBAC
* Shared space
* Search
* Analytics
* Notifications
* Flutter mobile
* Laravel API

---

## Future Enhancements

* File uploads
* Real-time collaboration
* Offline mode
* Report exports
* Workflow approvals
* Audit center
* Multi-language support
* Custom modules
* AI insights

---

## Development Goal

Build a scalable organization operations platform using:

* Laravel Backend
* PostgreSQL Database
* Flutter Mobile

Priorities:

* Scalability
* Security
* Clean architecture
* Modular growth
* Maintainability
* Responsive experience

---

## Notes for Codex

When generating code:

* Use Laravel best practices
* Use PostgreSQL features where appropriate
* Prefer UUID primary keys
* Use Services over fat controllers
* Use Policies and Gates
* Use Request validation
* Keep organization isolation strict
* Use Riverpod in Flutter
* Build incrementally
* Keep code readable
* Avoid unnecessary complexity
