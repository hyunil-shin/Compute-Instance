## Data & Analytics > DataFlow > Console Guide

DataFlow can be used in the following order:

* Enable the Service
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

This is a page where you can retrieve and manage flow metadata information.
Click **Data & Analytics > DataFlow > Management**.

![management_main.png](http://static.toastoven.net/prod_dataflow/ko/console_user_guide/management_main_2025_06.png)

### Search

Search for flows based on given criteria.

* When searching by flow name, flows that include the search term in their name are retrieved.

### Filter

Search for flows based on given conditions.

* Provides filtering options based on flow status values.

### Flow List

Displays the search results as a table.

* Displays simple flow metadata and the current flow execution status.
* Sorts by the most recent modification date.
* By selecting a flow, you can use management functions such as modifying the flow, viewing flow details, and starting the flow.
* You can retrieve only flows with a specific status through the filter condition function.
* Once a flow is retrieved, you must click **Refresh** to update the search results.
* 12 flows are retrieved per page, and you can navigate pages by clicking **Previous** and **Next**.

#### Flow Status Information

| Flow Execution Status | Description |
|------|---|
| START_FAILED | Failed to request flow execution. |
| QUOTA_EXCEEDED | Flow execution failed due to insufficient resources for flow execution. |
| STARTING | Resources for flow execution are being secured. |
| PREPARING | Flow execution preparation has been completed. |
| RUNNING | The flow is running. |
| ERROR | An error occurred during flow execution due to communication failure or authentication failure. If <b>ERROR</b> continues to occur, please contact **Customer Support > Inquiry**. |
| STOP_FAILED | Failed to request flow termination. |
| STOPPED | The flow has been terminated. |
| DRAINING | The flow is draining. |
| UNKNOWN | An error occurred during flow execution due to an unknown cause. If <b>UNKNOWN</b> continues to occur, please contact **Customer Support > Inquiry**. |

#### Flow Status Change Notification Email
* You can receive notification emails when the status changes to the target flow status for notification.
* Target flow statuses for notification
    * RUNNING
    * ERROR
    * STOPPED
* Default notification recipients
    * Members with the **DataFlow ADMIN** role in the project where the DataFlow service in use is enabled

### Create Flow

Creates metadata to define a flow.

* Create flow metadata by adding a name and description to identify the flow.
* Flow names can be duplicated with other flows.
* Select the execution mode according to the flow's purpose.
* You can easily load flows with desired functions by specifying a flow template.
* You can set the instance type for executing the flow.

### Modify Flow

Modifies the metadata of a flow.

* Modify the existing flow name and description and reflect them in the flow metadata.
* Flow templates cannot be specified.
* You can modify flows even while they are running.
* You can change the instance type for executing the flow.
    * However, the changed instance type is applied from the next flow execution.

### Copy Flow

Creates new metadata using the definition of an existing flow.

* Creates new metadata with `_copy` appended to the name of the existing flow.
* Copies the flow logic of the existing flow as-is.
* Even running flows can be copied.
* Running flows are copied in a stopped state.
* If the current saved state of a flow is temporary, the last saved version of the existing flow is not copied.
* Even if a flow with a registered scheduler is copied, the copied flow does not have a scheduler registered.
* The copied flow is completely separate from the existing flow.

### Delete Flow

Deletes the flow metadata.

* Completely deletes the flow metadata.
* Deleted flows cannot be recovered.
* Running flows cannot be deleted.

### More - Start Flow
Starts a stopped flow.

* Each flow can only run one at a time.
* Temporarily saved flows are started with the last saved version.
* Flows that have only been temporarily saved without ever being saved cannot be started.
* Flows must be saved at least once before they can be started.
* Even if a flow is being executed by a scheduler, it cannot be started the same way as a flow started by a user.

### More - Stop Flow
* You can stop flows that are in preparation, running, or draining.
* Terminates without processing remaining events.

### More - Drain and Stop Flow
* You can drain and stop a running flow.
* Draining means processing the remaining events of the flow.
* If the timeout is exceeded, the flow is terminated even if draining is not complete.
* If draining is completed while timeout remains, the flow is terminated immediately.
* Flows in the draining state can be terminated immediately through flow termination.