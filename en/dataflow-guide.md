## Data & Analytics > DataFlow > Console Guide

DataFlow can be used in the following order:

* Service activation
    1. Create a project.
    2. Select the desired project.
    3. Activate the DataFlow service.
* Flow execution
    1. Create a flow.
    2. Add necessary nodes and define their behavior by entering configuration values.
    3. Complete the flow by connecting nodes to determine their execution order.
    4. Execute the flow.
    5. Check log information to verify that the flow executed successfully.

## Management

This is the page for querying and managing flow metadata information.
Click **Data & Analytics > DataFlow > Management**.

![management_main.png](images/management_main_2025_06.png)

### Search

Search flows based on given criteria.

* Searching by flow name returns flows that contain the search term in their name.

### Filter

Search flows based on given conditions.

* Provides filtering options based on flow status values.

### Flow List

Displays query result flows in table format.

* Displays simple flow metadata and current flow execution status.
* Sorted by last modified date.
* You can select flows to use management features such as flow modification, flow details view, and flow start.
* You can view only flows with specific statuses through the filter condition feature.
* Once queried, flows must be refreshed by clicking **Refresh** to update query results.
* Displays 12 flows per page, and you can navigate pages by clicking **Previous** and **Next**.

#### Flow Status Information

| Flow Execution Status                                         | Description |
|---------------------------------------------------| --- |
| START\_FAILED  | Flow execution request failed. |
| QUOTA\_EXCEEDED | Flow execution failed due to insufficient resources for execution. |
| STARTING       | Securing resources for flow execution. |
| PREPARING      | Flow execution preparation completed. |
| RUNNING        | Flow is executing. |
| ERROR              | An error occurred during flow execution due to communication failure or authentication failure. If <b>ERROR</b> persists, please contact **Customer Support > Inquiry**. |
| STOP\_FAILED   | Flow termination request failed. |
| STOPPED        | Flow has been terminated. |
| DRAINING       | Flow is draining. |
| UNKNOWN            | An error occurred during flow execution due to unknown causes. If <b>UNKNOWN</b> persists, please contact **Customer Support > Inquiry**. |

#### Flow Status Change Notification Email
* You can receive notification emails when the flow changes to a target status for notifications.
* Target flow statuses for notifications
    * RUNNING
    * ERROR
    * STOPPED
* Default recipients
    * Members with the **DataFlow ADMIN** role in projects where the DataFlow service in use is activated


### Create Flow

Create metadata to define a flow.

* Create flow metadata by adding a name and description for flow identification.
* Flow names can be duplicated with other flows.
* Select execution mode based on the flow purpose.
* You can easily load flows with desired functionality by specifying a flow template.
* You can set the instance type for executing the flow.

### Modify Flow

Modify the flow's metadata.

* Modify existing flow name and description to reflect in flow metadata.
* Flow templates cannot be specified.
* Flow modification is possible even during flow execution.
* You can change the instance type for executing the flow.
    * However, the changed instance type applies from the next flow execution.

### Copy Flow

Create new metadata using an existing flow definition.

* Creates new metadata with `_copy` added to the existing flow name.
* Copies the flow logic from the existing flow as is.
* Running flows can also be copied.
* Running flows are copied in a stopped state.
* If the flow's current save state is temporary save, the last saved version of the existing flow is not copied.
* Even if you copy a flow with a registered scheduler, the copied flow does not have the scheduler registered.
* The copied flow is completely separate from the existing flow.

### Delete Flow

Delete flow metadata.

* Completely deletes flow metadata.
* Deleted flows cannot be recovered.
* Running flows cannot be deleted.

### More - Start Flow
Start a stopped flow.

* Each flow can only run one at a time.
* Temporarily saved flows start with the last saved version.
* Flows that have only been temporarily saved and never saved cannot be started.
* Flows must be saved at least once before they can be started.
* Even if a flow is running by a scheduler, you cannot start a flow the same as a flow started by a user.

### More - Stop Flow
* You can stop flows that are preparing to execute, executing, or draining.
* Stops without processing remaining events.

### More - Drain and Stop Flow
* You can drain and stop running flows.
* Draining means processing the flow's remaining events.
* If the timeout period is exceeded, it stops even if draining is not complete.
* If draining completes while timeout time remains, it stops immediately.
* Draining flows can be stopped immediately through flow termination.