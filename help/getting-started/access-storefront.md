---
title: Access the storefront
description: Learn how to access the Commerce storefront and change the default admin panel link.
---

# Access the Commerce storefront

Your environment must be in a "running" state before you can access the storefront. You can check the status in the Environments section of your Cloud Manager dashboard, and click the URL to open the storefront.

## Change the Admin URI

To prevent exploits, Adobe recommends that you do _not_ use a common word for the URI, like admin or backend. It is a best practice to change the Admin URI as soon as possible using alphanumeric values. The underscore character (_) is the only allowed character.

**To update the admin URL variable**:

1. First step placeholder to change variable. 

   If an environment enters a failure state after applying a custom variable, remove the variable that was added and test if the environment remains in error.

1. Verify the storefront admin URL.

>[!TIP]
>
> Learn how to use Git branches and environments to create build artifacts and pipelines.
>
>**Next step**: [Set up a non-production pipeline](create-pipeline.md)
