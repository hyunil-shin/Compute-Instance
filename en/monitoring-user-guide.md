## Monitoring > Cloud Monitoring > Usage Scenario
This covers the overall usage scenario from dashboard configuration to alert creation.<br>
The order of using Cloud Monitoring is as follows.

- Service Selection<br>
  Cloud Monitoring is a service provided by default when creating a project.<br>
  Therefore, you can use the service after creating a project without any additional work.<br>
  For how to create a project, see [NHN Cloud Console User Guide](https://docs.nhncloud.com/en/nhncloud/en/console-guide/).
- Metrics Collection Settings<br>
  Configure metrics collection for each service.
- Dashboard Configuration<br>
  Freely configure the dashboard by adding widgets.
- Create Alerts<br>
  Set thresholds to receive alerts when events occur.

## Metrics Collection Settings
To configure the dashboard, first set up metrics collection for each service.

1. Select **Cloud Monitoring > Metrics Management**.
2. Check the service-specific metrics provided by Cloud Monitoring on the Metrics Management page.
3. Click the **Metrics Collection Settings** toggle for the service you want to collect metrics from to enable it.
4. When the 'Do you want to start collecting metrics?' modal appears, click **Confirm**.
5. Once collection starts, you can add widgets using those metrics.

![image](images/cloud_monitoring_ug_01-1.png)

- Instance and GPU Instance services are metrics provided by default.
- Metrics are collected only for activated services. Check whether services are activated.
- If you click the **Metrics Collection Settings** toggle to disable it, collection of those metrics will stop and they will not be displayed on the dashboard.

## Dashboard Configuration
Now you're ready to configure the dashboard.<br>
Let's create a dashboard and add widgets.

### Create Dashboard
1. Click **+Create Dashboard**.
![image](images/cloud_monitoring_ug_02_01-1.png)
2. Enter the **Dashboard Name** and **Description**, then click **Confirm**.
![image](images/cloud_monitoring_ug_02_01-2.png)
3. Check the created dashboard.

### Add Widget
1. Click **Add Widget** to go to the widget addition page.
![image](images/cloud_monitoring_ug_02_02-1.png)
2. Enter the **Widget Name** and select **Graph Type** and **Service**.
   - You can only select services for which collection settings are enabled in **Metrics Management**.
3. Select the **Resource Type** and **Metrics Item** corresponding to the selected service.
   - Boxes for setting filters and legends are displayed for each selected metrics item.
![image](images/cloud_monitoring_ug_02_02-2.png)

4. Set filters to selectively check only the desired metrics.
   - For example, to monitor only specific instances in the Korea (Pangyo) region, set as follows:
     - Click **+Add** to add a filter.
     - Set the filter in the order of label, operator, condition: `Region` `=` `kr1`(Korea (Pangyo)).
     - Add a filter to select label, operator, condition in order: `Instance` `=` `{Instance Name}`.
     - This will display specific instance metrics from the kr1(Korea (Pangyo)) region on the graph.
5. You can set the legend name, unit, and Y-axis position as needed.
   - If metrics have the same unit, they are displayed with one Y-axis.
   - In Y-axis position settings, Auto automatically places Y-axes in left and right order when metrics have different units.
![image](images/cloud_monitoring_ug_02_02-3.png)

6. Use the **Preview** feature to check if the desired graph format is drawn.
7. Once confirmed, click **Add** to add the widget to the dashboard.
![image](images/cloud_monitoring_ug_02_02-4.png)

### Edit Dashboard
Check the widgets added to the dashboard and edit them to the desired format.

1. Click the toggle at the top right of the dashboard to change from **View Mode** to **Edit Mode**.
2. Drag and drop widgets to change their position or add widget groups to organize the dashboard.
   - Clicking **Add Widget Group** adds a group at the bottom. Drag and drop widgets to the group to arrange them.
![image](images/cloud_monitoring_ug_02_03-1.png)

## Alert Settings
Set up to receive alerts when events occur for more efficient monitoring.

### Create Alert
1. Select **Cloud Monitoring > Alert Management > Alert Settings**.
2. Click **Create Alert** to go to the creation page.
![image](images/cloud_monitoring_ug_03_01-1.png)

3. In **Basic Information**, enter the alert **Name** and **Description** and select **Service**.
4. Select the **Resource Type** and **Metrics** corresponding to the selected service.
   - Boxes for setting filters and alert conditions for each selected metric are displayed.
![image](images/cloud_monitoring_ug_03_01-2.png)

5. Set filters to configure alerts for the desired metrics.
6. Enter the **Threshold** and **Duration** which are the conditions for triggering alerts.
   - For example, to receive alerts when CPU usage is 30% or higher and this condition persists for 3 minutes or more, set as follows:
     - Select **CPU Usage** as the **Metric** and set filters as needed.
     - Select `>=` (greater than or equal) for **Comparison Method**.
     - Enter `30` for **Threshold** and `3` for **Duration**.
![image](images/cloud_monitoring_ug_03_01-3.png)

7. Select **Alert Recipients**.
   - You can select alert recipient groups created in the project as recipients.
   - Create project alert recipient groups first.
![image](images/cloud_monitoring_ug_03_01-4.png)

You can also quickly set up alerts from dashboard widgets.

1. Click the more options icon at the top right of the widget, then click **Create Alert** from the dropdown menu.
2. You'll go to the **Create Alert** page, and the filters for each metric selected when creating the widget are applied as-is.
![image](images/cloud_monitoring_ug_03_01-5.png)

Now alerts will be triggered when the set threshold is reached, and the occurrence history can be checked in **Alert Management > Alert History**.

## Project Dashboard Display Settings
You can check dashboards created in the Cloud Monitoring service from the project main screen.

1. Click **Cloud Monitoring > Dashboard > Dashboard Management**.
2. Click the **Project Dashboard Display Settings** toggle for the dashboard you want to display on the project main screen to enable it.
   ![image](images/cloud_monitoring_ug_04-1.png)

You can also check the configured dashboard in the project's **Custom Dashboard** for quick monitoring.