## Data & Analytics > DataFlow > Console Guide

DataFlow can be used in the following sequence:

* Enable the Service
    1. Create a project.
    2. Select the desired project.
    3. Enable the DataFlow service.
* Execute Flow
    1. Create a flow.
    2. Add necessary nodes and enter configuration values to define how each node operates.
    3. Complete the flow by determining the order of node operations through node connections.
    4. Execute the flow.
    5. Check log information to verify that the flow executed normally.

## Management

This page retrieves and manages flow metadata information.
Click **Data & Analytics > DataFlow > Management**.

![management_main.png](http://static.toastoven.net/prod_dataflow/ko/console_user_guide/management_main_2025_06.png)

### Search

Search for flows based on given criteria.

* When searching by flow name, flows with the search term included in the name are retrieved.

### Filter

Search for flows based on given conditions.

* Filter options are provided based on flow status values.

### Flow List

Display query results as a table of flows.

* Display simple flow metadata and current flow execution status.
* Sort by most recent modification date.
* Select a flow to use management functions such as modifying the flow, viewing flow details, and starting the flow.
* Use the filter condition feature to retrieve only flows of a specific status.
* Once a flow is retrieved, press **Refresh** to update the query results.
* 12 flows are retrieved per page, and you can navigate pages by clicking **Previous** and **Next**.

#### Flow Status Information

| Flow Execution Status                              | Description |
|---------------------------------------------------| --- |
| START\_FAILED  | Failed to request flow execution. |
| QUOTA\_EXCEEDED | Flow execution failed due to insufficient resources. |
| STARTING       | Securing resources for flow execution. |
| PREPARING      | Flow execution preparation is complete. |
| RUNNING        | Flow is executing. |
| ERROR              | An error occurred during flow execution due to communication failure, authentication failure, etc. If <b>ERROR</b> continues to occur, contact us through **Customer Support > 1:1 Inquiry**. |
| STOP\_FAILED   | Failed to request flow termination. |
| STOPPED        | Flow has been terminated. |
| DRAINING       | Flow is draining. |
| UNKNOWN            | An error occurred during flow execution due to an unknown cause. If <b>UNKNOWN</b> continues to occur, contact us through **Customer Support > 1:1 Inquiry**. |

#### Flow Status Change Notification Email
* You can receive notification emails when the flow status changes to the notification target status.
* Notification target flow statuses
    * RUNNING
    * ERROR
    * STOPPED
* Default notification recipients
    * Members with the **DataFlow ADMIN** role in the project where the active DataFlow service is enabled

### Create Flow

Create metadata to define a flow.

* Create flow metadata by adding name and description for flow identification.
* Flow names can be duplicated across different flows.
* Select an execution mode according to the flow purpose.
* Specify a flow template so users can easily load flows with desired functionality.
* You can configure the instance type for executing the flow.

### Modify Flow

Modify the flow's metadata.

* Modify the existing flow name and description and reflect them in the flow metadata.
* Flow template cannot be specified.
* Flow modification is possible even while the flow is executing.
* You can change the instance type for executing the flow.
    * However, the changed instance type applies from the next flow execution onward.

### Copy Flow

Create new metadata using existing flow definitions.

* Create new metadata with `_copy` appended to the existing flow name.
* Copy the flow logic of the existing flow as is.
* Flows in execution can also be copied.
* Flows in execution are copied in a stopped state.
* If the flow's current save state is temporary save, the last saved version of the existing flow is not copied.
* Even if you copy a flow with a registered scheduler, the copied flow does not have a scheduler registered.
* The copied flow is completely separate from the existing flow.

### Delete Flow

Delete flow metadata.

* Completely delete flow metadata.
* Deleted flows cannot be recovered.
* Flows in execution cannot be deleted.

### More - Start Flow
Start a stopped flow.

* Each flow can execute only one at a time.
* A temporarily saved flow starts with the last saved version.
* Flows that are only temporarily saved without being saved even once cannot be started.
* A flow must be saved at least once before it can be started.
* Even if a flow is executing due to a scheduler, it cannot be started the same way as a flow started by a user.

### More - Stop Flow
* You can stop flows that are preparing to execute, executing, or draining.
* Stop without processing remaining events.

### More - Drain and Stop Flow
* You can drain and stop an executing flow.
* Draining means processing the remaining events of the flow.
* If the timeout is exceeded, the flow is stopped even if draining is not complete.
* If draining completes while there is remaining timeout, the flow stops immediately.
* A draining flow can be stopped immediately through flow termination.