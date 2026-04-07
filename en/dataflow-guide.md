## Data & Analytics > DataFlow > Console Guide

DataFlow can be used in the following order:

* Service Activation
    1. Create a project.
    2. Select the desired project.
    3. Activate the DataFlow service.
* Flow Execution
    1. Create a flow.
    2. Add necessary nodes and enter configuration values to define the behavior of each node.
    3. Complete the flow by determining the execution order of nodes through node connections.
    4. Execute the flow.
    5. Check log information to verify that the flow executed successfully.

## Management

This is a page for retrieving and managing flow metadata information.
Click **Data & Analytics > DataFlow > Management**.

![management_main.png](images/management_main_2025_06.png)

### Search

Search for flows based on given criteria.

* When searching based on flow name, it searches for flows that contain the search term in the name.

### Filter

Search for flows based on given conditions.

* Provides filtering options based on flow status values.

### Flow List

Displays the retrieved flows in table format.

* Displays simple flow metadata and current flow execution status.
* Sorted by most recent modification date.
* You can select a flow to use management functions such as flow modification, flow details view, and flow start.
* You can retrieve only flows with specific status through filter condition functions.
* Once retrieved, flows require clicking **Refresh** to update the retrieval results.
* Retrieves 12 flows per page, and you can navigate pages by clicking **Previous** and **Next**.

#### Flow Status Information

| Flow Execution Status                                         | Description |
|---------------------------------------------------| --- |
| START\_FAILED  | Failed to request flow execution. |
| QUOTA\_EXCEEDED | Failed to execute due to insufficient resources for flow execution. |
| STARTING       | Securing resources for flow execution. |
| PREPARING      | Flow execution preparation completed. |
| RUNNING        | Flow is executing. |
| ERROR              | An error occurred during flow execution due to communication failure or authentication issues. If <b>ERROR</b> continues to occur, please contact **Customer Support > Contact Us**. |
| STOP\_FAILED   | Failed to request flow termination. |
| STOPPED        | Flow has been terminated. |
| DRAINING       | Flow is draining. |
| UNKNOWN            | An error occurred during flow execution due to unknown causes. If <b>UNKNOWN</b> continues to occur, please contact **Customer Support > Contact Us**. |

#### Flow Status Change Notification Email
* You can receive notification emails when changed to notification target flow status.
* Notification target flow status
    * RUNNING
    * ERROR
    * STOPPED
* Default recipients
    * Members with **DataFlow ADMIN** role in the project where the DataFlow service in use is activated


### Create Flow

Creates metadata to define a flow.

* Creates flow metadata by adding name and description for flow identification.
* Flow names can be duplicated with other flows.
* Select execution mode based on flow purpose.
* You can specify a flow template to easily load flows with desired functionality.
* You can configure the instance type for executing the flow.

### Modify Flow

Modifies the metadata of a flow.

* Modifies existing flow name and description and reflects them in the flow metadata.
* Flow templates cannot be specified.
* Flow modification is possible even while the flow is executing.
* You can change the instance type for executing the flow.
    * However, the changed instance type applies from the next flow execution.

### Copy Flow

Creates new metadata with existing flow definition.

* Creates new metadata with `_copy` text added to the existing flow name.
* Copies the flow logic of the existing flow as-is.
* Running flows can also be copied.
* Running flows are copied in stopped status.
* If the current save status of the flow is temporary save, the last saved version of the existing flow is not copied.
* Even if you copy a flow with a registered scheduler, the copied flow does not have a scheduler registered.
* The copied flow is completely separate from the existing flow.

### Delete Flow

Deletes flow metadata.

* Completely deletes flow metadata.
* Deleted flows cannot be recovered.
* Running flows cannot be deleted.

### More - Start Flow
Starts a flow in stopped status.

* Each flow can only execute one at a time.
* Temporarily saved flows start with the last saved version.
* Flows that have only been temporarily saved without ever being saved cannot be started.
* Flows must be saved at least once to be started.
* Even if a flow is being executed by the scheduler, you cannot start the flow same as a flow started by the user.

### More - Stop Flow
* You can terminate flows that are preparing for execution, executing, or draining.
* Terminates without processing remaining events.

### More - Drain and Stop Flow
* You can terminate running flows after draining.
* Draining means processing remaining events in the flow.
* If the timeout period is exceeded, it terminates even if draining has not finished.
* If draining finishes while timeout time remains, it terminates immediately.
* Flows that are draining can be terminated immediately through flow termination.