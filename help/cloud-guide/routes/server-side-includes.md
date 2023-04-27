---
title: Server-side includes
description: Learn how to use server-side includes with Adobe Commerce on cloud infrastructure.
feature: Cloud, Routes
exl-id: 34a38cb5-5f0e-49ac-9dba-bb581a06aeed
---
# Server-side includes

[Server-side includes](https://nginx.org/en/docs/http/ngx_http_ssi_module.html) (SSI) are directives in HTML pages that are evaluated on the server while the pages render. SSI enables you to add dynamically generated content to an existing HTML page without serving the entire page.

You can activate or deactivate SSI on a per-route basis in your `.magento/routes.yaml`; for example:

```yaml
    "http://{default}/":
        type: upstream
        upstream: "myapp:php"
        cache:
            enabled: false
            ssi:
                enabled: true
    "http://{default}/time.php":
        type: upstream
        upstream: "myapp:php"
        cache:
            enabled: true
```

SSI enables you to include in your HTML response directives that cause the server to fill in parts of the HTML, respecting any existing [caching configuration](caching.md).

The following example shows how to insert a dynamic date control at the top of a page and another date control at the bottom that updates every 600 seconds:

Add the following to any page, such as `/index.php`:

```php?start_inline=1
echo date(DATE_RFC2822);
<!--#include virtual="time.php" -->
```

Add the following to `time.php`:

```php?start_inline=1
header("Cache-Control: max-age=600");
echo date(DATE_RFC2822);
```

Browse to the page on which you added the control. Refresh the page several times and notice that the time at the top of the page changes but the time on the bottom changes only every 600 seconds.
