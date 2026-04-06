## Monitoring > Cloud Monitoring > Usage Scenario
This covers the overall usage scenario from dashboard configuration to notification creation.<br>
The order of using Cloud Monitoring is as follows.

- Service Selection<br>
  Cloud Monitoring is a service provided by default when creating a project.<br>
  Therefore, you can use the service after creating a project without any additional work.<br>
  For how to create a project, see [NHN Cloud Console User Guide](https://docs.nhncloud.com/en/nhncloud/en/console-guide/).
- Metric Collection Settings<br>
  Configure metric collection for each service.
- Dashboard Configuration<br>
  Add widgets to the dashboard to configure it freely.
- Notification Creation<br>
  Set thresholds to receive notifications when events occur.

## Metric Collection Settings
To configure the dashboard, first set up metric collection for each service.

1. Select **Cloud Monitoring > Metric Management**.
2. In the Metric Management page, check the service-specific metrics provided by Cloud Monitoring.
3. Click the **Metric Collection Settings** toggle for the service you want to collect metrics from to activate it.
4. When the 'Do you want to start metric collection?' modal appears, click **OK**.
5. Once collection starts, you can add widgets using those metrics.

![image](https://static.toastoven.net/prod_cloud_monitoring/cloud_monitoring_ug_01-1.png)

- Instance and GPU Instance services are metrics provided by default.
- Metrics are collected only for activated services. Check whether the service is activated.
- If you click the **Metric Collection Settings** toggle to deactivate it, collection of those metrics stops and they will not be displayed on the dashboard.

## Dashboard Configuration
Now you are ready to configure the dashboard.<br>
Let's create a dashboard and add widgets.

### Create Dashboard
1. Click **+Create Dashboard**.
![image](https://static.toastoven.net/prod_cloud_monitoring/cloud_monitoring_ug_02_01-1.png)
2. Enter the **Dashboard Name** and **Description**, then click **OK**.
![image](https://static.toastoven.net/prod_cloud_monitoring/cloud_monitoring_ug_02_01-2.png)
3. Check the created dashboard.

### Add Widget
1. Click **Add Widget** to go to the widget addition page.
![image](https://static.toastoven.net/prod_cloud_monitoring/cloud_monitoring_ug_02_02-1.png)
2. Enter the **Widget Name** and select **Graph Type** and **Service**.
   - You can only select services that have collection settings activated in **Metric Management**.
3. Select the **Resource Type** and **Metric Item** corresponding to the selected service.
   - Boxes for setting filters and legends for each selected metric item are displayed.
![image](https://static.toastoven.net/prod_cloud_monitoring/cloud_monitoring_ug_02_02-2.png)

4. Set filters to selectively check only the metrics you want.
   - For example, to monitor only specific instances in the Korea (Pangyo) region, set as follows:
     - Click **+Add** to add a filter.
     - Set the filter in the order of label, operator, condition as `Region` `=` `kr1` (Korea (Pangyo)).
     - Add a filter and select `Instance` `=` `{instance name}` in the order of label, operator, condition.
     - This will display specific instance metrics from the kr1 (Korea (Pangyo)) region on the graph.
5. You can set the legend name, unit, and Y-axis position as needed.
   - If the units are the same for each metric, they are displayed with one Y-axis.
   - In Y-axis position settings, auto automatically arranges Y-axes in left and right order when units differ by metric.
![image](https://static.toastoven.net/prod_cloud_monitoring/cloud_monitoring_ug_02_02-3.png)

6. Use the **Preview** function to check if the desired type of graph is drawn.
7. Once confirmed, click **Add** to add the widget to the dashboard.
![image](https://static.toastoven.net/prod_cloud_monitoring/cloud_monitoring_ug_02_02-4.png)

### Edit Dashboard
Check the widgets added to the dashboard and edit them into the desired form.

1. Click the toggle at the top right of the dashboard to change from **View Mode** to **Edit Mode**.
2. Drag and drop widgets to change their position or add widget groups to organize the dashboard.
   - Click **Add Widget Group** to add a group at the bottom. Drag and drop widgets into the group to arrange them.
![image](https://static.toastoven.net/prod_cloud_monitoring/cloud_monitoring_ug_02_03-1.png)

## Notification Settings
For more efficient monitoring, set up to receive notifications when events occur.

### Create Notification
1. Select **Cloud Monitoring > Notification Management > Notification Settings**.
2. Click **Create Notification** to go to the creation page.
![image](https://static.toastoven.net/prod_cloud_monitoring/cloud_monitoring_ug_03_01-1.png)

3. In **Basic Information**, enter the notification **Name** and **Description** and select **Service**.
4. Select the **Resource Type** and **Metrics** corresponding to the selected service.
   - Boxes for setting filters and notification conditions for each selected metric are displayed.
![image](https://static.toastoven.net/prod_cloud_monitoring/cloud_monitoring_ug_03_01-2.png)

5. Set filters to configure notifications for the desired metrics.
6. Enter the **Threshold** and **Duration** which are conditions for triggering notifications.
   - For example, to receive notifications when CPU usage is 30% or higher and this state persists for 3 minutes or more, set as follows:
     - Select **CPU Usage Rate** for **Metrics** and set filters as needed.
     - Select `>=` (greater than or equal to) for **Comparison Method**.
     - Enter `30` for **Threshold** and `3` for **Duration**.
![image](https://static.toastoven.net/prod_cloud_monitoring/cloud_monitoring_ug_03_01-3.png)

7. Select **Notification Recipients**.
   - You can select notification recipient groups created in the project as recipients.
   - Create project notification recipient groups first.
![image](https://static.toastoven.net/prod_cloud_monitoring/cloud_monitoring_ug_03_01-4.png)

You can also quickly set up notifications from dashboard widgets.

1. Click the more options icon at the top right of the widget, then click **Create Notification** from the dropdown menu.
2. You move to the **Create Notification** page, and the filters for each metric selected when creating the widget are applied as-is.
![image](https://static.toastoven.net/prod_cloud_monitoring/cloud_monitoring_ug_03_01-5.png)

Now notifications will be triggered when the set thresholds are reached, and the occurrence history can be checked in **Notification Management > Notification Occurrence History**.

## Project Dashboard Display Settings
You can check dashboards created in the Cloud Monitoring service from the project main screen.

1. Click **Cloud Monitoring > Dashboard > Dashboard Management**.
2. Click the **Project Dashboard Display Settings** toggle for the dashboard you want to display on the project main screen to activate it.
   ![image](https://static.toastoven.net/prod_cloud_monitoring/cloud_monitoring_ug_04-1.png)

You can also check the configured dashboard in the project's **Custom Dashboard** for quick monitoring.