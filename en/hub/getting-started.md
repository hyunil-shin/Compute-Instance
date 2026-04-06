<style>
.page__rnb .lst_rnb_item .rnb_item:first-of-type a { 
    display: inline !important;
}
</style>
<h1>Getting Started with Notification Hub</h1>

**Notification > Notification Hub > Console Guide > Getting Started with Notification Hub**

<span id="identity-verification"></span>

## Identity verification

After Notification Hub is enabled, you must complete identity verification to use the service. For more details on identity verification, see **Service Policy and Precondition Guide > Identity verification**.

* [Go to Identity verification guide](../service-policy-and-precondition/identity-verification)


<span id="manage-sender-info"></span>

## Sender Information Management

<span id="manage-sender-phone-number"></span>

### Sender Number Management

To send SMS, LMS, and MMS messages, you must register a sender number. After requesting sender number registration review and getting approval, the sender number is registered.

1. Click **+ Register Sender Number** and agree to the **Personal Information Collection and Use Agreement**.
2. Select the type of sender number to register and enter the sender number.
3. Attach the documents required for the sender number type.

For more details on the sender number pre-registration system, see **Service Policy and Precondition Guide > SMS > Implementation of Sender Number Pre-registration System**.

* [Go to Implementation of Sender Number Pre-registration System](../service-policy-and-precondition/sms#sender-phone-number-pre-registration)

<span id="manage-sender-brand"></span>

### Brand Management

To send RCS messages, you must complete brand linkage. If pre-registration is complete (brand approval) in RCS Biz Center, proceed with linkage to the NHN Cloud console. For brand creation in RCS Biz Center, see **Service Policy and Precondition Guide** > **RCS**.

* [Go to Service Policy and Precondition Guide > RCS](../service-policy-and-precondition/rcs)
* [Go to RCS Biz Center](https://www.rcsbizcenter.com/main)

Once brand creation, agency setup, chatroom (sender number) registration, and template registration are complete (approved) in RCS Biz Center, link the brand in the console.

* Click **+ Brand linkage** to complete synchronization.

<span id="manage-sender-domain"></span>

### Domain Management

To send emails, you need a domain you own, SPF authentication, DKIM authentication, and DMARC authentication.

For more details on sending domains and SPF, DKIM, DMARC, see **Service Policy and Precondition Guide > Email**.

* [Go to Service Policy and Precondition Guide > Email](../service-policy-and-precondition/email)

#### Email Domain Registration and Ownership Authentication

You must register a domain and verify domain ownership. Register the value provided by Notification Hub in the email domain DNS TXT record. Ownership is authenticated by matching the provided value with the TXT record of the registered domain.

1. Click **+ Register Domain**.
2. Enter the root domain to register and click **Verify**.
3. If verification is successful, click **Register** to complete registration.
4. In the domain list, click **Authenticate** under Domain Ownership Authentication Status.

When domain ownership authentication succeeds, the domain authentication status changes to 'Complete'.

#### SPF Authentication

SPF (sender policy framework) is a mechanism for verifying the trustworthiness of email senders and sending servers. Email receiving servers check whether emails sent from a specific domain actually came from authorized email sending servers. Mail receiving servers check SPF records registered in the sender's email domain DNS and treat emails sent from unregistered IP addresses as spam.

**SPF**
```
v=spf1 include:_spfblocka.toast.com ~all
```

1. Register the SPF record from the **SPF** item above in the domain TXT record.
2. Select the domain from the list.
3. Click **Check Status** in the **SPF Record Authentication Status** item to complete SPF authentication.


!!! danger "Caution"
    * Only one SPF record should be registered in the domain TXT record. If two or more SPF records are registered in the domain TXT record, SPF authentication may fail and email receiving servers may reject reception.
    * When checking SPF records, the use of mechanisms (include) and modifiers (redirect) that cause DNS lookups is limited to a maximum of 10, and exceeding this may cause email receiving servers to reject reception.
    
For more details on SPF, see the documents below.

* [Go to Email Security Enhancement Feature Introduction (SPF)](https://meetup.nhncloud.com/posts/244)
* [Go to RFC 4408 - 4.5 Selecting Records](https://datatracker.ietf.org/doc/html/rfc4408#section-4.5)
* [Go to RFC 4408 - 10.1 Processing Limits](https://datatracker.ietf.org/doc/html/rfc4408#section-10.1)

#### DKIM Authentication

DKIM (domainkeys identified mail) is an email verification method where email sending servers digitally sign emails and email receiving servers verify sender authenticity to confirm that messages were not forged or altered during transmission. DKIM can prevent spam senders and other malicious attackers from forging or altering emails.


1. After completing domain ownership authentication, check the domain from the list and click **DKIM Settings**.
2. Set the TXT record value for the provided DNS hostname for DKIM authentication and click **Authenticate** below.
    * If the registered domain is `example.com`, you must set the value in the `toast._domainkey.example.com` TXT record.
3. After authentication is complete, enable usage settings and click **Save** to complete DKIM authentication.

For more details on DKIM, see the documents below.

* [Go to Email Security Enhancement Feature Introduction - Domain Protection, DKIM, DMARC](https://meetup.nhncloud.com/posts/248)


#### DMARC Authentication

DMARC (domain-based message authentication reporting and conformance) is the final step in email security enhancement. It is a domain-based message authentication reporting and compliance policy to prevent phishing and fraud using email spoofing. Email receiving servers query DMARC records from the DNS of the sender address (From) domain. According to the policy defined in the DMARC record, receiving servers authenticate received emails.

**DMARC**
```
"v=DMARC1;p=none;sp=quarantine;pct=100;rua=mailto:${email_address_to_receive_reports}"
```

1. Add an email address to receive DMARC reports to the **DMARC** item value above to complete the DMARC TXT record.
2. Register in the subdomain TXT record with `_dmarc.` added.
    * Example: If the domain is `example.com`, register in the TXT record of `_dmarc.example.com`.
3. Click **Check Status** in the **DMARC Authentication Status** item to complete DMARC authentication.

For more details on DMARC, see the documents below.

* [Go to Email Security Enhancement Feature Introduction - Domain Protection, DKIM, DMARC](https://meetup.nhncloud.com/posts/248)

##### Domain Protection

Domains with domain protection enabled cannot be used in other projects. To use a protected domain in other projects, you must complete the same domain registration and ownership authentication.

!!! danger "Caution"
    If you disable domain protection, other projects can use the domain arbitrarily. For domains that have completed all authentication, emails sent from other projects will also be received normally by email receiving servers. If such sent emails are spam or phishing, it can cause damage to recipients and the domain's reputation may decline, causing email receiving servers to reject reception.

<span id="manage-sender-push-authorization"></span>

### Push Authentication Management

For information on how to issue Push authentication information, see **Service Policy and Precondition Guide > Push**.

* [Go to Service Policy and Precondition Guide > Push](../service-policy-and-precondition/push)

#### FCM Authentication Settings
1. Enable **Register Service Account Key**.
2. Copy and paste the contents of the issued FCM Service Account Credential file into Service Account Key (JSON).
3. Click **Verify > Save** to complete the settings.

#### APNS Authentication Settings
1. Enable **Register APNS JWT Certificate**.
2. Enter **Team ID** and **Key ID**.
3. Enter **Topic**. The topic is the app's Bundle ID.
4. Copy and paste the contents of the **Private Key** file.
5. Click **Verify > Save** to complete the settings.

#### ADM Authentication Settings
1. Enable **Register Credentials**.
2. Enter **Client ID** and **Client Key**.
3. Click **Verify > Save** to complete the settings.

<span id="manage-sender-profile"></span>

### Sender Profile Management

To send KakaoTalk notifications, you need to create and register a sender profile.

Sender profile creation can be done in Kakao Business.

* [Go to Sender Profile Creation Guide](../service-policy-and-precondition/alimtalk-and-friendtalk)


Once the sender profile creation is complete in Kakao Business, register it following these steps:

1. Click **+ Register Sender Profile**, set the sender profile ID, administrator mobile number, and category, then click **Request Token**.
2. Enter the token sent to the administrator's mobile phone and click **Confirm > Register** to complete sender profile registration.


<span id="manage-080-unsubscription-number"></span>

### 080 Unsubscription Number Management

The 080 unsubscription number is a service that provides recipients with the option to unsubscribe when sending advertising messages. When sending advertising information, you must include a free unsubscription method so that recipients can unsubscribe or withdraw consent to receive messages for free.

#### Subscription Application

* Click **+ Apply for 080 Unsubscription Number** and enter the company name. The entered company name is the business name announced when calling the 080 unsubscription number.
* Once the subscription application is complete, the status changes to registration reserved. Opening the 080 unsubscription service takes 3-4 business days, and you can use it once opening is complete.
* Once opening is complete, you can check the service start date and status. You cannot terminate SMS product usage when the 080 unsubscription service is in registration reserved or in use status. Product usage termination is possible after cancellation. To cancel, click **Cancel**.

#### Setting 080 Unsubscription Number When Sending Advertising Messages

* You can only send advertising messages when the 080 unsubscription number service is activated.
* In the **Send > SMS** tab, when you select advertising as the sending purpose, the 080 unsubscription number selection window appears.
* Click **Apply Selection** to add mandatory advertising text.
* When sending advertising messages, the message body must include mandatory advertising text, with the following rules:
    * Starting text: (광고)
    * Ending text: 무료수신 거부 {080수신 거부번호} or 무료거부 {080수신 거부번호} (These phrases may include spaces.)

##### Examples
```
(광고)

[무료 수신 거부]080XXXXXXX
```
```
(광고)

무료거부 080XXXXXXX
```

<h1>Statistics</h1>

**Notification > Notification Hub > Statistics**


## Statistics

You can collect various events occurring in Notification Hub and query them as statistical data.

### Statistics Query

You can query the reception results of sent messages by recipient contact information.

* Query contact reception results by setting message channel, sending time (immediate, scheduled), sending purpose, and sending/receiving/viewing status in combination.
* When querying, the period is set based on the request date and time.
    * The default maximum queryable period range is 7 days.
    * You can query up to 180 days ago.
* You can query contact reception results by additionally selecting one of the detailed conditions.
    * Message ID, template name, flow name, statistics key name, sender information, recipient information

* Query statistical data by setting message channel, statistics criteria, statistics key, and message ID in combination.
* The statistics criteria you can set vary depending on the message channel you set.

#### Statistical Events by Message Channel and Statistics Criteria

| Message Channel | Statistics Criteria | Events                                                                                                                 | Notes                     |
| - | - |---------------------------------------------------------------------------------------------------------------------|------------------------|
| All | Message | REQUESTED, CANCELED, SENT, SEND_FAILED, DELIVERED, DELIVERY_FAILED                 | Events that occur during the sending process.    |
| SMS | Message | REQUESTED, CANCELED, SENT, SEND_FAILED, DELIVERED, DELIVERY_FAILED                 |                        |
| RCS | Message | REQUESTED, CANCELED, SENT, SEND_FAILED, DELIVERED, DELIVERY_FAILED                 |                        |
| KakaoTalk Notification | Message | REQUESTED, CANCELED, SENT, SEND_FAILED, DELIVERED, DELIVERY_FAILED                 |                        |
| Push | Message | REQUESTED, CANCELED, SENT, SEND_FAILED, DELIVERED, DELIVERY_FAILED, OPENED    | Message viewing events are also collected. |
| Email | Message | REQUESTED, CANCELED, SENT, SEND_FAILED, DELIVERED, DELIVERY_FAILED, OPENED    | Message viewing events are also collected. |
| SMS | International SMS Message | REQUESTED, CANCELED, SENT, SEND_FAILED, DELIVERED, DELIVERY_FAILED, CONCAT | CONCAT: Actual message sending count sent through the Concatenated message (connection) feature for international SMS messages only|

### Statistics Key Management

When you set a statistics key when sending messages, you can set the statistics key as a query condition in statistics queries to query statistical data for messages sent with the same statistics key.

1. Click **+ Add Statistics Key**.
2. Set the statistics key name, detailed description, and collection period.
    * You can set the collection period to unlimited.
    * This applies to statistics keys set for notices without expiration dates or messages that require periodic sending.
3. Events that occur with statistics keys that have not reached the collection period or have passed the collection period are not collected.
    * For campaigns or events running for a specific period, you can set a collection deadline to collect statistical events.