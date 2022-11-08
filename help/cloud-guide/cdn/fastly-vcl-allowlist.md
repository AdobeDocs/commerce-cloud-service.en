---
title: Custom VCL for allowing requests
description: Filter incoming requests and allow access by IP address for Adobe Commerce sites by with a Fastly Edge ACL list and custom VCL snippet.
---

# Custom VCL for allowing requests

You can use a Fastly Edge ACL list with a custom VCL code snippet to filter incoming requests and allow access by IP address. The ACL list specifies the IP addresses to allow.

Create an allowlist to limit access to your Staging environment so that only requests from specified IP addresses for internal developers and approved external services are permitted. You can also create an allowlist to secure access to the Admin on Staging and Production environments.

The following example shows how to use a custom VCL snippet with a [Fastly Access Control List (ACL)](https://docs.fastly.com/guides/access-control-lists/about-acls) to secure access to the Admin for an Adobe Commerce on cloud infrastructure project environment. When you add the custom VCL snippet to the Cloud environment, Fastly allows only requests from IP addresses included in the ACL.

>[!TIP]
>
>For Staging and Integration environments that should not be publicly accessible, use the HTTP access control option available in the [Project Web Interface](../project/overview.md#access-the-project-web-interface) to manage access to the entire site by IP address.

**Prerequisites:**


{{$include /help/_includes/vcl-snippet-prerequisites.md}}

-  List of client IP addresses to include on the allowlist

## Create Edge ACL for allowing client IPs

Edge ACLs create IP address lists for managing access to your site. In this example, you create an Edge ACL and add the list of client IP addresses allowed to access the Admin for your project environment.

{{admin-login-step}}

1. Click **Stores** > Settings > **Configuration** > **Advanced** > **System**.

1. Expand **Full Page Cache** > **Fastly Configuration** > **Edge ACL**.

1. Create the ACL container:

   -  Click **Add ACL**.

   -  On the *ACL Container* page, enter an **ACL name**—`allowlist`.

   -  Select **Activate after the change** to deploy your changes to the version of the Fastly service configuration that you are editing.

   -  Click **Upload** to attach the ACL to your Fastly service configuration.

1. Add the list of IP addresses allowed to access the Admin:

   -  Click the Settings icon for the `allowlist` ACL.

   -  Add and save the *IP Value* for each client IP address.

   -  Click **Cancel** to return to the system configuration page.

1. Click **Save Config**.

1. Refresh the cache according to the notification at the top of the page.

## Create the custom VCL snippet to secure Admin access

The following custom VCL snippet code (JSON format) shows the logic to filter requests to the Admin and allow access if the client IP address matches an address in the `allowlist` ACL.

```json
{
  "name": "allowlist",
  "dynamic": "0",
  "type": "recv",
  "priority": "5",
  "content": "if ((req.url ~ \"^/admin\") && !(client.ip ~ allowlist) && !req.http.Fastly-FF) { error 403 \"Forbidden\"; }"
}
```

Before creating your own snippet from this example, review the values to determine whether you need to make any changes:

-  `name` — Name for the VCL snippet. For this example, `allowlist`.

-  `priority` — Determines when the VCL snippet runs. The priority  is `5` to immediately run and check whether an Admin requests are coming from an allowed IP address. The snippet runs before any of the default Magento VCL snippets (`magentomodule_*`) assigned a priority of 50. Set the priority for each custom snippet higher or lower than 50 depending on when you want your snippet to run. Snippets with lower priority numbers run first.

-  `type` — Specifies a location to insert the snippet in the versioned VCL code. This VCL is a `recv` snippet type which adds the snippet code to the `vcl_recv` subroutine below the default Fastly VCL code and above any objects.

-  `content` — The snippet of VCL code to run. In this example, the code filters requests to the Admin and allows access if the client IP address matches an address in the `allowlist` ACL. If the address does not match, the request is blocked with a `403 Forbidden` error.

   If the URL for your Admin was changed, replace the sample value `/admin` with the URL for your environment. For example, `/company-admin`.

In the code sample, the condition `!req.http.Fastly-FF` is important when using [Origin Shielding](fastly-custom-cache-configuration.md#configure-back-ends-and-origin-shielding). Do not remove or edit this code.

After reviewing and updating the code for your environment, use either of the following methods to add the custom VCL snippet to your Fastly service configuration:

-  [Add the custom VCL snippet from the Admin](#add-the-custom-vcl-snippet). This method is recommended if you can access the Admin. (Requires [Fastly CDN module for Magento 2 version 1.2.58](fastly-configuration.md#upgrade) or later.)

-  Save the JSON code example to a file (for example, `allowlist.json`) and [upload it using the Fastly API](fastly-vcl-custom-snippets.md#manage-custom-vcl-snippets-using-the-api). Use this method if you cannot access the Admin.

## Add the custom VCL snippet

{{admin-login-step}}

1. Click **Stores** > Settings > **Configuration** > **Advanced** > **System**.

1. Expand **Full Page Cache** > **Fastly Configuration** > **Custom VCL Snippets**.

1. Click **Create Custom Snippet**.

1. Add the VCL snippet values:

   -  **Name** — `allowlist`

   -  **Type** — `recv`

   -  **Priority** — `5`

   -  Add the **VCL** snippet content:

      ```conf
      if ((req.url ~ "^/admin") && !(client.ip ~ allowlist) && !req.http.Fastly-FF) { error 403 "Forbidden";}
      ```

1. Click **Create** to generate the VCL snippet file with the name pattern `type_priority_name.vcl`, for example `recv_5_allowlist.vcl`

1. After the page reloads, click **Upload VCL to Fastly** in the *Fastly Configuration* section to add the file to the Fastly service configuration.

1. After the upload completes, refresh the cache according to the notification at the top of the page.

Fastly validates the updated version of the VCL code during the upload process. If the validation fails, edit the custom VCL snippet to fix the issue. Then, upload the VCL again.

{{$include /help/_includes/vcl-snippet-modify.md}}

{{$include /help/_includes/vcl-snippet-delete.md}}
