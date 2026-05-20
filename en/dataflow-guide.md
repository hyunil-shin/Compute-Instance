## Data & Analytics > DataFlow > Console Guide

DataFlow can be used in the following order.

* Enable Service
    1. Create a project.
    2. Select the desired project.
    3. Enable the DataFlow service.
* Run Flow
    1. Create a flow.
    2. Add necessary nodes and enter configuration values to define how each node operates.
    3. Complete the flow by determining the order of node operations through node connections.
    4. Run the flow.
    5. Check log information to verify that the flow has executed normally.

## Management

This is the page where you can retrieve and manage flow metadata information.
Click **Data & Analytics > DataFlow > Management**.

![management_main.png](http://static.toastoven.net/prod_dataflow/ko/console_user_guide/management_main_2025_06.png)

### Search

Search for flows based on given criteria.

* When searching by flow name, flows that contain the search term in their name are displayed.

### Filter

Search for flows based on given conditions.

* Provides filtering options based on flow status values.

### Flow List

Displays the search results in table format.

* Displays simple flow metadata and current flow execution status.
* Sorted by the most recent modification date.
* You can manage flows by selecting a flow to change it, view flow details, start the flow, and more.
* You can view only flows with a specific status using the filter condition feature.
* Once a flow is retrieved, you must click **Refresh** to update the search results.
* 12 flows are displayed per page, and you can move between pages by clicking **Previous** and **Next**.

#### Flow Status Information

| Flow Execution Status                                  | Description |
|---------------------------------------------------| --- |
| START\_FAILED  | Failed to request flow execution. |
| QUOTA\_EXCEEDED | Flow execution failed due to insufficient resources. |
| STARTING       | Acquiring resources for flow execution. |
| PREPARING      | Flow execution preparation is complete. |
| RUNNING        | The flow is running. |
| ERROR              | An error occurred during flow execution due to communication failure or authentication failure. If <b>ERROR</b> persists continuously, contact **Customer Support > Inquiry**. |
| STOP\_FAILED   | Failed to request flow termination. |
| STOPPED        | The flow has been terminated. |
| DRAINING       | The flow is draining. |
| UNKNOWN            | An error occurred during flow execution due to an unknown cause. If <b>UNKNOWN</b> persists continuously, contact **Customer Support > Inquiry**. |

#### Flow Status Change Notification Email
* You can receive notification emails when the flow changes to a notification target status.
* Notification target flow status
    * RUNNING
    * ERROR
    * STOPPED
* Default notification recipients
    * Members with the **DataFlow ADMIN** role in the project where the DataFlow service in use is enabled


### Create Flow

Creates metadata to define a flow.

* Metadata is created by adding a name and description to identify the flow.
* Flow names can be duplicated with other flows.
* Select the execution mode according to the purpose of the flow.
* You can easily load the desired flow functionality by specifying a flow template.
* You can set the instance type for running the flow.

### Modify Flow

Modifies the metadata of a flow.

* The existing flow name and description are modified and reflected in the flow metadata.
* Flow templates cannot be specified.
* Flow modification is possible even while the flow is running.
* You can change the instance type for running the flow.
    * However, the changed instance type is applied from the next flow execution onward.

### Copy Flow

Creates new metadata based on an existing flow definition.

* Creates new metadata with `_copy` added to the existing flow name.
* Copies the flow logic of the existing flow as is.
* Running flows can also be copied.
* Running flows are copied in a stopped state.
* If the current save state of the flow is temporary save, the last saved version of the existing flow is not copied.
* Even if you copy a flow with a registered scheduler, the copied flow does not have a scheduler registered.
* The copied flow is completely separate from the existing flow.

### Delete Flow

Deletes the flow metadata.

* Completely deletes the flow metadata.
* Deleted flows cannot be recovered.
* Running flows cannot be deleted.

### More - Start Flow
Starts a stopped flow.

* Each flow can only be executed one at a time.
* A temporarily saved flow starts with the last saved version.
* Flows that have only been temporarily saved without being saved once cannot be started.
* A flow must be saved at least once before it can be started.
* Even if a flow is being executed by a scheduler, it cannot be started by a user in the same way.

### More - Stop Flow
* You can stop flows that are in preparation, running, or draining states.
* Terminates without processing remaining events.

### More - Drain and Stop Flow
* You can drain and stop running flows.
* Draining means processing the remaining events of the flow.
* If the timeout is exceeded, the flow is terminated even if draining is not complete.
* If draining completes before the timeout is exceeded, the flow is terminated immediately.
* Flows that are draining can be terminated immediately through flow termination.