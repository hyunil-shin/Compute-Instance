# Console Guide

**Data & Analytics > EasyQueue > Console Guide**

## Managing Topics

An EasyQueue topic is a unit for grouping related messages. It is used to asynchronously publish and subscribe to data between applications.

### Retrieve Topic List

* The list of registered EasyQueue topics is displayed.
* Clicking an item displays the topic basic information tabs at the bottom.
* To check the details of a topic, click the **View Details** button in the action column.

### Create Topic

1. To create a topic, click the **Create Topic** button.
2. Enter the topic information.
    * **Name**: The name of the topic. The Appkey is prepended to the entered name upon creation.
    * **Description**: The description of the topic.
    * **Number of partitions**: Data is distributed and stored across multiple partitions according to the number of partitions configured for the topic.
    * **Maximum message size**: The maximum size of a single message that can be stored in the topic. This size includes not only the message body but also overhead such as headers, keys, timestamps, and compression metadata. Messages exceeding this size are not stored.
    * **Maximum storage size per partition**: The maximum data size that can be stored in each partition. When this size is reached, the oldest messages are deleted first.
      Deletion occurs in segment file (1GB) units, and since segments currently being written to are not deleted, the actual size may exceed the configured value by approximately 1GB or more.
    * **Message retention period**: The maximum period that messages are retained in the topic. Messages are automatically deleted after the configured period has passed.
3. Click the **Confirm** button.

!!! tip "Note"
    * The message cleanup policy, number of replicas, and minimum in-sync replicas of a topic cannot be changed.
    * If either the maximum storage size per partition or the message retention period is exceeded, the oldest messages are automatically deleted.

!!! danger "Caution"
    * A maximum of **10** EasyQueue topics can be created per project.
    * A maximum of **64** EasyQueue partitions can be created per project and a maximum of **16** per topic.

### Modify Topic

1. To modify a topic, click the **Modify** button in the action column.
2. Modify the topic information. The modifiable items are description, number of partitions, maximum message size, maximum storage size per partition, and message retention period.
3. Click the **Confirm** button.

!!! danger "Caution"
    * The number of partitions for a topic cannot be reduced below the current number of partitions.

### Delete Topic

1. Click the **Delete** button in the action column of the list.
2. Enter the deletion phrase in the confirmation window and click the **Delete** button. Deleted data cannot be recovered.


## Viewing Topic Details

This is the page where you can check the details of a topic. You can view information on partitions, messages, consumer groups, and monitoring.

### Partitions
* The list of partitions for the EasyQueue topic is displayed.
* You can view information on partition ID, start offset, last offset, and total number of messages.

### Messages
* The list of messages for the EasyQueue topic is displayed. A maximum of 50 messages are retrieved.
* You can view information on message send time, partition ID, offset, key, value, and headers.
* Click the **View Message** button in the action column to see detailed information on the key, value, and headers.
* You can filter messages by setting the partition ID and message retrieval type.
    * Partition ID: Retrieves messages by specifying a specific partition.
    * Message retrieval type: From beginning, From offset, From new messages
        * From beginning: Retrieves messages in order from the oldest send time.
        * From offset: Retrieves only messages with offsets equal to or greater than the specified offset. An offset must be entered.
        * From new messages: Retrieves new messages that arrive from the time of the search.

#### Message Send Test

1. To test message sending, click the **Message Send Test** button.
2. Enter the message information to send.
    * **Partition ID**: The ID that specifies the particular partition to send the message to. If not specified, a partition is automatically selected.
    * **Header**: Metadata sent along with the message. Additional information about the message can be included in key-value pair format.
    * **Key**: An identifier used to determine the partition where the message will be stored.
    * **Value**: The body data of the message to actually send. It can be entered in various formats such as text, JSON, or binary.
3. Click the **Confirm** button.

!!! tip "Note"
    When testing message sending, you can send an empty message without entering any of the partition ID, header, key, or value.

### Consumer Groups
* The list of consumer groups for the EasyQueue topic is displayed. A maximum of 50 consumer groups are retrieved.
* You can view information on consumer group ID, number of consumers, assigned partitions, total lag, and status.
* Clicking an item displays the consumer list information tabs at the bottom for the consumer group.
    * The list of consumers belonging to the consumer group is displayed.
    * You can view information on consumer ID, partition ID, lag, current offset, and last offset.

!!! danger "Caution"
    * If a consumer group remains in 'No Members' status for more than 7 days, the group information and offsets are automatically deleted.


### Monitoring
* Through EasyQueue topic monitoring, you can check metrics for inbound/outbound byte transfer rates, message count, lag by consumer group, and total data size.

| Metric | Description |
|------|------|
| **Inbound / Outbound byte transfer rate** | **Inbound**: The data throughput that producers send to the topic<br>**Outbound**: The data throughput that consumers read from the topic |
| **Message count** | Indicates the total number of messages stored in the topic. |
| **Consumer group lag** | The number of messages that the consumer group has not yet processed. It represents the difference between the latest message produced and the last message read by the consumer.<br>The consumer group lag monitoring metric displays only the top 10 consumer groups based on the highest consumer lag values at the current point in time. |
| **Data storage size** | The disk storage space currently used by the topic.<br>The legend is displayed per partition of the topic, and both leader partitions and replica partitions are shown. |

!!! tip "Note"
    Monitoring data is retained for 90 days.