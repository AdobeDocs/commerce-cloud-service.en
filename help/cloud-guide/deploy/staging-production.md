---
title: Deploy to Staging and Production
description: See a summary of the actions to deploy your Adobe Commerce on cloud infrastructure code to Staging and Production environments for further testing.
---

# Deploy to Staging and Production

The process for deploying and going live begins with development, continues to Staging, and ends with going live in Production. To provide the best experience for developing, testing, and deploying your store with consistent configurations we provide an end-to-end environment solution. Every environment supports direct URL access to the store and Admin console and SSH access for CLI commands.

You can fully push, merge, and deploy through the [Project Web Interface](../project/overview.md) or [Cloud CLI commands](../dev-tools/cloud-cli.md) through a terminal application.

This section provides indepth instructions and information on the build and deploy process, migrating data and content, and testing.

## Starter project deployment

We recommend creating a `staging` branch from the `master` branch to best support your Starter plan development and deployment. With this in place, you have two of your four active environments ready: `master` for Production and `staging` for Staging.

Now you are ready to develop and deploy:

1. Create development branches from the `staging` branch. This allows you to merge up through Staging and Production.
1. Develop on local: custom modules, extensions, 3rd party integrations, and configurations.
1. Push your local branch to the Git remote branch to test in a full environment.
1. To fully test in a near-production level environment, push code to a staging branch.
1. Fully test in the Staging environment including payment gateways, shipping, price rules, various products, and full customer and admin interactions.
1. Finally, deploy to the Production `master` to complete testing, site launch steps, and start selling.

For detailed information of the process, see [Starter Develop and Deploy Workflow](../architecture/starter-develop-deploy-workflow.md).

## Pro project deployment

Pro comes with a large Integration environment with two active branches, a global `master` branch, Staging, and Production branches. When you create your project, code is ready to branch, develop, and push for building and deploying your site. Although the Integration environment can have many branches, Staging and Production have only one branch: the deployed Git `master`.

1. Create development branches from the Integration environment.
1. Develop on local: custom modules, extensions, 3rd party integrations, and configurations.
1. Push your local branch to the Git remote branch to test in a full environment.
1. Merge final code to the Integration `master` branch.
1. To fully test in a near-production level environment, push code to the Staging environment.
1. Fully test in the Staging environment including payment gateways, shipping, price rules, various products, and full customer and admin interactions.
1. Finally, deploy to the Production environment to complete testing, site launch steps, and start selling.

For detailed information of the process, see [Pro Develop and Deploy Workflow](../architecture/pro-develop-deploy-workflow.md).

### Enter a ticket for deploying hooks

{% include cloud/hooks.md %}

## Read-only environments

You should always deploy code by pushing your local Git branch to your environments. You should only directly modify configurations for a few key extensions directly in your Staging and Production environments through the Admin or using environment variables.

Always update your code in a branch on your local environment, push to Git, and complete the full deployment when you need to do the following:

*  Add extensions
*  Add 3rd party integrations
*  Fix issues and check errors
