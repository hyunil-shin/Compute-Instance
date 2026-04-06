## Data & Analytics > DataFlow > Console Guide

DataFlow can be used in the following order:

* Service Activation
    1. Create a project.
    2. Select the desired project.
    3. Activate the DataFlow service.
* Flow Execution
    1. Create a flow.
    2. Add required nodes and enter configuration values to define the behavior of each node.
    3. Complete the flow by determining the execution order of nodes through node connections.
    4. Execute the flow.
    5. Check log information to verify that the flow executed normally.

## Management

This page allows you to view and manage flow metadata information.
Click **Data & Analytics > DataFlow > Management**.

![management_main.png](images/management_main_2025_06.png)

### Search

Search flows based on given criteria.

* Searching by flow name will find flows that contain the search term in their names.

### Filter

Search flows based on given conditions.

* Provides filtering options based on flow status values.

### Flow List

Displays the query result flows in table format.

* Shows simple flow metadata and current flow execution status.
* Sorted by most recent modification date.
* You can select flows to use management functions such as modifying flows, viewing flow details, and starting flows.
* You can view only flows with specific statuses through the filter condition feature.
* Once flows are queried, you must click **Refresh** to update the query results.
* Displays 12 flows per page, and you can navigate pages by clicking **Previous** and **Next**.

#### Flow Status Information

| Flow Execution Status                                         | Description |
|---------------------------------------------------| --- |
| START\_FAILED  | Failed to request flow execution. |
| QUOTA\_EXCEEDED | Flow execution failed due to insufficient resources for flow execution. |
| STARTING       | Securing resources for flow execution. |
| PREPARING      | Flow execution preparation completed. |
| RUNNING        | Flow is executing. |
| ERROR              | An error occurred during flow execution due to communication failures or authentication issues. If <b>ERROR</b> occurs persistently, please contact us through **Customer Support > Inquiries**. |
| STOP\_FAILED   | Failed to request flow termination. |
| STOPPED        | Flow has been terminated. |
| DRAINING       | Flow is draining. |
| UNKNOWN            | An error occurred during flow execution due to unknown causes. If <b>UNKNOWN</b> occurs persistently, please contact us through **Customer Support > Inquiries**. |

#### Flow Status Change Notification Email
* You can receive notification emails when the status changes to a target flow status for notifications.
* Target flow statuses for notifications
    * RUNNING
    * ERROR
    * STOPPED
* Default recipients
    * Members with **DataFlow ADMIN** role in the project where the DataFlow service in use is activated


### Create Flow

Creates metadata to define a flow.

* Creates flow metadata by adding names and descriptions for flow identification.
* Flow names can be duplicated with other flows.
* Select execution mode based on flow purpose.
* You can easily load flows with desired functions by specifying flow templates.
* You can set the instance type for executing the flow.

### Modify Flow

Modifies flow metadata.

* Reflects changes to flow metadata by modifying existing flow names and descriptions.
* Flow templates cannot be specified.
* Flow modification is possible even while the flow is executing.
* You can change the instance type for executing the flow.
    * However, the changed instance type will be applied from the next flow execution.

### Copy Flow

Creates new metadata using existing flow definitions.

* Creates new metadata with `_copy` added to the existing flow name.
* Copies the flow logic from the existing flow as is.
* Running flows can also be copied.
* Running flows are copied in a stopped state.
* If the current save state of the flow is temporary save, the last saved version of the existing flow is not copied.
* Even if you copy a flow with a registered scheduler, the copied flow will not have the scheduler registered.
* The copied flow is completely separate from the existing flow.

### Delete Flow

Deletes flow metadata.

* Completely deletes flow metadata.
* Deleted flows cannot be recovered.
* Running flows cannot be deleted.

### More - Start Flow
Starts a flow in stopped state.

* Each flow can only execute one at a time.
* Temporarily saved flows start with the last saved version.
* Flows that have only been temporarily saved without ever being saved cannot be started.
* Flows must be saved at least once before they can be started.
* Even if a flow is being executed by the scheduler, flows cannot be started the same way as flows started by users.

### More - Terminate Flow
* You can terminate flows that are preparing to execute, executing, or draining.
* Terminates without processing remaining events.

### More - Terminate Flow After Draining
* You can terminate running flows after draining.
* Draining means processing the remaining events in the flow.
* If the timeout period is exceeded, it will terminate even if draining is not finished.
* If draining finishes while timeout time remains, it will terminate immediately.
* Flows that are draining can be terminated immediately through flow termination.