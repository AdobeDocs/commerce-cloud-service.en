---
title: Launch checklist
description: Review checklist items for site launch.
---

# Launch checklist

Before you deploy to the Production environment, download the [Launch checklist](../../assets/adobe-commerce-cloud-prelaunch-checklist.pdf), and use it with these instructions to confirm that you have completed all required configuration and testing. See an overview of the complete deployment process for Starter and Pro at [Deploy your store](https://devdocs.magento.com/cloud/live/stage-prod-live.html).

## Completely test in Production

See [Test deployment](https://devdocs.magento.com/cloud/live/stage-prod-test.html) for testing all aspects of your sites, stores, and environments. These tests include verifying Fastly, User Acceptance Tests (UAT), and performance testing.

## TLS and Fastly

Adobe provides a Let's Encrypt SSL/TLS certificate for each environment. This certificate is required for Fastly to serve secure traffic over HTTPS.

To use this certificate, you must update your DNS configuration so that Adobe can complete domain validation and apply the certificate to your environment. Each environment has a unique certificate that covers the domains for the Adobe Commerce on cloud infrastructure sites deployed in that environment. We recommend completing and the configuration updates during the [Fastly set up process](https://devdocs.magento.com/cloud/cdn/configure-fastly.html).

## Update DNS configuration with production settings

When you are ready to launch your site, you must update the DNS configuration to route traffic from your Production environment through the Fastly service.

**Prerequisites:**

-  [Set up and test Fastly in your development environment](https://devdocs.magento.com/cloud/cdn/configure-fastly.html)

-  Production environment configuration has been updated with all required domains

   Typically, you work with your Customer Technical Advisor to add all top-level domains and sub-domains required for your stores. To add or change the domains for your Production environment, submit a [Support ticket](https://support.magento.com/hc/en-us/articles/360019088251). Wait for confirmation that your project configuration has been updated.

   On Starter projects, you must add the domains to your project. See [Manage domains](https://devdocs.magento.com/cloud/cdn/configure-fastly-customize-cache.html#manage-domains).

-  SSL/TLS certificate provisioned for your production environments.

   If you added the ACME challenge records for your Production domains during the Fastly setup process, Adobe uploads the SSL/TLS certificate to your Production environment automatically when you update the DNS configuration to route traffic to the Fastly service. If you did not pre-provision the certificate, or if you updated your domains, Adobe must complete domain validation and provision the certificate, which can take up to 12 hours.

### To update DNS configuration for site launch:

1. Update the following DNS configuration for your Production site:

   -  Set all necessary redirects, especially if you are migrating from an existing site

   -  Set the zone's root resource record to address the hostname

   -  Lower the value for the Time-to-Live (TTL) to refresh DNS information to point customers to the correct Production store

      We recommend a significantly lower TTL value when switching the DNS record. This value tells the DNS how long to cache the DNS record. When shortened, it refreshes the DNS faster. For example, you can change the TTL value from three days to 10 minutes when you are updating your site. Be advised that shortening the TTL value adds load to the  DNS infrastructure. Restore the previous, higher value after site launch.

1. Add CNAME records to point the top-level domains and subdomains for your Production environment to the Fastly service `prod.magentocloud.map.fastly.net`, for example:

   | Domain or Subdomain  | CNAME|
   |----------------------|------|
   | www.your-domain.com  | prod.magentocloud.map.fastly.net|
   | mystore.your-domain.com | prod.magentocloud.map.fastly.net|

1. If needed, add A records to map the apex domain (`your-domain.com`) to the following Fastly IP addresses:

   | Apex domain     | ANAME|
   |-----------------|--------|
   | your-domain.com | `151.101.1.124`|
   | your-domain.com | `151.101.65.124`|
   | your-domain.com | `151.101.129.124`|
   | your-domain.com | `151.101.193.124`|

1. Update the Base URL.

   -  Use SSH to log in to the Production environment.

      ```bash
      magento-cloud ssh
      ```

   -  Use the CLI to change the base URL for your store.

      ```bash
      php bin/magento setup:store-config:set --base-url="https://www.your-domain.com/"
      ```

   **NOTE**: You can also update the Base URL from the [Admin](https://docs.magento.com/user-guide/stores/store-urls.html#configure-the-base-url).

1. Wait a few minutes for the site to update.

1. Test your site.

## Verify Production configuration

Make a final pass to validate the Production configuration for one or more stores. You can update the configuration in the Production environment. If settings are read-only, you may need to open an SSH connection and use CLI commands to change the configuration, or make configuration changes in your local environment. After you complete the updates, you can deploy the changes to Staging and Production environments.

The following are recommended changes and checks:

-  [Completed Outgoing email testing](../project/outgoing-emails.md)

-  [Secure configuration for Admin credentials and Base Admin URL](https://docs.magento.com/user-guide/stores/security-admin.html)

-  [Optimize all images for the web](https://devdocs.magento.com/cloud/cdn/fastly-image-optimization.html)

-  [Check minification settings for HTML, JavaScript, and CSS](../deploy/static-content.md)

## Verify Fastly caching

-  Test and verify that Fastly caching is working correctly on the Production site. For detailed tests and checks, see [Fastly testing](https://devdocs.magento.com/cloud/live/stage-prod-test.html#fastly).

-  [Ensure that the latest version of the Fastly CDN Module for Commerce is installed in your Production environment](https://devdocs.magento.com/cloud/cdn/configure-fastly.html#upgrade)

-  [Ensure that the most current version of the Fastly VCL code has been uploaded](https://devdocs.magento.com/cloud/cdn/configure-fastly.html#upload-vcl-snippets)

## Performance testing

We recommend that you review the [Performance Toolkit](https://github.com/magento/magento2/tree/2.4/setup/performance-toolkit) options as part of your pre-launch readiness process.

You can also test using the following third-party options:

-  [Siege](https://www.joedog.org/siege-home/): Traffic shaping and testing software to push your store to the limit. Hit your site with a configurable number of simulated clients. Siege supports basic authentication, cookies, HTTP, HTTPS, and FTP protocols.

-  [Jmeter](https://jmeter.apache.org/): Excellent load testing to help gauge performance for spiked traffic, like for flash sales. Create custom tests to run against your site.

-  [New Relic](https://support.newrelic.com/s/) (provided): Helps locate processes and areas of the site causing slow performance with tracked time spent per action like transmitting data, queries, Redis, and so on.

-  [WebPageTest](https://www.webpagetest.org/) and [Pingdom](https://www.pingdom.com/): Real-time analysis of your site pages load time with different origin locations. Pingdom may cost a fee. WebPageTest is a free tool.

## Security configuration

-  [Set up your Security Scan](overview.md#set-up-the-security-scan-tool)

-  [Secure configuration for Admin user](https://docs.magento.com/user-guide/stores/security-admin.html)

-  [Secure configuration for Admin URL](https://docs.magento.com/user-guide/stores/store-urls-custom-admin.html)

-  [Remove any users no longer on the Adobe Commerce on cloud infrastructure project](../project/user-access.md)

-  [Configure two-factor authentication](https://devdocs.magento.com/guides/v2.3/security/two-factor-authentication.html)

## Performance monitoring

You can use New Relic services for performance monitoring on Pro and Starter environments. On Pro plan accounts, we provide the Managed alerts for Adobe Commerce alert policy to monitor application and infrastructure performance using New Relic APM and Infrastructure agents. For details on using these services, see [Monitor performance with Managed Alerts](../monitor/new-relic.md#monitor-performance-with-managed-alerts).

### Next step

[Launch steps](steps.md)
