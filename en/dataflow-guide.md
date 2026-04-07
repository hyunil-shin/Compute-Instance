## Data & Analytics > DataFlow > Console Guide

DataFlow can be used in the following order.

* Enable the Service
    1. Create a project.
    2. Select the desired project.
    3. Enable the DataFlow service.
* Execute a Flow
    1. Create a flow.
    2. Add the necessary nodes and enter configuration values to define the behavior of each node.
    3. Determine the execution order of nodes by connecting them to complete the flow.
    4. Execute the flow.
    5. Check the log information to confirm that the flow executed successfully.

## Management

This is a page for retrieving and managing flow metadata information.
Click **Data & Analytics > DataFlow > Management**.

![management_main.png](images/management_main_2025_06.png)

### Search

Searches for flows based on given criteria.

* When searching by flow name, it searches for flows whose names contain the search term.

### Filter

Searches for flows based on given conditions.

* Provides filtering options based on flow status values.

### Flow List

Displays the retrieved flows in a table format.

* Displays simple flow metadata and the current flow execution status.
* Sorted by the most recent modification date.
* You can select a flow to use management features such as modifying the flow, viewing flow details, and starting the flow.
* You can retrieve only flows with a specific status using the filter conditions feature.
* Once retrieved, flows require clicking **Refresh** to update the results.
* 12 flows are displayed per page, and you can navigate pages by clicking **Previous** and **Next**.

#### Flow Status Information

| Flow Execution Status                                         | Description |
|---------------------------------------------------| --- |
| START\_FAILED  | The flow execution request failed. |
| QUOTA\_EXCEEDED | The flow failed to execute due to insufficient resources. |
| STARTING       | Resources for flow execution are being allocated. |
| PREPARING      | Flow execution preparation is complete. |
| RUNNING        | The flow is running. |
| ERROR              | An error occurred during flow execution due to communication failure or authentication issues. If <b>ERROR</b> persists, please contact us through **Customer Support > Contact Us**. |
| STOP\_FAILED   | The flow termination request failed. |
| STOPPED        | The flow has been terminated. |
| DRAINING       | The flow is draining. |
| UNKNOWN            | An error occurred during flow execution due to an unknown cause. If <b>UNKNOWN</b> persists, please contact us through **Customer Support > Contact Us**. |

#### Flow Status Change Notification Email
* You can receive notification emails when a flow changes to a notification-eligible status.
* Notification-eligible flow statuses
    * RUNNING
    * ERROR
    * STOPPED
* Default recipients
    * Members with the **DataFlow ADMIN** role in the project where the active DataFlow service is enabled


### Create Flow

Creates metadata to define a flow.

* Creates flow metadata by adding a name and description for flow identification.
* Flow names can be duplicated with other flows.
* Select an execution mode according to the flow's purpose.
* You can specify a flow template to easily load a flow with the desired functionality.
* You can set the instance type for executing the flow.

### Modify Flow

Modifies the metadata of a flow.

* Modifies the existing flow name and description to reflect changes in the flow metadata.
* Flow templates cannot be specified.
* Flows can be modified even while running.
* You can change the instance type for executing the flow.
    * However, the changed instance type will be applied starting from the next flow execution.

### Copy Flow

Creates new metadata based on an existing flow definition.

* Creates new metadata with `_copy` appended to the existing flow's name.
* Copies the flow logic of the existing flow as-is.
* Running flows can also be copied.
* Running flows are copied in a stopped state.
* If the current save state of the flow is a temporary save, the last saved version of the existing flow is not copied.
* Even if a flow with a registered scheduler is copied, the copied flow will not have the scheduler registered.
* The copied flow is a completely separate flow from the original.

### Delete Flow

Deletes the flow metadata.

* Permanently deletes the flow metadata.
* Deleted flows cannot be restored.
* Running flows cannot be deleted.

### More - Start Flow
Starts a flow that is in a stopped state.

* Only one instance of each flow can run at a time.
* A temporarily saved flow starts with the last saved version.
* A flow that has only been temporarily saved and never fully saved cannot be started.
* A flow must be saved at least once before it can be started.
* Even if a flow is being executed by a scheduler, it cannot be started in the same way as a flow started by a user.

### More - Stop Flow
* You can stop a flow that is preparing to run, running, or draining.
* The flow terminates without processing remaining events.

### More - Stop Flow After Draining
* You can stop a running flow after draining.
* Draining refers to processing the remaining events of the flow.
* If the timeout period is exceeded, the flow terminates even if draining has not finished.
* If draining finishes while the timeout period remains, the flow terminates immediately.
* A flow that is draining can be immediately terminated through the stop flow action.