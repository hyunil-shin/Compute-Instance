## Security > Secure Key Manager > Release Notes

### 2026. 04. 14.
#### Feature Improvements/Changes
  * Deleted `APPROVAL MEMBER` role
    * Simplified role system by migrating Secure Key Manager APPROVAL MEMBER role to Secure Key Manager ADMIN role
  * Granular permissions
    * Added `SecureKeyManager:API.ADMIN` and `SecureKeyManager:API.VIEWER` permissions to provide granular management of console and API permissions

### 2026. 03. 10.
#### New Features
  * Added API v1.3
    * Added token authentication method via `X-NHN-AUTHORIZATION` header. For more details, see [API v1.3 Guide](/Security/Secure%20Key%20Manager/en/api-guide-v1.3/).
  * Added confidential data modification API (v1.2, v1.3)
    * Added the ability to modify confidential data stored in Secure Key Manager using the API. For more details, see [API v1.2 Guide](/Security/Secure%20Key%20Manager/en/api-guide-v1.2/) or [API v1.3 Guide](/Security/Secure%20Key%20Manager/en/api-guide-v1.3/).

### 2026. 02. 10.
#### New Features
  * Added key store list detailed query API
    * Added the ability to query detailed information lists of key stores using the API. For more details, see [API v1.0 Guide](/Security/Secure%20Key%20Manager/en/api-guide-v1.0/) or [API v1.2 Guide](/Security/Secure%20Key%20Manager/en/api-guide-v1.2/).
  * Added key list detailed query API
    * Added the ability to query detailed information lists of keys using the API. For more details, see [API v1.0 Guide](/Security/Secure%20Key%20Manager/en/api-guide-v1.0/) or [API v1.2 Guide](/Security/Secure%20Key%20Manager/en/api-guide-v1.2/).

### 2025. 06. 24.
#### Feature Improvements/Changes
  * Added new error message
    * Added error message when making API requests with invalid URIs. For more details, see [Troubleshooting Guide](/Security/Secure%20Key%20Manager/en/troubleshooting-guide/#api-url-not-found).

### 2025. 04. 28.
#### Feature Improvements/Changes
  * Data retention period changed from 3 years to 1 year
    * [Related Notice](https://www.nhncloud.com/kr/support/notice/detail/6493)

### 2025. 03. 25.
#### New Features
  * Added key store list/detailed query API
    * Added the ability to query key store ID lists using the API and retrieve detailed key store information using key store IDs
  * Added key list/detailed query API
    * Added the ability to query key ID lists using the API and retrieve detailed key information using key IDs
  * Added authentication information list/detailed query API
    * Added the ability to query authentication information value lists using the API and retrieve detailed authentication information using authentication information values

### 2024. 09. 25.
#### Feature Improvements/Changes
  * Removed Number column from the approval list table

### 2024. 08. 27.
#### New Features
  * Added the ability to receive Secure Key Manager event notifications through the Resource Watcher service
#### Feature Improvements/Changes
  * Removed approval process self-approval feature
    * Changed to prevent users from approving their own requests

### 2024. 04. 23.
#### Bug Fixes
  * Fixed error where after deleting data (keys, authentication information) using API and then querying the deleted data, other non-deleted data could not be queried until refresh after the error modal appeared

### 2024. 03. 26.
#### New Features
  * Added authentication information registration/deletion API
    * Added the ability to register or delete authentication information for using keys via API
    * **User Access Key ID** and **Secret Access Key** are required to add or delete authentication information via API. For more details, see [Console User Guide](/Security/Secure%20Key%20Manager/en/getting-started/#api).

### 2024. 02. 27.
#### New Features
  * Added notification email recipient setting feature
    * Added the ability to set recipient email addresses in Organization/Project Dashboard > Notification Management.
#### Feature Improvements/Changes
  * Key store ID exposure
    * Added area to check key store ID in key store details
    * Added the ability to copy key store ID through the more button on the right side of the key store ID

### 2023. 11. 28.
#### New Features
  * Added key addition/deletion API
    * Added the ability to add or delete keys using the API
    * **User Access Key ID** and **Secret Access Key** are required to add or delete keys via API. For more details, see [Console User Guide](/Security/Secure%20Key%20Manager/en/getting-started/#api).

### 2023. 09. 26.
#### Feature Improvements/Changes
  * Added IPv4 bandwidth authentication feature
    * Added bandwidth authentication feature using CIDR notation for IPv4 authentication

### 2023. 07. 25.
#### Bug Fixes
  * Fixed approval process certificate revocation feature error
    * Fixed error where certificates in **In Use** status would display as **Scheduled for Deletion Cancellation** instead of the original **In Use** status when deletion requests were canceled after requesting deletion in the approval process

### 2023. 05. 30.
#### Bug Fixes
  * Fixed approval process notification (email) feature error
    * Fixed error where some administrators with approval authority did not receive notifications (emails)
  * Fixed approval process IP/MAC bulk registration feature error
    * Fixed error where approval process IP/MAC bulk registration was not immediately reflected on screen

### 2023. 04. 25.
#### New Features
  * Added approval process notification (email) feature
    * Added feature to send emails to administrators with approval authority when approval requests are registered

### 2023. 02. 28.
#### Bug Fixes
  * Fixed template file download error
    * Fixed error where bulk registration template files were downloaded as incorrect template formats

### 2023. 01. 31.
#### Bug Fixes
  * Approval feature improvements and error fixes
    * Modified to display data area as blank when accessing confidential data modification screen while using approval feature
    * Modified to display updated data after modifying confidential data while using approval feature
  * Fixed issue where MAC address tooltip in key store management tab displayed IPv4 instead of MAC address

### 2022. 12. 27.
#### Feature Improvements/Changes
  * API domain change
    * Changed SecureKeyManager API domain from `api-keymanager.cloud.toast.com` to `api-keymanager.nhncloudservice.com`

### 2022. 11. 29.
#### Bug Fixes
  * Approval feature improvements and error fixes
    * Improved error message text that occurs while using approval feature to be more understandable
    * Fixed error where adding key store for the first time while using approval feature proceeded without approval process
  * Fixed certificate authentication error
    * Fixed issue where certificate authentication occasionally failed

### 2022. 10. 25.
#### Bug Fixes
  * Fixed integrated appkey error
    * Fixed issue where API calls using project integrated appkey did not work properly
  * Fixed approval feature error
    * Fixed issue where key version-specific deletion feature did not work properly when using approval feature

### 2022. 09. 27.
#### New Features
  * Added asymmetric key query feature
    * Added asymmetric key query feature by key version

### 2022. 07. 26.
#### New Features
  * Added approval feature
    * Introduced approval process for major changes such as key creation, modification, deletion, and access control changes to key stores
  * Added new symmetric key query version
    * Added symmetric key query feature by key version

### 2021. 11. 23.
#### New Features
  * Added symmetric key query feature

### 2021. 10. 26.
#### New Features
  * Added key import feature
    * Added symmetric key import feature
#### Feature Improvements/Changes
  * Modified confidential data query feature
    * Provides masked fields when querying confidential data from web console
#### Bug Fixes
  * Fixed issue where users with overdue payments could still use the service normally

### 2021. 09. 28.
#### Bug Fixes
  * Fixed issue where permissions granted through permission groups were not properly recognized
  * Fixed issue where usage history reset button did not work properly

### 2020. 03. 24.
#### New Features
  * Records user actions performed in Secure Key Manager console to Cloud Trail
  * Added bulk registration feature for authentication data (IPv4 address/MAC address) using CSV files
  * Added download feature for authentication data (IPv4 address/MAC address) using CSV files

### 2019. 12. 24.
#### New Features
  * Added statistics screen
    * Added screen to query API usage statistics by project
#### Feature Improvements/Changes
  * Key store screen improvements
    * Changed display method of key store list
    * Changed sub-menus of key stores
    * Added quick menu to key stores
  * Usage history screen improvements
    * Changed to query API usage history by project

### 2019. 07. 23.
#### Feature Improvements/Changes
  * UI improvements
    * Fixed phenomenon of overlapping text and buttons
    * Fixed text line break phenomenon when displaying screen in Japanese

### 2019. 05. 28.
#### New Service Launch
  * A service that centrally and securely manages data that could be exposed to security risks if stored on application servers, such as confidential data (database connection information, app keys, passwords, etc.), symmetric keys, and asymmetric keys, and controls access so that only authenticated clients can access it.