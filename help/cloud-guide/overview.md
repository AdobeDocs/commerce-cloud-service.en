---
title: Commerce Overview
description: Learn about building, deploying, and managing Commerce on Cloud infrastructure.
---

# Commerce on Cloud Infrastructure

Adobe Commerce on cloud infrastructure provides an automated hosting platform with a **self-service** approach to building, deploying, and managing your Commerce application in a cloud-native environment. Adobe Commerce on cloud infrastructure comes with additional features that set it apart from the on-premises Adobe Commerce and Magento Open Source platforms:

* A pre-provisioned infrastructure that includes PHP, MySQL (MariaDB), Redis, RabbitMQ, and supported search engine technologies.
* Git-based workflow with automatic build and deploy for efficient Rapid development and Continuous deployment every time you push code changes in a Platform as a Service (PaaS) environment.
* Highly Customizable environment configuration files and command-line interface (CLI) manage and deploy tools.
* Amazon Web Services (AWS) hosting that offers a Scalable and Secure environment for online sales and retailing.

![Cloud benefits](../assets/CloudBenefits.svg)

## Technology stack

Think of the Adobe Commerce on cloud infrastructure as five functional layers, as shown below:

![Cloud stack](../assets/CloudStack.svg)

1. [**Cloud Infrastructure**](https://devdocs.magento.com/cloud/architecture/pro-architecture.html): Choose either Amazon Web Services (AWS) or Microsoft Azure as your Infrastructure as a Service (IaaS) foundation for your Adobe Commerce on cloud infrastructure Pro projects.
1. [**Platform as a Service**](https://devdocs.magento.com/cloud/architecture/cloud-architecture.html): Each Adobe Commerce on cloud infrastructure plan provides a Platform as a Service (PaaS) Integration environment for developing, testing, and integrating services.
1. [**Adobe Commerce**](https://devdocs.magento.com/cloud/requirements/cloud-requirements.html#cloud-arch-software):  Adobe Commerce on cloud infrastructure provides a pre-provisioned infrastructure that includes PHP, MySQL (MariaDB), Redis, RabbitMQ, and supported search engine technologies.
1. [**Performance Tools**](https://devdocs.magento.com/cloud/project/new-relic.html): New Relic performance tools enable you to debug, monitor, and manage your applications and infrastructure by collecting, analyzing, and displaying data from your Adobe Commerce on cloud infrastructure projects.
1. [**Content Delivery Network (CDN), Web Application Firewall ([!DNL WAF]) and Image Optimization (IO)**](https://devdocs.magento.com/cloud/cdn/cloud-fastly.html):

   * [Fastly CDN](https://devdocs.magento.com/cloud/cdn/cloud-fastly.html#ddos-protection)—Provides secure CDN services with built-in protection from Distributed Denial of Service (DDoS) attacks like [!DNL Ping of Death], [!DNL Smurf] attacks, and other Internet Control Message Protocol (ICMP) based flood attacks.
   * [Web Application Firewall (WAF)](https://devdocs.magento.com/cloud/cdn/fastly-waf-service.html)—WAF services ensure PCI compliance for Adobe Commerce storefronts in  Production environments and WAF policies that protect your Adobe Commerce web applications from injection attacks, malicious input, cross-site scripting, data exfiltration, HTTP protocol violations, and other [[!DNL OWASP] Top Ten security threats](https://www.owasp.org/index.php/Top_Ten).
   * [Image optimization (IO)](https://devdocs.magento.com/cloud/cdn/fastly-image-optimization.html)—Provides real-time image manipulation and optimization to speed up image delivery and simplify maintenance of image source sets for responsive web applications. Fastly IO offloads image processing and resizing load, freeing servers to process orders and conversions efficiently.

Monolithic applications are resource-intensive and difficult to scale and serve rapidly. With the Cloud infrastructure, Commerce customers gain unparalleled access to SaaS-based microservices that are rich, intelligent, and performant.

>microservices list or drawing goes here

Use the [Commerce Get Started guide](../get-started/overview.md) to set up your new Cloud program and begin managing your Commerce application in a cloud-native environment.

## Commerce guides

The Commerce on Cloud guide assumes that you have some working knowledge and understanding of the Commerce application. You can refer to the Commerce Developer and User guides below:

* [Commerce Developer Guides](https://devdocs.magento.com)
* [Commerce User Guides](https://docs.magento.com/user-guide)
