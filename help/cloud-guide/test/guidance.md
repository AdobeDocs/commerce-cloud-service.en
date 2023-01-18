---
title: Testing guidance
description: Read about testing types and best practices for launching Adobe Commerce on cloud infrastructure.
exl-id: 1d7897a2-af97-46ab-89c0-2ec54284190e
---
# Testing guidance

After configuring and customizing your Adobe Commerce on cloud infrastructure project, it is a best practice to test your application thoroughly before launching the store website. Testing helps to properly manage expectations of the cluster size and appropriately scale for future business needs.

## Functional testing

While in development, it is important to perform end-to-end functional testing on your Adobe Commerce on cloud infrastructure project. See the following guidance for performing functional testing in the Docker environment:

-  **Application testing**—Use the [Magento Functional Testing Framework (MFTF)](https://developer.adobe.com/commerce/cloud-tools/docker/test/application-testing/) for application testing in Cloud Docker environment.

-  **Code testing**—Use the [Codeception testing framework for PHP](https://developer.adobe.com/commerce/cloud-tools/docker/test/code-testing/) for validating code that is intended for contribution to Cloud package repositories.

## Best practices before launch

Consider the following testing types as a best practice to perform before site launch:

-  **Load test**—Conduct a load test to understand the behavior of the system under an expected load. For example, test a concurrent number of active users on the application, having each user perform a specific number of transactions within the set duration. This test reveals the response time of important business-critical transactions, such as the database or application server behavior. A load test can help to identify bottlenecks.

-  **Stress test**—Challenge the upper limits of capacity within the system to determine if the system performs sufficiently when the current load goes well above the expected maximum.

-  **Security Scan**—Adobe provides a free [Security Scan Tool](../launch/overview.md#set-up-the-security-scan-tool) for your sites.

-  **Penetration test**—Is an authorized simulated cyber attack on a computer system designed to evaluate the security of the system. The penetration test helps to identify weaknesses or vulnerabilities, including the potential for unauthorized parties to gain access to system features and data.

>[!WARNING]
>
>Customers are not permitted to conduct any security assessments of AWS infrastructure or the AWS services themselves. If you discover a security issue within any of the AWS services observed in your security assessment, [contact AWS Security](mailto:aws-security@amazon.com) immediately. See [AWS Customer policies for Penetration testing](https://aws.amazon.com/security/penetration-testing/).
