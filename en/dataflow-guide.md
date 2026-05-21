## Data & Analytics > DataFlow > Console Guide

DataFlow can be used in the following sequence:

* Enable Service
    1. Create a project.
    2. Select the desired project.
    3. Enable the DataFlow service.
* Run Flow
    1. Create a flow.
    2. Add the necessary nodes and enter configuration values to define how each node operates.
    3. Complete the flow by determining the execution order of nodes through node connections.
    4. Run the flow.
    5. Check the log information to verify that the flow has executed correctly.

## Management

This is a page to view and manage flow metadata information.
Click **Data & Analytics > DataFlow > Management**.

![management_main.png](https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_5524ad40cfc3478dbb73395d1fa9e2b9/cloud-user-guide-image/cloud-docs/hyunil-shin/Compute-Instance/en/management_main_2025_06.png)

### Search

Search for flows based on given criteria.

* When searching by flow name, flows that include the search term in their name are displayed.

### Filter

Search for flows based on given conditions.

* Provides filtering options based on flow status values.

### Flow List

Displays search results as a table of flows.

* Displays simple flow metadata and the current flow execution status.
* Sorted by the most recent modification date.
* You can select a flow to use management functions such as modifying the flow, viewing flow details, and starting the flow.
* You can view only flows in a specific status using the filter condition feature.
* Once a flow is retrieved, you must press **Refresh** to update the search results.
* Displays up to 12 flows per page, and you can navigate pages by clicking **Previous** and **Next**.

#### Flow Status Information

| Flow Execution Status                                         | Description |
|---------------------------------------------------| --- |
| START\_FAILED  | Failed to request flow execution. |
| QUOTA\_EXCEEDED | Flow execution failed due to insufficient resources. |
| STARTING       | Acquiring resources for flow execution. |
| PREPARING      | Flow execution preparation is complete. |
| RUNNING        | Flow is executing. |
| ERROR              | An error occurred during flow execution due to communication failure or authentication failure, etc. If <b>ERROR</b> continues to occur, please contact us via **Customer Support > Contact Us**. |
| STOP\_FAILED   | Failed to request flow termination. |
| STOPPED        | Flow has terminated. |
| DRAINING       | Flow is draining. |
| UNKNOWN            | An error occurred during flow execution due to an unknown cause. If <b>UNKNOWN</b> continues to occur, please contact us via **Customer Support > Contact Us**. |

#### Flow Status Change Notification Email
* You can receive notification emails when the flow status changes to a notification target status.
* Notification target flow statuses
    * RUNNING
    * ERROR
    * STOPPED
* Default notification recipients
    * Members with the **DataFlow ADMIN** role in the project where the DataFlow service in use is enabled

### Create Flow

Create metadata to define a flow.

* Create flow metadata by adding a name and description to identify the flow.
* Flow names can be duplicated with other flows.
* Select the execution mode according to the flow purpose.
* You can specify a flow template to easily load flows with the desired functionality.
* You can set the instance type to run the flow.

### Modify Flow

Modify the metadata of a flow.

* Modify the existing flow name and description and apply them to the flow metadata.
* Flow templates cannot be specified.
* You can modify the flow even while it is executing.
* You can change the instance type to run the flow.
    * However, the changed instance type will be applied from the next flow execution.

### Copy Flow

Create new metadata using the existing flow definition.

* Create new metadata with `_copy` added to the existing flow name.
* Copy the flow logic of the existing flow as is.
* You can copy even executing flows.
* Executing flows are copied in a stopped state.
* If the current save state of the flow is a draft save, the last saved version of the existing flow is not copied.
* Even if you copy a flow with a registered scheduler, the copied flow will not have a scheduler registered.
* The copied flow is completely separate from the existing flow.

### Delete Flow

Delete flow metadata.

* Completely delete the flow metadata.
* Deleted flows cannot be recovered.
* Executing flows cannot be deleted.

### More - Start Flow
Start a stopped flow.

* Each flow can run only one at a time.
* Draft-saved flows start with the last saved version.
* Flows that have only been draft-saved without ever being saved cannot be started.
* Flows must be saved at least once before they can be started.
* Even if a flow is being executed by a scheduler, it cannot be started the same way as a flow started by a user.

### More - Stop Flow
* You can stop flows that are preparing to execute, executing, or draining.
* Terminates without processing remaining events.

### More - Stop Flow After Draining
* You can stop an executing flow after draining.
* Draining means processing the remaining events in the flow.
* If the timeout period is exceeded, the flow terminates even if draining is not complete.
* If draining completes while timeout time remains, the flow terminates immediately.
* You can terminate a draining flow immediately through flow termination.