---
title: '[!DNL Onboarding] to Commerce'
description: Access your cloud account and set up an Adobe Commerce on cloud infrastructure project.
role: Admin
exl-id: c6b768d7-d835-4a8d-aad9-1c0324f7570d
---
# [!DNL Onboarding] to Commerce

After Adobe activates a Commerce on cloud infrastructure subscription, the initial project and code access is available only to the person designated as the License Owner (Account Owner).

The License Owner is the person in your business or finance organization that manages payments and other business-related transactions for the Adobe Commerce on cloud infrastructure account. This person serves as the point of contact with Adobe. If you must change the License Owner on your account, you must contact your Adobe Account Team.

To quickly onboard your project, so you can begin developing your site for live deployment, you must complete the required setup and [!DNL onboarding] tasks. Typically, the License Owner begins the process by securing Admin access and creating Technical Admin users that can help with setup, customization, and development work.

## Sign up for a Cloud account

If you do not have an Adobe Commerce on cloud infrastructure account, contact [Sales][]. When you sign up, Adobe creates your account and sends you a welcome email that provides instructions on how to access the project interface. The email contains a link so that you can log in to your account and complete your initial project setup.

### Cloud [!DNL Onboarding] UI

The Adobe Commerce on cloud infrastructure Project page in the ([!DNL Onboarding] UI) provides a Getting Started checklist to set up your project and services, determine access, and get started with development. From the OBUI, you can:

- Add a Technical Admin, a super user that can manage your project and branches
- Access your project environment, including a link to the Project Web Interface
- Provide your developer with a getting started for local development
- Complete a quick user acceptance test (UAT) checklist with links to further tests

**To open the project page**:

1. Log in to your [Adobe Commerce customer account](https://account.magento.com/customer/account/login).

1. On the _My Account_ page, click the **[!UICONTROL Commerce]** tab to see the projects in your account.

1. Click **View Project Page** in the [Projects section](https://cloud.magento.com/cloud/project/).

1. Click the project name and open the Cloud Project page ([!DNL Onboarding] UI).

   ![OBUI project page](../assets/onboarding-ui.png)

   Browse through the portal for helpful information and options to start planning your project, developing code, and preparing for UAT and site launch.

## Access project and add users

The License Owner can add user accounts to provide access to code, manage branches, enter tickets, and support environments. These user accounts can include in-house development, consultants, and solution specialists.

Typically, the only user the License Owner must create is the _Technical Admin_. The Technical Admin needs a user account with admin access to create user accounts for developers, set environment permissions, and manage all branches and environments. The Technical Admin can be a developer, a consultant, an [Adobe Solution Partner](https://business.adobe.com/products/magento/partners.html), or yourself.

You can create a Technical Admin through the Project portal, from the Project Web interface, or from the command line using the `magento-cloud` CLI.

### User registration

You can only add registered users to your Adobe Commerce on cloud infrastructure projects and environments. If you have a new user, ask them to [register for an account](https://account.magento.com/customer/account/login/) and to provide the email address associated with their account profile.

### Shared account access

The License Owner can set up shared access for the account. Shared access allows trusted employees and service providers to use the Help center to submit and track Support tickets related to your Adobe Commerce on cloud infrastructure projects. For setup instructions, see the [Shared Access][] article in the Help Center.

### Project web interface

You can use the [Project Web Interface](web-interface.md) to manage your project, add user accounts, and begin developing your store. The License Owner, Technical Admin users, and developers can use this interface to manage all environments and branches, environment variables, environment settings, and routes.

**To access the Project Web Interface**:

1. Log in to [My account](https://account.magento.com/customer/account/login).

1. On the _My Account_ page, click the **[!UICONTROL Commerce]** tab to see the projects in your account.

1. Click the **Projects** tab and select a project.

1. Click **Infrastructure access**, and then click **Project Access (Web UI)**.

   ![Cloud project portal](../assets/obui-project-access.png)

## Sign up for Adobe status

Get updates about Adobe Commerce on cloud infrastructure platform environments and related services from the [Status page][].

The page provides a status for Adobe Commerce components and services followed by notifications about incident reports, service upgrades, planned outages, and scheduled maintenance. Anyone working on your project can subscribe to the Adobe Commerce status site to receive event notifications and updates through email or Slack. You can customize your Adobe status subscription to track specific products by regions and events.

>[!TIP]
>
>Learn how to navigate the Cloud project web interface.
>
>**Next step**: [Project web interface](web-interface.md)

<!-- link definitions -->

[Sales]: https://business.adobe.com/products/magento/get-demo.html
[Shared Access]: https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#shared-access
[Status page]: https://status.adobe.com/products/503473
