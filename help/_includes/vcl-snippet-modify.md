# Include file for modifying custom VCL for Fastly

## Modify the custom VCL snippet

1. [Log in](/help/get-started/onboarding.md#access-your-admin-panel) to the Admin.

1. Click **Stores** > **Settings** > **Configuration** > **Advanced** > **System**.

1. Expand **Full Page Cache** > **Fastly Configuration** > **Custom VCL Snippets**.

   ![Manage custom VCL snippets]

1. In the _Action_ column, click the settings icon next to the snippet to edit.

1. After the page reloads, click **Upload VCL to Fastly** in the _Fastly Configuration_ section.

1. After the upload completes, refresh the cache according to the notification at the top of the page.

>[!WARNING]
>
>The _Custom VCL snippets_ UI option shows only the snippets added through the Adobe Commerce Admin. If you add snippets using the Fastly API, use the API to [manage them](/help/cloud-guide/cdn/fastly-vcl-custom-snippets.md#manage-custom-vcl-snippets-using-the-api).
