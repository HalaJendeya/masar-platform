# MASAR Database Design

MASAR uses PostgreSQL as the main database.

The system should use UUID identifiers where possible to improve security and scalability.

---

## users

Stores platform users.

Fields:

- id: uuid
- name
- email
- phone
- password
- status
- email_verified_at
- created_at
- updated_at

---

## organizations

Stores organizations.

Fields:

- id: uuid
- name
- slug
- type
- sector
- country
- city
- status
- created_by
- created_at
- updated_at

---

## organization_members

Stores organization membership and staff relation.

Fields:

- id: uuid
- organization_id
- user_id
- role_id
- department
- job_title
- status

---

## modules

Stores platform modules.

Fields:

- id: uuid
- name
- slug
- description
- is_active

---

## organization_modules

Stores enabled modules for each organization.

Fields:

- id: uuid
- organization_id
- module_id
- enabled_at

---

## roles

Stores organization-specific roles.

Fields:

- id: uuid
- organization_id
- name
- description

---

## permissions

Stores module permissions.

Fields:

- id: uuid
- module_id
- name
- slug

---

## role_permissions

Stores the relation between roles and permissions.

Fields:

- id: uuid
- role_id
- permission_id

---

## shared_posts

Stores posts inside the shared space.

Fields:

- id: uuid
- organization_id
- user_id
- title
- content
- visibility

---

## notifications

Stores user notifications.

Fields:

- id: uuid
- organization_id
- user_id
- type
- title
- body
- read_at

---

## activity_logs

Stores system activity logs.

Fields:

- id: uuid
- organization_id
- user_id
- action
- metadata: jsonb
- ip_address
