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

You can use the [New Relic service](../monitor/new-relic.md#use-new-relic) to monitor the CPU usage for  The following is an example New Relic query to show CPU usage for web nodes.

```sql
SELECT average(cpuPercent) FROM SystemSample FACET hostname WHERE apmApplicationNames LIKE '%|72gmfuvykea6o_stg3|%' AND instanceType LIKE 'c%' TIMESERIES SINCE 3 HOURS AGO
```

![New Relic web nodes CPU usage](../../assets/new-relic/web-node-cpu-usage.png)

## Enable auto scaling

To enable or disable Auto scaling for your Adobe Commerce on cloud infrastructure project, [Submit an Adobe Commerce Support ticket](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket). Include the following information in the ticket:

- Contact reason: Infrastructure Change Request

>[!IMPORTANT]
>
>The auto-scaling feature captures unanticipated events. Even if you have Auto scaling enabled, Adobe recommends that you continue to [Submit an Adobe Commerce Support ticket](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) if you expect an upcoming event.

### Load testing

After Adobe enables Auto scaling on your Cloud project, you should perform load testing in the Staging environment.

### IP allowlist

If you have the IP addresses for your core nodes (1, 2, and 3) and web nodes (4, 5, and 6) in an allowlist, then there is no action required. After enabling Auto scaling, the outbound web node traffic is routed through the IP addresses of the core nodes 1, 2, and 3. If you do not have the IP addresses for nodes 1, 2, and 3 in your allowlist, then you must update the allowlist.
