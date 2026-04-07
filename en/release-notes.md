## Security > Secure Key Manager > Release Notes

### 2026. 04. 14.
#### Feature Improvements/Changes
  * Removed `APPROVAL MEMBER` role
    * Simplified the role system by migrating the Secure Key Manager APPROVAL MEMBER role to the Secure Key Manager ADMIN role
  * Permission granularity
    * Added `SecureKeyManager:API.ADMIN` and `SecureKeyManager:API.VIEWER` permissions to enable granular management of Console and API permissions

### 2026. 03. 10.
#### New Features
  * Added API v1.3
    * Added token authentication method via the `X-NHN-AUTHORIZATION` header. For more details, see [API v1.3 Guide](/Security/Secure%20Key%20Manager/en/api-guide-v1.3/).
  * Added confidential data modification API (v1.2, v1.3)
    * Added the ability to modify confidential data stored in Secure Key Manager via API. For more details, see [API v1.2 Guide](/Security/Secure%20Key%20Manager/en/api-guide-v1.2/) or [API v1.3 Guide](/Security/Secure%20Key%20Manager/en/api-guide-v1.3/).

### 2026. 02. 10.
#### New Features
  * Added keystore list detailed query API
    * Added the ability to retrieve a detailed list of keystores via API. For more details, see [API v1.0 Guide](/Security/Secure%20Key%20Manager/en/api-guide-v1.0/) or [API v1.2 Guide](/Security/Secure%20Key%20Manager/en/api-guide-v1.2/).
  * Added key list detailed query API
    * Added the ability to retrieve a detailed list of keys via API. For more details, see [API v1.0 Guide](/Security/Secure%20Key%20Manager/en/api-guide-v1.0/) or [API v1.2 Guide](/Security/Secure%20Key%20Manager/en/api-guide-v1.2/).

### 2025. 06. 24.
#### Feature Improvements/Changes
  * Added new error message
    * Added an error message when an API request is made with an invalid URI. For more details, see [Troubleshooting Guide](/Security/Secure%20Key%20Manager/en/troubleshooting-guide/#api-url-not-found).

### 2025. 04. 28.
#### Feature Improvements/Changes
  * Data retention period changed from 3 years to 1 year
    * [Related notice](https://www.nhncloud.com/kr/support/notice/detail/6493)

### 2025. 03. 25.
#### New Features
  * Added keystore list/detail query API
    * Added the ability to retrieve a list of keystore IDs and query keystore details by keystore ID via API
  * Added key list/detail query API
    * Added the ability to retrieve a list of key IDs and query key details by key ID via API
  * Added authentication information list/detail query API
    * Added the ability to retrieve a list of authentication information values and query authentication information details by value via API

### 2024. 09. 25.
#### Feature Improvements/Changes
  * Removed the Number column from the approval list table

### 2024. 08. 27.
#### New Features
  * Added the ability to receive Secure Key Manager event notifications through the Resource Watcher service
#### Feature Improvements/Changes
  * Removed self-approval feature from the approval process
    * Changed so that users cannot approve their own requests

### 2024. 04. 23.
#### Bug Fixes
  * Fixed an issue where, after deleting data (keys, authentication information) via API and querying the deleted data, an error modal was displayed and non-deleted data also became unqueryable until the page was refreshed

### 2024. 03. 26.
#### New Features
  * Added authentication information register/delete API
    * Added the ability to register or delete authentication information for using keys via API
    * **User Access Key ID** and **Secret Access Key** are required to add or delete authentication information via API. For more details, see [Console Guide](/Security/Secure%20Key%20Manager/en/getting-started/#api).

### 2024. 02. 27.
#### New Features
  * Added notification email recipient settings
    * Added the ability to set recipient email addresses in Organization/Project Dashboard > Notification Management.
#### Feature Improvements/Changes
  * Exposed keystore ID
    * Displayed the keystore ID in the keystore detail page
    * Added the ability to copy the keystore ID via the more options button to the right of the keystore ID

### 2023. 11. 28.
#### New Features
  * Added key add/delete API
    * Added the ability to add or delete keys via API
    * **User Access Key ID** and **Secret Access Key** are required to add or delete keys via API. For more details, see [Console Guide](/Security/Secure%20Key%20Manager/en/getting-started/#api).

### 2023. 09. 26.
#### Feature Improvements/Changes
  * Added IPv4 bandwidth authentication
    * Added bandwidth authentication using CIDR notation for IPv4 authentication

### 2023. 07. 25.
#### Bug Fixes
  * Fixed approval process certificate cancellation error
    * Fixed an issue where canceling a deletion request for a certificate in **In Use** status within the approval process displayed the status as **Scheduled for Deletion Cancellation** instead of restoring it to the original **In Use** status

### 2023. 05. 30.
#### Bug Fixes
  * Fixed approval process notification (email) error
    * Fixed an issue where some administrators with approval permissions were not receiving notifications (emails)
  * Fixed approval process IP/MAC bulk registration error
    * Fixed an issue where bulk IP/MAC registrations in the approval process were not immediately reflected on the screen

### 2023. 04. 25.
#### New Features
  * Added approval process notification (email) feature
    * Added the ability to send emails to administrators with approval permissions when an approval request is submitted

### 2023. 02. 28.
#### Bug Fixes
  * Fixed template file download error
    * Fixed an issue where the bulk registration template file was downloaded in an incorrect template format

### 2023. 01. 31.
#### Bug Fixes
  * Improved approval feature and fixed errors
    * Fixed the confidential data modification screen to display the data area as blank when accessed while the approval feature is in use
    * Fixed the display to show the modified data after editing confidential data while the approval feature is in use
  * Fixed an issue where the MAC address tooltip in the keystore management tab displayed IPv4 instead of the MAC address

### 2022. 12. 27.
#### Feature Improvements/Changes
  * Changed API domain
    * Changed the SecureKeyManager API domain from `api-keymanager.cloud.toast.com` to `api-keymanager.nhncloudservice.com`

### 2022. 11. 29.
#### Bug Fixes
  * Improved approval feature and fixed errors
    * Improved error messages that occurred while using the approval feature to be more understandable
    * Fixed an issue where adding a keystore for the first time while using the approval feature proceeded without the approval process
  * Fixed certificate authentication error
    * Fixed an issue where certificate authentication intermittently failed

### 2022. 10. 25.
#### Bug Fixes
  * Fixed integrated Appkey error
    * Fixed an issue where API calls using the project integrated Appkey did not work properly
  * Fixed approval feature error
    * Fixed an issue where the per-key-version deletion feature did not work properly when using the approval feature

### 2022. 09. 27.
#### New Features
  * Added asymmetric key query feature
    * Added the ability to query asymmetric keys by key version

### 2022. 07. 26.
#### New Features
  * Added approval feature
    * Introduced an approval process for major changes such as key creation, modification, deletion, and access control changes for keystores
  * Added new symmetric key query version
    * Added the ability to query symmetric keys by key version

### 2021. 11. 23.
#### New Features
  * Added symmetric key query feature

### 2021. 10. 26.
#### New Features
  * Added key import feature
    * Added the ability to import symmetric keys
#### Feature Improvements/Changes
  * Modified confidential data query feature
    * Confidential data fields are now masked when queried in the Web console
#### Bug Fixes
  * Fixed an issue where users with overdue payments were still able to use the service normally

### 2021. 09. 28.
#### Bug Fixes
  * Fixed an issue where permissions granted through permission groups were not recognized properly
  * Fixed an issue where the usage history reset button did not work properly

### 2020. 03. 24.
#### New Features
  * Actions performed by users in the Secure Key Manager console are now recorded in CloudTrail
  * Added the ability to bulk register authentication data (IPv4 addresses/MAC addresses) using CSV files
  * Added the ability to download authentication data (IPv4 addresses/MAC addresses) using CSV files

### 2019. 12. 24.
#### New Features
  * Added statistics screen
    * Added a screen to view API usage statistics on a per-project basis
#### Feature Improvements/Changes
  * Improved keystore screen
    * Changed the display format of the keystore list
    * Changed the sub-menu of keystores
    * Added a quick menu to keystores
  * Improved usage history screen
    * Changed to allow viewing API usage history on a per-project basis

### 2019. 07. 23.
#### Feature Improvements/Changes
  * UI improvements
    * Fixed an issue where text and buttons were displayed overlapping
    * Fixed text line break issues when displaying the screen in Japanese

### 2019. 05. 28.
#### New Service Release
  * A service that centrally and securely manages data that could be exposed to security risks if stored on application servers, such as confidential data (database connection information, Appkeys, passwords, etc.), symmetric keys, and asymmetric keys, and controls access so that only authenticated clients can access them.