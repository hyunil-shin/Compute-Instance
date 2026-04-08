## Data & Analytics > DataFlow > Console Guide

DataFlow can be used in the following order.

* Service activation
    1. Create a project.
    2. Select the desired project.
    3. Enable the DataFlow service.
* Flow execution
    1. Create a flow.
    2. Add the necessary nodes and define the behavior of each node by entering configuration values.
    3. Complete the flow by determining the execution order of nodes through node connections.
    4. Execute the flow.
    5. Check log information to verify that the flow executed normally.

## Management

This is the page for retrieving and managing flow metadata information.
Click **Data & Analytics > DataFlow > Management**.

![management_main.png](images/management_main_2025_06.png)

### Search

Search flows based on given criteria.

* When searching by flow name, it searches for flows that contain the search term in their names.

### Filter

Search flows based on given conditions.

* Provides filtering options based on flow status values.

### Flow List

Displays the retrieved flows in a table format.

* Displays simple flow metadata and current flow execution status.
* Sorts by most recent modification date.
* You can select a flow to use management functions such as flow modification, flow details view, and flow start.
* You can retrieve only flows with specific statuses through the filter condition feature.
* Once flows are retrieved, you must click **Refresh** to update the search results.
* 12 flows are displayed per page, and you can navigate pages by clicking **Previous** and **Next**.

#### Flow Status Information

| Flow Execution Status                                         | Description |
|---------------------------------------------------| --- |
| START\_FAILED  | Failed to request flow execution. |
| QUOTA\_EXCEEDED | Failed to execute due to insufficient resources for flow execution. |
| STARTING       | Securing resources for flow execution. |
| PREPARING      | Flow execution preparation is complete. |
| RUNNING        | Flow is running. |
| ERROR              | An error occurred during flow execution due to communication failure or authentication issues. If <b>ERROR</b> persists, please contact us through **Customer Support > Contact Us**. |
| STOP\_FAILED   | Failed to request flow termination. |
| STOPPED        | Flow has been stopped. |
| DRAINING       | Flow is draining. |
| UNKNOWN            | An error occurred during flow execution due to unknown causes. If <b>UNKNOWN</b> persists, please contact us through **Customer Support > Contact Us**. |

#### Flow Status Change Notification Email
* You can receive notification emails when the status changes to a target flow status for notification.
* Target flow statuses for notification
    * RUNNING
    * ERROR
    * STOPPED
* Default recipients
    * Members with the **DataFlow ADMIN** role in the project where the DataFlow service in use is activated


### Create Flow

Create metadata to define a flow.

* Create flow metadata by adding a name and description for flow identification.
* Flow names can be duplicated with other flows.
* Select an execution mode based on the flow purpose.
* You can easily load a flow with the desired functionality by specifying a flow template.
* You can set the instance type for executing the flow.

### Modify Flow

Modify the metadata of a flow.

* Modify existing flow names and descriptions and reflect them in the flow metadata.
* Flow templates cannot be specified.
* Flow modification is possible even while the flow is running.
* You can change the instance type for executing the flow.
    * However, the changed instance type is applied from the next flow execution.

### Copy Flow

Create new metadata with an existing flow definition.

* Creates new metadata with `_copy` added to the existing flow's name.
* Copies the flow logic of the existing flow as-is.
* Running flows can also be copied.
* Running flows are copied in a stopped state.
* If the flow's current save state is temporary save, the last saved version of the existing flow is not copied.
* Even if you copy a flow with a registered scheduler, the copied flow does not have a scheduler registered.
* The copied flow is completely separate from the original flow.

### Delete Flow

Delete flow metadata.

* Completely deletes flow metadata.
* Deleted flows cannot be recovered.
* Running flows cannot be deleted.

### More - Start Flow
Start a flow in stopped state.

* Each flow can only run one at a time.
* Temporarily saved flows start with the last saved version.
* Flows that have only been temporarily saved without being saved cannot be started.
* A flow must be saved at least once before it can be started.
* Even if a flow is running by a scheduler, you cannot start the flow in the same way as a user-initiated flow.

### More - Stop Flow
* You can stop flows that are preparing for execution, running, or draining.
* Stops without processing remaining events.

### More - Drain and Stop Flow
* You can drain and then stop running flows.
* Draining means processing the remaining events in the flow.
* If the timeout period is exceeded, it stops even if draining is not finished.
* If draining finishes while there is still timeout remaining, it stops immediately.
* Draining flows can be stopped immediately through flow termination.