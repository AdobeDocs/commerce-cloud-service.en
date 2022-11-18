# Include file for deleting custom VCL for Fastly

## Delete the custom VCL snippet

1. [Log in](/help/get-started/onboarding.md#access-your-admin-panel) to the Admin.

1. Click **Stores** > **Settings** > **Configuration** > **Advanced** > **System**.

1. Expand **Full Page Cache** > **Fastly Configuration** > **Custom VCL Snippets**.

   ![Manage custom VCL snippets](/help/assets/cdn/fastly-manage-snippets.png)

1. In the _Action_ column, click the trash icon next to the snippet to delete.

1. On the next modal window, click **DELETE** and activate a new version.

>[!WARNING]
>
>The _Custom VCL snippets_ UI option shows only the snippets added through the Adobe Commerce Admin. If you add snippets using the Fastly API, use the API to [manage them](/help/cloud-guide/cdn/fastly-vcl-custom-snippets.md#manage-vcl-using-the-api).
