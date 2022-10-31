---
title: Overview of store options and configuration management
description: Customize your Adobe Commerce store on cloud infrastructure.
---

# Overview of store options and configuration management

There are many ways to customize your store, such as adding a custom theme, installing an extension, or enforcing a specific configuration across cloud infrastructure environments. You can configure settings for specific services directly in Staging and Production environments. You can set up multiple websites and stores. The Store configuration section helps you to configure these options in your local workstation and deploying specific settings across environments.

To access your storefront, use the `magento-cloud url` command and answer the prompts. Or you can find the url in the Project web interface under **Access site**.

## Configure store options

Store options include the following:

* [Business-to-business module (B2B)](b2b-module.md)
* [Custom themes](custom-theme.md)
* [Extensions](extensions.md)
* [Multiple sites](multiple-sites.md)
* [Payment services](paypal.md)

## Configure services and integrations

There are specific configuration files that manage certain deployment behaviors to remote environments. You can review these topics separately:

* [Application deployment](../application/configure-app-yaml.md)
* [Environment build and deploy actions](../environment/configure-env-yaml.md)
* [Incoming request routes](../routes/routes-yaml.md)
* [Supported services](../services/services-yaml.md)

## Configuration management

After configuring the store options, services, and integrations, use configuration management to deploy these configurations across all environments consistently and with minimal downtime. See [Configuration Management](store-settings.md).
