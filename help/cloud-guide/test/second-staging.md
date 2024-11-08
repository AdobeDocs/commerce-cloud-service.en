---
title: Second staging environment
description:
---

# Second staging environment

In Adobe Commerce Cloud infrastructure, the staging environment ensures comprehensive testing and validation in a setting that can mirror the production environment. It provides a safe space for identifying and resolving bugs and ensuring that any new features or changes are seamlessly integrated before they impact your live site.

Some projects demand a more sophisticated development workflow. To support this need, Adobe offers an additional staging environment as an add-on option to your cloud infrastructure. Having two staging environments can be really advantageous, especially for complex projects or when different teams need to test different aspects simultaneously. 

Let's dig into the benefits and potential uses of a secondary staging environment:

- **Parallel Testing**: With two staging environments, teams can test new features and critical updates simultaneously without stepping on each other's development. One environment can be dedicated to feature testing, while the other can focus on performance and stress testing.

- **Isolation of Issues**: When bugs or issues arise in the primary staging environment, they can be replicated and diagnosed in the secondary environment without halting overall testing progress. This ensures that troubleshooting doesn't interfere with ongoing tests.

- **Version Control**: Manage different versions of your application more effectively. The primary staging environment can run the latest stable build, while the secondary one tests experimental or early-stage features. This helps in managing release cycles better and ensures that experimental changes don't disrupt stable builds.

- **Enhanced Rollout Planning**: You can simulate different deployment scenarios. The primary staging environment can mimic the current production setup, while the secondary environment can be configured to test upcoming releases.

- **User Acceptance Testing (UAT)**: While the primary environment might be used for ongoing development, the secondary environment can be dedicated to UAT. This allows end-users or clients to test and provide feedback on new features in a controlled setting, without affecting the developer's testing cycles.

- **Regression Testing**: Use one environment for forward-facing tests and the other for regression testing. Ensuring that new changes don't break existing functionality is crucial, and having two environments allows this to happen concurrently with ongoing development.

- **Training and Demonstrations**: Use one environment for training new team members or demonstrating new features to stakeholders. This ensures that training activities do not interrupt the critical testing phases.

- **Private Link Setup**: Master and Integration environments do not support Private Link setup. If your development workflow requires additional environments connected via Private Link for development, testing, or any other purpose, you might consider adding an extra staging environment as an option.

In essence, two staging environments can vastly improve your workflow efficiency, risk management, and the overall quality of your application. They provide a safety net and flexibility that one staging environment might not be able to offer.

>[!NOTE]
>
>This setup is an add-on, and customers who wish to include this setup in their project must contact their sales representative to make a request for this offer. The sales representative provides information on the pricing and process required to purchase the additional staging environment.

If your project already has additional staging or you're thinking about upgrading your current project setup by acquiring a new staging environment, be aware of the following provisioning timelines and responsibilities:

- The provisioning process may take up to two weeks after you confirm the request with your Adobe Sales representative.

- Your new staging environment is configured in the same region as your current Staging and Production environments.

- You must update one of your Integration or Master environments with the codebase and specify which one to use as the base for your new staging environment. It is not possible to start the codebase and database copied from Staging or Production cluster environments.

- After you receive your new staging environment, you can include it in your development flow. Code and database updates are your responsibility, just like other environments.

## Request the environment

To facilitate your request, follow the steps:

1. Upgrade your branch.

   Begin by upgrading your Integration or Master branch with the code and database that you want to use for the new environment.

1. Contact your sales representative.

   Reach out to your Adobe Sales representative and provide them with the specific branch that you want to use as the base for your new staging environment (either Integration or Master).

1. Confirm details.

   After you confirm the details with your sales representative, wait for their confirmation that the provisioning request has been received and is being processed. When the provisioning process is complete, the Adobe team sends you a confirmation.

1. Deploy to your new environment.

   Follow the [standard deployment steps](../deploy/staging-production.md) to deploy your code and database to the new staging environment.
