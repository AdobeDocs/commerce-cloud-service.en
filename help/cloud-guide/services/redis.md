---
title: Set up Redis service
description: Learn how to set up and optimize Redis as a backend cache solution for Adobe Commerce on cloud infrastructure.
---

# Set up Redis service

[Redis](https://redis.io) is an optional, backend cache solution that replaces the Zend Framework [Zend_Cache_Backend_File](https://framework.zend.com/apidoc/1.0/Zend_Cache/Backend/Zend_Cache_Backend_File.html), which Adobe Commerce uses by default.

See [Configure Redis](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/cache/redis/config-redis.html) in the _Configuration guide_.

{{service-instruction}}

**To enable Redis**:

1. Add the required name and type to the `.magento/services.yaml` file.

   ```yaml
   myredis:
       type: redis:<version>
   ```

   To provide your own Redis configuration, add a `core_config` key in your `.magento/services.yaml` file:

   ```yaml
   cache:
       type: redis:<version>
   ```

1. Configure the relationships in the `.magento.app.yaml` file.

   ```yaml
   runtime:
       extensions:
           - redis

   relationships:
       redis: "redis:redis"
   ```

1. Add, commit, and push your code changes.

   ```bash
   git add -A && git commit -m "Enable redis service" && git push origin <branch-name>
   ```

1. [Verify the service relationships](services-yaml.md#service-relationships).

{{change-service-version}}

## Using the Redis CLI

Assuming your Redis relationship is named `redis`, you can access it using the `redis-cli` tool.

1. Use SSH to connect to the Integration environment with Redis installed and configured.

1. Open an SSH tunnel to a host.

   ```bash
   redis-cli -h redis.internal
   ```

## Get installed Redis version

Use the following command to get the Redis version installed on an Integration environment:

```bash
redis-cli -h redis.internal info | grep version
```

```terminal
redis_version:5.0.0
gcc_version:6.3.0
```

To get the Redis version installed on a Staging or Production environment, use the `redis-server` command:

```bash
redis-server -v
```

```terminal
Redis server v=5.0.5 sha=947ee0b5:0 malloc=jemalloc-5.1.0 bits=64 build=c1ca234caf5bd678
```

## Troubleshooting Redis

See the following Adobe Commerce Support articles for help with troubleshooting Redis problems:

-  [Redis issue delay Admin login or checkout](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/redis-issue-delay-magento-admin-login-or-checkout.html)
-  [Extended Redis cache implementation Magento Commerce and Cloud 2.3.5+](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/best-practices/redis/extended-redis-cache-implementation-magento-commerce-2.3.5.html)
-  [MDVA-30102 Magento patch: Redis cache getting full](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/support-tools/patches/mdva-30102-magento-patch-redis-cache-getting-full.html)
-  [Managed alerts on Magento Commerce: Redis memory warning alert](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/support-tools/managed-alerts/managed-alerts-on-magento-commerce-redis-memory-warning-alert.html)
-  [Managed alerts on Magento Commerce: Redis memory critical alert](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/support-tools/managed-alerts/managed-alerts-on-magento-commerce-redis-memory-critical-alert.html)
-  [Redis troubleshooter](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/redis-troubleshooter.html)
