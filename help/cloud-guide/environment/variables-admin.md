---
title: ADMIN variables
description: See a list of environment variables used when installing Adobe Commerce on cloud infrastructure.
feature: Cloud, Configuration, Install, Roles/Permissions
role: Developer
exl-id: 2829a9dc-40bb-4665-886e-a56d98468fc1
---
# Admin variables

Users that have administrative access to the Adobe Commerce on cloud infrastructure project can use the following project environment variables to override the configuration settings for the administrative user account to access the Admin UI.

## Admin credentials

You can override Admin user credentials during Commerce installation with the ADMIN variables in the following table.

If you want to change the values after installation, connect to your environment using SSH and use the Adobe Commerce CLI [`admin:user` command](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/tutorials/admin.html) to create or edit the Admin user credentials.

| Variable       | Default                     | Description |
| -------------- | --------------------------- | ----------- |
|`ADMIN_USERNAME`| License Owner email address | A username for the administrative user with the ability to create other users, including administrative users.|
|`ADMIN_EMAIL`   |                             | Email address for the administrative user. This address is used to send password reset notifications.|
|`ADMIN_PASSWORD`|                             | Password for the administrative user. When the project is created, a random password is generated and an email is sent to the License Owner. During project creation, the License Owner should have already changed the password. Contact the License Owner for the updated password.|
|`ADMIN_LOCALE`  | `en_US`                     | The default locale used by the Admin.|

## Admin URL

Use the following environment variable to secure access to your Admin UI. If specified, this value overrides the default URL during installation.

`ADMIN_URL`—The relative URL to access the Admin UI. The default URL is `/admin`. For security reasons, Adobe recommends that you change the default to a unique, custom Admin URL that is not easy to guess.

### Change the Admin URL

Adobe recommends changing the environment-level variable for the Admin URL after installation. Configure this setting for security reasons before branching from the cloned `master` environment. All branches created from the `master` branch inherit the environment-level variables and their values.

Use the `magento-cloud variable:update` command to update the variable value. (The `variable:set` command has been deprecated and is not available.) The following example updates the ADMIN_URL to `newAdmin_A8v10`:

```bash
magento-cloud variable:update ADMIN_URL --value newAdmin_A8v10 -e master
```

>[!NOTE]
>
>The `ADMIN_URL` value accepts letters (a-z or A-Z), numbers (0-9), and the underscore character (_) for a custom admin path. Spaces or other characters are **not** accepted.

**To change the URL using the Project Web Interface**:

1. Log in to [the Project Web Interface](https://console.magento.cloud).

1. Select a project from the _All projects_ list.

1. In the project overview, select the environment and click the configuration icon.

   ![Project configuration](../../assets/icon-configure.png){width="36"}

1. Select the **Variables** tab.

1. Click **Create Variable**.

1. Enter the following:

    - **Variable name** = `ADMIN_URL`
    - **value** = New URL. For example, set the Admin URL to `magento_A8v10`.

    By default, `Available during runtime` and `Make inheritable` are selected.

1. Click **Create variable** and wait until deployment completes. This button is only visible when the required fields contain values.
