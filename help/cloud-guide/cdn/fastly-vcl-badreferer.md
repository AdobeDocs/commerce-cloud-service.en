---
title: Block referral spam
description: Block referral spam from your site using the Fastly Edge dictionary and a custom VCL snippet.
---

# Block referral spam

The following example shows how to configure [Fastly Edge Dictionary](https://docs.fastly.com/guides/edge-dictionaries/working-with-dictionaries-using-the-api) with a custom VCL snippet to block referral spam from your Adobe Commerce on cloud infrastructure site.

>[!NOTE]
>
>We recommend adding custom VCL configurations to a Staging environment where you can test them before running them against the Production environment.

**Prerequisites:**

{{$include /help/_includes/vcl-snippet-prerequisites.md}}

-  Review your site logs for fake referral URLs, and make a list of domains to block.

## Create a referrer blocklist

Edge Dictionaries create key-value pairs accessible to VCL functions during VCL snippet processing. In this example, you create an edge dictionary that provides the list of referrer websites to block.

{{admin-login-step}}

1. Click **Stores** > **Settings** > **Configuration** > **Advanced** > **System**.

1. Expand **Full Page Cache** > **Fastly Configuration** > **Edge dictionaries**.

1. Create the Dictionary container:

   -  Click **Add container**.

   -  On the *Container* page, enter a **Dictionary name**—`referrer_blocklist`.

   -  Select **Activate after the change** to deploy your changes to the version of the Fastly service configuration that you are editing.

   -  Click **Upload** to attach the dictionary to your Fastly service configuration.

1. Add the list of domain names to block to the `referrer_blocklist` dictionary:

   -  Click the Settings icon for the `referrer_blocklist` dictionary.

   -  Add and save key-value pairs in the new dictionary. For this example, each **Key** is the domain name of a referrer URL to block and **Value** is `true`.

      ![Add bad referrer dictionary items](../../assets/cdn/fastly-referrer-blocklist-dictionary.png)

   -  Click **Cancel** to return to the system configuration page.

1. Click **Save Config**.

1. Refresh the cache according to the notification at the top of the page.

For more information about Edge Dictionaries, see [Creating and using Edge Dictionaries](https://docs.fastly.com/guides/edge-dictionaries/working-with-dictionaries-using-the-api) and [custom VCL snippets](https://docs.fastly.com/guides/edge-dictionaries/working-with-dictionaries-using-the-api#custom-vcl-examples) in the Fastly documentation.

## Create a custom VCL snippet to block referrer spam

The following custom VCL snippet code (JSON format) shows the logic to check and block requests. The VCL snippet captures the host of a referrer website into a header, and then compares the host name to the list of URLs in the `referrer_blocklist` dictionary. If the host name matches, the request is blocked with a `403 Forbidden` error.

```json
{
  "name": "block_bad_referrer",
  "dynamic": "0",
  "type": "recv",
  "priority": "5",
  "content": "set req.http.Referer-Host = regsub(req.http.Referer, \"^https?:\/\/?([^:\/s]+).*$\", \"\\1\"); if (table.lookup(referrer_blocklist, req.http.Referer-Host)) { error 403 \"Forbidden\"; }"
}
```

Before creating a snippet based on this example, review the values to determine whether you need to make any changes:

-  `name` — Name for the VCL snippet. For this example, we used `block_bad_referrer`.

-  `dynamic` — Value 0 indicates a [regular snippet](https://docs.fastly.com/en/guides/using-regular-vcl-snippets) to upload to the versioned VCL for the Fastly configuration.

-  `priority` — Determines when the VCL snippet runs. The priority is `5` to run this snippet code before any of the default Magento VCL snippets (`magentomodule_*`) assigned a priority of 50. Set the priority for each custom snippet higher or lower than 50 depending on when you want your snippet to run. Snippets with lower priority numbers run first.

-  `type` — Specifies a location to insert the snippet in the VCL version. In this example, the VCL snippet is a `recv` snippet. When the snippet is inserted into the VCL version, it is added to the `vcl_recv` subroutine,  below the default Fastly VCL code and above any objects.

-  `content` — The snippet of VCL code to run in one line, without line breaks.

After reviewing and updating the code for your environment, use either of the following methods to add the custom VCL snippet to your Fastly service configuration:

-  [Add the custom VCL snippet from the Admin](#add-the-custom-vcl-snippet). This method is recommended if you can access the Admin. (Requires [Fastly version 1.2.58](fastly-configuration.md#upgrade) or later.)

-  Save the JSON code example to a file (for example, `allowlist.json`) and [upload it using the Fastly API](fastly-vcl-custom-snippets.md#manage-custom-vcl-snippets-using-the-api). Use this method if you cannot access the Admin.

## Add the custom VCL snippet

{{admin-login-step}}

1. Click **Stores** > Settings > **Configuration** > **Advanced** > **System**.

1. Expand **Full Page Cache** > **Fastly Configuration** > **Custom VCL Snippets**.

1. Click **Create Custom Snippet**.

1. Add the VCL snippet values:

   -  **Name** — `block_bad_referrer`

   -  **Type** — `recv`

   -  **Priority** — `5`

   -  **VCL** snippet content —

      ```conf
      set req.http.Referer-Host = regsub(req.http.Referer,
      "^https?://?([^:/\s]+).*$", "1");
      if (table.lookup(referrer_blocklist, req.http.Referer-Host)) {
        error 403 "Forbidden";
      }
      ```

1. Click **Create**.

   ![Create custom referrer block VCL snippet](/help/assets/cdn/fastly-create-referrer-block-snippet.png)

1. After the page reloads, click **Upload VCL to Fastly** in the *Fastly Configuration* section.

1. After the upload completes, refresh the cache according to the notification at the top of the page.

Fastly validates the updated VCL version during the upload process. If the validation fails, edit your custom VCL snippet to fix any issues. Then, upload the VCL again.

{{automate-vcl-snippet-deployment}}

{{$include /help/_includes/vcl-snippet-modify.md}}

{{$include /help/_includes/vcl-snippet-delete.md}}
