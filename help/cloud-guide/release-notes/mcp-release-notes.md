---
title: Cloud Patches for Commerce
description: Learn about the latest improvements to the Magento Cloud Patches package.
---

# Cloud Patches for Commerce

The [Magento Cloud Patches](https://github.com/magento/magento-cloud-patches) package provides a set of required patches which improve the integration of all Adobe Commerce versions with Cloud environments and supports quick delivery of critical fixes.

The Magento Cloud Patches package is a dependency for the ece-tools package and is installed and updated when you install or update the ece-tools package. You can also use and manage Cloud Patches for Commerce as a stand-alone package to apply patches to a Adobe Commerce project that is not on the Cloud platform. These release notes describe the latest improvements to this package.

>[!TIP]
>
>To ensure that your project has all required patches, update to the [latest version of ece-tools](https://devdocs.magento.com/cloud/project/ece-tools-update.html).

>[!NOTE]
>
>See [Apply patches](https://devdocs.magento.com/cloud/project/project-patch.html) for instructions on applying patches to your projects.

The `magento/magento-cloud-patches` package uses the following version sequence: `<major>.<minor>.<patch>`

<!--Add release notes below-->
## v1.0.19 {#latest}

Release date: September 13, 2022

-  **Enhanced support for PHP 8.1**—Fixed compatibility issues with certain PHP 8.1.x versions.

## v1.0.18

Release date: August 11, 2022

Critical patch for Adobe Commerce 2.4.5:

-  **Issue with orders using Braintree payments**—This patch resolves a critical issue preventing admins from placing new orders or reorders.<!-- MCLOUD-9137 -->

See [Admin can't create order/reorder when Braintree payment enabled](https://support.magento.com/hc/en-us/articles/8322266352525).

## v1.0.17

Release date: May 24, 2022

Fixed constraints for security patches in the patches.json file.

## v1.0.16

Release date: March 31, 2022

Critical patch for Adobe Commerce 2.3.3-p1 and later versions:

Updated patches to resolve a **critical** vulnerability resulting in unauthenticated remote code execution.<!-- MCLOUD-8479 -->

See [Adobe Security bulletin APSB22-12](https://helpx.adobe.com/security/products/magento/apsb22-12.html).

## v1.0.15

Release date: March 10, 2022

-  **Support PHP 8.1**—Added support for PHP 8.1 and dropped support for PHP 7.0 and 7.1.
-  **Added patch for Adobe Commerce 2.3.3**—Fixed currency displaying on product page.

## v1.0.14

Release date: February 13, 2022

Critical patch for Adobe Commerce 2.3.3-p1 and later versions:

Added a patch to resolve a **critical** vulnerability resulting in unauthenticated remote code execution.<!-- MCLOUD-8461 -->

See [Adobe Security bulletin APSB22-12](https://helpx.adobe.com/security/products/magento/apsb22-12.html).

## v1.0.13

Release date: October 25, 2021

-  **Update Monolog**—Updated the minimum version required for the `monolog` package to `^2.3`.<!-- ACMP-1263 -->
-  **Incompatible PHP Method**—Fixed incompatible PHP method for Adobe Commerce versions 2.4.3 and 2.3.7-p1.<!-- AC-384 -->
-  **PHP error**—Fixed a `PHP error 'Undefined variable: errorMessage' ...` error that occurred while trying to apply a patch.<!-- ACP2E-138 -->

## v1.0.12

Release date: August 12, 2021

Critical patch for Adobe Commerce 2.4.3 and 2.3.7-p1:

-  **Issue with API rate limiting**—This patch corrects a default rate limit that prevented Web APIs from processing requests with more than 20 items in an array. This patch raises the default value of the rate limit. See the Adobe Commerce [2.4.3 release notes](https://devdocs.magento.com/guides/v2.4/release-notes/commerce-2-4-3.html#apply-mc-43048__set_rate_limits__243patch-to-address-issue-with-api-rate-limiting) and the [2.3.7 release notes](https://devdocs.magento.com/guides/v2.3/release-notes/2-3-7-p1.html#apply-mc-43048__set_rate_limits__237-p1patch-to-address-issue-with-api-rate-limiting).<!-- MC-43048 -->

## v1.0.11

Release date: July 29, 2021

-  **Fixed an issue caused by applying the B2B Layered navigation patch**—For customers that have applied the B2B Layered navigation patch, this fix resolves an `Undefined offset` error that displays on the Search page after switching the Store view.<!--MCLOUD-5287-->

-  **Paypal Checkout patch**—Fixes a Adobe Commerce 2.3.7 issue with PayPal Express where the previously placed order price is displayed.<!--MC-42674-->

-  **Patch category support**—Added support for processing patch categories and origin sources assigned to Quality Patches. The categories allow customers to use filters and sorting to find patches more quickly when using the [Quality Patches Tool](https://github.com/magento/quality-patches) and the Site-wide Analysis Tool (SWAT). <!--MC-38577-->

## v1.0.10

Release date: May 10, 2021

-  **Compatibility with Adobe Commerce 2.3.7**—Resolved composer dependencies conflict for installation on Adobe Commerce 2.3.7.<!--MC-42131-->
-  **Fixed an issue caused by applying a bundled patch multiple times**—Applying a bundled patch (one that includes other deprecated patches) more than once could revert the included deprecated packages. All patches are now applied only once. Trying to apply the same package again shows a message that the patch has already been applied.<!--MC-41912-->
-  **B2B Layered navigation patch**—Fixed another issue that prevented layered navigation from showing all product options when the user enables the B2B Shared Catalog.<!--MCLOUD-7742-->

## v1.0.9

Release date: February 1, 2021

-  **B2B Layered navigation patch**—Fixed the issue that prevented layered navigation from showing all product options when the B2B Shared Catalog was enabled.<!--MCLOUD-6923-->
-  **Compatibility with PHP 7.4**—Fixed a cloud-patches compatibility issue with PHP 7.4.<!--MCLOUD-7367-->
-  **Deprecated patches become visible**—Fixed a cloud-patches issue in which deprecated patches become visible in the patches table after applying a replacement patch that contains the entire contents of the deprecated patch. This could happen if you applied a patch that combined several other patches.<!--MC-40626-->
-  **Silent failures when applying patches**—Fixed a cloud-patches issue in which the `git apply` command silently failed to apply patches in some environments.<!--MC-40529-->

## v1.0.8

Release date: October 14, 2020

-  **Compatibility updates for magento/magento-cloud-patches**—Updated the `symfony` and `semver` version constraints in the `composer.json` file for compatibility with Adobe Commerce 2.4.1 and later releases.<!--MCLOUD-7111-->

## v1.0.7

Release date: October 14, 2020

-  **Redis patches for Adobe Commerce 2.3.0 to 2.3.5, 2.4.0**—Updated the Redis patches to support adding products to a category when implementing a Level 2 cache. <!--MCLOUD-6659-->

-  **Braintree VBE patch**—Fixes an issue that generated an error when an Administrator tried to view a Braintree Settlement Report. <!--MCLOUD-6684-->

-  Now, the `ece-patches apply` command uses the Unix `patch` command to apply patches if Git is not available on the host system. <!--MCLOUD-7069-->

## v1.0.6

Release date:

-  **Redis patches for Adobe Commerce 2.3.0 - 2.3.4**—Optimize communication and improve performance
   -  Reduce size of network transfers between Redis and Adobe Commerce
   -  Fix race conditions on Redis load and write operations
   -  Rewrite base cache adapter to handle errors on save
   -  Decrease Redis CPU consumption<!--MCLOUD-6139-->

-  **Redis patches for Adobe Commerce 2.3.0 - 2.3.5**—Improve performance and fix errors
   -  Fix the Cache lock implementation to prevent infinite locks
   -  Improve the current locking mechanism
   -  Implement signed locks to prevent unlock from parallel requests
   -  Fix the following error that occurs on Redis write operation: `OOM command not allowed when used memory > maxmemory`
   -  Fix processing for clean cache by `cat_p` tag that runs during product updates<!--MCLOUD-6110-->

-  Fixed an issue that caused an error when applying the required `amzn/amazon-pay-module` patch to Adobe Commerce on cloud infrastructure projects with Adobe Commerce v2.2.6 or 2.3.5, which do not include this module. Now, the patching process skips the `amzn/amazon-pay-module` patch if the module is not installed.<!--MCLOUD-6588-->

## v1.0.5

Release date: June 26, 2020

-  **Redis performance improvements**—Adds Redis optimization features to Adobe Commerce versions 2.3.3 and 2.3.4. These fixes were included in the Adobe Commerce version 2.3.5 release. See [Performance boosts](https://devdocs.magento.com/guides/v2.3/release-notes/release-notes-2-3-5-commerce.html#performance-boosts) in the _Adobe Commerce 2.3.5 Release Notes_.<!--MCLOUD-5771-->

-  **New Relic log enricher**—Adds the Monolog ProcessorInterface required to support improvements to New Relic logging capabilities introduced in Cloud Components of Commerce version 1.0.4. This patch is required to deploy Adobe Commerce 2.1.x. If the patch is not applied, the build fails during the `di:compile` process.<!--MCLOUD-6029-->

## v1.0.4

Release date: May 12, 2020

-  **Amazon Pay checkout**—Fixes an issue with the Amazon Pay payment widget that prevented customers from changing the payment method on the _Review & Payments_ step during the checkout process.<!--MCLOUD-5930-->

-  **Product display on Category page**—Fixes an issue that prevented products from displaying on the category page in _Show all pages_ view.<!--MCLOUD-5684-->

-  **Page Builder image upload**—Fixes a Page Builder interface issue that sometimes caused the following error when uploading images to the image gallery: `Destination folder is not writable or does not exist`<!--MCLOUD-5837-->

-  **Suppress unnecessary sitemap generation warnings**—Adds a retry attempt when errors occur during sitemap generation and skips customer email notification in cases where errors can be recovered automatically.<!--MCLOUD-3025-->

-  **Site performance improvement**—Fixes a performance issue with the `Magento\Framework\App\DeploymentConfig\Reader::load` function, which periodically experienced long load times that affected site performance. <!--MCLOUD-5650-->

-  Updated patch assignment for payment method patches to target the payment modules instead of the Magento base package (magento/magento2-base) so that the payment patches are applied only if the payment modules exist.<!--MCLOUD-5666-->

-  Updated patches for compatibility with Magento Open Source.<!--MCLOUD-5701-->

## v1.0.3

Release date: April 28, 2020

-  Added fix for the "FPC is getting disabled during deployments" patch to support Adobe Commerce 2.3.5.

## v1.0.2

Release date: February 27, 2020

This release includes the following patches and critical fixes:

-  **Compatibility updates for magento/magento-cloud-patches**

   -  Updated the `symfony` and `semver` version constraints in the `composer.json` file for compatibility with Adobe Commerce 2.4 and later releases.<!--MAGECLOUD-5127-->

   -  Updated constraints in `composer.json` for compatibility with `ece-tools` 2002.0.22 and later 2002.0.x releases.

-  **PayPal Express Checkout**—Published on February 12, 2020, this patch resolves an issue that affects orders placed with PayPal Express Checkout where the shipping address for the order specifies a country region that has been manually entered into the text field rather than selected from the drop-down menu on the Shipping page. See the complete patch description on the [patch download page](https://magento.com/tech-resources/download#download2353).

-  **Application deployment fix**—Added a patch to fix an issue that disabled the full page cache during the deployment process. This patch applies to Adobe Commerce 2.3.2 and later releases.

-  **Scope parameter for Async/Bulk API**—Updated this patch to fix a syntax error in the `composer.json` file. This patch applies to Magento Open Source 2.3.1 and 2.3.2. See the complete patch description on the [patch download page](https://magento.com/tech-resources/download#download2312).

## v1.0.1

Release date: February 6, 2020

We have included all Magento Open Source 2.x patches from the [software downloads page](https://magento.com/tech-resources/download) in the magento/magento-cloud-patches v1.0.1 release. If you copied any patches into your project previously, remove them to avoid conflicts.

This release includes the following patches and critical fixes:

-  **Fix cron deadlocks and improve cron locking**—

   -  Fixes an issue with some cron jobs not running due to an incorrect status value in the `cron_schedule` table. Now, we use the Adobe Commerce lock framework to check and update cron job status instead of using the `cron_schedule` table. Cron jobs that have ended with an error status are retried during the next cron run instead of waiting 24 hours.

   -  Adds a _retry_ operation to avoid deadlock during updates to the data in the `cron_schedule` table.

-  **Updated `magento/magento-cloud-patches` to include all available patches for Magento Open Source 2.x**—Updated the magento/magento-cloud-patches package to include all Magento Open Source 2.x patches available on the [software downloads page](https://magento.com/tech-resources/download). If you copied any Magento Open Source patches into your Adobe Commerce on cloud infrastructure project previously, remove them to avoid conflicts.<!--MAGECLOUD-4606-->

-  **Elasticsearch catalog pagination fix** —Replaced the Elasticsearch catalog pagination patch delivered in magento/magento-cloud-patches v1.0 with a more effective fix.<!--MAGECLOUD-4847-->

-  **Page Builder patches**—In Cloud Patches for Commerce 1.0.0, we bundled Page Builder patches to address a known Page Builder remote code execution (RCE) vulnerability, with the initial fix based on Adobe Commerce 2.3.3. We have updated these patches with a more stable implementation based on Adobe Commerce 2.3.4., which includes multiple optimizations for fixing the issue.<!--MAGECLOUD-4884-->

   If you have the magento/magento-cloud-patches 1.0.0 package, you are still protected from the Page Builder RCE vulnerability issues. If you update to 1.0.1 or later, you have a better implementation of the same fix.

## v1.0.0

Release date: November 14, 2019

This is the first release of the [`magento/magento-cloud-patches`](https://github.com/magento/magento-cloud-patches) package, which is a new dependency for the `ece-tools` package version 2002.0.22 or later releases.

This release includes the following patches and critical fixes:

-  **Page Builder security patches for 2.3.1.x and 2.3.2.x releases**—Fixes an issue in Page Builder preview that allows unauthenticated users to access some templating methods that can be used to trigger arbitrary code execution over the network (RCE) resulting in global information leaks. This issue can occur when using unsupported versions of Page Builder with Adobe Commerce versions 2.3.1 and 2.3.2.<!--MAGECLOUD-4649-->

-  **MSI patches**—Fixes issues that caused indexing errors and performance issues when using default inventory settings for managing stock.<!--MAGECLOUD-4428-->

-  **Backward Compatibility of new Mail Interfaces**-Fixes a backward incompatibility issue caused by the `Magento\Framework\Mail\EmailMessageInterface` PHP interface introduced in Adobe Commerce v2.3.3. In the scope of this patch, the new `EmailMessageInterface` inherits from the old `MessageInterface`, and Adobe Commerce core modules are reverted to depend on `MessageInterface`.<!--MAGECLOUD-4422-->

-  **Catalog pagination does not work on Elasticsearch 6.x**—Fixes a critical issue with search result pagination that affects customers using Elasticsearch 6.x as the catalog search engine.<!--MAGECLOUD-4448-->
