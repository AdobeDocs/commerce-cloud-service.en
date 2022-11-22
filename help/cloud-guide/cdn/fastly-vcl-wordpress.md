---
title: Reroute requests to a CMS backend
description: Learn how to reroute incoming requests from an Adobe Commerce store to a separate WordPress site using the Fastly edge module.
exl-id: 5bd9c56f-4412-4643-89b6-590a8ec65ac0
---
# Reroute requests to a CMS backend

Reroute incoming requests from an Adobe Commerce store to a separate WordPress site using the Fastly Edge Module _Other CMS/backend integration_ with an Edge Dictionary. You can follow a similar process to reroute requests to other CMS backends.

Use Fastly Edge Modules to create and upload custom VCL code from the Admin instead of manually writing the VCL code and uploading it using the Fastly API.

>[!NOTE]
>
>We recommend adding custom VCL configurations to a Staging environment where you can test them before updating the Fastly service configuration in the Production environment.

**Prerequisites**

{{$include /help/_includes/vcl-snippet-prerequisites.md}}

**To reroute requests from Adobe Commerce to WordPress**:

1. Enable Fastly Edge Modules in the Staging or Production environment.

   - Log in to the Admin.

   - Navigate to **Stores** > Settings > **Configuration** > **Advanced** > **System** > **Full Page Cache** > **Fastly Configuration** > **Advanced Configuration**.

   - Set the value for **Fastly Edge Modules** to **Yes**.

   - Save the configuration.

1. Identify the URL paths to reroute to the WordPress backend.

1. Complete the following tasks to configure the Fastly service and create the custom VCL code for rerouting requests to the WordPress backend.

   - Create an Edge Dictionary that specifies the paths to reroute from the Adobe Commerce store to the backend.

   - Add the WordPress backend to the Fastly service configuration and attach the request condition for the URL rewrites.

   - Configure the _Other CMS/backend integration_ Edge Module to handle the URL rewrites from Adobe Commerce to the WordPress backend.

     For detailed instructions, see [Fastly Edge Modules - Other CMS/Backend integration](https://github.com/fastly/fastly-magento2/blob/master/Documentation/Guides/Edge-Modules/EDGE-MODULE-OTHER-CMS-INTEGRATION.md) in the _Fastly CDN module for Magento 2_ documentation.

1. After updating the Fastly service configuration, test your Adobe Commerce store to ensure that the specified URL requests for WordPress are rerouted correctly.
