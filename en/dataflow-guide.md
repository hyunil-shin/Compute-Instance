## Data & Analytics > DataFlow > Console Guide

DataFlow can be used in the following order.

* Enable the Service
    1. Create a project.
    2. Select the desired project.
    3. Enable the DataFlow service.
* Execute a Flow
    1. Create a flow.
    2. Add the necessary nodes and enter settings to define the behavior of each node.
    3. Determine the execution order of nodes by connecting them to complete the flow.
    4. Execute the flow.
    5. Check the log information to confirm that the flow executed successfully.

## Management

This is the page for retrieving and managing flow metadata information.
Click **Data & Analytics > DataFlow > Management**.

![management_main.png](images/management_main_2025_06.png)

### Search

Searches for flows based on the given criteria.

* When searching by flow name, it searches for flows whose names contain the search term.

### Filter

Searches for flows based on the given conditions.

* Provides filtering options based on flow status values.

### Flow List

Displays the retrieved flows in a table format.

* Displays simple flow metadata and the current flow execution status.
* Sorted by the most recent modification date.
* Select a flow to use management features such as modifying a flow, viewing flow details, and starting a flow.
* Use the filter conditions feature to view only flows in a specific status.
* Once retrieved, flows require clicking **Refresh** to update the results.
* 12 flows are displayed per page, and you can navigate pages by clicking **Previous** and **Next**.

#### Flow Status Information

| Flow Execution Status                                         | Description |
|---------------------------------------------------| --- |
| START\_FAILED  | The flow execution request failed. |
| QUOTA\_EXCEEDED | The flow failed to execute due to insufficient resources. |
| STARTING       | Resources for flow execution are being secured. |
| PREPARING      | Flow execution preparation is complete. |
| RUNNING        | The flow is running. |
| ERROR              | An error occurred during flow execution due to communication failure or authentication issues. If <b>ERROR</b> persists, please contact us via **Customer Support > Contact Us**. |
| STOP\_FAILED   | The flow termination request failed. |
| STOPPED        | The flow has been terminated. |
| DRAINING       | The flow is draining. |
| UNKNOWN            | An error occurred during flow execution due to an unknown cause. If <b>UNKNOWN</b> persists, please contact us via **Customer Support > Contact Us**. |

#### Flow Status Change Notification Emails
* You can receive notification emails when a flow changes to a status that is subject to notification.
* Flow statuses subject to notification
    * RUNNING
    * ERROR
    * STOPPED
* Default recipients
    * Members with the **DataFlow ADMIN** role in the project where the DataFlow service in use is enabled


### Create Flow

Creates metadata to define a flow.

* Creates flow metadata by adding a name and description for flow identification.
* Flow names can be duplicated with other flows.
* Select an execution mode based on the purpose of the flow.
* Specify a flow template to easily load a flow with the desired functionality.
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

* Creates new metadata with `_copy` appended to the existing flow name.
* Copies the flow logic from the existing flow as-is.
* Running flows can also be copied.
* Running flows are copied in a stopped state.
* If the flow's current save state is a temporary save, the last saved version of the existing flow is not copied.
* Even if a flow with a registered scheduler is copied, the copied flow will not have the scheduler registered.
* The copied flow is completely separate from the original flow.

### Delete Flow

Deletes flow metadata.

* Permanently deletes the flow metadata.
* Deleted flows cannot be restored.
* Running flows cannot be deleted.

### More - Start Flow
Starts a flow that is in a stopped state.

* Each flow can only run one instance at a time.
* Temporarily saved flows start with the last saved version.
* Flows that have only been temporarily saved without being saved at least once cannot be started.
* A flow must be saved at least once before it can be started.
* Even if a flow is being run by a scheduler, it cannot be started in the same way as a flow started by a user.

### More - Stop Flow
* You can stop flows that are preparing to run, running, or draining.
* Remaining events are not processed upon termination.

### More - Stop Flow After Draining
* You can stop a running flow after draining.
* Draining refers to processing the remaining events of a flow.
* If the timeout period is exceeded, the flow will be terminated even if draining has not finished.
* If draining finishes while the timeout period remains, the flow will be terminated immediately.
* A flow that is draining can be terminated immediately by stopping the flow.