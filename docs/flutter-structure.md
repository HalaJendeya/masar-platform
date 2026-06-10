# MASAR Flutter Mobile Structure

The MASAR mobile app is built using Flutter and Dart.

The app follows a feature-based structure to keep the code organized, scalable, and easy to maintain.

---

## State Management

Preferred state management:

- Riverpod

Alternative:

- BLoC

Riverpod is preferred because it supports:

- Clean dependency injection
- Better scalability
- Easier testing
- Clear separation between UI and logic

---

## Folder Structure

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
