---
title: Authentication keys
description: Learn how to apply authentication keys to a development project in Adobe Commerce on cloud infrastructure.
---

# Authentication keys

You must have an authentication key to access the Adobe Commerce repository and to enable install and update commands for your Adobe Commerce on cloud infrastructure project. There are two methods for specifying Composer authorization credentials.

-  **authentication file**—You must have an `auth.json` file that contains your Adobe Commerce [authorization credentials](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/prerequisites/authentication-keys.html) in your Adobe Commerce on cloud infrastructure root directory.
-  **environment variable**—Alternatively, you can use an environment variable to set up authentication keys in your Adobe Commerce on cloud infrastructure project to prevent accidental exposure.

**To create a `auth.json` file**:

1. If you do not have an `auth.json` file in your project root directory, create one.

   -  Using a text editor, create an `auth.json` file in your project root directory.
   -  Copy the contents of the [sample `auth.json`](https://github.com/magento/magento2/blob/2.3/auth.json.sample) into the new `auth.json` file.

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

The following method is best to prevent accidental exposure of credentials, such as pushing an `auth.json` file to a public repository.

**To add authentication keys using an environment variable**:

1. In the _Project Web Interface_, click the configuration icon in the upper left corner.

1. In the _Configure Project_ view, click the **Variables** tab.

1. Click **Add Variable**.

1. In the _Name_ field, enter `env:COMPOSER_AUTH`.

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

1. Select **Visible during build** and deselect **Visible at run**.

1. Click **Add Variable**.

1. Remove the `auth.json` file from each environment.
