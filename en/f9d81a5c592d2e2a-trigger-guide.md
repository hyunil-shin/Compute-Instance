## Compute > Cloud Functions > Trigger Guide

This document describes the trigger types provided by Cloud Functions and how to configure them.

## Trigger Overview

A trigger is an event source that executes a function. Cloud Functions provides various types of triggers, allowing you to invoke functions in multiple ways.

### Supported Trigger Types

| Trigger Type   | Description                          | Built-in |
|---|------|---|
| HTTP        | Execute function through HTTP request      | O     |
| Timer       | Execute function at specified time or interval | X     |
| API Gateway | Execute function through API Gateway  | X     |

## HTTP Trigger

The HTTP trigger is provided by default when creating a function and allows you to execute a function through HTTP requests.

### Features

- Automatically created when a function is created.
- Cannot be deleted; only enabled/disabled.
- Supports GET and POST methods.

### HTTP Trigger URL Format

```
https://{userdomain}/{function-name}
```

### Usage Examples

#### GET Request

```bash
curl -X GET "https://{userdomain}/{function-name}?param1=value1&param2=value2"
```

#### POST Request

```bash
curl -X POST "https://{userdomain}/{function-name}" \
  -H "Content-Type: application/json" \
  -d '{"key": "value"}'
```

### Enable/Disable HTTP Trigger

1. Select a function in the Cloud Functions console.
2. Go to the **Trigger** tab.
3. Click the enable/disable toggle for the HTTP trigger.

> **[Note]**
> <br>If you send a request to a disabled HTTP trigger, the function will not execute.

## Timer Trigger

A Timer trigger automatically executes a function at a specified time or interval. You can set the execution interval using a Cron expression.

### Create Timer Trigger

![trigger-guide-05](https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_5524ad40cfc3478dbb73395d1fa9e2b9/cloud-user-guide-image/cloud-docs/hyunil-shin/Compute-Instance/en/trigger-guide-01.png)

1. Select a function in the Cloud Functions console.
2. Go to the **Trigger** tab.
3. Click **Create Trigger**.
4. Select **Timer** as the trigger type.
5. Enter a Cron expression in **Value**.
6. Click **Create**.

### Cron Expression Format

A Cron expression follows the format below:

```
* * * * * *
│ │ │ │ │ │
│ │ │ │ │ └─ Day of week (0-6 or SUN-SAT, 0: Sunday)
│ │ │ │ └─── Month (1-12 or JAN-DEC)
│ │ │ └───── Day of month (1-31)
│ │ └─────── Hour (0-23)
│ └───────── Minute (0-59)
└─────────── Second (0-59)
```

#### Cron Expression Fields

| Field              | Required  | Allowed Values            | Allowed Special Characters  |
|---|---|---|---|
| Seconds      | Yes | 0-59            | * / , -   |
| Minutes      | Yes | 0-59            | * / , -   |
| Hours        | Yes | 0-23            | * / , -   |
| Day of month | Yes | 1-31            | * / , - ? |
| Month        | Yes | 1-12 or JAN-DEC | * / , -   |
| Day of week | Yes | 0-6 or SUN-SAT  | * / , - ? |

#### Special Character Descriptions

`*`

Matches all values in the field. For example, using `*` in the 5th field (Month) means all months.

`/`

Used to represent increments within a range. For example, using `3-59/15` in the 2nd field (Minute) means starting from minute 3 and executing every 15 minutes (3, 18, 33, 48). The form `*/...` is equivalent to `first-last/...` and represents an increment of the largest range for the field. The form `N/...` means `N-MAX/...`, starting from N to the end of that range with the specified increment. If the range is exceeded, it does not wrap around to the beginning.

`,`

Used to separate items in a list. For example, using `MON,WED,FRI` in the 6th field (Day of week) means Monday, Wednesday, and Friday.

`-`

Used to define a range. For example, using `9-17` in the 3rd field (Hour) means all hours from 9 AM to 5 PM (inclusive).

`?`

Can be used instead of `*` to leave the Day of month or Day of week field empty.

### Cron Expression Examples

| Cron Expression               | Description                              |
|---|---|
| `0 * * * * *`          | Execute every minute (at second 0)                  |
| `0 0 * * * *`          | Execute at the top of every hour                     |
| `0 0 0 * * *`          | Execute every day at midnight                       |
| `0 0 9 * * MON`        | Execute every Monday at 9 AM                |
| `0 0 0 1 * *`          | Execute at midnight on the 1st of every month                    |
| `0 */5 * * * *`        | Execute every 5 minutes                         |
| `0 0 9-18 * * MON-FRI` | Execute every hour from 9 AM to 6 PM on weekdays (Monday-Friday) |
| `30 0 12 * * *`        | Execute at 12:00:30 PM every day            |
| `0 0 0 1 JAN *`        | Execute at midnight on January 1st every year                 |

### Modify Timer Trigger

![trigger-guide-02](https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_5524ad40cfc3478dbb73395d1fa9e2b9/cloud-user-guide-image/cloud-docs/hyunil-shin/Compute-Instance/en/trigger-guide-02.png)

1. Select a function in the Cloud Functions console.
2. Go to the **Trigger** tab.
3. Select the Timer trigger you want to modify.
4. Click **Modify Trigger**.
5. Modify the Cron expression in **Value**.
6. Click **Modify**.

> **[Note]**
> <br>The Month and Day of week field values are case-insensitive. "SUN", "Sun", and "sun" are all recognized identically.

## API Gateway Trigger

The API Gateway trigger allows you to execute a function by using the API Gateway service in the same project. With API Gateway, you can achieve more granular API management and control.

### Prerequisites

- The API Gateway service must be enabled in the same project.
  - If not enabled, you can enable it when creating a trigger.

### Create API Gateway Trigger

![trigger-guide-04](https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_5524ad40cfc3478dbb73395d1fa9e2b9/cloud-user-guide-image/cloud-docs/hyunil-shin/Compute-Instance/en/trigger-guide-04.png)

1. Select a function in the Cloud Functions console.
2. Go to the **Trigger** tab.
3. Click **Create Trigger**.
4. Select API Gateway as the trigger type.
5. Enter the path you want to use.
   * Duplicate paths cannot be used.
6. Click **Create**.

### API Gateway Trigger URL Format

```
https://{stageurl}/{path}
```

### Usage Examples

#### GET Request

```bash
curl -X GET "https://{stageurl}/{path}?param1=value1&param2=value2"
```

#### POST Request

```bash
curl -X POST "https://{stageurl}/{path}" \
  -H "Content-Type: application/json" \
  -d '{"key": "value"}'
```

### API Gateway Trigger Features

- You can utilize various features of API Gateway.
  - Authentication and authorization
  - Request/response transformation
  - Usage plans and API key management
  - Request rate limiting
- You can manage API settings from the API Gateway console.
- Function integration is only possible with a single automatically created service.
- Supports GET and POST methods, just like the HTTP trigger.

### Modify API Gateway Trigger

![trigger-guide-05](https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_5524ad40cfc3478dbb73395d1fa9e2b9/cloud-user-guide-image/cloud-docs/hyunil-shin/Compute-Instance/en/trigger-guide-05.png)

1. Select a function in the Cloud Functions console.
2. Go to the **Trigger** tab.
3. Select the API Gateway trigger you want to modify.
4. Click **Modify Trigger**.
5. Change the path.
6. Click **Modify**.

> **[Note]**
> <br>Modifying an API Gateway trigger is performed by deleting the existing trigger within the API Gateway service and creating a new one.
> <br>As a result, all plugins applied to that resource will be removed.
> <br>If you want to change the resource path with plugins applied, it is recommended to add a new trigger instead of modifying.

### Using with API Gateway

Once you create an API Gateway trigger, you can make additional settings in the API Gateway console.

For more details, refer to the [API Gateway Guide](https://docs.nhncloud.com/en/Application%20Service/API%20Gateway/ko/overview/).

## Delete Trigger

### How to Delete a Trigger

![trigger-guide-03](https://kr1-api-object-storage.nhncloudservice.com/v1/AUTH_5524ad40cfc3478dbb73395d1fa9e2b9/cloud-user-guide-image/cloud-docs/hyunil-shin/Compute-Instance/en/trigger-guide-03.png)

1. Select a function in the Cloud Functions console.
2. Go to the **Trigger** tab.
3. Select the trigger you want to delete. (Multiple selections are possible)
4. Click **Delete Trigger**.
5. In the **Delete Trigger** modal window, click **Delete**.

### Precautions

- The HTTP trigger cannot be deleted. The HTTP trigger is provided as a default trigger and can only be enabled/disabled.
- If you delete a trigger, you cannot execute the function through that event.
- Deleted triggers cannot be recovered.

## Trigger Limitations

### API Gateway Trigger Limitations

- Only API Gateway in the same project can be connected.
- One API Gateway Resource can be connected to only one function.
- Multiple API Gateway triggers can be registered for a single function.
- If the API Gateway service is disabled or the connected resource is deleted or changed, the trigger will not work.
  - In this case, the trigger cannot be modified, so you must delete it and register it again.