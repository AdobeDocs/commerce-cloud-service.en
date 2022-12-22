---
title: Customize cache configuration
description: Learn how to review and customize cache configuration settings after Fastly service setup is complete.
exl-id: f1fc85d4-7867-4bb5-9f11-bc8d2d80383b
---
# Customize cache configuration

After you set up and test the Fastly service in your Staging and Production environments, review and customize cache configuration settings. For example, you can update settings to enable force TLS to redirect HTTP requests to Fastly, update purge settings, and enable basic authentication to password-protect your site during development.

The following sections provide an overview and instructions for configuring some cache settings. Find additional information about the available configuration options in the [Fastly CDN Module for Magento 2](https://github.com/fastly/fastly-magento2/tree/master/Documentation) documentation.

## Force TLS

Fastly provides the _Force TLS_ option for redirecting unencrypted requests (HTTP) to Fastly. After your Staging or Production environment has been provisioned with a [valid SSL/TLS certificate](fastly-configuration.md#provision-ssltls-certificates), you can update the Fastly configuration for your store to enable the Force TLS option. See the Fastly [Force TLS guide](https://github.com/fastly/fastly-magento2/blob/master/Documentation/Guides/FORCE-TLS.md) in the _Fastly CDN Module for Magento 2_ documentation.

>[!NOTE]
>
>Enabling the Force TLS option is a recommended best practice for Adobe Commerce on cloud infrastructure stores.

## Extend Fastly timeout

The Fastly service configuration specifies a default timeout period of 180 seconds for HTTPS requests to the Admin. Any request processing that exceeds the timeout period returns a 503 error. As a result, you can receive 503 errors in response to requests that require lengthy processing, or when trying to perform bulk operations.

To complete bulk actions that take longer than 3 minutes change the _Admin path timeout_ value_ to prevent 503 errors.

>[!NOTE]
>
>To extend Fastly timeout parameters for other than Admin in the Fastly UI, see [Increase Timeouts for Long Jobs](https://github.com/fastly/fastly-magento2/blob/master/Documentation/Guides/Edge-Modules/EDGE-MODULE-INCREASE-TIMEOUTS-LONG-JOBS.md).

**To extend the Fastly timeout for the Admin**:

{{admin-login-step}}

1. Click **Stores** > Settings > **Configuration** > **Advanced** > **System** and expand **Full Page Cache**.

1. In the _Fastly Configuration_ section, expand **Advanced Configuration**.

1. Set the **Admin path timeout** value in seconds. This value cannot be more than 10 minutes (600 seconds).

1. Click **Save Config** at the top of the page.

1. After the page reloads, select **Upload VCL to Fastly** in the _Fastly Configuration_ section.

Fastly retrieves the Admin path for generating the VCL file from the `app/etc/env.php` configuration file.

## Configure purge options

Fastly provides multiple types of purge options on your Magento Cache Management page, including options to purge product category, product assets, and content. When enabled, Fastly watches for events to automatically purge those caches. If you disable a purge option, you can manually purge Fastly caches after finishing updates through the Cache Management page.

The purge options include:

- **Purge category**–Purges product category content (not product content) when you add and update a single product. You may want to keep this disabled and enable purge product, which purges products and product categories.
- **Purge product**–Purges all product and product category content when saving a single modification to a product. Enabling purge product can be helpful to immediately get updates to customers when changing a price, adding a product option, and when product inventory is out-of-stock.
- **Purge CMS page**–Purges page content when updating and adding pages to the Adobe Commerce CMS. For example, you may want to purge when updating your Terms and Conditions or Return policy. If you rarely make these changes, you could disable automatic purging.
- **Soft purge**–Sets changed content to stale and purges according to the stale timing. In addition to the stale timings, customers are served stale content while Fastly updates the content in the background.

![Configure purge options](../../assets/cdn/fastly-purge-options.png)

**To configure Fastly purge options**:

1. In the _Fastly Configuration_ section, expand **Advanced Configuration** to display the purge options.

1. For each purge option, select **Yes** to enable automatic purging, or **No** to disable automatic purging.

   When you disable a purge option, you must manually purge the cache for that category from the _Cache Management_ page.

1. Click **Save Config** at the top of the page.

1. After the page reloads, select **Upload VCL to Fastly** in the _Fastly Configuration_ section.

For more information, see [the Fastly configuration options](https://github.com/fastly/fastly-magento2/blob/21b61c8189971275589219d418332798efc7db41/Documentation/CONFIGURATION.md#further-configuration-options).

## Configure GeoIP handling

The Fastly module includes GeoIP handling to automatically redirect visitors or provide a list of stores matching their obtained country code. If you already use an extension for GeoIP handling, you may need to verify the features with Fastly options.

**To set up GeoIp handling**:

{{admin-login-step}}

1. Click **Stores** > Settings > **Configuration** > **Advanced** > **System** and expand **Full Page Cache**.

1. In the _Fastly Configuration_ section, expand **Advanced Configuration**.

1. Scroll down and select **Yes** to **Enable GeoIP**. Additional configuration options display.

1. For GeoIP Action, select if the visitor is automatically redirected with **Redirect** or provided a list of stores to select from with **Dialog**.

1. For **Country Mapping**, select **Add** to enter a two-letter country code to map with a specific Adobe Commerce store from a list. For a list of country codes, see [this site](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2).

   ![Add GeoIP country maps](/help/assets/cdn/fastly-geo-code.png)

1. Click **Save Config** at the top of the page.

1. After page reload, select **Upload VCL to Fastly** in the _Fastly Configuration_ section.

>[!NOTE]
>
>The current Adobe Commerce Fastly GeoIP module implementation does not support redirects between multiple websites.

Fastly also provides a series of [geolocation-related VCL features](https://docs.fastly.com/guides/vcl/geolocation-related-vcl-features) for customized geolocation coding.

## Enable Fastly Edge modules

Fastly Edge Modules is a flexible framework that allows definition of UI components and associated VCL code through a template. These modules make it easy to customize and extend the Fastly service configuration through the user interface instead of using custom VCL snippets.

Edge modules allow you to enable specific functionality like CORS headers, Cloud Sitemap rewrites, and to configure integration between your Adobe Commerce store and other CMSs or back ends.

To access the Edge Modules menu to view, configure, and manage the available modules, turn on the _Enable Fastly Edge modules_ option. See [Fastly Edge Modules](https://github.com/fastly/fastly-magento2/blob/master/Documentation/Guides/Edge-Modules/EDGE-MODULES.md) in the Fastly CDN module documentation.

## Configure back ends and Origin shielding

Back-end settings provide fine tuning for Fastly performance with Origin shielding and timeouts. A _back end_ is a specific location (IP or domain) with configured Origin shield and timeout settings for checking and providing cached content.

_Origin shielding_ routes all requests for your store to a specific Point of Presence (POP). When a request is received, the POP checks for cached content and provides it. If it is not cached, it continues to the Shield POP, then to the Origin server which caches the content. The shields reduce traffic directly to the origin.

The default Fastly VCL code specifies default values for Origin shielding and timeouts for your Adobe Commerce on cloud infrastructure sites. We recommend using the default values. In some case, you might need to modify the default values. For example, if you are getting numerous time to first byte (TTFB) errors, you might need to adjust the _first byte timeout_ value.

>[!NOTE]
>
>If your site requires functionally delivered through a backend integration like [Wordpress](fastly-vcl-wordpress.md), customize your Fastly service configuration to add the backend and manage redirects from your Adobe Commerce store to Wordpress. For details, see [Fastly Edge Modules - Other CMS/Backend integration](https://github.com/fastly/fastly-magento2/blob/master/Documentation/Guides/Edge-Modules/EDGE-MODULE-OTHER-CMS-INTEGRATION.md) in the Fastly module documentation.

**To review the back end setting configuration**:

{{admin-login-step}}

1. Click **Stores** > Settings > **Configuration** > **Advanced** > **System** and expand **Full Page Cache**.

1. Expand the **Fastly Configuration** section.

1. Expand **Backend settings** and select the gear to check the default back end. A modal opens that shows current settings with options to change them.

   ![Modify the back end](../../assets/cdn/fastly-backend.png)

1. Select the **Shield** location (or data center).

   The default Fastly configuration for your project sets the location closest to your Cloud service region. If you need to change it, select a location close to the default location.

1. Modify the timeout values (in microseconds) for the connection to the shield, time between bytes, and time for the first byte. We recommend keeping the default timeout settings.

1. Optionally, select to **Activate the backend and Shield after editing or saving**.

1. Click **Upload** to save your changes and upload them to the Fastly servers.

1. In the Admin, select **Save Config**.

For more information, see the [Backend settings guide](https://github.com/fastly/fastly-magento2/blob/21b61c8189971275589219d418332798efc7db41/Documentation/Guides/BACKEND-SETTINGS.md) in the Fastly module documentation.

## Basic authentication

Basic authentication is a feature to protect every page and asset on your site
with a username and password. We **do not recommend** activating basic
authentication on your Production environment. You can configure it on Staging
to protect your site during the development process. See the [Basic Authentication Guide](https://github.com/fastly/fastly-magento2/blob/master/Documentation/Guides/BASIC-AUTH.md) in the Fastly CDN module documentation.

If you add user access and enable basic authentication on Staging, you can still
access the Admin without requiring additional credentials.

## Create custom VCL snippets

Fastly supports a customized version of the Varnish Configuration Language (VCL) to customize the Fastly service configuration. For example, you can allow, block, or redirect access for specific users or IPs using VCL code blocks with edge and ACL dictionaries.

For instructions to create custom VCL snippets, edge dictionaries, and ACLs, see [Custom Fastly VCL snippets](fastly-vcl-custom-snippets.md).

>[!NOTE]
>
>Before adding custom VCL code, edge dictionaries, and ACLs to your Fastly module configuration, verify that the Fastly caching service works with the default configuration. See [Set up Fastly](fastly-configuration.md).

## Manage domains

For both Starter and Pro projects, you can use the [!UICONTROL Domains] option to add and manage the Fastly domain configuration for your store.

- For Starter projects, go to Project URL under the [!UICONTROL Domains] tab in the Project Web interface to add your Project URL.

- For Pro projects, submit an [Adobe Commerce Support ticket](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) to add the domain to your Cloud configuration rbefore you can add the domain to your cloud configuration. Also, after you add the domain configuration to Adobe Commerce, the Support team must update the Fastly domain configuration for your project.

**To manage Fastly domain configuration from the Admin**:

{{admin-login-step}}

1. Select **Stores** > Settings > **Configuration** > **Advanced** > **System** and expand **Full Page Cache**.

1. In the Admin _Fastly Configuration_ section, select **Domains**.

1. Click **Manage Domains** to open the Domains page.

1. Add the top-level and subdomain names for the stores in the Cloud environment.

   You can only specify domains that have already been added to your Cloud infrastructure configuration.

   ![Add Fastly domain configuration for Starter](../../assets/cdn/fastly-starter-activate-domain.png)

1. Click **Activate** to update the Fastly domain configuration.


>[!NOTE]
>
>If the same domain has been configured on a different Fastly account, you must submit an Adobe Commerce support ticket to request Domain Delegation before you can add the domain to Adobe Commerce. See [Multiple Fastly accounts and assigned domains](fastly.md#multiple-fastly-accounts-and-assigned-domains).


## Enable Maintenance Mode

Use the _Maintenance Mode_ option to allow administrative access to your site from specified IP addresses while returning an error page for all other requests.

**To enable Maintenance mode with Administrative access**:

1. Open the _Fastly configuration_ section in the Admin.

1. In the _Edge ACL_ section, update the `maint_allow` access control list (ACL) with the administrative IP addresses that can access your store while it is in Maintenance mode.

   ![Update IP maintenance mode allow list](../../assets/cdn/fastly-maint-allowlist.png)

1. In the _Maintenance Mode_ section, select **Enable Maintenance Mode**.

   After you enable maintenance mode, all traffic is blocked except requests from the IP addresses in the `maint_allowlist` ACL. You can update the `maint_allowlist` to change the IP addresses in the ACL.

   For detailed configuration instructions, see the [Maintenance Mode guide](https://github.com/fastly/fastly-magento2/blob/master/Documentation/Guides/MAINTENANCE-MODE.md) in the Fastly CDN for Magento 2 module documentation.
