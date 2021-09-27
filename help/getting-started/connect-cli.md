---
title: Set up local development
description: Set up your development environment with the required command-line tools.
---

# Set up local development

Adobe Commerce environments are Read Only. You can write and test code on your local machine using the command line. Install the following tools before continuing:

- [Node.js version 14 or 12](https://nodejs.org/en/download/package-manager/)
- [Adobe I/O Extensible CLI (AIO)](https://github.com/adobe/aio-cli)
- [Cloud Manager plugin for AIO](https://github.com/adobe/aio-cli-plugin-cloudmanager)

Step through the following sections to gather your credentials; use your credentials to create a configuration file; and set default values for your local development environment.

## Gather credentials

Your development _project_ is a collection of products and services for customizing your application. Before accessing the Cloud Manager tool from the command line, you must add a REST API for a Service Account (server-to-server) integration to your project.

The Service Account credentials contain a Client ID and secret, Technical Account ID,  Organization ID, and public key. These credentials are used to authenticate requests to the Cloud Manager API. After this one-time setup, you do not have to add this service and authentication again.

**To add a service account integration**:

1. Log in to the _Developer Console_ for your organization. (Location advice TBD)

1. Select a project. Optionally, you can create a project.

1. Click **[!UICONTROL Add API]**.

1. Select **[!UICONTROL Experience Cloud]**, choose **[!UICONTROL Cloud Manager]**, and click **[!UICONTROL Next]**.

1. Select the server-to-server **[!UICONTROL Service Account]** integration.

1. Select **[!UICONTROL Option 1: Generate keypair]** to generate a keypair and download the configuration file that contains a copy of your private key.

1. Click **[!UICONTROL Next]**.

1. Select the **[!UICONTROL Deployment Manager]** product profile. (Advisement TBD)

1. Click **[!UICONTROL Save configured API]**.

## Create a configuration file

You connect to the Cloud Manager API using the files that you downloaded while adding the Service Account integration in the _Gather credentials_ section. The ZIP file includes the `certificate_pub.cert` and `private.key` files.

**To create a configuration file for CLI integration**:

1. Create a file named `config.json` and save in your local `config` folder.

1. Open `config.json` and add the following:

    ```json
    //config.json 
    {
        "client_id": "value from your CLI integration (String)",
        "client_secret": "value from your CLI integration (String)",
        "technical_account_id": "value from your CLI integration (String)",
        "ims_org_id": "value from your CLI integration (String)",
        "meta_scopes": [
            "ent_cloudmgr_sdk"
        ]
        "env": "stage"
    }
    ```

    Fill in the string values with your corresponding credentials.
    
   >[!TIP]
   >
   >To find your credentials, select your project in the Developer console. In your project overview, click the **[!UICONTROL Service Account (JWT)]** under the _Credentials_ section.


1. Save the `config.json` file.

1. Add the `certificate_pub.cert` and `private.key` files to the same `config` folder.

1. Set the default configuration file.

   ```bash
   aio config:set ims.contexts.aio-cli-plugin-cloudmanager config/config.json --file --json
   ```

1. Set the private key.

   ```bash
   aio config:set ims.contexts.aio-cli-plugin-cloudmanager.private_key config/private.key --file
   ```

## Set default environment values

You can set local default values for program ID and environment ID to avoid repeating them with each command. The following steps set your organization base URL, program, and environment IDs in the configuration file.

1. Set your organization URL.

   ```bash
   aio config:set cloudmanager.base_url  https://cloudmanager-dev.tenant.io
   ```

1. Verify the CLI and find your program ID.

   ```bash
   aio cloudmanager:list-programs
   ```

   Note your program ID from the response:

   ```terminal
   Program Id  Name                  Enabled 
   00001       Program 1             true    
   00002       Program 2             true 
   ```

1. Set the default program ID.

   ```bash
   aio config:set cloudmanager_programid [PROGRAM-ID]
   ```

1. Find your environment ID. A default environment has been provided during the program initialization.

   ```bash
   aio cloudmanager:program:list-environments
   ```

   Note your environment ID from the response:

   ```terminal
   Environment Id Name            Type Description
   100001         my-environment  dev  This is a test environment.
   ```

1. Set the following default environment ID.

   ```bash
   aio config:set cloudmanager_environmentid [ENVIRONMENT-ID]
   ```

1. Verify the Cloud Manager settings.

   ```bash
   aio config:list | grep "cloudmanager_"
   ```

   Sample response:

   ```terminal
   cloudmanager_programid: "00002",
   cloudmanager_environmentid: "100001"
   ```

>[!TIP]
>
>The next step helps you to understand what an environment is and how you can customize an environment using the command line.
>
>**Next step**: [Create a default environment](create-environment.md)
