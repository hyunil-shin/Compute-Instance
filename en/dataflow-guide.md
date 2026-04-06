## Data & Analytics > DataFlow > Console Guide

DataFlow can be used in the following order:

* Service Activation
    1. Create a project.
    2. Select the desired project.
    3. Activate the DataFlow service.
* Flow Execution
    1. Create a flow.
    2. Add required nodes and enter configuration values to define the behavior of each node.
    3. Complete the flow by connecting nodes to determine the execution order of nodes.
    4. Execute the flow.
    5. Check log information to verify that the flow executed normally.

## Management

This is a page for retrieving and managing flow metadata information.
Click **Data & Analytics > DataFlow > Management**.

![management_main.png](images/management_main_2025_06.png)

### Search

Search for flows based on given criteria.

* When searching by flow name, it searches for flows that contain the search term in their name.

### Filter

Search for flows based on given conditions.

* Provides filtering options based on flow status values.

### Flow List

Displays retrieved flows in table format.

* Shows simple flow metadata and current flow execution status.
* Sorted by last modified date.
* You can select flows to use management functions such as modify flow, view flow details, and start flow.
* You can view only flows with specific statuses through filter condition functionality.
* Once flows are retrieved, you must click **Refresh** to update the query results.
* Displays 12 flows per page, and you can navigate pages by clicking **Previous** and **Next**.

#### Flow Status Information

| Flow Execution Status                                         | Description |
|---------------------------------------------------| --- |
| START\_FAILED  | Flow execution request failed. |
| QUOTA\_EXCEEDED | Flow execution failed due to insufficient resources for flow execution. |
| STARTING       | Securing resources for flow execution. |
| PREPARING      | Flow execution preparation completed. |
| RUNNING        | Flow is running. |
| ERROR              | An error occurred during flow execution due to communication failure or authentication issues. If <b>ERROR</b> occurs persistently, please contact **Customer Support > 1:1 Inquiry**. |
| STOP\_FAILED   | Flow termination request failed. |
| STOPPED        | Flow has been terminated. |
| DRAINING       | Flow is draining. |
| UNKNOWN            | An error occurred during flow execution due to unknown causes. If <b>UNKNOWN</b> occurs persistently, please contact **Customer Support > 1:1 Inquiry**. |

#### Flow Status Change Notification Email
* You can receive notification emails when the status changes to target flow statuses.
* Target flow statuses for notifications
    * RUNNING
    * ERROR
    * STOPPED
* Default recipients
    * Members with **DataFlow ADMIN** role in the project where the DataFlow service in use is activated


### Create Flow

Creates metadata to define a flow.

* Creates flow metadata by adding name and description for flow identification.
* Flow names can be duplicated with other flows.
* Selects execution mode based on flow purpose.
* You can easily load flows with desired functionality by specifying flow templates.
* You can set the instance type for executing flows.

### Modify Flow

Modifies flow metadata.

* Modifies existing flow name and description to reflect in flow metadata.
* Flow templates cannot be specified.
* Flow modification is possible even while the flow is running.
* You can change the instance type for executing flows.
    * However, the changed instance type applies from the next flow execution.

### Copy Flow

Creates new metadata using existing flow definition.

* Creates new metadata with `_copy` added to the existing flow's name.
* Copies the flow logic from the existing flow as-is.
* Running flows can also be copied.
* Running flows are copied in stopped state.
* If the flow's current save state is temporary save, the last saved version of the existing flow is not copied.
* Even if you copy a flow with a registered scheduler, the copied flow does not have a scheduler registered.
* The copied flow is completely separate from the original flow.

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
* Even if a flow is running by the scheduler, you cannot start the flow the same as a flow started by a user.

### More - Terminate Flow
* You can terminate flows that are preparing for execution, running, or draining.
* Terminates without processing remaining events.

### More - Drain and Terminate Flow
* You can drain and then terminate running flows.
* Draining means processing remaining events in the flow.
* If the timeout period is exceeded, it terminates even if draining is not finished.
* If draining finishes while there is remaining timeout time, it terminates immediately.
* Flows that are draining can be terminated immediately through flow termination.