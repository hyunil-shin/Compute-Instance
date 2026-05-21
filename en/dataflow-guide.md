## Data & Analytics > DataFlow > Console User Guide

DataFlow can be used in the following order.

* Service activation
    1. Create a project.
    2. Select the desired project.
    3. Activate the DataFlow service.
* Flow execution
    1. Create a flow.
    2. Add the necessary nodes and enter configuration values to define how each node operates.
    3. Complete the flow by connecting nodes to determine the order of node operations.
    4. Execute the flow.
    5. Check the log information to verify that the flow has executed normally.

## Management

This is a page to view and manage flow metadata information.
Click **Data & Analytics > DataFlow > Management**.

![management_main.png](https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_5524ad40cfc3478dbb73395d1fa9e2b9/cloud-user-guide-image/cloud-docs/hyunil-shin/Compute-Instance/en/management_main_2025_06.png)

### Search

Search for flows based on given criteria.

* When searching by flow name, flows that include the search term in their name are returned.

### Filter

Search for flows based on given conditions.

* Provides filtering options based on flow status values.

### Flow List

Displays search results as a table.

* Displays simple flow metadata and the current flow execution status.
* Sorted by the most recent modification date.
* You can select a flow to use management functions such as modifying the flow, viewing flow details, and starting the flow.
* You can view only flows with a specific status using the filter condition feature.
* Once a flow is queried, you must click **Refresh** to update the search results.
* Up to 12 flows are displayed per page, and you can navigate pages by clicking **Previous** and **Next**.

#### Flow Status Information

| Flow Execution Status                            | Description |
|---------------------------------------------------| --- |
| START_FAILED  | Failed to request flow execution. |
| QUOTA_EXCEEDED | Flow execution failed due to insufficient resources. |
| STARTING       | Securing resources for flow execution. |
| PREPARING      | Flow execution preparation is complete. |
| RUNNING        | The flow is running. |
| ERROR              | An error occurred during flow execution due to communication failure or authentication failure, etc. If <b>ERROR</b> continues to occur, contact **Customer Support > Contact Us**. |
| STOP_FAILED   | Failed to request flow termination. |
| STOPPED        | The flow has been terminated. |
| DRAINING       | The flow is draining. |
| UNKNOWN            | An error occurred during flow execution due to an unknown cause. If <b>UNKNOWN</b> continues to occur, contact **Customer Support > Contact Us**. |

#### Flow Status Change Notification Email
* Receive notification emails when the flow status changes to the notification target status.
* Notification target flow status
    * RUNNING
    * ERROR
    * STOPPED
* Default recipients
    * Members with the **DataFlow ADMIN** role in the project where the DataFlow service is activated

### Create Flow

Create metadata to define a flow.

* Create flow metadata by adding a name and description to identify the flow.
* Flow names can be duplicated across different flows.
* Select the execution mode according to the flow purpose.
* You can easily load flows with desired functionality by specifying a flow template.
* You can set the instance type for executing the flow.

### Modify Flow

Modify the metadata of a flow.

* Modify the existing flow name and description and reflect them in the flow metadata.
* Flow templates cannot be specified.
* You can modify the flow even while it is running.
* You can change the instance type for executing the flow.
    * However, the changed instance type is applied from the next flow execution.

### Copy Flow

Create new metadata using an existing flow definition.

* Create new metadata with `_copy` added to the name of the existing flow.
* Copy the flow logic of the existing flow as is.
* You can copy a flow that is running.
* Running flows are copied in a stopped state.
* If the flow's current save state is a temporary save, the last saved version of the existing flow is not copied.
* Even if you copy a flow with a registered scheduler, the copied flow will not have a registered scheduler.
* The copied flow is completely separate from the existing flow.

### Delete Flow

Delete flow metadata.

* Completely delete the flow metadata.
* Deleted flows cannot be recovered.
* Running flows cannot be deleted.

### More - Start Flow
Start a stopped flow.

* Each flow can run only one at a time.
* A temporarily saved flow starts with the last saved version.
* A flow that has only been temporarily saved without ever being saved cannot be started.
* A flow must be saved at least once before it can be started.
* Even if a flow is running due to a scheduler, the flow cannot be started in the same way as a flow started by a user.

### More - Stop Flow
* You can stop a flow that is in preparation, running, or draining.
* Remaining events are not processed and the flow is terminated.

### More - Stop Flow After Draining
* You can stop a running flow after draining it.
* Draining means processing the remaining events in the flow.
* If the timeout is exceeded, the flow is terminated even if draining is not complete.
* If draining completes while timeout remains, the flow is terminated immediately.
* A flow that is draining can be terminated immediately through flow termination.