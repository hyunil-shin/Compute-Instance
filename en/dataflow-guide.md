## Data & Analytics > DataFlow > Console Guide

DataFlow can be used in the following order:

* Service activation
    1. Create a project.
    2. Select the desired project.
    3. Enable the DataFlow service.
* Flow execution
    1. Create a flow.
    2. Add necessary nodes and define the behavior of each node by entering configuration values.
    3. Complete the flow by connecting nodes to determine the execution order of nodes.
    4. Execute the flow.
    5. Check log information to verify that the flow executed normally.

## Management

This is a page for viewing and managing flow metadata information.
Click **Data & Analytics > DataFlow > Management**.

![management_main.png](images/management_main_2025_06.png)

### Search

Search for flows based on given criteria.

* When searching by flow name, it searches for flows that contain the search term in their names.

### Filter

Search for flows based on given conditions.

* Provides filtering options based on flow status values.

### Flow List

Displays the search results of flows in table format.

* Displays simple flow metadata and current flow execution status.
* Sorted by most recent modification date.
* You can select flows to use management functions such as modifying flows, viewing flow details, and starting flows.
* You can view only flows with specific statuses through filter condition functionality.
* Once flows are retrieved, you need to click **Refresh** to update the search results.
* Displays 12 flows per page, and you can move between pages by clicking **Previous** and **Next**.

#### Flow Status Information

| Flow Execution Status                                         | Description |
|---------------------------------------------------| --- |
| START\_FAILED  | Flow execution request failed. |
| QUOTA\_EXCEEDED | Flow execution failed due to insufficient resources for flow execution. |
| STARTING       | Securing resources for flow execution. |
| PREPARING      | Flow execution preparation completed. |
| RUNNING        | Flow is running. |
| ERROR              | An error occurred during flow execution due to communication failures or authentication issues. If <b>ERROR</b> occurs continuously, please contact **Customer Support > 1:1 Inquiry**. |
| STOP\_FAILED   | Flow termination request failed. |
| STOPPED        | Flow has been terminated. |
| DRAINING       | Flow is draining. |
| UNKNOWN            | An error occurred during flow execution due to unknown causes. If <b>UNKNOWN</b> occurs continuously, please contact **Customer Support > 1:1 Inquiry**. |

#### Flow Status Change Notification Email
* You can receive notification emails when the status changes to target flow statuses for notifications.
* Target flow statuses for notifications
    * RUNNING
    * ERROR
    * STOPPED
* Default recipients
    * Members with **DataFlow ADMIN** role in the project where the DataFlow service in use is enabled


### Create Flow

Creates metadata to define a flow.

* Creates flow metadata by adding name and description for flow identification.
* Flow names can be duplicated with other flows.
* Select the execution mode according to the flow purpose.
* You can easily load flows with desired functionality by specifying a flow template.
* You can configure the instance type for executing the flow.

### Modify Flow

Modifies the flow's metadata.

* Modifies existing flow name and description and reflects them in the flow metadata.
* Flow templates cannot be specified.
* Flow modification is possible even while the flow is running.
* You can change the instance type for executing the flow.
    * However, the changed instance type will be applied from the next flow execution.

### Copy Flow

Creates new metadata with existing flow definitions.

* Creates new metadata with `_copy` added to the existing flow's name.
* Copies the flow logic of the existing flow as is.
* Running flows can also be copied.
* Running flows are copied in a stopped state.
* If the current save state of the flow is a temporary save, the last saved version of the existing flow is not copied.
* Even if a flow with a registered scheduler is copied, the copied flow will not have the scheduler registered.
* The copied flow is completely separate from the existing flow.

### Delete Flow

Deletes flow metadata.

* Completely deletes flow metadata.
* Deleted flows cannot be recovered.
* Running flows cannot be deleted.

### More - Start Flow
Starts a flow in stopped state.

* Each flow can only run one at a time.
* Temporarily saved flows start with the last saved version.
* Flows that have only been temporarily saved without ever being saved cannot be started.
* Flows must be saved at least once to be started.
* Even if a flow is being executed by a scheduler, you cannot start the flow the same way as a flow started by a user.

### More - Terminate Flow
* You can terminate flows that are preparing for execution, running, or draining.
* Terminates without processing remaining events.

### More - Drain and Terminate Flow
* You can drain and terminate running flows.
* Draining means processing the remaining events in the flow.
* If the timeout period is exceeded, it terminates even if draining is not complete.
* If draining completes while timeout time remains, it terminates immediately.
* Flows that are draining can be terminated immediately through flow termination.