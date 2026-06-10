# MASAR Flutter Mobile Structure

The MASAR mobile application is built using Flutter and Dart.

The mobile app is not responsible for organization registration. Organization registration, organization setup, staff creation, role management, permission management, and module activation are handled mainly through the web platform.

The mobile app is used by existing organization users after their organization account has already been created and configured on the web platform.

Mobile users can log in, access their authorized dashboard, view allowed modules, use shared spaces, search accessible data, receive notifications, and view analytics based on their role and permissions.

---

## Mobile Scope

The MASAR mobile app supports:

* Login for existing organization users
* Secure authentication
* Token-based API access
* Dashboard
* Authorized modules
* Shared space
* Search
* Notifications
* Analytics
* Profile and account settings
* Permission-based UI rendering

The MASAR mobile app does not support:

* Organization registration
* Organization approval
* Full organization setup
* Creating the organization workspace
* Full staff creation flow
* Full role and permission management
* Full module activation management

These actions are handled through the web platform.

---

## Technology Stack

The Flutter mobile application uses:

* Flutter
* Dart
* REST API integration
* Laravel API backend
* Laravel Sanctum authentication
* Secure token storage
* Riverpod state management
* Responsive UI
* Permission-based navigation

---

## Recommended State Management

Preferred state management:

* Riverpod

Alternative:

* BLoC

Riverpod is preferred because it supports:

* Clean dependency injection
* Better scalability
* Easier testing
* Clear separation between UI and business logic
* Better modular structure
* Easier API state handling

---

## Main Mobile Features

The Flutter mobile app should support the following features:

### 1. Login

Users log in using an email and password that already exist in the MASAR system.

The app sends the login request to the Laravel API and receives:

* Authentication token
* User data
* Organization data
* Role
* Permissions
* Enabled modules

---

### 2. Dashboard

The dashboard displays a personalized overview based on the logged-in user's permissions.

Dashboard may include:

* Active modules
* Recent activity
* Notifications count
* Pending tasks or approvals
* Analytics summary
* Quick actions
* Organization insights

Users should only see dashboard widgets they are allowed to access.

---

### 3. Modules

The app displays only the modules enabled for the organization and allowed for the logged-in user.

Example modules:

* Staff Management
* Shared Space
* Analytics
* Notifications
* Tasks
* Documents
* Reports

The user should not see disabled or unauthorized modules.

---

### 4. Shared Space

The shared space allows users to collaborate through:

* Announcements
* Internal posts
* Comments
* Shared notes
* Files
* Discussions
* Organization updates

Shared space visibility may depend on:

* Organization
* Department
* Module
* Private access

---

### 5. Search

The search feature allows users to search accessible organization data.

Search may include:

* Staff
* Modules
* Records
* Reports
* Shared posts
* Files
* Tasks

Search results must respect:

* Organization isolation
* User permissions
* Module restrictions

---

### 6. Analytics

Analytics provides operational insights based on the user's permissions.

Analytics may include:

* Staff activity
* Module usage
* Search trends
* Monthly growth
* Operational statistics
* Dashboard metrics

Users should not see analytics data they are not allowed to access.

---

### 7. Notifications

The notification system shows updates related to:

* Staff invitations
* Activity alerts
* Module updates
* Shared space updates
* Organization events
* Task updates

The app should support:

* Listing notifications
* Marking one notification as read
* Marking all notifications as read
* Showing unread notification count

---

### 8. Profile and Settings

The profile section may include:

* User profile
* Organization information
* Role information
* Account settings
* Notification settings
* Logout

The profile should display information based on the authenticated user returned from the API.

---

## Authentication Flow

### Mobile Login Flow

1. User opens the mobile app.
2. User enters email and password.
3. App sends login request to the Laravel API.
4. API validates credentials.
5. API checks organization status.
6. API checks user membership.
7. API checks role and permissions.
8. API returns authentication token, user data, organization data, role, and permissions.
9. App stores the token securely.
10. App loads the authorized dashboard.
11. App shows only the modules and actions allowed for that user.

---

### Staff Member Flow

1. Staff member is added or invited from the web platform.
2. Staff member activates the account if required.
3. Staff member opens the mobile app.
4. Staff member logs in using email and password.
5. App receives authentication token.
6. App loads user role and permissions.
7. Staff member sees only authorized modules and screens.

---

### Organization Admin Flow on Mobile

1. Organization admin already has an account created from the web platform.
2. Admin opens the mobile app.
3. Admin logs in using email and password.
4. App loads admin permissions.
5. Admin sees the mobile features allowed for their role.

Note: Full organization setup, staff creation, role management, permission management, and module activation are mainly handled from the web portal.

---

## Suggested Folder Structure

```text
lib/

core/
  config/
  constants/
  network/
  storage/
  theme/
  errors/
  routing/
  utils/

features/

  auth/
    data/
    models/
    providers/
    screens/
    services/
    widgets/

  dashboard/
    data/
    models/
    providers/
    screens/
    services/
    widgets/

  modules/
    data/
    models/
    providers/
    screens/
    services/
    widgets/

  shared_space/
    data/
    models/
    providers/
    screens/
    services/
    widgets/

  search/
    data/
    models/
    providers/
    screens/
    services/
    widgets/

  analytics/
    data/
    models/
    providers/
    screens/
    services/
    widgets/

  notifications/
    data/
    models/
    providers/
    screens/
    services/
    widgets/

  profile/
    data/
    models/
    providers/
    screens/
    services/
    widgets/

shared/
  widgets/
  services/
  models/
  helpers/
```

---

## Folder Responsibilities

### core/config

Contains application configuration.

Examples:

* API base URL
* Environment settings
* App constants

---

### core/network

Contains network-related logic.

Examples:

* API client
* HTTP interceptors
* Token handling
* Error handling
* API response wrapper

---

### core/storage

Contains secure local storage logic.

Examples:

* Store token
* Read token
* Delete token on logout
* Store basic user session data

---

### core/theme

Contains app theme and design rules.

Examples:

* Colors
* Text styles
* Spacing
* Button styles
* Input styles

---

### core/routing

Contains app navigation and route guards.

Examples:

* App routes
* Protected routes
* Redirect unauthenticated users to login
* Redirect authenticated users to dashboard

---

### features/auth

Contains login and authentication logic.

Screens may include:

* Splash screen
* Login screen
* Forgot password screen
* Account activation screen if required

Auth feature should handle:

* Login request
* Token storage
* Current user loading
* Logout
* Auth state

---

### features/dashboard

Contains dashboard screens and widgets.

Dashboard should show data based on:

* User role
* User permissions
* Enabled modules
* Organization status

---

### features/modules

Contains module list and module access logic.

This feature should:

* Display enabled modules
* Hide unauthorized modules
* Open module screens based on permissions

---

### features/shared_space

Contains shared space posts, announcements, comments, and discussions.

This feature should respect:

* Visibility rules
* Permissions
* Organization isolation

---

### features/search

Contains global search logic.

Search should:

* Send query to API
* Display grouped results
* Hide unauthorized results
* Handle empty search state

---

### features/analytics

Contains analytics screens and charts.

Analytics should:

* Show only authorized statistics
* Handle loading and empty states
* Keep sensitive data protected

---

### features/notifications

Contains notification list and notification actions.

This feature should support:

* View notifications
* Mark notification as read
* Mark all as read
* Show unread count

---

### features/profile

Contains user profile and account settings.

Profile may include:

* User information
* Organization information
* Role
* Permissions summary
* Settings
* Logout

---

## API Integration

The Flutter app communicates with the Laravel REST API.

Main API areas:

* Authentication
* Current user
* Dashboard
* Modules
* Shared space
* Search
* Analytics
* Notifications
* Profile

The app should not hardcode data that should come from the backend.

---

## Token Handling

After login:

1. API returns a Sanctum token.
2. App stores token securely.
3. App attaches token to protected API requests.
4. If token expires or becomes invalid, app redirects user to login.
5. On logout, app removes the token from secure storage.

Recommended storage:

* flutter_secure_storage

---

## Permission-Based UI Rules

The mobile UI must respect user permissions.

Rules:

* Do not show unauthorized modules.
* Do not show unauthorized buttons.
* Do not show unauthorized dashboard widgets.
* Do not show unauthorized analytics.
* Do not show unauthorized shared space actions.
* Do not allow hidden actions to be triggered manually.
* Always rely on backend authorization as the final security layer.

Example:

If the user does not have `view_analytics`, the analytics screen should not appear in navigation.

If the user does not have `manage_shared_space`, the create post button should not appear.

---

## Common App States

Each screen should handle:

* Loading state
* Success state
* Empty state
* Error state
* Unauthorized state
* No internet state where needed

---

## Suggested Screens

### Auth

* Splash Screen
* Login Screen
* Forgot Password Screen
* Account Activation Screen if needed

### Dashboard

* Dashboard Screen
* Module Overview Cards
* Recent Activity
* Quick Actions
* Notification Summary

### Modules

* Modules List Screen
* Module Details Screen
* Unauthorized Module State

### Shared Space

* Shared Space Feed
* Post Details
* Create Post if authorized
* Comments if supported
* Empty Shared Space State

### Search

* Search Screen
* Search Results Screen
* Empty Search State
* Unauthorized Results Handling

### Analytics

* Analytics Overview
* Module Usage Analytics
* Staff Activity Analytics
* Empty Analytics State

### Notifications

* Notifications List
* Notification Details
* Empty Notifications State

### Profile

* Profile View
* Account Settings
* Notification Settings
* Logout

---

## Navigation Rules

Navigation should depend on:

* Authentication status
* Organization status
* User role
* User permissions
* Enabled modules

Suggested flow:

```text
Splash
  ↓
Check token
  ↓
If no token → Login
  ↓
If token exists → Load current user
  ↓
If valid → Dashboard
  ↓
If invalid → Login
```

---

## Suggested API Models

### User Model

Fields may include:

* id
* name
* email
* phone
* status

---

### Organization Model

Fields may include:

* id
* name
* slug
* type
* sector
* country
* city
* status

---

### Role Model

Fields may include:

* id
* name
* description

---

### Permission Model

Fields may include:

* name
* slug

---

### Module Model

Fields may include:

* id
* name
* slug
* description
* enabled

---

### Notification Model

Fields may include:

* id
* type
* title
* body
* read_at
* created_at

---

### Shared Post Model

Fields may include:

* id
* title
* content
* visibility
* created_by
* created_at

---

## Development Rules

* Use feature-first structure.
* Use Riverpod for state management.
* Keep UI separate from API logic.
* Keep reusable widgets inside `shared/widgets`.
* Keep API services separate from screens.
* Keep models inside their feature folders.
* Keep secure storage inside `core/storage`.
* Keep routes inside `core/routing`.
* Use responsive UI.
* Handle loading, success, empty, and error states.
* Do not hardcode API responses.
* Do not show unauthorized actions.
* Do not build mobile registration.
* All screens must respect user permissions.
* Keep code readable for the team.
* Build incrementally.

---

## MVP Mobile Priority

Build the mobile app in this order:

1. Splash screen
2. Login screen
3. Secure token storage
4. Current user loading
5. Permission loading
6. Dashboard
7. Modules list
8. Shared space
9. Search
10. Notifications
11. Analytics
12. Profile and logout

---

## Notes for Codex

When generating Flutter code for MASAR:

* Do not create organization registration screens.
* Organization registration is handled on the web platform.
* Start with login and authenticated user flow.
* Use Riverpod.
* Use feature-first folder structure.
* Connect to Laravel REST API.
* Store token securely.
* Render UI based on permissions.
* Hide unauthorized screens and actions.
* Keep API services separate from UI.
* Keep widgets reusable.
* Handle loading, error, empty, and unauthorized states.
* Build one feature at a time.
* Avoid unnecessary complexity.
