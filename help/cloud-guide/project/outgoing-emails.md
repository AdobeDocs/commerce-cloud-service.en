---
title: Configure outgoing emails
description: Learn how to enable outgoing emails for Adobe Commerce on cloud infrastructure.
---

# Configure outgoing emails

By default, email support is **disabled** on Staging and Production environments. You must enable email support on an environment to send emails including Welcome, password reset, and two-factor authentication emails for Cloud project users.

You can manage email support for each Cloud project environment from the Project Web Interface or from the command line.

-  On `master` and integration branches, use the **[!UICONTROL Outgoing emails]** toggle in the Configure environment view to enable or disable email support.

-  On Production and Staging environments, or other environments where the **Outgoing emails** toggle is not available in the Project Web Interface, change the configuration using the [`magento-cloud` CLI](https://devdocs.magento.com/cloud/reference/cli-ref-topic.html) `environment:info` command to set the `enable_smtp` property.

   Enabling SMTP updates the `MAGENTO_CLOUD_SMTP_HOST` environment variable with the IP address of the SMTP host for sending mail.

{{redeploy-warning}}

**To manage email support from the Project Web Interface**:

1. Log in to [the Project Web UI](https://accounts.magento.cloud/user/)
1. Click on the project.
1. In the left environment list, click the name of the branch.
1. To enable or disable outgoing emails, toggle _Outgoing emails_ **On** or **Off**.

   ![Enable outgoing email configuration](../../assets/outgoing-emails.png)

After you change the setting, the environment builds and deploys with the new configuration.

**To manage email support from the command line**:

1. Check the current email configuration in the Project Web Interface.

1. If needed, change the email configuration.

1. From the command line, change to the directory where you [cloned your Cloud project](https://devdocs.magento.com/cloud/before/before-setup-env-2_clone.html#clone-the-project).

1. Log in to the project.

   ```bash
   magento-cloud login
   ```

1. If you do not have the project ID and environment ID for the environment, use the following commands to get the values.

   ```bash
   magento-cloud projects
   ```

   ```bash
   magento-cloud environments -p <project-id>
   ```

1. Change the email support configuration by setting the `enable_smtp` environment variable to `true` or `false`.

   ```bash
   magento-cloud environment:info --refresh -p <project-id> -e <environment-id> enable_smtp true
   ```

   Wait for the environment to build and deploy.

1. Verify that the email works; send a test email to an address that you can check.

      ```bash
      php -r 'mail("mail@example.com", "test message", "just testing", "From: tester@example.com");'
      ```

