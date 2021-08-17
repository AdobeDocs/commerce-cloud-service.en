---
title: Set up local development
description: Set up your development environment with the required command-line tools.
---

# Set up local development

Adobe Commerce environments are Read Only. You can write and test code in your local environment using the command line. Install the following tools before continuing:

- [Node.js version 14, 12, or 10](https://nodejs.org/en/download/package-manager/)
- [Adobe I/O Extensible CLI (AIO)](https://github.com/adobe/aio-cli)
- [Cloud Manager plugin for AIO](https://github.com/adobe/aio-cli-plugin-cloudmanager)

## Gather credentials

Before accessing the Cloud Manager tool and Commerce repository from the command line, you must add a REST API for a server-to-server Service Account integration to your project. After this one-time setup, you do not have to authenticate again.

**To add a service account integration**:

1. Log in to the Developer Console for your organization. (Location advice TBD)
1. Select the project. Optionally, you can create a project.
1. Click **[!UICONTROL Add API]**.
1. Select **[!UICONTROL Experience Cloud]**, choose **[!UICONTROL Cloud Manager]**, and click **[!UICONTROL Next]**.
1. Select the server-to-server **[!UICONTROL Service Account]** integration.
1. Select Option 1 and **[!UICONTROL Generate keypair]** to generate a keypair and download the configuration file that contains a copy of your private key.
1. Click Next.
1. Select the **[!UICONTROL Deployment Manager]** product profile. (Advisement TBD)
1. Click **[!UICONTROL Save configured API]**.

The Service Account credentials contain a Client ID and secret, Technical Account ID,  Organization ID, and public key that are used to authenticate requests to Cloud Manager API.

## Connect the Cloud Manager API

You connect to the Cloud Manager API using the files that you downloaded while creating the service account integration in the _Gather credentials_ section.

**To create a configuration file for CLI integration**:

1. Create a file named `config.json` and save in your local `.config` folder.

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

    Fill in the String values with the values from your credentials. From the project overview in the Developer console, click the **[!UICONTROL Service Account (JWT)]** under the _[!UICONTROL Credentials]_ section.

1. Save the `config.json` file.

To connect Cloud Manager API:

1. TBD

Next step: [Create a default environment](create-environment.md)
