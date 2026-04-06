## Data & Analytics > DataFlow > Console Guide

DataFlow can be used in the following order:

* Service Activation
    1. Create a project.
    2. Select the desired project.
    3. Enable the DataFlow service.
* Flow Execution
    1. Create a flow.
    2. Add necessary nodes and enter configuration values to define the behavior of each node.
    3. Complete the flow by determining the execution order of nodes through node connections.
    4. Execute the flow.
    5. Check the log information to verify that the flow executed successfully.

## Management

This is the page for viewing and managing flow metadata information.
Click **Data & Analytics > DataFlow > Management**.

![management_main.png](images/management_main_2025_06.png)

### Search

Search for flows based on given criteria.

* When searching by flow name, flows containing the search term in their name are found.

### Filter

Search for flows based on given conditions.

* Provides filtering options based on flow status values.

### Flow List

Displays the search results of flows in table format.

* Displays simple flow metadata and current flow execution status.
* Sorted by most recent modification date.
* You can select flows to use management functions such as modify flow, view flow details, and start flow.
* You can view only flows with specific statuses through filter condition functionality.
* Once flows are retrieved, you must click **Refresh** to update the search results.
* Displays 12 flows per page, and you can navigate pages by clicking **Previous** and **Next**.

#### Flow Status Information

| Flow Execution Status                                         | Description |
|---------------------------------------------------| --- |
| START_FAILED  | Flow execution request failed. |
| QUOTA_EXCEEDED | Flow execution failed due to insufficient resources for flow execution. |
| STARTING       | Securing resources for flow execution. |
| PREPARING      | Flow execution preparation completed. |
| RUNNING        | Flow is running. |
| ERROR              | An error occurred during flow execution due to communication failure or authentication issues. If <b>ERROR</b> occurs continuously, please contact us through **Customer Support > Inquire**. |
| STOP_FAILED   | Flow termination request failed. |
| STOPPED        | Flow has been stopped. |
| DRAINING       | Flow is draining. |
| UNKNOWN            | An error occurred during flow execution due to unknown causes. If <b>UNKNOWN</b> occurs continuously, please contact us through **Customer Support > Inquire**. |

#### Flow Status Change Notification Email
* You can receive notification emails when the flow status changes to a target notification status.
* Target flow statuses for notification
    * RUNNING
    * ERROR
    * STOPPED
* Default recipients
    * Members with **DataFlow ADMIN** role in the project where the DataFlow service in use is activated


### Create Flow

Create metadata to define a flow.

* Create flow metadata by adding a name and description for flow identification.
* Flow names can be duplicated with other flows.
* Select the execution mode based on the flow purpose.
* Specify a flow template to easily load flows with the functionality users want.
* You can configure the instance type for executing the flow.

### Modify Flow

Modify the metadata of a flow.

* Modify existing flow name and description to reflect in the flow metadata.
* Flow templates cannot be specified.
* Flow modification is possible even while the flow is running.
* You can change the instance type for executing the flow.
    * However, the changed instance type will be applied from the next flow execution.

### Copy Flow

Create new metadata using an existing flow definition.

* Create new metadata with the existing flow name plus `_copy` added.
* Copy the flow logic of the existing flow as is.
* Running flows can also be copied.
* Running flows are copied in a stopped state.
* If the current save state of the flow is a temporary save, the last saved version of the existing flow is not copied.
* Even if a flow with a registered scheduler is copied, the copied flow does not have a scheduler registered.
* The copied flow is completely separate from the original flow.

### Delete Flow

Delete flow metadata.

* Completely delete flow metadata.
* Deleted flows cannot be recovered.
* Running flows cannot be deleted.

### More - Start Flow
Start a stopped flow.

* Each flow can only run one at a time.
* Temporarily saved flows start with the last saved version.
* Flows that have only been temporarily saved without ever being saved cannot be started.
* Flows must be saved at least once to be started.
* Even if a flow is running by the scheduler, you cannot start a flow in the same way as a flow started by a user.

### More - Stop Flow
* You can stop flows that are preparing for execution, running, or draining.
* Terminates without processing remaining events.

### More - Drain and Stop Flow
* You can drain and then stop running flows.
* Draining means processing the remaining events in the flow.
* If the timeout period is exceeded, it terminates even if draining is not finished.
* If draining finishes while timeout time remains, it terminates immediately.
* Draining flows can be terminated immediately through flow termination.