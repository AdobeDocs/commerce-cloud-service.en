---
user-guide-title: Commerce on Cloud Infrastructure Guide
user-guide-description: Learn how to manage the Adobe Commerce application on cloud infrastructure.
product: magento
---

# Commerce on Cloud Infrastructure {#user-guide}

+ [Commerce](overview.md)
+ Architecture {#architecture}
    + [Cloud infrastructure](architecture/cloud-architecture.md)
    + [Starter architecture](architecture/starter-architecture.md)
    + [Starter workflow](architecture/starter-develop-deploy-workflow.md)
    + [Pro architecture](architecture/pro-architecture.md)
    + [Pro workflow](architecture/pro-develop-deploy-workflow.md)
    + [Scaled architecture](architecture/scaled-architecture.md)
    + [Auto scaling](architecture/autoscaling.md)
+ [Get started](https://experienceleague.adobe.com/docs/commerce-cloud-service/start/overview.html)
+ Release notes {#release-notes}
    + [Cloud tools suite](release-notes/cloud-tools-suite.md)
    + [ECE-Tools package](release-notes/ece-tools-package.md)
    + [Cloud Patches](release-notes/cloud-patches.md)
    + [Cloud Docker package](release-notes/cloud-docker.md)
    + [Cloud Components](release-notes/cloud-components.md)
    + [Backward-incompatible changes](release-notes/backward-incompatible-changes.md)
    + [Release notes archive](release-notes/cloud-release-archive.md)
+ Cloud project {#project}
    + [Project overview](project/overview.md)
    + [Project structure](project/file-structure.md)
    + [User access](project/user-access.md)
    + [Multi-factor authentication](project/multi-factor-authentication.md)
    + [Outgoing emails](project/outgoing-emails.md)
    + [SendGrid email service](project/sendgrid.md)
    + [Console branch management](project/console-branches.md)
    + [Regional IP addresses](project/regional-ip-addresses.md)
+ Developer tools {#dev-tools}
    + [Cloud CLI](dev-tools/cloud-cli.md)
    + [Cloud Docker](dev-tools/cloud-docker.md)
    + ECE-Tools {#ece-tools}
        + [Package overview](dev-tools/package-overview.md)
        + [One-time upgrade to use ECE-Tools](dev-tools/install-package.md)
        + [Update ECE-Tools package](dev-tools/update-package.md)
        + [Error reference](dev-tools/error-reference.md)
    + Integrations {#integrations}
        + [Overview](integrations/overview.md)
        + [Bitbucket](integrations/bitbucket.md)
        + [GitHub](integrations/github.md)
        + [GitLab](integrations/gitlab.md)
        + [Health notifications](integrations/health-notifications.md)
+ Development {#develop}
    + [Overview](development/overview.md)
    + [Authentication keys](development/authentication-keys.md)
    + [CLI branch management](development/cli-branches.md)
    + [Secure connections](development/secure-connections.md)
    + Deploy {#deploy}
        + [Deployment process](deploy/process.md)
        + [Optimization](deploy/optimization.md)
        + [Best practices](deploy/best-practices.md)
        + [Scenario-based deployment](deploy/scenario-based.md)
        + [Zero downtime deployment](deploy/reduce-downtime.md)
        + [Static content deployment](deploy/static-content.md)
        + [Smart wizards](deploy/smart-wizards.md)
        + [Deploy to Staging and Production](deploy/staging-production.md)
        + [Recover from component failure](deploy/recover-failed-deployment.md)
    + Test {#test}
        + [Testing guidance](test/guidance.md)
        + [Logs](test/log-locations.md)
        + [Xdebug](test/debug.md)
        + [Sample data](test/sample-data.md)
        + [Staging and Production](test/staging-and-production.md)
    + [PrivateLink service](development/privatelink-service.md)
    + [Protective block](development/protective-block.md)
    + [Restore environment](development/restore-environment.md)
    + Storage {#storage}
        + [Manage disk space](storage/manage-disk-space.md)
        + [Profile database queries](storage/profile-database-queries.md)
        + [Back up the database](storage/database-dump.md)
        + [Snapshots and backup management](storage/snapshots.md)
    + Upgrades and patches {#upgrade}
        + [Best practices](development/best-practices.md)
        + [Upgrade Commerce version](development/commerce-version.md)
        + [Apply patches](development/apply-patches.md)
+ Configuration {#configure}
    + [Overview](environment/overview.md)
    + Application {#app}
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
    + Environment {#env}
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
    + Routes {#routes}
        + [Configure routes](routes/routes-yaml.md)
        + [Caching](routes/caching.md)
        + [Redirects](routes/redirects.md)
        + [Server-side includes](routes/server-side-includes.md)
    + Services {#service}
        + [Configure services](services/services-yaml.md)
        + [Elasticsearch](services/elasticsearch.md)
        + [MySQL](services/mysql.md)
        + [OpenSearch](services/opensearch.md)
        + [RabbitMQ](services/rabbitmq.md)
        + [Redis](services/redis.md)
+ Fastly services {#cdn}
    + [Overview](cdn/fastly.md)
    + Fastly Setup {#setup-fastly}
        + [Configure Fastly services](cdn/fastly-configuration.md)
        + [Customize cache configuration](cdn/fastly-custom-cache-configuration.md)
        + [Customize error and maintenance pages](cdn/fastly-custom-response.md)
    + [Web Application Firewall](cdn/fastly-waf-service.md)
    + [Image Optimization](cdn/fastly-image-optimization.md)
    + Customize with VCL {#custom-vcl-snippets}
        + [Get started](cdn/fastly-vcl-custom-snippets.md)
        + [Reroute requests to a CMS backend](cdn/fastly-vcl-wordpress.md)
        + [Block referral spam](cdn/fastly-vcl-badreferer.md)
        + [IP allowlist](cdn/fastly-vcl-allowlist.md)
        + [IP blocklist](cdn/fastly-vcl-blocking.md)
        + [Bypass Fastly cache](cdn/fastly-vcl-bypass-to-origin.md)
    + [Fastly troubleshooting](cdn/fastly-troubleshooting.md)
+ Store settings {#configure-store}
    + [Overview](store/overview.md)
    + [Best practices](store/best-practices.md)
    + [Custom theme](store/custom-theme.md)
    + [Extensions](store/extensions.md)
    + [B2B module](store/b2b-module.md)
    + [Multiple sites](store/multiple-sites.md)
    + [Site map and search engine robots](store/robots-sitemap.md)
    + [PayPal payment methods](store/paypal.md)
    + [Configuration management](store/store-settings.md)
+ Launch site {#launch}
    + [Overview](launch/overview.md)
    + [Launch checklist](launch/checklist.md)
    + [Launch steps](launch/steps.md)
+ Monitor site {#monitor}
    + [Performance](monitor/performance.md)
    + [New Relic service](monitor/new-relic.md)
