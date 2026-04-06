## Data & Analytics > DataFlow > Console Guide

DataFlow can be used in the following order:

* Service activation
    1. Create a project.
    2. Select the desired project.
    3. Enable the DataFlow service.
* Flow execution
    1. Create a flow.
    2. Add required nodes and enter configuration values to define each node's behavior.
    3. Complete the flow by connecting nodes to determine their execution order.
    4. Execute the flow.
    5. Check log information to verify that the flow executed normally.

## Management

This page allows you to query and manage flow metadata information.
Click **Data & Analytics > DataFlow > Management**.

![management_main.png](images/management_main_2025_06.png)

### Search

Search for flows based on given criteria.

* When searching by flow name, it finds flows that contain the search term in their name.

### Filter

Search for flows based on given conditions.

* Provides filtering options based on flow status values.

### Flow List

Displays query result flows in table format.

* Shows simple flow metadata and current flow execution status.
* Sorted by most recent modification date.
* You can select flows to use management functions such as modify flow, view flow details, and start flow.
* You can query only flows with specific statuses through filter condition functionality.
* Flows that have been queried once must be refreshed by clicking **Refresh** to update the query results.
* Displays 12 flows per page, and you can navigate pages by clicking **Previous** and **Next**.

#### Flow Status Information

| Flow Execution Status                                         | Description |
|---------------------------------------------------| --- |
| START\_FAILED  | Failed to request flow execution. |
| QUOTA\_EXCEEDED | Flow execution failed due to insufficient resources. |
| STARTING       | Securing resources for flow execution. |
| PREPARING      | Flow execution preparation is complete. |
| RUNNING        | Flow is executing. |
| ERROR              | An error occurred during flow execution due to communication failure or authentication issues. If <b>ERROR</b> persists, please contact **Customer Support > Inquiries**. |
| STOP\_FAILED   | Failed to request flow termination. |
| STOPPED        | Flow has been terminated. |
| DRAINING       | Flow is draining. |
| UNKNOWN            | An error occurred during flow execution due to unknown causes. If <b>UNKNOWN</b> persists, please contact **Customer Support > Inquiries**. |

#### Flow Status Change Notification Email
* You can receive notification emails when the flow changes to a notification target status.
* Notification target flow statuses
    * RUNNING
    * ERROR
    * STOPPED
* Default recipients
    * Members with **DataFlow ADMIN** role in projects where the DataFlow service in use is activated


### Create Flow

Creates metadata to define a flow.

* Creates flow metadata by adding a name and description for flow identification.
* Flow names can be duplicated with other flows.
* Select an execution mode based on the flow purpose.
* You can specify a flow template to easily load flows with desired functionality.
* You can configure the instance type for executing the flow.

### Modify Flow

Modifies the flow's metadata.

* Modifies existing flow name and description and reflects them in the flow metadata.
* Flow templates cannot be specified.
* Flow modification is possible even while the flow is running.
* You can change the instance type for executing the flow.
    * However, the changed instance type will be applied from the next flow execution.

### Copy Flow

Creates new metadata using an existing flow definition.

* Creates new metadata with `_copy` added to the existing flow's name.
* Copies the flow logic that the existing flow has as-is.
* Running flows can also be copied.
* Running flows are copied in stopped state.
* If the flow's current save state is temporary save, the existing flow's last saved version is not copied.
* Even if you copy a flow with a registered scheduler, the copied flow will not have a scheduler registered.
* The copied flow is completely separate from the original flow.

### Delete Flow

Deletes flow metadata.

* Completely deletes flow metadata.
* Deleted flows cannot be recovered.
* Running flows cannot be deleted.

### More - Start Flow
Starts a flow in stopped state.

* Only one of each flow can run simultaneously.
* Temporarily saved flows start with the last saved version.
* Flows that have only been temporarily saved without ever being saved cannot be started.
* Flows must be saved at least once to be started.
* Even if a flow is running by scheduler, it cannot be started the same way as a flow started by a user.

### More - Stop Flow
* You can stop flows that are preparing for execution, running, or draining.
* Terminates without processing remaining events.

### More - Drain and Stop Flow
* You can drain and stop running flows.
* Draining means processing the flow's remaining events.
* If the timeout period is exceeded, it terminates even if draining is not finished.
* If draining finishes while timeout time remains, it terminates immediately.
* Flows that are draining can be terminated immediately through flow termination.