## Data & Analytics > DataFlow > Console User Guide

DataFlow can be used in the following order:

* Service activation
    1. Create a project.
    2. Select the desired project.
    3. Enable the DataFlow service.
* Flow execution
    1. Create a flow.
    2. Add necessary nodes and enter configuration values to define the behavior of each node.
    3. Complete the flow by connecting nodes to determine the execution order of nodes.
    4. Execute the flow.
    5. Check log information to verify that the flow was executed normally.

## Management

This page is for querying and managing flow metadata information.
Click **Data & Analytics > DataFlow > Management**.

![management_main.png](images/management_main_2025_06.png)

### Search

Search for flows based on given criteria.

* When searching by flow name, it searches for flows that contain the search term in the name.

### Filter

Search for flows based on given conditions.

* Provides filtering options based on flow status values.

### Flow List

Displays query result flows in table format.

* Displays simple flow metadata and current flow execution status.
* Sorted by most recent modification date.
* You can select a flow to use management features such as flow modification, flow details view, and flow start.
* You can view only flows with specific statuses through filter conditions.
* Once flows are queried, you must click **Refresh** to update the query results.
* Displays 12 flows per page, and you can navigate pages by clicking **Previous** and **Next**.

#### Flow Status Information

| Flow Execution Status                                      | Description |
|----------------------------------------------------------| --- |
| START\_FAILED  | Failed to request flow execution. |
| QUOTA\_EXCEEDED | Failed to execute due to insufficient resources for flow execution. |
| STARTING       | Securing resources for flow execution. |
| PREPARING      | Flow execution preparation is complete. |
| RUNNING        | Flow is executing. |
| ERROR              | An error occurred during flow execution due to communication failures or authentication issues. If <b>ERROR</b> occurs continuously, please contact **Customer Support > Inquiry**. |
| STOP\_FAILED   | Failed to request flow termination. |
| STOPPED        | Flow has been terminated. |
| DRAINING       | Flow is draining. |
| UNKNOWN            | An error occurred during flow execution due to an unknown cause. If <b>UNKNOWN</b> occurs continuously, please contact **Customer Support > Inquiry**. |

#### Flow Status Change Notification Email
* You can receive notification emails when flow status changes to notification target status.
* Notification target flow statuses
    * RUNNING
    * ERROR
    * STOPPED
* Default recipients
    * Members with **DataFlow ADMIN** role in the project where the DataFlow service in use is activated


### Create Flow

Creates metadata to define a flow.

* Creates flow metadata by adding name and description for flow identification.
* Flow names can duplicate with other flows.
* Selects execution mode according to flow purpose.
* Users can easily load flows with desired functionality by specifying flow templates.
* You can configure instance types for executing flows.

### Modify Flow

Modifies flow metadata.

* Modifies existing flow name and description and reflects them in flow metadata.
* Flow templates cannot be specified.
* Flow modification is possible even during flow execution.
* You can change the instance type for executing flows.
    * However, the changed instance type will be applied from the next flow execution.

### Copy Flow

Creates new metadata with existing flow definition.

* Creates new metadata with `_copy` added to the existing flow name.
* Copies the flow logic of the existing flow as is.
* Running flows can also be copied.
* Running flows are copied in stopped state.
* If the current save state of the flow is temporary save, the last saved version of the existing flow is not copied.
* Even if a flow with a registered scheduler is copied, the copied flow does not have a scheduler registered.
* The copied flow is completely separate from the existing flow.

### Delete Flow

Deletes flow metadata.

* Completely deletes flow metadata.
* Deleted flows cannot be recovered.
* Running flows cannot be deleted.

### More - Start Flow
Starts a stopped flow.

* Each flow can only run one at a time.
* Temporarily saved flows start with the last saved version.
* Flows that have only been temporarily saved without ever being saved cannot be started.
* Flows must be saved at least once to be started.
* Even if a flow is running by scheduler, it cannot start flows in the same way as flows started by users.

### More - Stop Flow
* You can stop flows that are preparing for execution, executing, or draining.
* Terminates without processing remaining events.

### More - Drain and Stop Flow
* You can drain and then stop running flows.
* Draining means processing the remaining events of the flow.
* If the timeout period is exceeded, it terminates even if draining is not finished.
* If draining finishes while timeout time remains, it terminates immediately.
* Draining flows can be terminated immediately through flow stop.