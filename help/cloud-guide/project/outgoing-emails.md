---
title: Configure outgoing emails
description: Learn how to enable outgoing emails for Adobe Commerce on cloud infrastructure.
exl-id: 814fe2a9-15bf-4bcb-a8de-ae288fd7f284
---
# Configure outgoing emails

By default, email support is **disabled** on Staging and Production environments. You must enable email support on an environment to send emails including Welcome, password reset, and two-factor authentication emails for Cloud project users.

You can manage email support for each Cloud project environment from the Project Web Interface or from the command line.

-  On `master` and integration branches, use the **[!UICONTROL Outgoing emails]** toggle in the _Configure environment_ view to enable or disable email support.

-  On Production and Staging environments, or other environments where the **Outgoing emails** toggle is not available in the Project Web Interface, change the configuration using the [`magento-cloud` CLI](../dev-tools/cloud-cli.md) `environment:info` command to set the `enable_smtp` property.

   Enabling SMTP updates the `MAGENTO_CLOUD_SMTP_HOST` environment variable with the IP address of the SMTP host for sending mail.

{{redeploy-warning}}

**To manage email support from the Project Web Interface**:

1. Log in to [the Project Web Interface](https://accounts.magento.cloud/user/)
1. Click on the project.
1. In the left environment list, click the name of the branch.
1. To enable or disable outgoing emails, toggle _Outgoing emails_ **On** or **Off**.

   ![Enable outgoing email configuration](../../assets/outgoing-emails.png)

After you change the setting, the environment builds and deploys with the new configuration.

**To manage email support from the command line**:

1. Check the current email configuration in the Project Web Interface.

1. If needed, change the email configuration.

1. On your local workstation, change to your project directory.

1. Change the email support configuration by setting the `enable_smtp` environment variable to `true` or `false`.

   ```bash
   magento-cloud environment:info --refresh -p <project-id> -e <environment-id> enable_smtp true
   ```

   Wait for the environment to build and deploy.

1. Verify that the email works; send a test email to an address that you can check.

      ```bash
      php -r 'mail("mail@example.com", "test message", "just testing", "From: tester@example.com");'
      ```
