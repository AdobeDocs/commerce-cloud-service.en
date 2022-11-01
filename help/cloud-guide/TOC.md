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
    + [Starter workflow](architecture/starter-develop-deploy-workflow.md)
    + [Pro architecture](architecture/pro-architecture.md)
    + [Pro workflow](architecture/pro-develop-deploy-workflow.md)
    + [Scaled architecture](architecture/scaled-architecture.md)
+ Release notes {#release-notes}
    + [Cloud tools suite](release-notes/cloud-tools.md)
    + [ECE-Tools package](release-notes/ece-tools-package.md)
    + [Cloud Patches](release-notes/cloud-patches.md)
    + [Cloud Docker](release-notes/cloud-docker.md)
    + [Cloud Components](release-notes/cloud-components.md)
    + [Backward-incompatible changes](release-notes/backward-incompatible-changes.md)
    + [Release note archive](release-notes/cloud-release-archive.md)
+ Cloud project {#project}
    + [Project overview](project/overview.md)
    + [Project structure](project/file-structure.md)
    + [User access](project/user-access.md)
    + [Multi-factor authentication](project/multi-factor-authentication.md)
    + [Outgoing emails](project/outgoing-emails.md)
    + [SenGrid mail service](project/sendgrid.md)
    + [Branch management](project/console-branches.md)
+ Developer tools {#dev-tools}
    + [Cloud CLI](dev-tools/cloud-cli.md)
    + ECE-Tools {#ece-tools}
        + [Package overview](dev-tools/package-overview.md)
        + [One-time upgrade to use ECE-Tools](dev-tools/install-package.md)
        + [Update ECE-Tools package](dev-tools/update-package.md)
        + [Error reference](dev-tools/error-reference.md)
    + [Regional IP addresses](dev-tools/regional-ip-addresses.md)
+ Development {#develop}
    + [Overview](development/overview.md)
    + [Authentication keys](development/authentication-keys.md)
    + [Clone and branch management](development/cli-branches.md)
    + [Secure connections](development/secure-connections.md)
    + [PrivateLink service](development/privatelink-service.md)
    + [Protective block](development/protective-block.md)
    + [Restore environment](development/restore-environment.md)
    + Upgrades and patches {#upgrade}
        + [Best practices](development/best-practices.md)
        + [Upgrade Commerce](development/commerce-version.md)
        + [Apply patches](development/apply-patches.md)
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
        + [Crons](application/crons-property.md)
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
+ Store configuration {#configure-store}
    + [Overview](store/overview.md)
    + [Best practices](store/best-practices.md)
    + [Custom theme](store/custom-theme.md)
    + [Extensions](store/extensions.md)
    + [B2B module](store/b2b-module.md)
    + [Multiple sites](store/multiple-sites.md)
    + [Site map and search engine robots](store/robots-sitemap.md)
    + [PayPal payment methods](store/paypal.md)
    + [Configuration management](store/store-settings.md)
+ Deployment {#deploy}
    + [Optimization](deploy/optimization.md)
    + [Deployment process](deploy/process.md)
    + [Deployment best practices](deploy/best-practices.md)
    + [Scenario-based deployment](deploy/scenario-based.md)
    + [Zero downtime deployment](deploy/reduce-downtime.md)
    + [Static content deployment](deploy/static-content.md)
    + [Smart wizards](deploy/smart-wizards.md)
    + [Deploy to Staging and Production](deploy/staging-production.md)
+ Test {#test}
    + [Testing guidance](test/guidance.md)
    + [Sample data](test/sample-data.md)
    + [Xdebug](test/debug.md)
+ Launch site {#launch}
    + [Overview](launch/overview.md)
    + [Launch checklist](launch/checklist.md)
    + [Launch steps](launch/steps.md)
+ Monitor {#monitor}
    + [Logs](monitor/log-locations.md)
    + [Performance](monitor/performance.md)
    + [New Relic service](monitor/new-relic.md)
+ Storage {#storage}
    + [Manage disk space](storage/manage-disk-space.md)
    + [Profile database queries](storage/profile-database-queries.md)
    + [Snapshots and backup management](storage/snapshots.md)
