## Data & Analytics > DataFlow > Console Guide

DataFlow can be used in the following sequence:

* Enable Service
    1. Create a project.
    2. Select the desired project.
    3. Enable the DataFlow service.
* Run Flow
    1. Create a flow.
    2. Add necessary nodes and enter configuration values to define how each node operates.
    3. Complete the flow by determining the order of node operations through node connections.
    4. Run the flow.
    5. Check the log information to verify that the flow executed normally.

## Management

This page allows you to view and manage flow metadata information.
Click **Data & Analytics > DataFlow > Management**.

![management_main.png](http://static.toastoven.net/prod_dataflow/ko/console_user_guide/management_main_2025_06.png)

### Search

Search flows based on given criteria.

* When you search by flow name, flows that contain the search term in their name are displayed.

### Filter

Search flows based on given conditions.

* Filter options are provided based on flow status values.

### Flow List

Displays search results as a table.

* Displays simple flow metadata and the current flow execution status.
* Sorted by the most recent modification date.
* Select a flow to use management features such as modifying the flow, viewing flow details, and starting the flow.
* Use the filter condition feature to retrieve only flows with a specific status.
* To refresh the search results for a previously retrieved flow, you must click **Refresh**.
* Up to 12 flows are retrieved per page, and you can navigate pages by clicking **Previous** and **Next**.

#### Flow Status Information

| Flow Execution Status | Description |
|---------------------------------------------------| --- |
| START\_FAILED  | Failed to request flow execution. |
| QUOTA\_EXCEEDED | Failed to execute the flow due to insufficient resources. |
| STARTING       | Securing resources for flow execution. |
| PREPARING      | Flow execution preparation is complete. |
| RUNNING        | The flow is running. |
| ERROR              | An error occurred during flow execution due to communication failure or authentication failure. If <b>ERROR</b> continues to occur, contact **Customer Support > Inquiry**. |
| STOP\_FAILED   | Failed to request flow termination. |
| STOPPED        | The flow has stopped. |
| DRAINING       | The flow is draining. |
| UNKNOWN            | An error occurred during flow execution due to an unknown cause. If <b>UNKNOWN</b> continues to occur, contact **Customer Support > Inquiry**. |

#### Flow Status Change Notification Email
* You can receive notification emails when the flow status changes to a monitored status.
* Monitored flow statuses
    * RUNNING
    * ERROR
    * STOPPED
* Default recipients
    * Members with the **DataFlow ADMIN** role in the project where the DataFlow service is enabled

### Create Flow

Create metadata to define a flow.

* Add a name and description to create flow metadata for flow identification.
* Flow names can be duplicated with other flows.
* Select an execution mode based on the flow purpose.
* Specify a flow template to easily load flows with desired functionality.
* You can set the instance type for executing the flow.

### Modify Flow

Modify the flow's metadata.

* Modify the existing flow name and description and apply them to the flow metadata.
* Flow templates cannot be specified.
* You can modify the flow while it is running.
* You can change the instance type for executing the flow.
    * However, the changed instance type will be applied from the next flow execution onwards.

### Copy Flow

Create new metadata based on an existing flow definition.

* Create new metadata with `_copy` appended to the existing flow's name.
* Copy the flow logic of the existing flow as-is.
* Even running flows can be copied.
* Running flows are copied in a stopped state.
* If the current save state of the flow is temporary save, the last saved version of the existing flow is not copied.
* Even if you copy a flow with a registered scheduler, the copied flow will not have a scheduler registered.
* A copied flow is completely separate from the existing flow.

### Delete Flow

Delete flow metadata.

* Completely delete the flow metadata.
* Deleted flows cannot be recovered.
* Running flows cannot be deleted.

### More - Start Flow
Start a stopped flow.

* Only one flow can be executed at a time for each flow.
* A temporarily saved flow starts with the last saved version.
* A flow that is only temporarily saved without ever being saved cannot be started.
* A flow must be saved at least once before it can be started.
* Even if a flow is running by a scheduler, it cannot be started by a user in the same way.

### More - Stop Flow
* You can stop flows that are preparing to run, running, or draining.
* Stops without processing remaining events.

### More - Drain and Stop Flow
* You can drain and stop a running flow.
* Draining means processing remaining events in the flow.
* If the timeout period is exceeded, the flow stops even if draining is not complete.
* If draining is complete before the timeout period expires, the flow stops immediately.
* A draining flow can be stopped immediately through flow termination.