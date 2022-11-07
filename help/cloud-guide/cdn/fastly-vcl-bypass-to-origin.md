---
title: Custom VCL to bypass Fastly cache
description: Troubleshoot request traffic to the origin server by creating a custom VCL snippet to bypass the Fastly cache.
---

# Custom VCL to bypass Fastly cache

You can create a custom VCL snippet to bypass the Fastly cache so you can troubleshoot request traffic to the origin server. For example, you can create a snippet to determine whether site issues are caused by caching, or to troubleshoot headers.

You can configure the snippet to bypass Fastly caching for requests from a specific IP address or URL.

>[!NOTE]
>
>Before merging custom VCL configuration into a production environment, make sure to test the code in the Staging environment.

**Prerequisites:**

{{custom-vcl-prerequisites}}

**To bypass Fastly cache based on IP address or URL**:

{{admin-login-step}}

1. Click **Stores** > Settings > **Configuration** > **Advanced** > **System**.

1. Expand **Full Page Cache** > **Fastly Configuration** > **Custom VCL Snippets**.

1. Click **Create Custom Snippet**.

1. Add the VCL snippet values:

   - **Name** — `bypass_fastly`

   - **Type** — `recv`

   - **Priority** — `5`

   - **VCL** snippet content —

      The following example bypasses Fastly for a specific IP address:

      ```conf
      if (client.ip == "<Your IPv4 IP address>" || client.ip == "<Your IPv6 IP address>") {
        return(pass);
      }
      ```

      The following example bypasses Fastly for a specific URL pattern:

      ```conf
      if (req.url ~ "/media/feeds/GoogleShoppingHiVisNew.xml") {  return (pass);}
      ```

      For an exact URL match, use the `==` operator instead of the `~` operator. See the [Fastly VCL reference] for details.

1. Click **Create**.

   ![Create Fastly Bypass VCL snippet](/help/assets/cdn/fastly-create-bypass-snippet.png)

1. After the page reloads, click **Upload VCL to Fastly** in the *Fastly Configuration* section.

1. After the upload completes, refresh the cache according to the notification at the top of the page.

   Fastly validates the updated VCL version during the upload process. If the validation fails, edit your custom VCL snippet to fix any issues. Then, upload the VCL again.

After you add the VCL snippet, you can use cURL commands to submit requests to the origin server from the specified IP address or URL as shown in the following example:

```bash
curl -svo /dev/null www.example.com/index.html
```

Then, inspect the response to troubleshoot issues with the uncached content.

{{automate-vcl-snippet-deployment}}

## Modify custom VCL snippet

{{modify-custom-vcl-snippet}}

## Delete-custom-vcl-snippet

{{delete-custom-vcl-snippet}}


<!--External link definitions-->
[Fastly VCL reference]: https://docs.fastly.com/vcl/

