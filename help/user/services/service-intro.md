---
title: Configure services
description: Introduction to services and service compatibility chart for Magento on Cloud Manager.
---

# Configure services

You can customize the use of the various services for Magento...

## Service compatibility

The following table lists the services and the version support based on Magento application. (This is a sample table taken from the Magento Cloud guide and is not relevant for Commerce Manager.)

| Service         | Magento 2.4         | Magento 2.3                                                                                                                                         | Magento 2.2                                                                                                                                                                                                                                                                                                |
| --------------- | ------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `elasticsearch` | 7.5.x, 7.6.x, 7.7.x | **Magento version 2.3.5 and later**— 5.2, 6.5, 6.8, 7.5, 7.6, 7.7<br>**Magento version 2.3.1 to 2.3.4**— 5.2, 6.5<br>**Magento version 2.3.0**— 5.2 | **Magento version 2.2.8 and later**— 5.2, 6.5 <br>**Magento version 2.2.0 to 2.2.7**— 5.2                                                                                                                                                                                                                  |
| `mariadb`       | 10.2, 10.3, 10.4    | **Magento version 2.3.0 to 2.3.5**–10.1 to 10.2<br>                                                                                                 | 10.1 to 10.2                                                                                                                                                                                                                                                                                               |
| `nginx`         |                     | 1.9                                                                                                                                                 | 1.9                                                                                                                                                                                                                                                                                                        |
| `node`          |                     | 6, 8, 10, 11                                                                                                                                        | 6, 8, 10, 11                                                                                                                                                                                                                                                                                               |
| `php`           | 7.3, 7.4            | **Magento version 2.3.4 and later**— 7.1, 7.2, 7.3<br>**Magento version 2.3.3**— 7.1, 7.2, 7.3<br>**Magento version 2.3.0 to 2.3.2**— 7.1, 7.2      | **Magento version 2.2.10 and later**— 7.1, 7.2<br>**Magento version 2.2.5 to 2.2.9**— 7.0, 7.1<br>**Magento version 2.2.4 and earlier**— 7.0.2, 7.0.4, ~7.0.6, 7.1<br><br>**Note:** Beginning with {{ site.data.var.ct }} v2002.1.0, you must use PHP version 7.1.3 or later for both Magento 2.2 and 2.3. |
| `rabbitmq`      | 3.8                 | **Magento version 2.3.5**–3.8<br>**Magento version 2.3.3 - 2.3.4**— 3.7, 3.8<br>**Magento version 2.3.0 to 2.3.3**— 3.7                             | 3.5                                                                                                                                                                                                                                                                                                        |
| `redis`         | 5.x                 | **Magento version 2.3.1 - 2.3.5**–4.x, 5.x<br>**Magento version 2.3.0**— 3.2, 4.0                                                                   | 3.2, 4.0, 5.0                                                                                                                                                                                                                                                                                              |
| `varnish`       | 6.x                 | **Magento version 2.3.3 to 2.3.5**— 4.0, 5.0, 6.2<br>**Magento version 2.3.0 to 2.3.2**— 4.0, 5.0                                                   | 4.0, 5.0                                                                                                                                                                                                                                                                                                   |

>[!TIP]
>
>When you set up the Elasticsearch service, check to ensure that you use a version that is compatible with the installed [Elasticsearch PHP][es-php] client. See [Check Elasticsearch software compatibility][es-cloud].

<!-- link definitions -->

[es-cloud]: https://devdocs.magento.com/cloud/project/project-conf-files_services-elastic.html#elasticsearch-software-compatibility
[es-php]: https://github.com/elastic/elasticsearch-php
