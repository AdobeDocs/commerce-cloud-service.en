---
title: Update the Ece-tools package
description: Learn how to upgrade the Ece-tools package to take advantage of the latest fixes and features applied to Adobe Commerce on cloud infrastructure.
---

# Update the Ece-tools package

An update to the `ece-tools` package also updates the other [Cloud Suite for Commerce packages][release-notes], which are dependencies for `ece-tools`. Therefore, you must use a version of Adobe Commerce on cloud infrastructure that supports the `ece-tools` package.

{{ece-tools-package}}

**Prerequisites**:

-  Before you update `ece-tools`, review the [Cloud Suite for Commerce release notes][release-notes].
-  If you are updating from `ece-tools` 2002.0.22 or earlier to 2002.1.0, review [Backward incompatible changes][] and make any required changes to your Adobe Commerce on cloud infrastructure project.
-  Review [Upgrades and Patches][] to determine the ece-tools versions compatible with your Adobe Commerce on cloud infrastructure project.

{{upgrade-tip}}

**To update the `ece-tools` package**:

1. On your local workstation, perform an update using Composer.

   ```bash
   composer update magento/ece-tools --with-dependencies
   ```

   >[!NOTE]
   >
   >If you cannot update beyond `ece-tools` version 2002.0.8, see [Upgrade project to use Ece-tools package](install-package.md).

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

1. After test validation, merge this branch to the Integration branch.

<!-- link definitions -->

[Backward incompatible changes]: https://devdocs.magento.com/cloud/release-notes/backward-incompatible-changes.html
[release-notes]: https://devdocs.magento.com/cloud/release-notes/cloud-tools.html
[Upgrades and Patches]: https://devdocs.magento.com/cloud/project/project-upgrade-parent.html
