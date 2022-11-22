---
title: Fastly services overview
description: Learn how the Fastly services included with Adobe Commerce on cloud infrastructure help you optimize and secure content delivery operations for your Adobe Commerce sites.
exl-id: dc4500bf-f037-47f0-b7ec-5cd1291f73a1
---
# Fastly services overview

>[!WARNING]
>
>To maintain PCI compliance for Adobe Commerce sites deployed on the Cloud platform, set up Fastly on your Starter main branch, Pro Production, and Pro Staging environments. If you use Adobe Commerce in a headless deployment, we highly recommend that you use Fastly to cache GraphQL responses. See [Caching with Fastly] in the *GraphQL Developer Guide*.

Fastly provides the following services to optimize and secure content delivery operations for Adobe Commerce on cloud infrastructure projects. These services are included with Adobe Commerce on cloud infrastructure at no additional cost.

- **Content Delivery Network (CDN)**—Varnish-based service that caches your site pages, assets, CSS, and more in backend data centers you set up. As customers access your site and stores, the requests hit Fastly to load cached pages faster. The CDN service provides the following features:

- **Cache management**—Cache your site pages, assets, CSS, and more in back-end data centers that you set up to reduce bandwidth load and costs

  - Use [Fastly custom VCL snippets](fastly-vcl-custom-snippets.md) (Varnish 2.1 compliant) to modify how caching responds to requests

  - Set up [GeoIP service support](fastly-custom-cache-configuration.md#configure-geoip-handling)

  - [Force unencrypted requests over to TLS](fastly-custom-cache-configuration.md#force-tls)

  - [Customize Fastly timeout](fastly-custom-cache-configuration.md#extend-fastly-timeout) settings to prevent 503 responses on bulk operation requests

  - Create [custom error response pages](fastly-custom-response.md)

- **Security**—After you enable Fastly services for Adobe Commerce sites, additional security features are available to protect your sites and network:

  - [Web Application Firewall](fastly-waf-service.md) (WAF)—Managed web application firewall service that provides PCI-compliant protection to block malicious traffic before it can damage your production Adobe Commerce on cloud infrastructure sites and network. The WAF service is available on Pro and Starter Production environments only.

  - [Distributed Denial of Service (DDoS) protection](#ddos-protection)—Built-in DDoS protection against common attacks like Ping of Death, Smurf attacks, and other ICMP-based flood attacks.

  - [SSL/TLS certificates](fastly-configuration.md#provision-ssltls-certificates)—The Fastly service requires an SSL/TLS certificate to serve secure traffic over HTTPS.
  
    Adobe Commerce provides a Domain-validated Let's Encrypt SSL/TLS certificate for each Staging and Production environment. Adobe Commerce completes domain validation and certificate provisioning during the Fastly set up process.

- **Origin cloaking**—Prevents traffic from bypassing the Fastly WAF and hides the IP addresses of your origin servers to protect them from direct access and DDoS attacks.

  Origin cloaking is enabled by default on Adobe Commerce on cloud infrastructure Pro Production projects. To enable origin cloaking on Adobe Commerce on cloud infrastructure Starter Production projects, submit an [Adobe Commerce Support ticket](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket). If you have traffic that does not require caching, you can customize the Fastly service configuration to allow requests to [bypass the Fastly cache](fastly-vcl-bypass-to-origin.md).

- **[Image optimization](fastly-image-optimization.md)**—Offloads image processing and resizing load to the Fastly service so that servers can process orders and conversions more efficiently.

- **[Fastly CDN and WAF logs](../monitor/new-relic.md#new-relic-logs)**—For Adobe Commerce on cloud infrastructure Pro projects, you can use the New Relic Logs service to review and analyze Fastly CDN and WAF log data.

## Fastly CDN module for Magento 2

Fastly services for Adobe Commerce on cloud infrastructure use the [Fastly CDN module for Magento 2] installed in the following environments: Pro Staging and Production, Starter Production (`master` branch).

On initial provisioning or upgrade of your Adobe Commerce project, Adobe installs the latest version of the Fastly CDN module in your Staging and Production environments. When Fastly releases module updates, you receive notifications in the Admin for your environments. Adobe recommends that you update your environments to use the latest release. See [Upgrade Fastly](fastly-configuration.md#upgrade-the-fastly-module).

## Fastly service account and credentials

Adobe Commerces on cloud infrastructure projects do not require a dedicated Fastly account or account owner. Instead, each Staging and Production environment has unique Fastly credentials (API token and service ID) to configure and manage Fastly services from the Admin. You also need the credentials to submit Fastly API requests.

During project provisioning, Adobe adds your project to the Fastly service account for Adobe Commerce on cloud infrastructure and adds the Fastly credentials to the configuration for the Staging and Production environments. See [Get Fastly credentials](fastly-configuration.md#get-fastly-credentials).

### Change Fastly API token

Submit an Adobe Commerce Support ticket to change the Fastly API token credential. When you receive the new token, update your Staging or Production environment with the 

**To change the Fastly API token credential**:

1. [Submit an Adobe Commerce Support ticket](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) requesting new Fastly API credentials.

   Include your Adobe Commerce on cloud infrastructure project ID and the environments that require a new credential.

1. After you receive the new API token, update the API token value in the [Fastly credentials configuration](fastly-configuration.md#test-the-fastly-credentials) in the Admin or from the [Project Web UI environment configuration variables](../project/overview.md#configure-environment).

1. [Test the new credential](fastly-configuration.md#test-the-fastly-credentials).

1. After you update the credential, submit an Adobe Commerce Support ticket to delete the old API token.

### Multiple Fastly accounts and assigned domains

Fastly only allows you to assign an apex domain and associated subdomains to one Fastly service and account. If you have an existing Fastly account that links the same apex and subdomains used for your Adobe Commerce site, you have the following options:

-  Remove the apex and subdomains from the existing account before requesting Fastly service credentials for your Adobe Commerce on cloud infrastructure project environments. See [Working with Domains] in the Fastly documentation.

   Use this option to link the apex domain and all subdomains to the Fastly service account for Adobe Commerce on cloud infrastructure.

-  Submit an Adobe Commerce support ticket to request domain delegation so that apex and subdomains can be linked to different accounts.

   Use this option if you have an apex domain that has multiple subdomains for Adobe Commerce and non-Adobe Commerce sites, and you want to link these subdomains to different Fastly accounts.

#### Request domain delegation

*Scenario 1:*

The apex domain (`testweb.com` and `www.testweb.com`) is linked to an existing Fastly account. You have an Adobe Commerce on cloud infrastructure project configured with the following subdomains: `mcstaging.testweb.com` and `mcprod.testweb.com`. You do not want to move the apex domain to the Fastly service account for Adobe Commerce on cloud infrastructure.

Submit a [Fastly support ticket] requesting that the subdomains be delegated from the existing Fastly account to the Fastly account for Adobe Commerce on cloud infrastructure. Include your Adobe Commerce project ID in the ticket.

After the delegation is complete, your project subdomains can be added to the Fastly service account for Adobe Commerce on cloud infrastructure. See [Get Fastly credentials](fastly-configuration.md#get-fastly-credentials).

*Scenario 2:*

The apex domain (`testweb.com` and `www.testweb.com`) is linked to the Adobe Commerce on cloud infrastructure Fastly service account. You want to manage Fastly services for the `service.testweb.com` and `product-updates.testweb.com` subdomains from a different Fastly account.

Submit an Adobe Commerce Support ticket requesting that the subdomains be delegated from the Adobe Commerce on cloud infrastructure Fastly service account to the Fastly account. Include the service ID for the Fastly account in the ticket.

## DDoS protection

DDOS protection is built in to the Fastly CDN service. Once you have enabled Fastly services for your Adobe Commerce sites, Fastly filters all web and admin traffic to detect and block potential attacks.

- For attacks targeting layer 3 or 4, the Fastly service filters out traffic based on port and protocol, inspecting only HTTP or HTTPS requests. ICMP, UDP, and other network-initiated attacks are dropped at our network edge. This includes reflection and amplification attacks, which use UDP services like SSDP or NTP. By providing this level of protection, we effectively block multiple common attacks like Ping of Death, Smurf attacks, and other ICMP-based floods.

  Fastly manages TCP level attacks at the cache layer. This strategy provides the necessary scale and context per client to deal with a SYN flood attack and its many variants, including TCP stack, resource attacks, and TLS attacks within Fastly systems.

- Fastly also provides protection against Layer 7 attacks. If your store is experiencing performance issues and you suspect a Layer 7 DDoS attack, submit an Adobe Commerce Support ticket. Adobe can create and apply custom rules to the Fastly service to inspect for and filter out malicious requests based on header, payload, or a combination of attributes that identify the attack traffic. See [Checking for DDoS attacks][] and [How to block malicious traffic] in the *Adobe Commerce Help Center*.

<!--Link definitions-->

[Caching with Fastly]: https://developer.adobe.com/commerce/webapi/graphql/usage/caching/#caching-with-fastly

[Checking for DDoS attacks]: https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/checking-for-ddos-attack-from-cli.html

[Fastly CDN module for Magento 2]: https://github.com/fastly/fastly-magento2

[Fastly support ticket]: https://docs.fastly.com/products/support-description-and-sla#support-requests

[How to block malicious traffic]: https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/block-malicious-traffic-for-magento-commerce-on-fastly-level.html

[Working with Domains]: https://docs.fastly.com/en/guides/working-with-domains
