## Security > Secure Key Manager > Release Notes

### 2026. 04. 14.
#### Feature Improvements/Changes
  * Removal of `APPROVAL MEMBER` role
    * Simplified role system by migrating Secure Key Manager APPROVAL MEMBER role to Secure Key Manager ADMIN role
  * Detailed permissions
    * Added `SecureKeyManager:API.ADMIN` and `SecureKeyManager:API.VIEWER` permissions to enable detailed management of console and API permissions

### 2026. 03. 10.
#### New Features
  * API v1.3 added
    * Added token authentication method through `X-NHN-AUTHORIZATION` header. For more details, see [API v1.3 Guide](/Security/Secure%20Key%20Manager/en/api-guide-v1.3/).
  * Secret data modification API added (v1.2, v1.3)
    * Added functionality to modify secret data stored in Secure Key Manager using API. For more details, see [API v1.2 Guide](/Security/Secure%20Key%20Manager/en/api-guide-v1.2/) or [API v1.3 Guide](/Security/Secure%20Key%20Manager/en/api-guide-v1.3/).

### 2026. 02. 10.
#### New Features
  * Key store list detailed query API added
    * Added functionality to query detailed information list of key stores using API. For more details, see [API v1.0 Guide](/Security/Secure%20Key%20Manager/en/api-guide-v1.0/) or [API v1.2 Guide](/Security/Secure%20Key%20Manager/en/api-guide-v1.2/).
  * Key list detailed query API added
    * Added functionality to query detailed information list of keys using API. For more details, see [API v1.0 Guide](/Security/Secure%20Key%20Manager/en/api-guide-v1.0/) or [API v1.2 Guide](/Security/Secure%20Key%20Manager/en/api-guide-v1.2/).

### 2025. 06. 24.
#### Feature Improvements/Changes
  * New error message added
    * Added error message when making API request with invalid URI. For more details, see [Troubleshooting Guide](/Security/Secure%20Key%20Manager/en/troubleshooting-guide/#api-url-not-found).

### 2025. 04. 28.
#### Feature Improvements/Changes
  * Data retention period changed from 3 years to 1 year
    * [Related announcement](https://www.nhncloud.com/kr/support/notice/detail/6493)

### 2025. 03. 25.
#### New Features
  * Key store list/detailed query API added
    * Added functionality to query key store ID list and detailed key store information using key store ID through API
  * Key list/detailed query API added
    * Added functionality to query key ID list and detailed key information using key ID through API
  * Authentication information list/detailed query API added
    * Added functionality to query authentication information value list and detailed authentication information using authentication information values through API

### 2024. 09. 25.
#### Feature Improvements/Changes
  * Removed Number column from approval list table

### 2024. 08. 27.
#### New Features
  * Added functionality to receive Secure Key Manager event notifications through Resource Watcher service
#### Feature Improvements/Changes
  * Removed approval process self-approval functionality
    * Changed to prevent self-approval of requests made by the same user

### 2024. 04. 23.
#### Bug Fixes
  * Fixed error where after deleting data (keys, authentication information) using API and querying deleted data, an error modal would appear and no other data could be queried until page refresh

### 2024. 03. 26.
#### New Features
  * Authentication information register/delete API added
    * Added functionality to register or delete authentication information for using keys through API
    * **User Access Key ID** and **Secret Access Key** are required to add or delete authentication information using API. For more details, see [Console User Guide](/Security/Secure%20Key%20Manager/en/getting-started/#api).

### 2024. 02. 27.
#### New Features
  * Notification email recipient setting functionality added
    * Added functionality to set recipient email addresses in Organization/Project Dashboard > Notification Management.
#### Feature Improvements/Changes
  * Key store ID exposure
    * Exposed area to check key store ID in key store details
    * Added functionality to copy key store ID through the more button to the right of the key store ID

### 2023. 11. 28.
#### New Features
  * Key add/delete API added
    * Added functionality to add or delete keys using API
    * **User Access Key ID** and **Secret Access Key** are required to add or delete keys using API. For more details, see [Console User Guide](/Security/Secure%20Key%20Manager/en/getting-started/#api).

### 2023. 09. 26.
#### Feature Improvements/Changes
  * IPv4 bandwidth authentication functionality added
    * Added bandwidth authentication functionality using CIDR notation for IPv4 authentication

### 2023. 07. 25.
#### Bug Fixes
  * Fixed approval process certificate cancellation functionality error
    * Fixed error where when requesting deletion of a certificate in **In Use** status in the approval process and then canceling the request, it was displayed as **Deletion Cancellation Pending** status instead of the original **In Use** status

### 2023. 05. 30.
#### Bug Fixes
  * Fixed approval process notification (email) functionality error
    * Fixed error where some administrators with approval permissions were not receiving notifications (emails)
  * Fixed approval process IP/MAC bulk registration functionality error
    * Fixed error where bulk registration of IP/MAC in approval process was not immediately reflected on screen

### 2023. 04. 25.
#### New Features
  * Approval process notification (email) functionality added
    * Added functionality to send emails to administrators with approval permissions when approval requests are registered

### 2023. 02. 28.
#### Bug Fixes
  * Fixed template file download error
    * Fixed error where bulk registration template files were downloaded as incorrect template format

### 2023. 01. 31.
#### Bug Fixes
  * Approval functionality improvements and error fixes
    * Modified to display data area as blank when entering secret data modification screen while using approval functionality
    * Modified to display updated data after modifying secret data while using approval functionality
  * Fixed issue where MAC address tooltip in key store management tab displayed IPv4 instead of MAC address

### 2022. 12. 27.
#### Feature Improvements/Changes
  * API domain change
    * Changed SecureKeyManager API domain from `api-keymanager.cloud.toast.com` to `api-keymanager.nhncloudservice.com`

### 2022. 11. 29.
#### Bug Fixes
  * Approval functionality improvements and error fixes
    * Improved error messages that occur while using approval functionality to be more understandable
    * Fixed error where adding key store for the first time while using approval functionality proceeded without approval process
  * Certificate authentication error fix
    * Fixed issue where certificate authentication occasionally failed

### 2022. 10. 25.
#### Bug Fixes
  * Integrated appkey error fix
    * Fixed issue where API calls using project integrated appkey were not working properly
  * Approval functionality error fix
    * Fixed issue where key deletion by version functionality was not working properly when using approval functionality

### 2022. 09. 27.
#### New Features
  * Asymmetric key query functionality added
    * Added asymmetric key query functionality by key version

### 2022. 07. 26.
#### New Features
  * Approval functionality added
    * Introduced approval process for major changes such as key creation, modification, deletion, and access control changes for key stores
  * New symmetric key query version added
    * Added symmetric key query functionality by key version

### 2021. 11. 23.
#### New Features
  * Symmetric key query functionality added

### 2021. 10. 26.
#### New Features
  * Key import functionality added
    * Added symmetric key import functionality
#### Feature Improvements/Changes
  * Secret data query functionality modified
    * Provided masked fields when querying secret data in web console
#### Bug Fixes
  * Fixed issue where users with unpaid bills could still use the service normally

### 2021. 09. 28.
#### Bug Fixes
  * Resolved issue where permissions granted through permission groups were not properly recognized
  * Fixed issue where usage history reset button was not working properly

### 2020. 03. 24.
#### New Features
  * Record user actions performed in Secure Key Manager console to Cloud Trail
  * Added bulk registration functionality for authentication data (IPv4 address/MAC address) using CSV files
  * Added download functionality for authentication data (IPv4 address/MAC address) using CSV files

### 2019. 12. 24.
#### New Features
  * Statistics screen added
    * Added screen to query API usage statistics by project
#### Feature Improvements/Changes
  * Key store screen improvements
    * Changed display method of key store list
    * Changed sub-menu of key store
    * Added quick menu to key store
  * Usage history screen improvements
    * Changed to enable querying API usage history by project

### 2019. 07. 23.
#### Feature Improvements/Changes
  * UI improvements
    * Fixed issue where text and buttons were displayed overlapping
    * Fixed text line break issue when displaying screen in Japanese

### 2019. 05. 28.
#### New Service Launch
  * A service that centrally and securely manages data that could be exposed to security risks if stored on application servers, such as confidential data (database connection information, app keys, passwords, etc.), symmetric keys, and asymmetric keys, and controls access so that only authenticated clients can access them.