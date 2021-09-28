---
title: Set up local development
description: Set up your development environment with the required command-line tools.
---

# Set up local development

Adobe Commerce environments are Read Only. However, you can write and test code on your local machine using the command line. Install the following tools before continuing:

- [Node.js version 14 or 12][node]
- [Adobe I/O Extensible CLI (AIO)][aio-cli]
- [Cloud Manager plugin for AIO][cm-plugin]

## Authentication

As noted in the Cloud Manager plugin readme file, there are two methods of authentication. The _browser-based_ method uses your personal permissions, and the [_service account_ method](../user/develop/cli-authentication.md#service-account-authentication) is ideal for automation tasks. For the Getting Started workflow, use the AIO tool to launch the browser-based authentication process.

**To log in with your Adobe ID**:

1. Open a terminal and use AIO to authenticate with your Adobe ID.

   ```bash
   aio auth:login
   ```

1. In the browser that opens, follow the instruction to enter the email and password associated with your Adobe ID.

1. In the terminal, verify the installation by listing the programs available to your identity:

   ```bash
   aio cloudmanager:list-programs
   ```

## Recap

At this point in the Getting Started workflow, you have completed the following:

- toured your program UI in Cloud Manager
- cloned your project to a local machine
- installed the CLI tools
- authenticated and verified the connection between your local environment and the remote environment

Now you are ready to interact with your Commerce application.

>[!TIP]
>
>The next step helps you to understand what an environment is and how you can customize an environment using the command line.
>
>**Next step**: [Create a default environment](create-environment.md)

<!-- link definitions -->

[aio-cli]: https://github.com/adobe/aio-cli
[cm-plugin]: https://github.com/adobe/aio-cli-plugin-cloudmanager
[node]: https://nodejs.org/en/download/package-manager/
