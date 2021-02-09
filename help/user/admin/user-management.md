---
title: Commerce Manager User management
description: Describes the user roles and accessibility levels.
---

# User management

As an Admin manager, you can manage user access to each program you provision, and you can manage the level of access a user has within a program or environment.

## Role-based access control

Magento Cloud Manager provides pre-defined roles that can be assigned at a program level or an environment level.

The _program_ level grants the user a level of access across all environments in the program.

The _environment_ level grants the user a more granular level of access specific to that environment. A user can be an Admin for one environment, but only a contributor for another. By default, a user is not assigned an environment role. The user is automatically granted the access level equal to their assigned program role.

A user can have the following roles:

| Role          | Level                | Description                                                                                                                                |
| ------------- | -------------------- | ------------------------------------------------------------------------------------------------------------------------------------------ |
| Admin         | Program, Environment | (Program manager) Manages the Magento program, and manages users and pipelines.                                                            |
| Contributor   | Program, Environment | (Developer) This is the default assigned program-level role for new users. Develops and tests application code and views logs and reports. |
| License owner | Program              | (Business owner) Provisions new Magento programs and controls productions process.                                                         |
| Read-only     | Program, Environment | View-only access for the program or environment.                                                                                           |
| Tech-admin    | Program              | (Deployment Manager) Manages the Magento environment and deployment operations.                                                            |

<!-- link definitions -->
