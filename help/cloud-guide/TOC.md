---
user-guide-title: Commerce on Cloud Infrastructure Guide
user-guide-description: Learn how to manage the Adobe Commerce application on cloud infrastructure.
product: magento
---

# Commerce on Cloud Infrastructure {#cloud}

+ [Commerce](overview.md)
+ Architecture {#architecture}
    + [Architecture](architecture/cloud-architecture.md)
    + [Starter architecture](architecture/starter-architecture.md)
    + [Starter develop-and-deploy workflow](architecture/starter-develop-deploy-workflow.md)
    + [Pro architecture](architecture/pro-architecture.md)
    + [Pro develop-and-deploy workflow](architecture/pro-develop-deploy-workflow.md)
    + [Split-tier architecture](architecture/split-tier-architecture.md)
+ Cloud project {#project}
    + [Project overview](project/overview.md)
    + [Project structure](project/file-structure.md)
    + [User access](project/user-access.md)
    + [Multi-factor authentication](project/multi-factor-authentication.md)
    + [Outgoing emails](project/outgoing-emails.md)
    + [Branch management](project/console-branches.md)
+ Developer tools {#dev-tools}
    + [Cloud CLI](dev-tools/cloud-cli.md)
    + Ece-tools {#ece-tools}
        + [Package overview](dev-tools/package-overview.md)
        + [One-time upgrade to use Ece-tools](dev-tools/install-package.md)
        + [Update Ece-tools package](dev-tools/update-package.md)
    + [Regional IP addresses](dev-tools/regional-ip-addresses.md)
+ Local development {#develop}
    + [Clone and branch management](development/cli-branches.md)
    + [Secure connections](development/secure-connections.md)
    + [Restore environment](development/restore-environment.md)
+ Integrations {#integrations}
    + [Overview](integrations/overview.md)
    + [Bitbucket](integrations/bitbucket.md)
    + [GitHub](integrations/github.md)
    + [GitLab](integrations/gitlab.md)
    + [Health notifications](integrations/health-notifications.md)
+ Application {#configure-app}
    + [Configure application deployment](application/configure-app-yaml.md)
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
+ Environment {#configure-env}
    + [Configure environment deployment](environment/configure-env-yaml.md)
    + [Variable levels and options](environment/variable-levels.md)
    + Override variables {#stage}
        + [Environment variables](environment/variables-intro.md)
        + [ADMIN](environment/variables-admin.md)
        + [Cloud variables](environment/variables-cloud.md)
        + [Global](environment/variables-global.md)
        + [Build](environment/variables-build.md)
        + [Deploy](environment/variables-deploy.md)
        + [Post-deploy](environment/variables-post-deploy.md)
    + Configure notifications {#log}
        + [Notifications](environment/set-up-notifications.md)
        + [Log handlers](environment/log-handlers.md)
+ Routes {#configure-routes}
    + [Configure routes](routes/routes-yaml.md)
    + [Caching](routes/caching.md)
    + [Redirects](routes/redirects.md)
    + [Server-side includes](routes/server-side-includes.md)
+ Services {#configure-service}
    + [Configure services](services/services-yaml.md)
    + [Elasticsearch](services/elasticsearch.md)
    + [MySQL](services/mysql.md)
    + [OpenSearch](services/opensearch.md)
    + [RabbitMQ](services/rabbitmq.md)
    + [Redis](services/redis.md)
+ Fastly services {#cdn}
+ Store configuration {#store}
    + Overview
    + Best practices
    + Custom theme
    + [PayPal payment methods](store/paypal.md)
    + [B2B module](store/b2b-module.md)
    + Multiple sites
+ Deployment {#deploy}
    + [Optimization](deploy/optimization.md)
    + [Deployment process](deploy/process.md)
    + [Scenario-based deployment](deploy/scenario-based.md)
    + [Zero downtime deployment](deploy/reduce-downtime.md)
    + [Static content deployment](deploy/static-content.md)
    + [Smart wizards](deploy/smart-wizards.md)
+ Test {#test}
    + [Sample data](test/sample-data.md)
    + [Xdebug](test/debug.md)
+ Launch site {#launch}
    + [Site launch](launch/index.md)
    + [Launch checklist](launch/site-launch-checklist.md)
    + [Launch steps](launch/launch-steps.md)
+ Monitor {#monitor}
    + [Logs](monitor/log-locations.md)
    + [Error messages](monitor/error-messages.md)
    + [Performance](monitor/performance.md)
    + [New Relic service](monitor/new-relic.md)
+ Storage {#storage}
    + [Manage disk space](storage/manage-disk-space.md)
    + [Profile database queries](storage/profile-database-queries.md)
    + [Snapshots and backup management](storage/snapshots.md)
+ Release notes {#release-notes}
    + [Cloud tools suite](release-notes/cloud-tools.md)
    + [ece-tools package](release-notes/ece-release-notes.md)
    + [Cloud Patches](release-notes/mcp-release-notes.md)
    + [Cloud Docker](release-notes/mcd-release-notes.md)
    + [Cloud Components](release-notes/mcc-release-notes.md)
    + [Backward-incompatible changes](release-notes/backward-incompatible-changes.md)
    + [Release note archive](release-notes/cloud-release-archive.md)
