---
title: Variables property
description: Use the variables property to customize store configuration options for the Commerce application.
---

# Variables property

You can use application-based environment variables to customize store configurations. These variables use a specific syntax. See [Override configuration settings](https://experienceleague.adobe.com/docs/commerce-operations/configuration-guide/paths/override-config-settings.html) in the _Configuration guide_.

The following environment variables included in the `.magento.app.yaml` file are required for specific versions of the Commerce application.

Required for Adobe Commerce 2.2.x to 2.3.x:

```yaml
variables:
    env:
        CONFIG__DEFAULT__PAYPAL_ONBOARDING__MIDDLEMAN_DOMAIN: 'payment-broker.magento.com'
        CONFIG__STORES__DEFAULT__PAYMENT__BRAINTREE__CHANNEL: 'Magento_Enterprise_Cloud_BT'
        CONFIG__STORES__DEFAULT__PAYPAL__NOTATION_CODE: 'Magento_Enterprise_Cloud'
```

For Adobe Commerce 2.4.x, set the following variables:

```yaml
variables:
    env:
        CONFIG__DEFAULT__PAYPAL_ONBOARDING__MIDDLEMAN_DOMAIN: 'payment-broker.magento.com'
        CONFIG__STORES__DEFAULT__PAYPAL__NOTATION_CODE: 'Magento_Enterprise_Cloud'
```
