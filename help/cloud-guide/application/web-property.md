---
title: Web property
description: See examples on how to configure the web property in the Commerce application configuration file.
feature: Cloud, Configuration
exl-id: 2ca94908-6fe1-42fd-bc3b-ef2dd473f1bb
---
# Web property

The `web` property defines how your application is exposed to the web (in HTTP), determines how the web application serves content, and controls how the application container responds to incoming requests by setting rules in each location _block_. A block represents an absolute path leading with a forward slash (`/`).

```yaml
web:
    locations:
        "/":
            # The public directory of the app, relative to its root.
```

You can fine-tune your `locations` configuration using the following key values for each `locations` block:

| Attribute  | Description |
| :--- | :--- |
| `allow` | Serve files that do not match "rules". Default value = `true` |
| `expires` | Set the number of seconds to cache content in the browser. This key enables the `cache-control` and `expires` headers for static content. If this value is not set, the `expires` directive and resulting headers are not included when serving static content files. A negative 1 (`-1`) value results in no caching and is the default value. You can express time value with the following units:  `ms` (milliseconds), `s` (seconds), `m` (minutes), `h` (hours), `d` (days), `w` (weeks), `M` (months, 30d), or `y` (years, 365d) |
| `headers` | Set custom headers, such as `X-Frame-Options`, for static content served from this location. |
| `index` | List the static files to serve your application, such as the `index.html` file. This key expects a collection. This only works if access to the file or files is "allowed" by the `allow` or `rules` key for this location. |
| `rules` | Specify overrides for a location. Use a regular expression to match a request. If an incoming request matches the rule, then regular handling of the request is overridden by the keys used in the rule. |
| `passthru` | Set the URL used in case a static file or PHP file cannot be found. Typically, this URL is the front controller for your applications, such as `/index.php` or `/app.php`. |
| `root` | Set the path relative to the root of the application that is exposed on the web. The public directory (location "/") for a Cloud project is set to "pub" by default. |
| `scripts` | Allow loading scripts in this location. Set the value to `true` to allow scripts. |

Our default configuration allows the following:

-  From the root (`/`) path, only web and media can be accessed
-  From the `~/pub/static` and `~/pub/media` paths, any file can be accessed

The following example shows the default configuration in the `.magento.app.yaml` file for a set of web-accessible locations associated with an entry in the  [`mounts` property](properties.md#mounts):

```yaml
 # The configuration of app when it is exposed to the web.
web:
    locations:
        "/":
            # The public directory of the app, relative to its root.
            root: "pub"
            # The front-controller script to send non-static requests to.
            passthru: "/index.php"
            index:
                - index.php
            expires: -1
            scripts: true
            allow: false
            rules:
                \.(css|js|map|hbs|gif|jpe?g|png|tiff|wbmp|ico|jng|bmp|svgz|midi?|mp?ga|mp2|mp3|m4a|ra|weba|3gpp?|mp4|mpe?g|mpe|ogv|mov|webm|flv|mng|asx|asf|wmv|avi|ogx|swf|jar|ttf|eot|woff|otf|html?)$:
                    allow: true
                ^/sitemap(.*)\.xml$:
                    passthru: "/media/sitemap$1.xml"
        "/media":
            root: "pub/media"
            allow: true
            scripts: false
            expires: 1y
            passthru: "/get.php"
        "/static":
            root: "pub/static"
            allow: true
            scripts: false
            expires: 1y
            passthru: "/front-static.php"
            rules:
                ^/static/version\d+/(?<resource>.*)$:
                    passthru: "/static/$resource"

```

>[!NOTE]
>
>This example shows the default web configuration for a Cloud project configured to support a single domain. For a project that requires support for multiple websites or stores, the `web` configuration must be set up to support shared domains. See [Configure locations for shared domains](../store/multiple-sites.md#configure-locations-for-shared-domains).
