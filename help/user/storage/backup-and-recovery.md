---
title: Backup database
description: Step through the process of backing up your Commerce database.
---
# Backup

The backup and recovery approach uses a high-availability architecture combined with full-system backups. The backups replicate each Commerce Program—all data, code, and assets—across each AWS or Azure Availability Zone.

In addition to the redundancy of the high-availability architecture, you can schedule incremental backups or perform a backup on demand. By default, backups are scheduled to run every hour.

After a 24-hour period, the infrastructure retains the backups according to the following schedule:

| Time Period         | Backup Retention Policy |
| ------------------- | ----------------------- |
| Days 1 through 3    | Each backup             |
| Days 4 through 6    | One backup per day      |
| Weeks 2 through 6   | One backup per week     |
| Weeks 8 through 12  | One bi-weekly backup    |
| Weeks 12 through 22 | One backup per month    |

Commerce creates the backup using TBD.

## Recover backup

There are two ways to recover backups:

- Manual
- Automated
