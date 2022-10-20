---
title: Custom theme
description: Learn how to install a custom theme with Adobe Commerce on cloud infrastructure.
---

# Custom theme

You can install one or multiple themes to use for one or all of your stores and sites in your project. Themes include multiple static files including images, fonts, CSS, JavaScript, PHP, and more to fully design your stores. You can add the theme by either extracting its code to the file system or using Composer.

## Install a theme manually

To install a theme manually, you must have the theme's code in a compressed archive or in a directory structure similar to the following:

```text
<VendorName>
  ├── composer.json
      ├── etc
      │   └── view.xml
      ├── media
      ├── registration.php
      ├── theme.xml
      └── web
          ├── css
          │   └── source
          ├── fonts
          ├── images
          └── js
```

**To install a theme manually**:

1. Copy the theme's code under `<Project root dir>/app/design/frontend` for a storefront theme or `<Project root dir>/app/design/adminhtml` for an Admin theme. Verify that the top-level directory is `<VendorName>`; otherwise, the theme does not install properly.

   ```bash
   cp -r ExampleTheme <project-root>/app/design/frontend
   ```

1. Confirm the theme copied to the correct place.

   *  Storefront theme: `ls <project-root>/app/design/frontend`
   *  Admin theme: `ls <project-root>/app/design/adminhtml`

   A sample follows:

      ExampleTheme Adobe Commerce

1. Add and commit files.

   ```bash
   git add -A && git commit -m "Add theme"
   ```

1. Push the files to your branch.

   ```bash
   git push origin <branch name>
   ```

1. Wait for deployment to complete.
1. Log in to the Admin.
1. Click **Content** > Design > **Themes**.

   The theme displays in the right pane.

## Install a theme using Composer

Installing a theme using Composer is the same as installing any other extension using Composer. See [Install, manage, and upgrade modules](https://devdocs.magento.com/cloud/howtos/install-components.html) for details.

To install a theme using Composer:

1. Purchase the theme from Commerce Marketplace.
1. Get the theme's Composer name.
1. Change to your Adobe Commerce root directory and enter the command:

   ```bash
   composer require <vendor>/<name>:<version>
   ```

   For example,

   ```bash
   composer require zero1/theme-fashionista-theme:1.0.0
   ```

1. Wait for dependencies to update.
1. Enter the following commands:

   ```bash
   git add -A && git commit -m "Add theme"
   ```

   ```bash
   git push origin <branch name>
   ```

1. Log in to the Admin.
1. Click **Content** > Design > **Themes**.

   The theme displays in the right pane.

## Multiple themes

When using multiple themes, such as different themes per locale, review the `SCD_MATRIX` environment variable for customizing theme deployment. See the [build](../environment/variables-build.md#scd_matrix) or [deploy](../environment/variables-deploy.md#scd_matrix) stages in the [environment configuration](../environment/configure-env-yaml.md).
