---
title: Protective block
description: Learn about the protective block feature of Adobe Commerce on cloud infrastructure and how it works to protect your site against known security vulnerabilities.
feature: Cloud, Configuration, Security
topic: Security
exl-id: bc1def41-9521-4005-872e-9ecaab1d4d16
---
# Protective block

Adobe Commerce on cloud infrastructure has a protective blocking feature that, under certain circumstances, restricts access to websites with security vulnerabilities. This partial blocking method prevents exploitation of known security vulnerabilities. Outdated software often contains exploits, so it is important to protect against these exploits by partially blocking access to these sites.

## How the protective block works

Adobe Commerce maintains a database of signatures of known security vulnerabilities in open-source software that are commonly deployed on cloud infrastructure. The security check analyzes only known vulnerabilities in open-source projects; it cannot examine customizations you write.

Security scan runs:

-  When you push new code to Git
-  When new vulnerabilities are added to the database

If a critical vulnerability is detected in your application, it rejects the Git push.

There are two types of blocks that run:

1. **Complete block**—for development websites. The error message accompanying `git push` provides detailed information about the vulnerability.

1. **Partial block**—for production websites, which allows the site to stay mostly online. Depending on the nature of the vulnerability, parts of a request, such as a query string, cookies, or any additional headers, might be removed from GET requests. All other requests may be blocked entirely, such as logging in, form submission, or product checkout.

Unblocking is automated upon resolution of the security risk. The block is removed soon after you apply a security upgrade that removes the vulnerability.

## Opt out of the protective block

The protective block is there to protect you against known vulnerabilities in the software you deploy Adobe Commerce on cloud infrastructure.

However, you can opt out of the protective block by adding the following to [`.magento.app.yaml`](../application/configure-app-yaml.md):

```yaml
   preflight:
      enabled: false
```

You can explicitly opt out of a specific check, for example:

```yaml
   preflight:
      enabled: true
      ignore_rules: [ "drupal:SA-CORE-2014-005" ]
```
