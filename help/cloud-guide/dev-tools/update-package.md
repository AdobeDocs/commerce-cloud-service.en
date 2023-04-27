---
title: Update the ECE-Tools package
description: Learn how to upgrade the ECE-Tools package to take advantage of the latest fixes and features applied to Adobe Commerce on cloud infrastructure.
feature: Cloud, Upgrade
exl-id: 7cce45eb-ae53-4468-b16d-4f4d3422ac52
---
# Update the ECE-Tools package

An update to the `ece-tools` package also updates the other [Cloud Tools Suite for Commerce packages](../release-notes/cloud-tools-suite.md), which are dependencies for `ece-tools`. Therefore, you must use a version of Adobe Commerce on cloud infrastructure that supports the `ece-tools` package.

{{ece-tools-package}}

**Prerequisites**:

-  Before you update `ece-tools`, review the [Cloud Tools Suite for Commerce release notes](../release-notes/cloud-tools-suite.md).
-  If you are updating from `ece-tools` 2002.0.22 or earlier to 2002.1.0, review [Backward incompatible changes](../release-notes/backward-incompatible-changes.md) and make any required changes to your Adobe Commerce on cloud infrastructure project.
-  Review [Upgrades and Patches](../development/commerce-version.md#upgrade-from-older-versions) to determine the ECE-Tools versions compatible with your Adobe Commerce on cloud infrastructure project.

{{upgrade-tip}}

**To update the `ece-tools` package**:

1. On your local workstation, perform an update using Composer.

   ```bash
   composer update magento/ece-tools --with-dependencies
   ```

   >[!NOTE]
   >
   >If you cannot update beyond `ece-tools` version 2002.0.8, see [Upgrade project to use ECE-Tools package](install-package.md).

1. Add, commit, and push code changes.

   ```bash
   git add -A
   ```

   ```bash
   git commit -m "Update magento/ece-tools"
   ```

   ```bash
   git push origin <branch-name>
   ```

1. After test validation, merge this branch to the integration branch.
