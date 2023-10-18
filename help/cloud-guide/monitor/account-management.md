---
title: New Relic Account Management
description: Learn how to access your New Relic account and manage access, integrations, and tool usage for your Adobe Commerce on cloud infrastructure project.
feature: Cloud, Observability
role: Admin
exl-id: ee639e2e-4074-4384-8f68-152bc3bac93b
---
# New Relic account management

When Adobe provisions your cloud infrastructure project, the License Owner receives an email from New Relic with credentials and instructions for accessing the New Relic account. If you did not receive the email, use the License Owner email address to reset the New Relic password.

## Manage user access

A New Relic account can have only one person assigned to the Owner role. If you must change the account owner, assign the Admin role to the current Owner, and then assign the Owner role to another user. See [Update the account owner](https://docs.newrelic.com/docs/accounts/original-accounts-billing/original-users-roles/users-roles-original-user-model/) in the _New Relic documentation_ for instructions.

Guidelines for managing New Relic access:

- Project Owners and Admin users can add and remove users from the New Relic account.
- Do not create more than five full-access **Users**.
- Only grant full access to users that strictly require access to the complete feature set.
- There is no specific guidance on free **Restricted** users.

>[!TIP]
>
>Before assigning the Owner role to a user, verify that the user exists on the New Relic account for Adobe Commerce on cloud infrastructure. If you must add the user to that account and an existing account Owner or Admin cannot help, any user with access to the [Adobe Partnership Owner Account](https://account.newrelic.com/accounts/1311131/users) for New Relic can add users on behalf of the customer.

Add at least one **Admin** user to your New Relic account that can manage all access, integrations, and tool usage.

**To access User management in New Relic**:

1. Log in to your [New Relic account](https://login.newrelic.com/login).

1. Select your username from the lower left navigation.

1. Click **[!UICONTROL Administration]** and select one of the following from the list:

   - **[!UICONTROL User management]** to add a user and manage active users and pending invites.

   - **[!UICONTROL Access management]** to manage user groups, roles, and accounts.

See [User management](https://docs.newrelic.com/docs/accounts/accounts-billing/new-relic-one-user-management/user-management-ui-and-tasks/) in the _New Relic_ documentation.

## Configure New Relic for Starter environment

>[!NOTE]
>
>**Pro environments** are preconfigured to use New Relic services and can skip enable and connect instructions. If New Relic APM is not installed on the Staging and Production environments or New Relic Infrastructure is not available in the Production environment, [submit an Adobe Commerce Support ticket](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) to request installation.

For Starter environments, you must check the `.magento.app.yaml` file to verify that the `runtime` section includes the New Relic extension. If the extension has not been configured, add the following:

> `.magento.app.yaml`

```yaml
runtime:
    extensions:
        - newrelic
```

### Apply license key

To connect a Cloud environment to New Relic, add the New Relic license key to the environment.

- For **Pro projects**, Adobe adds the license key to your Production and Staging environments during the provisioning process. You can log in to your [New Relic account](https://login.newrelic.com/login) to verify connectivity between your Adobe Commerce on cloud infrastructure site and New Relic.

- For **Starter projects**, you have a New Relic license key that supports up to _three_ environments. You must add the key to your environment configurations manually. Starter environments are not pre-provisioned to use the New Relic service.

For Starter environments, enable the New Relic integration by adding the New Relic license key to the environment configuration. Add the key to the Staging and Production environments and one other environment of your choice. Only the New Relic license key is required for configuration. You can find information about additional configuration options in the [New Relic Reporting](https://experienceleague.adobe.com/docs/commerce-admin/config/general/new-relic-reporting.html) topic in the _Adobe Commerce User Guide_.

{{redeploy-warning}}

>[!PREREQUISITES]
>
>- Login credentials for the Adobe Commerce account page, or for the New Relic license associated with your project
>- [Admin-level access](../project/user-access.md) to the Starter environments to configure
>- Credentials to access the [Admin](https://experienceleague.adobe.com/docs/commerce-admin/systems/user-accounts/permissions.html) for the environment

**To configure New Relic for Starter environments**:

1. Find your New Relic license key from the Project Web Interface or the Cloud CLI.

   **Project WI method**:

   - Open your cloud project [account page](https://accounts.magento.cloud/user).

   - On the _Projects_ tab, find your project.

   - Click **View Details** for project infrastructure information.

   - Expand the **New Relic Service** section to view the license key.

   - Copy the license key.

   **Cloud CLI method**:

   ```bash
   magento-cloud subscription:info services.newrelic
   ```

1. Add the New Relic license key to an environment using the `magento-cloud` CLI.

   - Change to the environment that needs the license key.
   - Update the variable value using the following `magento-cloud` CLI command:

      ```bash
      magento-cloud variable:update php:newrelic.license --value <newrelic-license-key>
      ```
    
    Optionally, you can add it from the [Commerce Admin](https://experienceleague.adobe.com/docs/commerce-admin/start/reporting/new-relic-reporting.html#step-3%3A-configure-your-store).

1. Log in to your [New Relic account](https://login.newrelic.com/login) to verify that you can view data from the Adobe Commerce environment. See [Investigate performance](investigate-performance.md).

### Remove license key

You can only use your New Relic license key on three active environments. If the key is in use in three environments, you must remove the key from one of the environments before you can add it to a different environment.

**To remove a license key from an environment**:

1. List environment variables.

   ```bash
   magento-cloud variable:list
   ```

   Sample response:

   ```terminal
    +----------------------+-------------+----------------------+---------+
    | Name                 | Level       | Value                | Enabled |
    +----------------------+-------------+----------------------+---------+
    | php:newrelic.license | environment | newrelic-license-key | true    |
    +----------------------+-------------+----------------------+---------+
   ```

   >[!WARNING]
   >
   >If you added the license key as a _project_ variable, you must remove that project-level variable. A project variable adds the license to _every_ environment branch created, which can consume or exceed the license limit. To list project variables: `magento-cloud variable:list --level project`

1. Delete the license variable.

   ```bash
   magento-cloud variable:delete php:newrelic.license
   ```
