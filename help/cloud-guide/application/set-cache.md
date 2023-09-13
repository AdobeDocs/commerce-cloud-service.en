---
title: Set cache for static files
description: Learn to set cache storage options in the Commerce application configuration file.
feature: Cloud, Configuration, Cache, SCD
exl-id: ca6db004-47fc-45ea-b8db-c0ecc3c2136b
---
# Set cache for static files

The cache TTL (time-to-live) for your media and static files is set in the `.magento.app.yaml` configuration file using the `expires` key.

>[!NOTE]
>
>Before updating your Production environment, it is important to test changes in your Staging environment. [Submit an Adobe Commerce Support ticket](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) for help with updating the configuration on these environments.

1. Specify the TTL time (in seconds) in the [`web` property](web-property.md) of the `.magento.app.yaml` file. You can add the `expires` key under `locations` or under `"/media"` and `"/static"`.

   To prevent the cache from expiring, use the `expires: -1` key-value pair. See the following example:

   ```yaml
   # The configuration of app when it is exposed to the web.
   web:
     locations:
       "/media":
         ...
         expires: -1

       "/static":
         ...
         expires: -1
   ```

1. Add, commit, and push your code changes.

   ```bash
   git add -A && git commit -m "Set cache TTL for static files" && git push origin <branch-name>
   ```
