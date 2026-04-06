## Data & Analytics > DataFlow > Console User Guide

DataFlow can be used in the following order:

* Enable Service
    1. Create a project.
    2. Select the desired project.
    3. Enable the DataFlow service.
* Execute Flow
    1. Create a flow.
    2. Add the nodes you need, and enter settings to define how each node behaves.
    3. Node connections determine the order of nodes' actions to complete the flow.
    4. Execute the file.
    5. Verify that the flow ran successfully by checking the log information.

## Management

Page that queries and manages the flow metadata information.
Click **Data & Analytics > DataFlow > Management**.

![management_main.png](http://static.toastoven.net/prod_dataflow/ko/console_user_guide/management_main_2025_06.png)

### Search

Search for flows with given criteria.

* Searches for flows that contain search items in the name.

### Filter

Searches flows with given conditions.

* Provides filtering options based on the flow status values.

### Flow List

Display query results of flows in a table form.

* Displays simple flow metadata and current flow execution status.
* Sort based on last modified date.
* You can select a flow to use management features such as changing flows, viewing flow details, and starting flow.
* The filter condition feature allows to query specific flows in certain states.
* Once queried flows need to be refreshed to update Query results.
* You can view 12 flows per page and move pages with the previous, next buttons.

#### Flow Status Information

| Flow Running Status                                         | Description |
|---------------------------------------------------| --- |
| START_FAILED  | Failed to request flow running. |
| QUOTA_EXCEEDED | Failed to run the flow due to insufficient resources. |
| STARTING       | Freeing up resources to run the flow. |
| PREPARING      | Ready to run the flow. |
| RUNNING        | Flow is running. |
| ERROR              | An error occurred during flow running due to communication failure or authentication failure. If <b>ERROR</b> continues to occur, contact the Customer Center. |
| STOP_FAILED   | Failed to request flow stop. |
| STOPPED        | Flow is stopped. |
| DRAINING       | Flow is draining. |
| UNKNOWN            | An error occurred for unknown reasons during the running of the flow. If UNKNOWN continues to occur, contact the Customer Center. |

#### Flow Status Change Notifications
* You can be notified via email when the flow status is changed to a status set for notifications
* Flow status for notifications
    * RUNNING
    * ERROR
    * STOPPED
* Default recipients
    * A member with the **DataFlow ADMIN** role in the project where the **DataFlow** service you are using is enabled.


### Create Flow

Create metadata to define flows.

* Create flow metadata by adding name and description to identify a flow.
* Flow names can overlap with other flows.
* Select an engine type. The default ls V1, and refer to **Engine Type** section for features by engine.
* Select the execution mode according to the flow purpose.
* You can specify Flow Template to easily load flows of features users wants.
* You can set an instance type to run flows.

#### Engine Type

* Select either V1 or V2 from the **Engine Type** option on the Create Flow screen.
    * V1: the existing engine supports a variety of nodes.
    * V2: the latest architecture-based engine provides faster performance than V1.
* The engine cannot be changed after creating the flow.


!!! tip "Notice"
    The provided node and monitoring information vary by engine type.


### Change Flow

Modify metadata of flows.

* Modify the existing flow name and description to reflect it in flow metadata.
* Engine type cannot be changed.
* Flow templates cannot be specified.
* Changing flows are possible even when the flow is running.
* You cannot change the instance type to run flows.
    * However, the changed instance type applies when running the next flow.

### Copy Flow

Create new metadata with existing flow definitions.

* Create new metadata with the phrase `_copy` added to the name of existing flow.
* Copy the flow logic of existing flow exactly as it is.
* You can also copy flows in running.
* Even though you copied a running flow, the flow is copied in a stopped status.
* If the current storage state of flows is temporary, it does not copy the last saved version of existing flows.
* If Scheduler copies the registered flow, the copied flow does not register the Scheduler.
* Copied flow is completely separate from an existing flow.

### Delete Flow

Delete flow metadata

* Completely delete flow metadata
* Deleted flow cannot be recovered again.
* Running flow cannot be deleted.

### More - Start a flow
Start a flow that is stopped.

* Each flow can run only one at a time.
* Temporarily saved flow starts with the version that was last saved.
* You cannot start a flow that has never been saved, only drafted.
* You cannot start a flow if it has never been saved even once.
* A flow cannot be started the same as the flow initiated by the user, even if the flow is already being run by Scheduler.

### More - End a flow
* You can end flows that are preparing to run, running, or draining.
* End flows without processing any remaining events.

### More - End after flow draining
* You can end a running flow after draining it.
* Draining means processing the remaining events in the flow.
* If the timeout time is exceeded, the draining will end without finishing.
* If the draining ends with timeouts remaining, exit immediately.
* A flow that is draining can be terminated directly via End Flow.
