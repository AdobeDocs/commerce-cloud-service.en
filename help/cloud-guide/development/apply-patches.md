---
title: Apply patches
description: Learn how to apply patches in the Adobe Commerce on cloud infrastructure project.
feature: Cloud, Upgrade
exl-id: a7bf672f-7b89-45cd-8436-e885bca9029d
---
# Apply patches

[Cloud Patches for Commerce](https://github.com/magento/magento-cloud-patches) and the [Quality Patches Tool](https://github.com/magento/quality-patches) deliver patches to your installed Adobe Commerce application.

-  The Cloud Patches for Commerce package delivers required patches with critical fixes
-  Quality Patches deliver optional, low-impact quality fixes as [individual patches](https://experienceleague.adobe.com/docs/commerce-operations/release/planning/versioning-policy.html#individual-patch) that do not contain backward incompatible changes

See [Available Patches](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) in the _Commerce Operations Tools Guide_ to review a full list of released patches.

Both packages improve the integration of all Adobe Commerce versions with Cloud environments and support quick delivery of critical, optional, and custom fixes. You can use these packages to apply, revert, and view general information about all individual patches that are available for Commerce.

>[!TIP]
>
>You can use the [Quality Patches Tool](https://experienceleague.adobe.com/tools/commerce-quality-patches/index.html) and Cloud Patches for Commerce as stand-alone packages for Magento Open Source and Adobe Commerce projects. We recommend using the Quality Patches Tool for non-Cloud projects.

When you deploy changes to the remote environment, `ECE-Tools` uses `magento/magento-cloud-patches` and `magento/quality-patches` to check for pending patches and applies them automatically in the following order:

1. Apply all required Commerce patches included in the Cloud Patches for Commerce package.
1. Apply selected optional Commerce patches included in the Quality Patches Tool.
1. Apply custom patches in the `/m2-hotfixes` directory in alphabetical order by patch name.

>[!NOTE]
>
>When you update `ECE-Tools` or the Cloud Patches for Commerce package, the latest required patches are applied the next time you deploy your project, or you can deploy them immediately using the `ece-patches apply` CLI command and redeploying your Cloud environment. You cannot skip [required patches](https://github.com/magento/magento-cloud-patches/tree/develop/patches) during the deployment process.

## Prerequisites

{{upgrade-tip}}

The Quality Patches Tool is a dependency for the Cloud Patches for Commerce and ECE-Tools packages. To apply the latest patches, you must have [the latest version of ECE-Tools](../dev-tools/update-package.md) installed. The minimum required version of ECE-Tools is 2002.1.2.

## View available patches and status

To view the list of available individual patches:

```bash
php ./vendor/bin/ece-patches status
```

Sample response:

```terminal
More detailed information about patches you can find on https://support.magento.com/
╔════════════════╤═════════════════════════════════════════════════╤══════════╤═════════════╤═════════════════════════════════╗
║ Id             │ Title                                           │ Type     │ Status      │ Details                         ║
╠════════════════╪═════════════════════════════════════════════════╪══════════╪═════════════╪═════════════════════════════════╣
║ MAGECLOUD-5069 │ FPC is getting disabled during deployments      │ Required │ Applied     │ Affected components:            ║
║                │                                                 │          │             │  - magento/module-page-cache    ║
╟────────────────┼─────────────────────────────────────────────────┼──────────┼─────────────┼─────────────────────────────────╢
║ MCLOUD-5650    │ Hold deployment config after reading from file  │ Required │ Applied     │ Affected components:            ║
║                │                                                 │          │             │  - magento/framework            ║
╟────────────────┼─────────────────────────────────────────────────┼──────────┼─────────────┼─────────────────────────────────╢
║ MCLOUD-5684    │ Pagination Not working - product_list_limit=all │ Required │ Applied     │ Affected components:            ║
║                │                                                 │          │             │  - magento/module-elasticsearch ║
╟────────────────┼─────────────────────────────────────────────────┼──────────┼─────────────┼─────────────────────────────────╢
║ MC-65837       │ Fix load balancer issue                         │Deprecated│ Applied     │ Recommended replacement: MC-1   ║
║                │                                                 │          │             │ Affected components:            ║
║                │                                                 │          │             │  - magento/framework            ║
╟────────────────┼─────────────────────────────────────────────────┼──────────┼─────────────┼─────────────────────────────────╢
║ BUNDLE-2554    │ Set Payment info bug                            │ Required │ Not applied │ Affected components:            ║
║                │                                                 │          │             │  - amzn/amazon-pay-module       ║
╟────────────────┼─────────────────────────────────────────────────┼──────────┼─────────────┼─────────────────────────────────╢
║ MC-1           │ Fixes issue 1                                   │ Optional │ Applied     │ Affected components:            ║
║                │                                                 │          │             │  - magento/module-cms           ║
╟────────────────┼─────────────────────────────────────────────────┼──────────┼─────────────┼─────────────────────────────────╢
║ MC-2           │ Fixes issue 2                                   │ Optional │ Not applied │ Affected components:            ║
║                │                                                 │          │             │  - magento/module-cms           ║
╟────────────────┼─────────────────────────────────────────────────┼──────────┼─────────────┼─────────────────────────────────╢
║ MC-3           │ Fixes issue 3                                   │ Optional │ Not applied │ Required patches:               ║
║                │                                                 │          │             │  - MC-2                         ║
║                │                                                 │          │             │ Affected components:            ║
║                │                                                 │          │             │  - magento/module-cms           ║
╟────────────────┼─────────────────────────────────────────────────┼──────────┼─────────────┼─────────────────────────────────╢
║ N/A            │ ../m2-hotfixes/MDVA_custom__2.3.5_ce.patch      │ Custom   │ N/A         │ Affected components:            ║
║                │                                                 │          │             │  - magento/module-framework     ║
╚════════════════╧═════════════════════════════════════════════════╧══════════╧═════════════╧═════════════════════════════════╝
Magento 2 Enterprise Edition, version 2.3.5.0
```

The status table contains the following types of information:

- **Type**:
    - `Optional`—All patches from the Quality Patches Tool and the Cloud Patches package are optional for Adobe Commerce and Magento Open Source installations. For Adobe Commerce on cloud infrastructure, all patches are optional.
    - `Required`—All patches from the Cloud Patches for Commerce package are required for Cloud customers.
    - `Deprecated`—The individual patch is marked as deprecated and we recommend reverting it if you have applied it. After you revert a deprecated patch, it will no longer be displayed in the status table.
    - `Custom`—All patches from the 'm2-hotfixes' directory.

- **Status**:
    - `Applied`—The patch has been applied.
    - `Not applied`—The patch has not been applied.
    - `N/A`—The status of the patch cannot be defined due to conflicts.

- **Details**:
    - `Affected components`—The list of affected modules.
    - `Required patches`—The list of required patches (dependencies).
    - `Recommended replacement`—The patch that is a recommended replacement for a deprecated patch.

## Apply a patch in a local environment

You can apply patches manually in a local environment and test them before you deploy.

**To apply individual patches in a local development environment**:

1. Add the 'QUALITY_PATCHES' variable to the `.magento.env.yaml` file and list the required patches underneath.

   ```yaml
   stage:
     build:
       QUALITY_PATCHES:
         - MCTEST-1002
         - MCTEST-1003
   ```

1. From the project root, apply the patches.

   ```bash
   php ./vendor/bin/ece-patches apply
   ```

   The `ece-patches apply` command applies patches in the following order:
   -  Required patches
   -  Optional individual patches
   -  Custom patches from the `/m2-hotfixes` directory

1. Clear the cache.

   ```bash
   php ./bin/magento cache:clean
   ```

1. Test the patches, make any necessary changes to custom patches.

## Apply a patch in a remote environment

>[!WARNING]
>
>We strongly recommend testing all patches in an Integration or Staging environments before deploying to the Production environment.

**To apply patches in a remote environment**:

1. Add the `QUALITY_PATCHES` variable to the `.magento.env.yaml` file and list the required patches underneath.

   ```yaml
   stage:
     build:
       QUALITY_PATCHES:
         - MCTEST-1002
         - MCTEST-1003
   ```

   >[!NOTE]
   >
   >After upgrading to a new version of Adobe Commerce, you must re-apply patches if the patches are not included in the new version.

1. Add, commit, and push the updated `.magento.env.yaml` file.

   ```bash
   git add .magento.env.yaml
   ```

   ```bash
   git commit -m "Apply patch"
   ```

   ```bash
   git push origin <branch-name>
   ```

## Apply a custom patch

When you deploy, `ECE-Tools` applies all Adobe patches and any custom patches that you add to the `/m2-hotfixes` directory in the project root.

>[!NOTE]
>
>All patch file names must end with the `.patch` extension.

**To apply and test a custom patch on a Cloud environment**:

1. In the project root, create a directory called `m2-hotfixes` if it does not exist

   ```bash
   mkdir m2-hotfixes
   ```

1. Copy the patch file to the `/m2-hotfixes` directory.

1. Add, commit, and push code changes.

   ```bash
   git add m2-hotfixes/
   ```

   ```bash
   git commit -m "Apply patch"
   ```

   ```bash
   git push origin <branch-name>
   ```

   >[!NOTE]
   >
   >Make sure to test all patches in a pre-production environment. For Adobe Commerce on cloud infrastructure, you can create branches with the `magento-cloud environment:branch <branch-name>` CLI command.

## Revert a custom patch

To revert or uninstall a previously applied custom patch:

1. Delete the patch file from the `/m2-hotfixes` directory.

1. Add, commit, and push code changes.

   ```bash
   git add m2-hotfixes/
   ```

   ```bash
   git commit -m "Revert patch"
   ```

   ```bash
   git push origin <branch-name>
   ```

   >[!NOTE]
   >
   >Make sure to test in a pre-production environment. For Adobe Commerce on cloud infrastructure, you can create branches with the `magento-cloud environment:branch <branch-name>` CLI command.

## Apply patches to a non-Cloud project

Use the [Quality Patches Tool](https://github.com/magento/quality-patches) for Magento Open Source and Adobe Commerce projects.

## Revert a patch in a local environment

You can revert all previously applied patches in a local development environment using the `ece-patches` CLI.

To revert all applied patches:

```bash
php ./vendor/bin/ece-patches revert
```

This command reverts all patches in the following order:

-  Reverts all applied custom patches from the /m2-hotfixes directory.
-  Reverts all applied optional individual patches.
-  Reverts all applied required patches.

## Logging

The Quality Patches Tool logs all operations to the `<Project_root>/var/log/patch.log` file.
