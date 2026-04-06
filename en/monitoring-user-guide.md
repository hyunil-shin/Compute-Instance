## Monitoring > Cloud Monitoring > Usage Scenario
This covers the overall usage scenario from dashboard configuration to notification creation.<br>
The order for using Cloud Monitoring is as follows.

- Service selection<br>
  Cloud Monitoring is a service provided by default when creating a project.<br>
  Therefore, you can use the service after creating a project without any additional work.<br>
  For how to create a project, see [NHN Cloud Console User Guide](https://docs.nhncloud.com/en/nhncloud/en/console-guide/).
- Metrics collection settings<br>
  Configure metrics collection for each service.
- Dashboard configuration<br>
  Freely configure by adding widgets to the dashboard.
- Create notifications<br>
  Set thresholds to receive notifications when events occur.

## Metrics Collection Settings
To configure a dashboard, first set up metrics collection for each service.

1. Select **Cloud Monitoring > Metrics Management**.
2. On the Metrics Management page, check the service-specific metrics provided by Cloud Monitoring.
3. Click the **Metrics Collection Settings** toggle for the service you want to collect metrics from to enable it.
4. When the 'Do you want to start collecting metrics?' modal appears, click **Confirm**.
5. Once collection starts, you can add widgets using those metrics.

![image](images/cloud_monitoring_ug_01-1.png)

- Instance and GPU Instance services have metrics provided by default.
- Metrics are collected only for enabled services. Check whether the service is enabled.
- If you click the **Metrics Collection Settings** toggle to disable it, collection of those metrics will stop and they will not be displayed on the dashboard.

## Dashboard Configuration
Now you're ready to configure a dashboard.<br>
Let's create a dashboard and add widgets.


### Create Dashboard
1. Click **+Create Dashboard**.
![image](https://static.toastoven.net/prod_cloud_monitoring/cloud_monitoring_ug_02_01-1.png)
2. Enter the **Dashboard Name** and **Description**, then click **Confirm**.
![image](images/cloud_monitoring_ug_02_01-2.png)
3. Check the created dashboard.


### Add Widget
1. Click **Add Widget** to go to the widget addition page.
![image](images/cloud_monitoring_ug_02_02-1.png)
2. Enter the **Widget Name** and select **Graph Type** and **Service**.
   - You can only select services that have collection settings enabled in **Metrics Management**.
3. Select the **Resource Type** and **Metrics Item** corresponding to the selected service.
   - Boxes for setting filters and legends are displayed for each selected metrics item.
![image](images/cloud_monitoring_ug_02_02-2.png)

4. Set filters to selectively check only the desired metrics.
   - For example, to monitor only a specific instance in the Korea (Pangyo) region, set as follows:
     - Click **+Add** to add a filter.
     - Set a filter with label, operator, and condition in order: `Region` `=` `kr1` (Korea (Pangyo)).
     - Add a filter and select label, operator, and condition in order: `Instance` `=` `{instance name}`.
     - This will display specific instance metrics from the kr1 (Korea (Pangyo)) region on the graph.
5. You can set the legend name, unit, and Y-axis position as needed.
   - If metrics have the same unit, they are displayed with one Y-axis.
   - Auto in Y-axis position setting automatically places Y-axes in left and right order when metrics have different units.
![image](images/cloud_monitoring_ug_02_02-3.png)

6. Use the **Preview** function to check if the desired graph format is drawn.
7. Once confirmed, click **Add** to add the widget to the dashboard.
![image](images/cloud_monitoring_ug_02_02-4.png)


### Edit Dashboard
Check widgets added to the dashboard and edit them as desired.

1. Click the toggle at the top right of the dashboard to change from **View Mode** to **Edit Mode**.
2. Drag and drop widgets to change their position or add widget groups to organize the dashboard.
   - Click **Add Widget Group** to add a group at the bottom. Drag and drop widgets into the group to arrange them.
![image](images/cloud_monitoring_ug_02_03-1.png)

## Notification Settings
For more efficient monitoring, set up to receive notifications when events occur.

### Create Notification
1. Select **Cloud Monitoring > Notification Management > Notification Settings**.
2. Click **Create Notification** to go to the creation page.
![image](images/cloud_monitoring_ug_03_01-1.png)

3. In **Basic Information**, enter the notification **Name** and **Description** and select **Service**.
4. Select the **Resource Type** and **Metrics** corresponding to the selected service.
   - Boxes for setting filters and notification conditions for each selected metric are displayed.
![image](images/cloud_monitoring_ug_03_01-2.png)

5. Set filters to configure notifications for the desired metrics.
6. Enter the **Threshold** and **Duration** that are conditions for triggering notifications.
   - For example, to receive notifications when CPU usage is 30% or more and this state persists for 3 minutes or more, set as follows:
     - Select **CPU Usage Rate** as the **Metrics** and set filters as needed.
     - Select `>=` (greater than or equal to) as the **Comparison Method**.
     - Enter `30` for **Threshold** and `3` for **Duration**.
![image](images/cloud_monitoring_ug_03_01-3.png)

7. Select **Notification Recipients**.
   - You can select notification recipient groups created in the project as recipients.
   - Create project notification recipient groups first.
![image](images/cloud_monitoring_ug_03_01-4.png)

You can also quickly set up notifications from dashboard widgets.

1. Click the more options icon at the top right of the widget, then click **Create Notification** in the dropdown menu.
2. Navigate to the **Create Notification** page, where the filters for each metric selected when creating the widget are applied as-is.
![image](images/cloud_monitoring_ug_03_01-5.png)

Now notifications will be triggered when the set threshold is reached, and the occurrence history can be checked in **Notification Management > Notification Occurrence History**.

## Project Dashboard Display Settings
You can check dashboards created in the Cloud Monitoring service on the project main screen.

1. Click **Cloud Monitoring > Dashboard > Dashboard Management**.
2. Click the **Project Dashboard Display Settings** toggle for the dashboard you want to display on the project main screen to enable it.
   ![image](images/cloud_monitoring_ug_04-1.png)

You can also check configured dashboards in the project's **Custom Dashboard** for quick monitoring.