---
title: Global variables
description: List of variables that control actions in the deployment process.
---

# Global variables

Global variables control actions across each phase of the Commerce deployment process: build, deploy, and post-deploy.

## `MIN_LOGGING_LEVEL`

Override the minimum logging level for all output streams without updating the code and to help when troubleshooting problems with deployment. For example, if your deployment fails, you can use this variable to increase the logging granularity.

## `SCD_ON_DEMAND`

Enable generation of static content when requested by a user, which is ideal for the development and testing workflow because it decreases deployment time.

## `SCD_MAX_EXECUTION_TIME`

Allows users to increase the maximum expected execution time for static content deployment. By default, the maximum expected execution is set at 400 seconds; however, in some scenarios users might need more time to complete the static content deployment.

## `SCD_USE_BALER`

[Baler][] is a Commerce module that scans generated JavaScript code and creates an optimized JavaScript bundle. Deploying the optimized bundle to your site can reduce the number of network requests when loading your site and improve page load times.

## `SKIP_HTML_MINIFICATION`

Enable or disable the copying of static view files to the `<magento_root>/init/` directory at the end of the build stage. If enabled (`true`), files are not copied and HTML minification is available on request.

- `false`—Copies the `view_preprocessed` directory to the `<magento_root>/init/ directory` at the end of the build phase, and restores the directory in the `<magento_root>/var` directory at the beginning of the deploy phase.
- `true`—Enables on-demand HTML minification; does not copy the `<magento_root>var/view_preprocessed` to the `<magento_root>/init/` directory at the end of the build phase. Reduces downtime when deploying to staging and production environments.

## `X_FRAME_CONFIGURATION`

Change the X-Frame-Options header configuration for your Commerce site. This configuration controls how the browser renders a page in a `<frame>`, `<iframe>`, or `<object>`. Use one of the following options:

- `DENY`—Page cannot be displayed in a frame.
- `SAMEORIGIN`—(_default_) Page can be displayed only in a frame on the same origin as the page.
- `ALLOW-FROM <uri>`—Page can be displayed only in a frame on the specified origin.

<!-- link definitions -->

[Baler]: https://github.com/magento/baler
