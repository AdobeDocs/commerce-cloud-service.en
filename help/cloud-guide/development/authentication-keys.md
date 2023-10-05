---
title: Authentication keys
description: Learn how to apply authentication keys to a development project in Adobe Commerce on cloud infrastructure.
feature: Cloud, Security
topic: Security
exl-id: b05cd4c2-0804-49c8-980a-4c7b6932082b
---
# Authentication keys

You must have an authentication key to access the Adobe Commerce repository and to enable install and update commands for your Adobe Commerce on cloud infrastructure project. There are two methods for specifying Composer authorization credentials.

- **authentication file**—A file that contains your Adobe Commerce [authorization credentials](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/prerequisites/authentication-keys.html) in your Adobe Commerce on cloud infrastructure root directory.
- **environment variable**—An environment variable to set up authentication keys in your Adobe Commerce on cloud infrastructure project to prevent accidental exposure.

>[!BEGINSHADEBOX]

**Security note**

Adobe recommends using the [environment variable](#composer-auth-environment-variable) method with your cloud project to prevent accidental exposure of your authorization credentials.

The authentication file method is ideal when using Cloud Docker for Commerce as a local development tool, but be careful not to upload the `auth.json` file to a public Git-based repository. You can add the `auth.json` file to the [`.gitignore` file](../project/file-structure.md#ignoring-files).

>[!ENDSHADEBOX]

## Authentication file

**To create an `auth.json` file**:

1. If you do not have an `auth.json` file in your project root directory, create one.

   - Using a text editor, create an `auth.json` file in your project root directory.
   - Copy the contents of the [sample `auth.json`](https://github.com/magento/magento2/blob/2.3/auth.json.sample) into the new `auth.json` file.

1. Replace `<public-key>` and `<private-key>` with your Adobe Commerce authentication credentials.

   ```json
   {
       "http-basic": {
           "repo.magento.com": {
               "username": "<public-key>",
               "password": "<private-key>"
           }
       }
   }
   ```

1. Save your changes and exit the text editor.

## Composer auth environment variable

The following method is the best way to prevent accidental exposure of sensitive credentials in a public Git-based repository.

**To add authentication keys using an environment variable**:

1. In the _Project Web Interface_, click the configuration icon on the right side of the project navigation.

   ![Configure project](../../assets/icon-configure.png){width="36"}

1. In the _Project Settings_ list, click **[!UICONTROL Variables]**.

1. Click **[!UICONTROL Create variable]**.

1. In the **[!UICONTROL Variable name]** field, enter `env:COMPOSER_AUTH`.

1. In the _Value_ field, add the following and replace `<public-key>` and `<private-key>` with your Adobe Commerce authentication credentials:

   ```json
   {
       "http-basic": {
           "repo.magento.com": {
               "username": "<public-key>",
               "password": "<private-key>"
           }
       }
   }
   ```

1. Select **[!UICONTROL Available during buildtime]** and deselect **[!UICONTROL Available during runtime]**.

1. Click **[!UICONTROL Create variable]**.

1. Remove the `auth.json` file from each environment.
