---
title: Automatic scaling
description: Learn about the automatic scaling feature for Adobe Commerce on cloud infrastructure.
hide: yes
hidefromtoc: yes
---

# Automatic scaling

The auto-scaling feature automatically adds or removes resources to the cloud infrastructure in order to maintain optimal performance and reasonable costs. This feature is available for projects configured with a [Scaled architecture](scaled-architecture.md).

To enable or disable automatic scaling for your Adobe Commerce on cloud infrastructure project, [Submit an Adobe Commerce Support ticket](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket). There is no downtime, indexing, or deployment necessary to update this configuration.

>[!IMPORTANT]
>
>The auto-scaling feature captures unanticipated events. Even if you have the auto-scaling feature enabled, Adobe recommends that you continue to [Submit an Adobe Commerce Support ticket](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) if you expect an upcoming event.

## Web server nodes

The [web tier](scaled-architecture.md#web-tier) scales to accommodate an increase in process requests and higher traffic requirements. Currently, the auto-scaling feature only scales horizontally by adding or removing web server nodes.

An auto-scaling event occurs when CPU usage and traffic reach a predefined threshold:

- **Nodes added**—CPUs/cores across all active web nodes are at 75% capacity for 1 minute and traffic is increasing by 20% for 5 consecutive minutes.
- **Nodes removed**—CPUs/cores across all active web nodes are loaded at 60% for 20 minutes. Nodes are removed in the order that they were added.

The minimum and maximum thresholds are determined and set based on the contracted resource limits of each merchant; this reduces the risk of infinite scaling.

## IP allowlist

TBD
