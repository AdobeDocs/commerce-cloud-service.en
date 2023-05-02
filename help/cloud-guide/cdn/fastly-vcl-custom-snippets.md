---
title: Get started with custom VCL snippets
description: Learn about using Varnish Control Language code snippets to customize the Fastly service configuration for Adobe Commerce.
feature: Cloud, Configuration, Services
exl-id: df0f0906-8ffa-41a1-a31c-d36deb5a6a31
---
# Getting started with custom VCL

Fastly supports a customized version of the Varnish Configuration Language (VCL) to tailor the Fastly service configuration to your requirements.

Custom VCL snippets are blocks of VCL logic added to the active VCL version uploaded to your Adobe Commerce site. A custom VCL snippet modifies how Fastly caching services respond to request traffic. For example, you can add a custom VCL snippet to allow request traffic only from specified client IP addresses. Or, create a snippet to block traffic from websites known for sending referral spam to your Adobe Commerce sites.

Custom VCL snippets—generated, compiled, and transmitted to all Fastly caches—load and activate without server downtime.

>[!NOTE]
>
>Before adding custom VCL code, edge dictionaries, and ACLs to your Fastly module configuration, verify that the Fastly caching service works with the default configuration. See [Configure Fastly services](fastly-configuration.md).

Fastly supports two types of custom VCL snippets:

-  [Regular snippets](https://docs.fastly.com/en/guides/about-vcl-snippets)—Custom regular VCL snippets are coded for specific VCL versions. You can create, modify, and deploy regular VCL snippets from the Admin or the Fastly API.

-  [Dynamic snippets](https://docs.fastly.com/en/guides/using-dynamic-vcl-snippets)—VCL snippets created using the Fastly API. You can modify and deploy dynamic snippets without having to update the Fastly VCL version for your service.

We recommend using custom VCL snippets with Edge Dictionaries and Access Control Lists (ACL) to store data used in your custom code.

-  [**Edge dictionary**](https://docs.fastly.com/guides/edge-dictionaries/about-edge-dictionaries)—Stores data as key-value pairs in a dictionary container that can be referenced from custom VCL snippets

-  [**Edge ACL**](https://docs.fastly.com/guides/access-control-lists/about-acls)—Stores the client IP address data that defines the access control list for block or allow rules implemented using custom VCL snippets

The dictionary and ACL data is deployed to the Fastly Edge nodes accessible across network regions. Also, the data can be updated dynamically across the network without requiring you to redeploy the VCL code for your staging or production environment.

>[!NOTE]
>
>You can only add custom VCL snippets to a Staging or Production environment if you have [configured Fastly services](fastly-configuration.md) for that environment.

## Tutorial

This tutorial and examples demonstrate the use of regular custom VCL snippets with Edge Dictionaries and Edge ACLs to customize the Fastly service configuration for Adobe Commerce. For more detailed information, see the Fastly documentation:

-  [Guide to Fastly VCL](https://docs.fastly.com/guides/vcl/guide-to-vcl)—Information about the Fastly Varnish implementation, Fastly VCL extensions, and resources for learning more about Varnish and VCL.
-  [Fastly VCL reference](https://docs.fastly.com/guides/vcl/)—Detailed programming reference to develop and troubleshoot Fastly custom VCL and custom VCL snippets.

You can create and manage custom VCL snippets from the Adobe Commerce Admin or by using the Fastly API:

-  [Adobe Commerce Admin](#manage-custom-vcl-from-admin)—We recommend using the Adobe Commerce Admin to manage custom VCL snippets because it automates the process to validate, upload, and apply the VCL changes to the Fastly service configuration. Also, you can view and edit the custom VCL snippets added to the Fastly service configuration from the Admin.

- [Fastly API](#manage-vcl-using-the-api)—If you cannot access the Admin, use the Fastly API to manage custom VCL snippets. For example, use the API to troubleshoot the Fastly service configuration when the site is down, or to add a custom VCL snippet. Also, some operations can be completed only using the API. For example, you must use the API to reactivate an older VCL version or to view all the VCL snippets included in a specified VCL version. See [API quick reference for VCL snippets](#api-quick-reference-for-vcl-snippets).

### Example VCL snippet code

The following example shows the custom VCL snippet (JSON format) that filters traffic by client IP address:

```json
{
  "service_id": "FASTLY_SERVICE_ID",
  "version": "{Editable Version #}",
  "name": "apply_acl",
  "priority": "100",
  "dynamic": "1",
  "type": "hit",
  "content": "if ((client.ip ~ {ACLNAME}) && !req.http.Fastly-FF){ error 403; }"
}
```

>[!WARNING]
>
>In this example, the VCL code is formatted as a JSON payload that can be saved to a file and submitted in a Fastly API request. To prevent JSON validation errors when sending the snippet as JSON for an API request, use a backslash to escape special characters in the code. See [Using dynamic VCL snippets](https://docs.fastly.com/vcl/vcl-snippets/) in the Fastly VCL documentation. If you submit the VCL snippet from the Admin, you do not have to escape special characters.

The VCL logic in the `content` field performs the following actions:

-  Checks the incoming IP address, `client.ip` on each request

-  Blocks any request with an IP address included in the *ACLNAME* edge ACL, returning a `403 Forbidden` error

The following table provides details about key data for custom VCL snippets. For a more detailed reference, see the [VCL snippets](https://docs.fastly.com/api/config#api-section-snippet) reference in the Fastly documentation.

| Value        | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
|--------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `API_KEY`    | The API Key to access your Fastly account. See [Get credentials](fastly-configuration.md).                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| `active`     | Active status of snippet or version. Returns `true` or `false`. If true, the snippet or version is in use. Clone an active snippet using its version number.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| `content`    | The snippet of VCL code to run. Fastly does not support all VCL language features. Also, Fastly provides extensions with custom functionality. For details about supported features, see the [Fastly VCL programming reference](https://docs.fastly.com/vcl/reference/).                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| `dynamic`    | Dynamic status of a snippet. Returns `false` for [regular snippets](https://docs.fastly.com/en/guides/about-vcl-snippets) included in the versioned VCL for the Fastly service configuration. Returns `true` for a [dynamic snippet](https://docs.fastly.com/vcl/vcl-snippets/using-dynamic-vcl-snippets/) which can be modified and deployed without requiring a new VCL version.                                                                                                                                                                                                                                                                                                                                      |
| `number`     | VCL version number where the snippet is included. Fastly uses *Editable Version #* in their example values. If you add custom snippets from the API, include the version number in the API request. If you add custom VCL from the Admin, the version is provided for you.                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| `priority`   | Numeric value from `1` to `100` that specifies when the custom VCL snippet code runs. Snippets with lower priority values run first. If not specified, the `priority` value defaults to `100`.<br><br> Any custom VCL snippet with a priority value of `5` runs immediately, which is best for VCL code that implements request routing (block and allowlists and redirects). Priority `100` is best for overriding default VCL snippet code. <br><br>All [default VCL snippets](fastly-configuration.md#upload-vcl-snippets) included in the Magento-Fastly module have `priority=50`.<br>-  Assign a high priority like `100` to run custom VCL code after all other VCL functions and override the default VCL code. |
| `service_id` | The Fastly Service ID for a specific Staging or Production environment. This ID is assigned when your project is added to the Adobe Commerce on cloud infrastructure [Fastly service account](fastly.md#fastly-service-account-and-credentials).                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| `type`       | Specifies the location for inserting the generated snippet, such as `init` (above subroutines) and `recv` (within subroutines). For details, see the Fastly [VCL snippets](https://docs.fastly.com/api/config#api-section-snippet) reference.                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |

## Manage custom VCL from Admin

You can [add custom VCL snippets](https://github.com/fastly/fastly-magento2/blob/master/Documentation/Guides/CUSTOM-VCL-SNIPPETS.md) from the *Fastly Configuration* > *Custom VCL Snippets* section in the Admin.

![Manage custom VCL snippets](../../assets/cdn/fastly-edit-snippets.png)

The *Custom VCL snippets* view shows only snippets that have been added through the Admin. If snippets are added using the Fastly API, use the API to [manage them](#manage-vcl-using-the-api).

The following examples show how to create and manage custom VCL snippets from the Admin, and to use Fastly Edge modules and Edge dictionaries:

- [Reroute requests to a CMS backend](fastly-vcl-wordpress.md)
- [Block referrral spam](fastly-vcl-badreferer.md)
- [Block referral spam](fastly-vcl-badreferer.md)
- [Custom VCL for IP allowlist](fastly-vcl-allowlist.md)
- [Custom VCL for IP blocklist](fastly-vcl-blocking.md)
- [Bypass Fastly cache](fastly-vcl-bypass-to-origin.md)

## Manage VCL using the API

The following walk-through shows you how to create regular VCL snippet files and add them to your Fastly service configuration using the Fastly API. You can create and manage the snippets from the *terminal* application. You do not need an SSH connection into a specific environment.

**Prerequisites:**

-  Configure your Adobe Commerce on cloud infrastructure environment for Fastly services. See [Set up Fastly](fastly-configuration.md).

-  [Get Fastly API credentials](fastly-configuration.md) to authenticate requests to the Fastly API. Make sure that you get the credentials for the correct environment: Staging or Production.

-  Save Fastly service credentials as bash environment variables that you can use in cURL commands:

   ```bash
   export FASTLY_SERVICE_ID=<Service-ID>
   ```

   ```bash
   export FASTLY_API_TOKEN=<API-Token>
   ```

   The exported environment variables are available only in the current bash session and are lost when you close the terminal. You can redefine variables by exporting a new value. To view the list of exported variables related to Fastly:

   ```bash
   export | grep FASTLY
   ```

## Add VCL snippets

This tutorial provides the basic steps to add custom snippets using the Fastly API.


>[!NOTE]
>
>To learn how to manage custom VCL snippets from the Adobe Commerce Admin, see [Manage VCL from the Adobe Commerce Admin](#manage-custom-vcl-from-admin).


**Prerequisites**

{{$include /help/_includes/vcl-snippet-prerequisites.md}}

### Step 1: Locate the active VCL version

Use the Fastly API [get version](https://docs.fastly.com/api/config#version_dfde9093f4eb0aa2497bbfd1d9415987) operation to get the active VCL version number:

```bash
curl -H "Fastly-Key: $FASTLY_API_TOKEN" https://api.fastly.com/service/$FASTLY_SERVICE_ID/version/active
```

In the JSON response, note the active VCL version number returned in the `number` key, for example `"number": 99`. You need the version number when you clone the VCL for editing.

```json
{
  "testing": false,
  "locked": true,
  "number": 99,
  "active": true,
  "service_id": "872zhjyxhto5SIRb3GAE0",
  "staging": false,
  "created_at": "2019-01-29T22:38:53Z",
  "deleted_at": null,
  "comment": "Magento Module uploaded VCL",
  "updated_at": "2019-01-29T22:39:06Z",
  "deployed": false
}
```

Save the active version number in a bash environment variable for use in subsequent API requests:

```bash
export FASTLY_VERSION_ACTIVE=<Version>
```

### Step 2: Clone the active VCL version and all snippets

Before you can add or modify custom VCL snippets, you must create a copy of the active VCL version for editing. Use the Fastly API [clone](https://docs.fastly.com/api/config#version_7f4937d0663a27fbb765820d4c76c709) operation:

```bash
curl -H "Fastly-Key: $FASTLY_API_TOKEN" https://api.fastly.com/service/$FASTLY_SERVICE_ID/version/$FASTLY_VERSION_ACTIVE/clone -X PUT
```

In the JSON response, the version number is incremented, and the *active* key value is `false`. You can modify the new, inactive VCL version locally.

```json
{
  "testing": false,
  "locked": false,
  "number": 100,
  "active": false,
  "service_id": "vW2bLFWhhto5SIRb3GAE0",
  "staging": false,
  "created_at": "2019-01-29T22:38:53Z",
  "deleted_at": null,
  "comment": "Magento Module uploaded VCL",
  "updated_at": "2019-01-29T22:39:06Z",
  "deployed": false
}
```

Save the new version number in a bash environment variable for use in subsequent commands:

```bash
export FASTLY_EDIT_VERSION=<Version>
```

### Step 3: Create a custom VCL snippet

Create and save your custom VCL code in a JSON file with the following content and format:

```json
{
  "name": "<name>",
  "dynamic": "0",
  "type": "<type>",
  "priority": "100",
  "content": "<code all in one line>"
}
```

The values include:

- `name`—Name for the VCL snippet.

- `dynamic`—Indicates if this is a [regular snippet](https://docs.fastly.com/en/guides/about-vcl-snippets) or a [dynamic snippet](https://docs.fastly.com/guides/vcl-snippets/using-dynamic-vcl-snippets).

- `type`—Specifies the location for inserting the generated snippet, such as `init` (above subroutines) and `recv` (within subroutines). See [Fastly VCL snippet object values](https://docs.fastly.com/api/config#snippet) for information on these values.

- `priority`—A value from `1` to `100` that determines when the custom VCL snippet code runs. Custom VCL snippets with lower values run first.

   All default VCL code from the Fastly VCL module has a `priority` of `50`. If you want an action to occur last or to override the default VCL code, use a higher number, such as `100`. To run custom VCL snippet code immediately, set the priority to a lower value, such as `5`.

- `content`—The snippet of VCL code to run in one line, without line breaks. See [Example custom VCL snippet](#example-vcl-snippet-code).

### Step 4: Add VCL snippet to Fastly configuration

Use the Fastly API [create snippet](https://docs.fastly.com/api/config#snippet_41e0e11c662d4d56adada215e707f30d) operation to add the custom VCL snippet to the VCL version.

```bash
curl -H "Fastly-Key: $FASTLY_API_TOKEN" https://api.fastly.com/service/$FASTLY_SERVICE_ID/version/$FASTLY_EDIT_VERSION/snippet -H 'Content-Type: application/json' -X POST --data @<filename.json>
```

The `<filename.json>` is the name of the file that you prepared in the previous step. Repeat this command for each VCL snippet.

If you receive a `500 Internal Server Error` response from the Fastly service, check the JSON file syntax to make sure you are uploading a valid file.

### Step 5: Validate and activate custom VCL snippets

After you add a custom VCL snippet, Fastly inserts the snippet in the VCL version that you are editing. To apply changes, complete the following steps to validate the VCL snippet code and activate the VCL version.

1. Use the Fastly API [validate VCL version](https://docs.fastly.com/api/config#version_97f8cf7bfd5dc2e5ea1933d94dc5a9a6) operation to verify the updated VCL code.

   ```bash
   curl -H "Fastly-Key: $FASTLY_API_TOKEN" https://api.fastly.com/service/$FASTLY_SERVICE_ID/version/$FASTLY_EDIT_VERSION/validate
   ```

   If the Fastly API returns an error, fix the issue and validate the updated VCL version again.

1. Use the Fastly API [activate](https://docs.fastly.com/api/config#version_0b79ae1ba6aee61d64cc4d43fed1e0d5) operation to activate the new VCL version.

   ```bash
   curl -H "Fastly-Key: $FASTLY_API_TOKEN" https://api.fastly.com/service/$FASTLY_SERVICE_ID/version/$FASTLY_EDIT_VERSION/activate -X PUT
   ```

## API quick reference for VCL snippets

These API request examples use exported environment variables to provide the credentials to authenticate with Fastly. For details on these commands, see the [Fastly API reference](https://docs.fastly.com/api/config#vcl).

>[!NOTE]
>
>Use these commands to manage snippets that you added using the Fastly API. If you added snippets from the Admin, see [Manage VCL snippets using the Admin](#manage-vcl-using-the-api).

-  **Get active VCL version number**

   ```bash
   curl -H "Fastly-Key: $FASTLY_API_TOKEN" https://api.fastly.com/service/$FASTLY_SERVICE_ID/version/active
   ```

-  **List all regular VCL snippets attached to a service**

   ```bash
   curl -H "Fastly-Key: $FASTLY_API_TOKEN" https://api.fastly.com/service/$FASTLY_SERVICE_ID/version/$FASTLY_VERSION/snippet
   ```

-  **Review an individual snippet**

   ```bash
   curl -H "Fastly-Key: $FASTLY_API_TOKEN" https://api.fastly.com/service/$FASTLY_SERVICE_ID/version/$FASTLY_VERSION/snippet/<snippet_name>
   ```

   The `<snippet_name>` is the name of a snippet, such as `my_regular_snippet`.

-  **Update a snippet**

   Modify the [prepared JSON file](#step-3-create-a-custom-vcl-snippet) and send the following request:

   ```bash
   curl -H "Fastly-Key: $FASTLY_API_TOKEN" https://api.fastly.com/service/$FASTLY_SERVICE_ID/version/$FASTLY_VERSION/snippet/<snippet_name> -H 'Content-Type: application/json' -X PUT --data @<filename.json>
   ```

-  **Delete an individual VCL snippet**

    Get a list of snippets and use the following `curl` command with the specific snippet name to delete:

   ```bash
   curl -H "Fastly-Key: $FASTLY_API_TOKEN" https://api.fastly.com/service/$FASTLY_SERVICE_ID/version/$FASTLY_VERSION/snippet/<snippet_name> -X DELETE
   ```

-  **Override values in the [default Fastly VCL code](https://github.com/fastly/fastly-magento2/tree/master/etc/vcl_snippets)**

   Create a snippet with updated values and assign a priority of `100`.
