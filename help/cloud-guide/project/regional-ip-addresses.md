---
title: Regional IP addresses
description: See a list of IP addresses for the AWS and Azure regions used by Adobe Commerce on cloud infrastructure for integration environments.
exl-id: 27d8b489-7ecd-4701-ad92-06aa7cf98c8d
---
# Regional IP addresses

The following tables list the incoming and outgoing IP addresses used by Adobe Commerce on cloud infrastructure [integration environments](../architecture/pro-architecture.md#integration-environment). These IP addresses are stable, but might change. We always notify customers before making any IP address changes.

The URI syntax for the integration environments:

```text
https://<branch>-<unique-ID>-<project-ID>.<region>.magentosite.cloud/
```

- **Unique ID** = 7 random alpha-numeric characters
- **Project ID** = 13-character project ID
- **Region** = AWS or Azure region name

You can use the `ping` command to retrieve the incoming IP address:

```bash
ping integration-abcd123-abcd78910.us-3.magentosite.cloud
```

Sample response:

```console
PING integration-abcd123-abcd78910.us-3.magentosite.cloud (34.210.133.187): 56 data bytes
Request timeout for icmp_seq 0
Request timeout for icmp_seq 1
Request timeout for icmp_seq 2
```

If you have a corporate firewall that blocks outgoing SSH connections, you can add the inbound IP addresses to your allowlist.

## AWS regions

|     | United States |       |      | Europe |      |      |      | Asia-Pacific |
| --- | :------------ | :---- | :--- | :----- | :--- | :--- | :--- | :----------- |
|     | US            | US-3  | US-5 | EU     | EU-3 | EU-5 | EU-6 | AP-3         |
| Incoming | <!--US-->52.200.159.23<br><br>52.200.159.125<br><br>52.200.160.5 | <!--US-3-->34.210.133.187<br><br>34.214.72.239<br><br>34.215.10.85 | <!--US-5-->50.112.160.58<br><br>54.213.195.223<br><br>35.163.170.185 | <!--EU-->52.209.44.44<br><br>52.209.23.96<br><br>52.51.117.101 | <!--EU-3-->34.240.75.192<br><br>34.251.110.37<br><br>52.19.113.35 | <!--EU-5-->35.157.81.88<br><br>3.122.198.131<br><br>52.28.102.195 | <!--EU-6-->35.181.23.47<br><br>35.181.24.165<br><br>35.180.237.48 | <!--AP-3-->52.65.39.201<br><br>52.65.10.202<br><br>52.65.30.37 |
| Outgoing | <!--US-->52.200.155.111<br><br>52.200.149.44<br><br>50.17.163.75 | <!--US-3-->34.210.166.180<br><br>34.215.83.92<br><br>34.213.20.158 | <!--US-5-->54.70.238.217<br><br>52.88.113.98<br><br>52.36.188.230 | <!--EU-->52.51.163.159<br><br>52.209.44.60<br><br>52.208.156.247 | <!--EU-3-->34.240.57.142<br><br>52.16.140.48<br><br>52.209.134.55 | <!--EU-5-->3.121.163.221<br><br>3.121.79.229<br><br>18.197.3.230 | <!--EU-6-->52.47.155.26<br><br>35.181.0.157<br><br>35.181.12.15 | <!--AP-3-->52.65.143.178<br><br>13.54.80.197<br><br>52.62.224.4 |

## Azure regions

|          |  United States  | Europe          |
| -------- | :-------------- | :-------------- |
|          | US-A1           | AZ-WESTEUROPE-1 |
| Incoming | <!--US-A1--> 20.186.27.68<br><br>20.186.58.163<br><br>20.186.113.8 | <!--AZ-W-1-->50.112.160.58<br><br>54.213.195.223<br><br>35.163.170.185 |
| Outgoing | <!--US-A1-->20.186.58.163<br><br>20.186.27.68<br><br>20.186.113.8 | <!--AZ-W-1-->104.45.78.98<br><br>51.105.168.218<br><br>51.105.163.143 |
