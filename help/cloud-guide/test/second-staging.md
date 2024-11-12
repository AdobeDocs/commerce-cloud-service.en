---
title: Second staging environment
description: Learn the benefits and uses of having a second staging environment for parallel testing, issue isolation, version control, and more.
---

# Second staging environment

In Adobe Commerce Cloud infrastructure, the staging environment ensures comprehensive testing and validation in a setting that can mirror the production environment. This environment allows you to safely identify and resolve bugs, while ensuring that any new features or changes are seamlessly integrated before they impact your live site.

Some projects demand a more sophisticated development workflow. To support this need, Adobe offers an additional staging environment as an add-on option to your cloud infrastructure. Having two staging environments is advantageous for complex projects and simultaneous collaboration across teams. 

Having a secondary staging environment provides the following benefits:

- **Parallel Testing**: With two staging environments, teams can test new features and critical updates simultaneously without interfering with each other's development. For example, you can dedicate an environment to feature testing, while reserving the other environment for performance and stress testing.

- **Isolation of Issues**: When bugs or issues arise in the primary staging environment, you can replicate and diagnose them in the secondary environment without halting testing progress. This ensures that troubleshooting does not interfere with ongoing tests.

- **Version Control**: Manage different versions of your application more effectively. The primary staging environment can run the latest stable build, while the secondary tests experimental features. This helps you better manage release cycles and ensures that experimental changes do not disrupt stable builds.

- **Enhanced Rollout Planning**: You can simulate different deployment scenarios. The primary staging environment can mimic the current production setup, while the secondary environment can be configured to test upcoming releases.

- **User Acceptance Testing (UAT)**: While using the primary environment for ongoing development, you can dedicate secondary environment to UAT. This allows users or clients to test and provide feedback on new features in a controlled setting, without affecting testing.

- **Regression Testing**: You can use one environment for forward-facing tests and the other for regression testing, ensuring that new changes do not break existing functionality.

- **Training and Demonstrations**: Use one environment for training new team members or demonstrating new features to stakeholders. This ensures that training activities do not interrupt testing.

- **Private Link Setup**: Master and Integration environments do not support Private Link setup. If your development workflow requires additional environments connected via Private Link for development, testing, or any other purpose, consider adding an extra staging environment.

Having two staging environments can vastly improve your workflow efficiency, risk management, and the overall quality of your application. These environments provide safety and flexibility that one staging environment would not be able to offer.

>[!NOTE]
>
>This setup is an add-on. Customers who want a secondary environment must contact their sales representative to request one. The sales representative can provide information on pricing and the provisioning process.

If your project already has an additional staging environment or you are considering upgrading your current project, consider the following provisioning timelines and responsibilities:

- The provisioning process can take up to two weeks after you confirm the request with your Adobe sales representative.

- New staging environments are only available in the same region as your current Staging and Production environments.

- You must update either your Integration or Master environment and specify which of your environments your secondary staging environment will be based on. The secondary staging environment cannot be copied from the Staging or Production environments.

- After you receive your new staging environment, you can include it in your development flow. Like with other environments code and database updates are your responsibility.

## Request the environment

To facilitate your request, follow the steps:

1. Upgrade your branch.

   Upgrade your Integration or Master branch with the code and database that you want to use for the new environment.

1. Contact your sales representative.

   Contact your Adobe Sales representative and provide them with the specific branch that you want to use as the base for your new staging environment (Integration or Master).

1. Confirm details.

   After you confirm the details with your sales representative, wait for their confirmation that the provisioning request has been received and is being processed. When the provisioning process is complete, the Adobe team will send you a confirmation.

1. Deploy to your new environment.

   Follow the [standard deployment steps](../deploy/staging-production.md) to deploy your code and database to the new staging environment.
