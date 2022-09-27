---
user-guide-title: Commerce on Cloud Infrastructure Guide
user-guide-description: Learn how to manage the Adobe Commerce application on cloud infrastructure.
product: magento
---

# Commerce on Cloud Infrastructure {#cloud}

+ [Commerce](overview.md)
+ Architecture {#architecture}
    + [Cloud infrastructure](architecture/cloud-architecture.md)
    + [Split-tier architecture](architecture/split-tier-architecture.md)
+ [Getting started](https://experienceleague.corp.adobe.com/docs/commerce-cloud-service/start/overview.md)
+ Developer tools {#dev-tools}
    + [Ece-tools package](dev-tools/ece-tools.md)
    + Cloud CLI {#cloud-cli}
        + [magento-cloud CLI](dev-tools/magento-cloud-cli.md)
        + [Variable levels and options](environment/variable-levels.md)
+ Application {#app-config}
    + [Configure application deployment](application/magento-app-yaml.md)
    + [PHP settings](application/php-settings.md)
    + Properties {#properties}
        + [Application properties](application/properties.md)
        + [Cron](application/crons-property.md)
        + [Firewall (Starter only)](application/firewall-property.md)
        + [Hooks](application/hooks-property.md)
        + [Variables](application/variables-property.md)
        + [Web](application/web-property.md)
        + [Workers](application/workers-property.md)
    + [Set cache for static files](application/set-cache.md)
+ Environment {#env-config}
    + [Configure environment deployment](environment/magento-env-yaml.md)
    + Override variables {#stage}
        + [Environment variables](environment/variables-intro.md)
        + [ADMIN](environment/variables-admin.md)
        + [MAGENTO_CLOUD](environment/variables-cloud.md)
        + [Global](environment/variables-global.md)
        + [Build](environment/variables-build.md)
        + [Deploy](environment/variables-deploy.md)
        + [Post-deploy](environment/variables-post-deploy.md)
    + Configure notifications {#log}
        + [Notifications](environment/set-up-notifications.md)
        + [Log handlers](environment/log-handlers.md)
+ Services {#service-config}
    + [Configure services](services/services-yaml.md)
    + [Elasticsearch](services/elasticsearch.md)
    + [MySQL](services/mysql.md)
    + [OpenSearch](services/opensearch.md)
    + [RabbitMQ](services/rabbitmq.md)
    + [Redis](services/redis.md)
+ Monitor {#monitor}
    + [Logs](monitor/log-locations.md)
    + [Performance](monitor/performance.md)
+ Storage {#storage}
    + [Backup and recovery](storage/backup-and-recovery.md)
    + [Manage disk space](storage/manage-disk-space.md)
    + [Profile database queries](storage/profile-database-queries.md)
+ Test {#test}
    + [Xdebug](test/xdebug.md)
+ [Release notes](release-notes/cloud-tools.md)
