---
title: Caching
description: Learn how to enable caching for your Adobe Commerce on cloud infrastructure environments.
feature: Cloud, Cache, Routes
exl-id: 4856aa94-2947-4dc8-b0d1-0960869dc39c
---
# Caching

You can enable caching in your cloud infrastructure project environment. If you disable caching, Adobe Commerce directly serves the files.

{{route-placeholder}}

## Set up caching

Enable caching for your application by configuring cache rules in the `.magento/routes.yaml` file as follows:

```yaml
http://{default}/:
    type: upstream
    upstream: php:php
    cache:
        enabled: true
        headers: [ "Accept", "Accept-Language", "X-Language-Locale" ]
        cookies: ["*"]
        default_ttl: 60
```

## Route-based caching

Enable fine-grained caching by setting up caching rules for several routes separately as the following example shows:

```yaml
http://{default}/:
    type: upstream
    upstream: php:php
    cache:
        enabled: true

http://{default}/path/:
    type: upstream
    upstream: php:php
    cache:
        enabled: false

http://{default}/path/more/:
    type: upstream
    upstream: php:php
    cache:
        enabled: true
```

The preceding example caches the following routes:

-  `http://{default}/`
-  `http://{default}/path/more/`
-  `http://{default}/path/more/etc/`

And the following routes are **not** cached:

-  `http://{default}/path/`
-  `http://{default}/path/etc/`

>[!NOTE]
>
>Regular expressions in routes are **not** supported.

## Cache duration

The cache duration is determined by the `Cache-Control` response header value. If no `Cache-Control` header is in the response, we use the `default_ttl` key.

## Cache key

To decide how to cache a response, Adobe Commerce builds a cache key that depends on several factors and store the response associated with this key. When a request comes with the same cache key, the response is reused. Its purpose is similar to the HTTP [`Vary` header](https://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.44).

The parameters `headers` and `cookies` keys enable you to change this cache key.

The default value for these keys follows:

```yaml
cache:
    enabled: true
    headers: ["Accept-Language", "Accept"]
    cookies: ["*"]
```

## Cache attributes

### `enabled`

When set to `true`, enable the cache for this route. When set to `false`, disable the cache for this route.

### `headers`

Defines on which values the cache key must depend.

For example, if the `headers` key is the following:

```yaml
cache:
    enabled: true
    headers: ["Accept"]
```

Then Adobe Commerce caches a different response for each value of the `Accept` HTTP header.

### `cookies`

The `cookies` key defines on which values the cache key must depend.

For example:

```yaml
cache:
    enabled: true
    cookies: ["value"]
```

The cache key depends on the value of the `value` cookie in the request.

A special case exists if the `cookies` key has the `["*"]` value. This value means that any request with a cookie bypasses the cache. This is the default value.

>[!NOTE]
>
>You cannot use wildcards in the cookie name. Use either a precise cookie name or match all cookies with an asterisk (`*`). For example, `SESS*` or `~SESS` are currently **not** valid values.

Cookies have the following restrictions:

-  You can set maximum of **50 cookies** in the system. Otherwise, the application throws an `Unable to send the cookie. Maximum number of cookies would be exceeded` exception.
-  A maximum cookie size is **4096 bytes**. Otherwise, the application throws an `Unable to send the cookie. Size of '%name' is %size bytes` exception.

### `default_ttl`

If the response does not have a `Cache-Control` header, the `default_ttl` key is used to define the cache duration, in seconds. The default value is `0`, which means nothing is cached.
