---
title: Magento Account security
description: Describes the various layers of security and the requirements for interacting with the Magento.
---

# Account security

Magento Commerce environments are Read Only; therefore, you must develop in a local workstation using a cloned environment and push changes to the remote, read-only Magento Commerce Git repository. This process requires that you have the following keys:

- Magento authentication keys (Composer keys)
- Magento Encryption Key
- Commerce Program account

## Magento authentication keys

Magento authentication keys are 32-character authentication tokens that provide secure access to the Magento 2 Composer repository (repo.magento.com), and any other Git services required for Magento development such as GitHub. Your account can have multiple Magento authentication keys. For the workstation setup, start with one specific key for your code repository. If you do not have any keys, contact the License Owner to create them.

## Magento encryption key

When importing an existing Magento system only, capture the Magento encryption key used to protect your access and data for the Magento database.

## Commerce Program account

Only a Commerce Admin can invite you to the Magento Commerce on Cloud Manager program. When you receive the e-mail invitation, click the link and follow the prompts to create your account. See Set up an account for details.
