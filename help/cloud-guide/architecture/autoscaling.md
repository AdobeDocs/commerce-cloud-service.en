---
title: Auto scaling
description: Learn about the auto-scaling feature for Adobe Commerce on cloud infrastructure.
hide: yes
hidefromtoc: yes
exl-id: 2ba49c55-d821-4934-965f-f35bd18ac95f
---
# Auto scaling

The Auto scaling feature automatically adds or removes resources to the cloud infrastructure in order to maintain optimal performance and reasonable costs. Currently, this feature is only available for projects configured with a [Scaled architecture](scaled-architecture.md).

## Web server nodes

The [web tier](scaled-architecture.md#web-tier) scales to accommodate an increase in process requests and higher traffic requirements. Currently, the auto-scaling feature only scales horizontally by adding or removing web server nodes.

An auto-scaling event occurs when CPU usage and traffic reach a predefined threshold:

- **Nodes added**—CPUs/cores across all active web nodes are at 75% capacity for 1 minute and traffic is increasing by 20% for 5 consecutive minutes.
- **Nodes removed**—CPUs/cores across all active web nodes are loaded at 60% for 20 minutes. Nodes are removed in the order that they were added.

The minimum and maximum thresholds are determined and set based on the contracted resource limits of each merchant; this reduces the risk of infinite scaling.

### Monitor web tier CPU usage

You can use the [New Relic service](../monitor/new-relic.md#use-new-relic) to monitor thresholds. The following example New Relic query shows CPU usage for web nodes (instance type `c%`):

**To show all clusters in a project**:

```sql
SELECT average(cpuPercent) FROM SystemSample FACET hostname, apmApplicationNames WHERE instanceType LIKE 'c%' TIMESERIES SINCE 3 HOURS AGO
```

![New Relic web nodes CPU usage](../../assets/new-relic/web-node-cpu-usage.png)

## Enable auto scaling

To enable or disable Auto scaling for your Adobe Commerce on cloud infrastructure project, [Submit an Adobe Commerce Support ticket](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket). Include the following information in the ticket:

- Contact reason: Infrastructure Change Request

>[!IMPORTANT]
>
>The auto-scaling feature captures unanticipated events. Even if you have Auto scaling enabled, Adobe recommends that you continue to [Submit an Adobe Commerce Support ticket](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) if you expect an upcoming event.

### Load testing

First, Adobe enables Auto scaling on your Cloud project staging cluster. Then after you perform and complete load testing in the Staging environment, Adobe enables Auto scaling on your production cluster. For guidance on load testing, see [Performance testing](../launch/checklist.md#performance-testing).

### IP allowlist

After enabling Auto scaling, the outbound web node traffic is routed through the IP addresses of the service nodes. It is best to include the IP addresses of all six nodes. If you use an allowlist with a third-party service that is not bundled with your Adobe Commerce on cloud infrastructure project, then you may need to update the IP addresses in the third-party sevice allowlist:

- If the allowlist contains the IP addresses for your service nodes (1, 2, and 3), then there is no action required.
- If the allowlist contains the IP addresses for your service nodes (1, 2, and 3) and web nodes (4, 5, and 6)—all six nodes—then there is no action required.
- If the allowlist contains the IP addresses _only_ for your web nodes (4, 5, and 6), then you need to update the allowlist to include the IP addresses for the service nodes.
