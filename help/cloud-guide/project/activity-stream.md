---
title: Activity stream
description: Learn how to read the activity stream in the Project Web Interface or the Cloud CLI for Adobe Commerce on Cloud infrastructure.
---
# Activity stream

The main view for each environment displays an **Activity** list of historical events similar to a Git log. The Activity list is a stream of the recent events for active environments. The following is a list of the activity types and their icons that display in the Activity stream:

![Activity types](../../assets/activity-types.svg){width="500" align="center"}

## View logs

In the Activity list, click the status icon of an activity to view the log. Alternatively, click the (_more_) icon ![more](../../assets/icon-more.png) to access more options for managing the activity.

## Manage an activity

Some activities are in a _running_ or _pending_ status. You can act on a running activity by accessing the (_more_) menu and selecting an action, such as `Cancel` or `View log`.

Select the **Cancel** option to stop the activity. Not all activities have this option.

![Cancel activity](../../assets/activity-icons/cancel-activity.png){width="200" align="center"}

You can only cancel a running deployment during the _build_ phase. Once the application has moved into the _deploy_ phase, you no longer have the option to cancel the activity.

If you have a terminal running the activity, canceling in the Project Web Interface results in the cancellation in the terminal:

![Activity cancelled in terminal](../../assets/activity-icons/activity-cancelled.png){width="200" align="center"}

## Filter activity stream

The ability to filter the activity list is useful when you are looking for something specific, such as a backup or a merge event.

**To filter the activity list in the Project Web Interface**:

1. Select an environment and choose the Activity **[!UICONTROL All]** view to include the full event history.

1. Click ![Filter by](../../assets/icon-filterby.png) and select the **[!UICONTROL Filter by]** options:

   ![Filter activities](../../assets/activity-filter.png)

1. Choose the Activity **[!UICONTROL Recent]** view and reset the list.

## Activity stream with Cloud CLI

The `magento-cloud` CLI provides most of the same abilities as the Project Web Interface. The `activity` command can:

- `list` the stream of activities for an environment
- `get` details about a specific activity
- display the `log` for a specific activity
- `cancel` an activity

**To view the Activity stream with the Cloud CLI**:

1. List the activities for the current environment:

   ```bash
   magento-cloud activity:list
   ```

1. Each activity has a unique ID. Select an ID from the earlier list and view the details for that activity.

   ```bash
   magento-cloud activity:get wvl5wm7s5vkhy
   ```

1. View the full log for that activity.

   ```bash
   magento-cloud activity:log wvl5wm7s5vkhy
   ```

   Sample response:

    ```bash
    Activity ID: wvl5wm7s5vkhy
    Type: environment.backup
    Description: Guthrie created a backup of Master
    Created: 2023-09-08T14:03:33+00:00
    State: complete
    Log:
    Creating backup of master
    Created backup eg5pu63egt2dcojkljalzjdopa
    ```
